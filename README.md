

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

1. app.py             # Main Flask application code
2. requirements.txt   # Python dependencies
3. Dockerfile         # Dockerfile to containerize the app
4. README.md          # This README
5. static/
   └── gandalf.jpg    # Gandalf image
6. venv/              # Optional: local Python virtual environment

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
* `requirements.txt`
* `static/gandalf.jpg`
* `Dockerfile`
* `README.md`

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

> **Why virtual environment (venv)?**
> It keeps all project dependencies isolated from other Python projects and avoids conflicts.

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
python3 -m pip install -r requirements.txt
```

> Make sure the file name is exactly `requirements.txt`.

---

## Step 4: Run the Flask App Locally

```bash
python3 app.py
```

You should see something like:

```
 * Serving Flask app 'app'
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:8080
 * Running on http://192.168.0.16:8080
```

---

## Step 5: Test the Application

Open your browser or use `curl`:

* Gandalf image:

```bash
http://127.0.0.1:8080/gandalf
```

* Colombo time:

```bash
http://127.0.0.1:8080/colombo
```

* Prometheus metrics:

```bash
http://127.0.0.1:8080/metrics
```

---

## Step 6: Dockerize the Application

Your Dockerfile is configured as follows:

```dockerfile
FROM python:3.12-slim-bookworm AS base

WORKDIR /usr/src/app

# Copy and install dependencies
COPY requirements.txt ./
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# Copy app code and static folder
COPY . .

# Expose the internal Flask port
EXPOSE 8080

# Run the Flask app
ENTRYPOINT ["python", "app.py"]
```

Build and run the container:

```bash
docker build -t gandalf-webapp:1.0 .
sudo docker run -d -p 80:8080 gandalf-webapp:1.0
```

### Explanation:

* **Internal Flask port:** 8080 (inside container)
* **External port:** 80 (host/public), satisfies assignment requirement “only port 80 should be open”
* Browser and Prometheus can access the app using port 80.

Explanation:

The container itself does not have a public IP.

Your host machine’s IP (127.0.0.1 or 192.168.x.x) is what you can use to access it from your laptop.

This is fine for local testing only.

Check running containers:

```bash
docker ps
```

You should see something like:

```
CONTAINER ID   IMAGE                 COMMAND        STATUS     PORTS
8cb653912f8f   gandalf-webapp:1.0   "python app.py"  Up 5s   0.0.0.0:80->8080/tcp
```

---
