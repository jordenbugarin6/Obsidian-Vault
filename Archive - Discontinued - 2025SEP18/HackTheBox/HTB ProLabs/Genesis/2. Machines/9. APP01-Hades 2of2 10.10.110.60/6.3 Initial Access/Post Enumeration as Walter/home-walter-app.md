# `/home/walter/app`

```bash
walter@APP01-Hades:~/app$ ls
ls
app.py
license.txt
products.db
static
templates
```
 
![[Pasted image 20240502104211.png]]
## `app.py`

```bash
from flask import Flask, session, render_template, request, Response, render_template_string, g                                                                                                             
import functools, sqlite3, os                                                                                                                                                                               
app = Flask(__name__, static_folder="static", static_url_path="/static")                                                                                                                                    
acc_tmpl = '''{% extends 'products.html' %}                                                                                                                                                                 
{% block content %}                                                                                                                                                                                         
No results for query
{% endblock %}
'''

index_tmpl = '''{% extends 'index.html' %}

{% block content %}
No results for query
{% endblock %}
'''

index_tmpl = '''{% extends 'index.html' %}
{% block content %}
{% endblock %}
'''

card_tmpl = '<div class="card"><div class="card__image-holder"><img height=240px width=300px class="card__image" src="url" alt="wave"/></div><div class="card-title"><h2>name<small>desc</small></h2></div></div>'

def get_products(product):
    db = sqlite3.connect('products.db')
    cur = db.cursor()
    try:
        cur.execute(f"SELECT * FROM products WHERE name LIKE '%{product}%'")
    except:
        db.close()
        return []
    rows = cur.fetchall()
    db.close()
    return rows

@app.route('/')
def index():
    return render_template_string(index_tmpl)

@app.route('/products')
def search():
    cards = ""
    q = request.args.get('search')
    if not q:
        q = ""
    products = get_products(q)
    if products:
        for product in products:
            cards += card_tmpl.replace("url", product[2]).replace("name", product[1]).replace("desc", product[-1])
        return render_template_string(acc_tmpl.replace("No results for query", cards))
    else:
        return render_template_string(acc_tmpl.replace("query", q))

app.run(host='0.0.0.0', port=80)
```

## `products.db`

```bash
dP++Ytablesqlite_sequencesqlite_sequenceCREATE TABLE sqlite_sequence(name,seq)tableproductsproductsCREATE TABLE products ( id INTEGER PRIMARY KEY AUTOINCREMENT, name VARCHAR(100), url varchar(500), description varchar(500))
9M
B



 f
  7
   "



    m
     #

 9DELETEDELETE FROM table_name=sUPDATEUPDATE table_name SET col1="work" WHERE col2="test"HINSERTINSERT INTO table_name (col1, col2) VALUES ("example","test")"=SELECTSELECT * FROM table_name.UCREATECREATE 
i.Color#9393ad-e (col1, col2)9SQLSyntax example library@uai.ImageBlob - png, jpg, gif or String(base64) [DbClick] row
               Sai.Urlhttps://twitter.com/SqliteOnlineCom
                                                         7ShareCreate public link DB&
!=Size tableFast sc-
                    Super -mSuper BlockChainhttps://unsplash.com/photos/p60CjQTbPtw/download?force=true&w=640New blockchain technology introducing the GCoin.؁
                                                                                                                                                              '{Nextgen Cloudhttps://unsplash.com/photos/JKUTrJ4vK00/download?force=true&w=640All new and advanced cloud services with best security.yDeepNNhttps://unsplash.com/photos/JjGXjESMxOY/download?force=true&w=640Deep learning and Neural networks for next-gen robots!{Among Themhttps://unsplash.com/photos/VW2oU66mwbc/download?force=true&w=640Framework to test and discover games for security bugs.
!PseudoSofthttps://unsplash.com/photos/tpAyLp9Ro50/download?force=true&w=640Advanced framework to test projects powered by the ARM processors.{RichAIhttps://unsplash.com/photos/jIBMSMs4_kA/download?force=true&w=640Created a new algorithm to detect anomalies in AI & ML.

```

