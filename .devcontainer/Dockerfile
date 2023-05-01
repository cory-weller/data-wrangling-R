ARG VARIANT="16-buster"
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    build-essential \
    libssl-dev \
    uuid-dev \
    libgpgme11-dev \
    squashfs-tools \
    libseccomp-dev \
    wget \
    pkg-config \
    git \
    cryptsetup \
    dirmngr \
    gnupg \
    wget \
    apt-transport-https \
    ca-certificates \
    software-properties-common \
    gcc \
    make \
    libbz2-dev \
    zlib1g-dev \
    libncurses5-dev  \
    libncursesw5-dev \
    liblzma-dev \
&&  apt -y update \
&&    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 \
&&    add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/' \
&& apt-get install -y \
        r-base \
        r-base-core \
        r-recommended \
        r-base-dev \
        libcurl4-openssl-dev \
        libssl-dev \
        g++ \
        curl \
        libxml2 \
        libxml2-dev \
        xauth \
&&    R --no-echo -e "install.packages('data.table', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('R.utils', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('ggplot2', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('foreach', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('doMC', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('ggthemes', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('ggrepel', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('optparse', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('umap', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('corrplot', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('reshape2', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('Seurat', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('HGNChelper', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "install.packages('BiocManager', repos='http://cran.us.r-project.org')" \
&&    R --no-echo -e "BiocManager::install('DESeq2')" \
&&    R --no-echo -e "BiocManager::install('apeglm')" 
