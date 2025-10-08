FROM quay.io/jupyter/r-notebook:hub-5.2.1

USER root

# ======================================================================================================================
# General system packages and jupyterhub dependencies
#
RUN apt-get update && \
    apt-get install -y \
    vim \
    less \
    curl \
    wget \
    jq \
    patch \
    pandoc \
    git

# ======================================================================================================================
# R system pacakges
#
RUN apt update -qq && apt install -y --no-install-recommends software-properties-common dirmngr
RUN wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc
RUN add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
RUN sudo apt install --no-install-recommends -y r-base

# ======================================================================================================================
# RStudio
#
RUN apt install -y gdebi-core
RUN wget https://download2.rstudio.org/server/jammy/amd64/rstudio-server-2025.05.0-496-amd64.deb -O /tmp/rstudio.deb
RUN sudo gdebi -n /tmp/rstudio.deb

# Reconfigure RStudio defaults -- DO NOT MODIFY!
RUN echo "session-default-working-dir=/home/jovyan/work" >> /etc/rstudio/rsession.conf; \
    echo "session-default-new-project-dir=/home/jovyan/work" >> /etc/rstudio/rsession.conf

# ======================================================================================================================
# Jupyter extensions (Python packages)
#
RUN pip install --upgrade \
    ipywidgets \
    nbconvert \
    playwright \
    ipython \
    ipympl  \
    jupyter-rsession-proxy==2.3.0 \
    grader-service==0.9.0 \
    grader-labextension==0.9.0 \
    && \
    playwright install chromium && \
    fix-permissions "/home/${NB_USER}/.cache"

# ======================================================================================================================
# Additional R packages
#
RUN mamba install --yes \
        "r-reticulate" \
        "r-png" \
        "r-mosaic" \
        "r-nortest"

# ======================================================================================================================
# Final preparations
#
RUN mamba clean --all -f -y && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}" && \
    fix-permissions "/home/${NB_USER}/.cache"

# Always set the default user to 'jovyan' (UID: 1000) at the end -- DO NOT MODIFY!
USER 1000
