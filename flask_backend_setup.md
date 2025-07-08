# Install & Configure – Python + Flask Backend

## Description
This document explains how to 

1. install **Python 3** on Windows, macOS, Linux (and WSL),
2. create an isolated **virtual environment**,
3. install **Flask 3 .x** and its dependencies,
4. run a “Hello Flask” application, and  
5. understand the resulting project structure.

> **Tested with:**  
> • Python 3.12.3 (Apr 9 2025)  
> • Flask 3.0.3 (Mar 2025) – supports Python 3.9 +

---

## Table of Contents
1. [Install Python 3](#install-python-3)  
   1.1 [Windows](#windows) 1.2 [macOS](#macos) 1.3 [Linux / WSL](#linux--wsl)  
2. [Verify Installation](#verify-installation)  
3. [Create a Virtual Environment](#create-a-virtual-environment)  
4. [Activate the Environment](#activate-the-environment)  
5. [Install Flask](#install-flask)  
   5.1 [Core dependencies](#core-dependencies) 5.2 [Optional extras](#optional-extras)  
6. [Hello World Example](#hello-world-example)  
7. [Project Structure](#project-structure)  
8. [Next Steps](#next-steps)

---

## Install Python 3

> **Quick check first:**  
> ```bash
> python --version   # or python3 --version
> ```
> If you already have **≥ 3.9**, jump to [Create a Virtual Environment](#create-a-virtual-environment).

### Windows
1. Download the **LTS (3.12.x)** installer from <https://www.python.org/downloads/windows/>.  
2. **IMPORTANT:** Tick “*Add Python 3.x to PATH*”.  
3. Keep the default “Install Now” settings.  
4. Re‑open *PowerShell* or *Command Prompt*.

### macOS
```bash
# Install Homebrew if needed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Use Homebrew to install Python
brew install python  # installs latest 3.12.x and pip
````

### Linux / WSL (Ubuntu 22.04 +)

```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv
```

> For multiple Python versions, consider **pyenv**:
>
> ```bash
> curl https://pyenv.run | bash
> exec $SHELL
> pyenv install 3.12.3
> pyenv global 3.12.3
> ```

---

## Verify Installation

```bash
python3 --version   # e.g. Python 3.12.3
pip3 --version      # ensures pip is linked to the same Python
```

---

## Create a Virtual Environment

```bash
# 1 Create a project root
mkdir flask_app
cd flask_app

# 2 Create venv inside “.venv”
python3 -m venv .venv
```

---

## Activate the Environment

|  OS                  | Command to Activate      | Prompt Change         |
| -------------------- | ------------------------ | --------------------- |
| macOS / Linux / WSL  | `. .venv/bin/activate`   | `(.venv) user@host $` |
| Windows (PowerShell) | `.venv\Scripts\Activate` | `(.venv) PS C:\…>`    |

> Deactivate with `deactivate`.

---

## Install Flask

### Core Dependencies

Inside the activated environment:

```bash
pip install --upgrade pip
pip install Flask
```

This automatically installs:

* **Werkzeug** – WSGI utilities
* **Jinja** – template engine
* **MarkupSafe** – HTML‑escaping
* **ItsDangerous** – secure signatures
* **Click** – CLI framework
* **Blinker** – signal support

### Optional Extras

```bash
pip install python-dotenv watchdog
# If you plan on async workers:
pip install greenlet  # gevent / eventlet need it
```

* **python‑dotenv** – loads `.env` files during `flask run`
* **watchdog** – high‑performance file‑change reloader

---

# Hello World Example

Create ```app.py``` in your project root:

```bash
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/")
def home():
    return jsonify(message="Hello, Flask!", status="success")

if __name__ == "__main__":
    app.run(debug=True)

```

Run the app:

```bash
flask --app app --debug run  # or: python app.py
```

Visit `http://127.0.0.1:5000/` – you should see:

```json
{"message":"Hello, Flask!","status":"success"}
```

---

## Project Structure

After the steps above your tree looks like:

```
flask_app/
├── .venv/             # isolated Python interpreter + libs
├── app.py             # minimal Flask entry point
├── requirements.txt   # created via: pip freeze > requirements.txt
└── .flaskenv          # optional, holds FLASK_APP, FLASK_ENV vars
```

> **Tip:** Keep `requirements.txt` committed so deployments can replicate: It means
You should include the requirements.txt file in your version control system (like Git), so that others — or future you — can easily recreate the same environment with the exact same packages and versions.
> 
> ```bash
> pip freeze > requirements.txt
> ```

---

## Next Steps

* **Blueprints**: Split routes into modular files.
* **Templates & Static**: Create `templates/` for Jinja HTML and `static/` for CSS/JS.
* **Environment Variables**: Add a `.env` file (kept out of VCS!) and load with *python‑dotenv*.
* **Production Server**: Use **Gunicorn** + **Nginx** or **uWSGI**.
* **Testing**: Add `pytest` and `pytest‑flask` for unit and integration tests.
* **CI/CD**: Automate with GitHub Actions to lint, test, and deploy.

