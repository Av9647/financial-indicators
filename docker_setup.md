## Docker Setup Guide

### 1. Download Docker Desktop

If you install **Docker Desktop**, it includes everything you need to build images and run containers, including:

- Docker Engine (for running containers)
- Docker CLI (command-line interface for managing Docker)
- Docker Compose (for multi-container applications)
- A Kubernetes environment (optional)
- A GUI Dashboard (for managing containers and images visually)

#### Platform-Specific Considerations

#### Windows Users
- Ensure **WSL 2 (Windows Subsystem for Linux)** is installed and enabled for better performance.

#### Linux Users
- Docker Desktop is **not required** on Linux.
- Installing **Docker Engine (`docker-ce`)** is sufficient.

#### Mac Users
- Works natively on macOS (Intel or Apple Silicon).
- For Apple Silicon (M1/M2), ensure you are using **multi-arch images** or emulation.

---

### 2. Start Docker Engine

Open **Docker Desktop** so that the Docker Engine keeps running.

---

### 3. Navigate to Project Root

Open **Command Prompt / Terminal** and navigate to the **root directory** of the project that contains both frontend and backend folders.

---

### 4. Create Dockerfile

Create a `Dockerfile` containing **multi-stage build commands** for:

- React front-end
- Python (Flask) back-end

#### Required Container Directory Structure

```
/app/                                <-- 🔹 Root directory inside the container
├── app/                             <-- ✅ Flask backend files
│   ├── __init__.py
│   ├── db.py
│   ├── financial_controller.py
│   ├── models.py
│   ├── analysis_service.py
│   └── redflags_service.py
│
├── static/                          <-- ✅ React frontend build files
│   ├── index.html
│   ├── static/                      <-- ✅ Contains JS, CSS, Media
│   │   ├── js/
│   │   │   ├── main.xxxxxx.js
│   │   │   └── chunk.js files
│   │   ├── css/
│   │   │   └── main.xxxxxx.css
│   │   └── media/
│   ├── asset-manifest.json
│   ├── favicon.ico
│   ├── manifest.json
│   └── robots.txt
│
├── run.py                           <-- ✅ Flask entry point
├── requirements.txt                 <-- ✅ Python dependencies
├── runtime.txt
└── venv/                            <-- ✅ Python virtual environment
```

---

### 5. (Optional) Create docker-compose.yml

Create a `docker-compose.yml` file if you plan on adding future service integrations.

---

### 6. Build Docker Image

Run the following command from the **project root directory** where the `Dockerfile` is present:

```bash
docker-compose build --no-cache
```

### 7. Fix Build Issues

Fix any issues in the code that might raise exceptions during the build.

----------

### 8. Run the Container

Once the image is built successfully, run:

```
docker-compose up
```

### 9. Verify Application

Open a browser and navigate to:

```
http://127.0.0.1:5000
```

### 10. Check Front-End Console

Check for any path or runtime issues in the front-end console:

-   **Windows:** `Ctrl + Shift + I`
    
-   Open the **Console** tab
    
----------

### 11. Run Commands Inside the Container

Open an interactive shell inside the container:

```
docker exec -it company_risk_analysis-web-1 sh
```

> This opens an interactive shell (`sh`) inside the Flask container.  
> Container name: `company_risk_analysis-web-1`

#### Useful Debug Commands

List files inside `/app/static`:

```
ls -l /app/static
```

View contents of `run.py`:

```
cat /app/run.py
```

### 12. Troubleshooting

Confirm that paths are correctly configured inside the container in the following files:

-   `run.py`
    
-   `index.html`
    
-   `package.json`
    
-   Any related configuration files
    
----------

### Docker Commands Reference

Build Docker images: `docker-compose build`

Build without cache: `docker-compose build --no-cache`

Start containers: `docker-compose up`

Stop and remove containers: `docker-compose down`

Clean up unused Docker resources: `docker system prune -a`

List running containers: `docker ps`
