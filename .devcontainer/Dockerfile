FROM rocker/tidyverse:latest

# We need to install extra packages as the root user
USER root

# Install system dependencies (including LaTeX and libglpk for igraph)
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
        python3-pip \
        libgit2-dev \
        libcurl4-openssl-dev \
        libssl-dev \
        libxml2-dev \
        libxt-dev \
        texlive-latex-base \
        texlive-latex-extra \
        texlive-fonts-recommended \
        texlive-xetex \
        libglpk-dev \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* \
    \
    && python3 -m pip --no-cache-dir install radian --break-system-packages \
    \
    && install2.r --error --skipinstalled --ncpus -1 \
        devtools \
        languageserver \
    && rm -rf /tmp/downloaded_packages

# VSCode R Debugger dependency
RUN Rscript -e 'remotes::install_github("ManuelHentschel/vscDebugger@*release", dependencies = FALSE)'

# Fix permissions for the RStudio startup script
RUN chmod +x /etc/services.d/rstudio/run

# Switch back to the default non-root rstudio user
USER rstudio