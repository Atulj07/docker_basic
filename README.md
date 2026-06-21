# Docker Flask Demo

A minimal Flask app containerized with Docker.

## Files

- [app.py](app.py) — Flask app with two routes: `/` (returns "hello") and `/contact` (returns "Contact"), served on port 5000.
- [requirements.txt](requirements.txt) — Python dependencies (`flask`).
- [Dockerfile](Dockerfile) — Builds the app on `python:3.11.15-alpine3.23`, installs dependencies, and runs `app.py` on port 5000.

### app.py

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return "hello"

@app.route('/contact')
def contact():
    return "Contact"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

### requirements.txt

```
flask
```

### Dockerfile

```dockerfile
FROM python:3.11.15-alpine3.23
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python","app.py"]
```

## Commands

1. Build the image:

   ```sh
   docker build . -t demoappb17b:v1.0
   ```

2. List images:

   ```sh
   docker images
   ```

3. Run the container, mapping host port 5001 to container port 5000:

   ```sh
   docker run -p 5001:5000 demoappb17b:v1.0
   ```

   Or run detached (in the background):

   ```sh
   docker run -d -p 5001:5000 demoappb17b:v1.0
   ```

4. List running containers:

   ```sh
   docker ps
   ```

5. Open the app in your browser:

   - http://localhost:5001/
   - http://localhost:5001/contact

6. Stop the running container:

   ```sh
   docker stop <container_id>
   ```

## Docker Hub

1. Version update — bump the tag for the new release and rebuild:

   ```sh
   docker build . -t demoappb17b:v2.0
   ```

2. Create the repository — create `atulj07/demoappb17b` on Docker Hub (via [hub.docker.com](https://hub.docker.com) → Create Repository, or it is created automatically on first push), then log in and tag the image for that namespace:

   ```sh
   docker login
   docker tag demoappb17b:v2.0 atulj07/demoappb17b:v2.0
   ```

3. Push to Docker Hub:

   ```sh
   docker push atulj07/demoappb17b:v2.0
   ```

4. Delete the local image:

   ```sh
   docker image rm atulj07/demoappb17b:v2
   ```

5. Pull the image back from Docker Hub:

   ```sh
   docker pull atulj07/demoappb17b:v2.0
   ```

