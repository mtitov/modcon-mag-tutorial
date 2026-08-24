# MAG Access Guide

This repository provides a hands-on Jupyter notebook covering MAG access onboarding, PAT handling, live model discovery, model selection, and a first Model Access Gateway (MAG) request.

## Direct Use

1. Install the package environment:
   ```bash
   python -m pip install -r requirements.txt
   ```
2. In a terminal, set `AMSC_I2_API_KEY` to your project MAG PAT:
   ```bash
   export AMSC_I2_API_KEY="paste-your-PAT-here"
   ```
3. Launch Jupyter from that same terminal and run the tutorial notebook:
   ```bash
   jupyter lab notebooks/mag-access.ipynb
   ```

> **Security Note:** Never put a PAT in this repository, notebook files, output cells, or screenshots. The notebook queries `/v1/models` live because model permissions are scoped to your project credential.

## Packaging and Running with Tutorial SDK (Optional)

This tutorial can be validated, packaged, and containerized into a reproducible environment using the [Tutorial SDK](https://bnl-peso-hub.github.io/tutorial-sdk/).

### Step 1: Validate the Package

Validate `tutorial.yml`, declared dependencies, and notebook paths:
```bash
tutorial-sdk validate
```

### Step 2: Generate the Dockerfile

Generate the container definition based on `tutorial.yml`:
```bash
tutorial-sdk generate dockerfile
```

### Step 3: Build the Container Image

> **Note:** Building and running containers require a Docker-compatible runtime (e.g., [Docker Desktop](https://www.docker.com/products/docker-desktop/) or [OrbStack](https://orbstack.dev/)) to be installed and running.

Build the container image (`mag-access:latest`):
```bash
tutorial-sdk build
```

### Step 4: Run the Containerized Tutorial

Export your MAG PAT in your terminal session, then run the container with the credential passed through:

- **Using Docker directly (recommended for passing credentials):**
  ```bash
  docker run --rm -it \
    -p 8888:8888 \
    -e AMSC_I2_API_KEY="$AMSC_I2_API_KEY" \
    mag-access:latest
  ```

- **Using the Tutorial SDK launcher:**
  ```bash
  tutorial-sdk run --port 8888
  ```

Once running, navigate to `http://localhost:8888` (or the URL printed in the terminal) to open JupyterLab with `notebooks/mag-access.ipynb`.

## Sources

- [Model Access Gateway (MAG) Documentation](https://docs.amsc.energy.gov/model-access-gateway)
- [Tutorial SDK Documentation](https://bnl-peso-hub.github.io/tutorial-sdk/)

## Repository Layout

```text
.
├── LICENSE
├── tutorial.yml
├── requirements.txt
├── README.md
└── notebooks/
    └── mag-access.ipynb
```

## License

This project is licensed under the [MIT License](LICENSE).
