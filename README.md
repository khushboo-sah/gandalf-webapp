

---

```markdown
# Gandalf Web App

## Overview
This is a simple Python Flask web application with three main features:

1. **`/gandalf`** – Shows an image of Gandalf.  
2. **`/colombo`** – Shows the current time in Colombo, Sri Lanka in JSON format.  
3. **`/metrics`** – Provides Prometheus metrics counting requests to `/gandalf` and `/colombo`.

The app uses Python 3 and the Flask framework. Gandalf’s image is stored in the `static/` folder as `gandalf.jpg`.

---

## Project Structure

```

gandalf-webapp/
├── app.py             # Main Flask application code
├── requirement.txt    # Python dependencies
└── static/
└── gandalf.jpg    # Gandalf image

````

---

## Step 1: Download the Code

1. Clone the repository:
```bash
git clone <your-repo-url>
cd gandalf-webapp
````

2. Ensure the following files exist:

* `app.py`
* `requirement.txt`
* `static/gandalf.jpg`

---

## Step 2: Set Up Python Environment

1. Check Python version (Python 3.12+ required):

```bash
python3 --version
```

2. Create a virtual environment (recommended):

```bash
python3 -m venv venv
```

> We recommend using a virtual environment (venv) to keep all project dependencies isolated from other Python projects and avoid conflicts.

3. Activate the virtual environment:

```bash
source venv/bin/activate   # MacOS/Linux
venv\Scripts\activate      # Windows
```

---

## Step 3: Install Dependencies

1. Upgrade pip and install required packages:

```bash
python3 -m pip install --upgrade pip
python3 -m pip install -r requirement.txt
```

> Make sure the file name is exactly `requirement.txt`.

---

## Step 4: Run the Flask App

```bash
python3 app.py
```

**Note:** The Flask app is set to run on **port 80**. On Mac/Linux, using ports below 1024 may require **root permissions**.
If you get a permission error, run:

```bash
sudo python3 app.py
```

You should see something like:

```
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:80
 * Running on http://192.168.0.16:80
```

---

## Step 5: Test the Application

Open your browser or use `curl` to test:

* Gandalf image:

```bash
http://127.0.0.1:80/gandalf
```

* Colombo time:

```bash
http://127.0.0.1:80/colombo
```

* Prometheus metrics:

```bash
http://127.0.0.1:80/metrics
```

---




