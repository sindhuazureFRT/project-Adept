from flask import Flask ,request,render_template,redirect,flash,session


import sqlite3

sqlconnection =sqlite3.connect("login.db")
sqlconnection.execute("create table if not exists users(id integer primary key,username text,password integer, email text)")
sqlconnection.close()

app=Flask(__name__)
app.secret_key="123"

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/login')
def login():
    return render_template('login.html')

@app.route('/client')
def client():
    return render_template('client.html')
@app.route('/client_product')
def clientproduct():
    return render_template('client_product.html')
@app.route('/chat')
def chat():
    return render_template('chat.html')
@app.route('/ccart')
def ccart():
    return render_template('client_cart.html')

@app.route('/cart')
def cart():
    return render_template('cart.html')

@app.route('/log',methods =["GET","POST"])
def log():
    if request.method =="POST":
        name=request.form['username']
        psswd=request.form['password']
        sqlconnection= sqlite3.connect('login.db')
        sqlconnection.row_factory=sqlite3.Row
        cur=sqlconnection.cursor()
        
        cur.execute("select * from users where username =? and password =?",(name,psswd))
        data=cur.fetchone()
        if (data):
          session['name']=data["username"] 
          session['mail']=data["email"] 
          flash("Welcome to Zomaika","logged")
          return redirect("/client")
        else:
            flash("Invalid Username and Password","danger")
            return redirect('/login')
    return redirect('/')
@app.route('/signup',methods =["GET","POST"])
def signup():
    if request.method =="POST":
        try:
            name=request.form['username']
            psswd=request.form['password']
            mail=request.form['email']
            sqlconnection=sqlite3.connect('login.db')
            cur=sqlconnection.cursor()
            cur.execute("insert into users(username,password,email)values(?,?,?)",(name,psswd,mail))
            sqlconnection.commit()
            flash("Record added Successfully","success")
        except:
            flash("Error in Insert Operation","danger")
        finally:   
           return redirect('/login')
           sqlconnection.close()
      
    return render_template('signup.html')

@app.route('/product')
def product():
    return render_template('product.html')

if __name__=="__main__":
    app.run(debug=True)

    