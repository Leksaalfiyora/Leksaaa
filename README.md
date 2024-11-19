# Leksaaa
rom flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# In-memory "database"
todos = []

@app.route("/")
def index():
    return render_template("index.html", todos=todos)

@app.route("/add", methods=["GET", "POST"])
def add():
    if request.method == "POST":
        task = request.form.get("task")
        if task:
            todos.append(task)
        return redirect(url_for("index"))
    return render_template("add.html")

@app.route("/delete/<int:task_id>")
def delete(task_id):
    if 0 <= task_id < len(todos):
        todos.pop(task_id)
    return redirect(url_for("index"))

if __name__ == "__main__":
    app.run(debug=True)
