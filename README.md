# TechBio-Data-Sciences-I

### Quick Start: To test the Docker Container

Build the Docker image and start a container with the following commands:

```bash
# 1. Build the Docker image
docker build -t biomathematik-docker:latest .

# 2. Run the Docker container
docker run -it --rm -p 8888:8888 -p 8787:8787 biomathematik-docker:latest
```

The container can be accessed on:  
http://localhost:8888/

### Installing packages

To install R-packages simply add the package name to the "Additional R packages" section:

RUN mamba install --yes \\  
&nbsp;&nbsp;&nbsp;&nbsp;"r-mosaic" \\  
&nbsp;&nbsp;&nbsp;&nbsp;"r-nortest" \\  
&nbsp;&nbsp;&nbsp;&nbsp;"&lt;r-package-1&gt;" \\  
&nbsp;&nbsp;&nbsp;&nbsp;"&lt;r-package-2&gt;"