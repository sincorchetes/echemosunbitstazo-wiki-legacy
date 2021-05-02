====== Kubernetes ======
===== Conceptos =====
===== Arquitectura =====
Para este ejemplo, utilizaremos este esquema:

|Servidor|CPU|RAM|Red|
|Master|2|2GB|1|
|Worker 1|1|1GB|1|
|Worker 2|1|1GB|1|

===== Master =====
==== Instalación y actualización ====
Desplegamos un servidor CentOS 8 y lo actualizamo a CentOS 8 Stream
<code bash>
sudo dnf install centos-stream-release
sudo dnf distro-sync
sudo dnf upgrade
</code>
==== Kubernetes ====
==== Requisitos ====
=== Swap, fstab y LVM ===
  * Deshabilitando y eliminando la swap
<code bash>
sudo swapoff -a
sudo lvremove /dev/cl_echemosunbitstazo/swap
</code>
  * Editar el archivo ''/etc/fstab'' y eliminar la línea de swap
  * Incrementar el espacio eliminado de la swap a ''/''
<code bash>
sudo lvextend -l100%FREE /dev/cl_echemosunbitstazo/root
sudo xfs_growfs /dev/cl_echemosunbitstazo/root
</code>
  * Editamos el archivo ''/etc/default/grub'' y eliminamos las entradas dónde hace referencia a la ''swap'':
<code bash> resume=/dev/mapper/cl_echemosunbitstazo-swap rd.lvm.lv=/dev/mapper/cl_echemosunbitstazo-swap
</code>
  * Regenerar el grub
<code bash>
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
</code>

=== Redes, módulos y cortafuegos ===
  * Habilitando el módulo ''br_netfilter'' y aplicando configuraciones para ''sysctl'':
<code bash>
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF
sudo sysctl --system
</code>
  * Abriendo puertos de comunicación ''firewalld''
<code bash>
sudo firewall-cmd --add-port 6443 --permanent
sudo firewall-cmd --add-port 64430-64439/tcp --permanent
sudo firewall-cmd--add-port 2379-2380/tcp --permanent
sudo firewall-cmd--add-port 10250/tcp --permanent
sudo firewall-cmd--add-port 10251/tcp --permanent
sudo firewall-cmd--add-port 10252/tcp --permanent
sudo firewall-cmd --reload
</code>
  * Reiniciando la máquina
<code bash>
sudo systemctl reboot
</code>


==== Habilitando repositorios ====

  * Instalando repositorios:
<code bash>
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
EOF
sudo curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/CentOS_8_Stream/devel:kubic:libcontainers:stable.repo
sudo curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable:cri-o:v1.20.repo https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/1.20/CentOS_7/devel:kubic:libcontainers:stable:cri-o:1.20.repo
</code>
  * Sincronizando los repositorios
<code bash>
sudo dnf check-update
</code>
==== SELinux ====
  * Deshabilitando de forma temporal SELinux (aunque no es compatible, quizás podamos moldearlo en un futuro)
<code bash>
sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
</code>
==== Paquetería ====
  * Instalando ''cri-o'' y los paquetes necesarios
<code bash>
dnf install cri-o kubelet kubeadm kubectl iproute-tc --disableexcludes=kubernetes
</code>
  * Configurando Kubeadm para que se ejecute con los cgroups correctos ''/usr/lib/systemd/system/kubelet.service.d/10-kubeadm.conf'':
<code bash>
Environment="KUBELET_KUBECONFIG_ARGS=--bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --cgroup-driver=systemd"
</code>
  * Habilitando ''kubelet.service''
<code bash>
sudo systemctl enable kubelet.service
</code>







