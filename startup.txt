from flask import Flask, request, render_template_string

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def calculator():
    result = ""

    if request.method == "POST":
        num1 = float(request.form["num1"])
        num2 = float(request.form["num2"])
        op = request.form["operation"]

        if op == "+":
            result = num1 + num2
        elif op == "-":
            result = num1 - num2
        elif op == "*":
            result = num1 * num2
        elif op == "/":
            result = "Error" if num2 == 0 else num1 / num2

    return render_template_string("""
    <!DOCTYPE html>
    <html>
    <head>
        <title>Python Calculator</title>
        <style>
            body {
                font-family: Arial;
                text-align: center;
                margin-top: 80px;
            }
            input, select, button {
                padding: 10px;
                margin: 5px;
                font-size: 16px;
            }
        </style>
    </head>
    <body>
        <h1>🧮 Python Web Calculator</h1>

        <form method="POST">
            <input type="number" name="num1" step="any" required>
            <select name="operation">
                <option value="+">+</option>
                <option value="-">−</option>
                <option value="*">×</option>
                <option value="/">÷</option>
            </select>
            <input type="number" name="num2" step="any" required>
            <br><br>
            <button type="submit">Calculate</button>
        </form>

        <h2>Result: {{ result }}</h2>
    </body>
    </html>
    """, result=result)

if __name__ == "__main__":
    app.run(debug=True)
