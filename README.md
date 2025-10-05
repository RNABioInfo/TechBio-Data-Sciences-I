# TechBio-Data-Sciences-I

## Quick Start: Test the Docker Container

Build the Docker image and start a container with the following commands:

```bash
# 1. Build the Docker image
docker build -t biomathematik-docker:latest .

# 2. Run the Docker container
docker run -it --rm -p 8888:8888 -p 8787:8787 biomathematik-docker:latest