====== Python y MongoDB ======

  * Recuperar registros de MongoDB sin importar mayúsculas|minúsculas
<code python> 
def find_post(search):
    db = db_manager()
    from bson.json_util import dumps
    
    result = []
    import re
    regx = re.compile(search, re.IGNORECASE)
    for post in db.echemosunbitstazo.post.find({"title": regx}):
        result.append(post)
    return dumps(result )
</code>