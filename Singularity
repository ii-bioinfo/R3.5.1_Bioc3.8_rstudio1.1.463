Bootstrap: docker
FROM: bioconductor/release_core2:R3.5.1_Bioc3.8

%help
  RStudio Desktop version 1.1.463
  R version 3.5.1

  Usage:
  $ singularity run rstudio.3.5.1.simg [args]
  $ singularity run --app R rstudio.3.5.1.simg [args]
  $ singularity run --app Rscript rstudio.3.5.1.simg [args]
  $ singularity run --app rstudio rstudio.3.5.1.simg

%setup

%files

%labels
  ii-bioinfo@imp.ac.at
  RStudio_Version 1.1.463
  R_Version 3.5.1
  based on "https://github.com/mjstealey/rstudio"

%environment
  RSTUDIO_VERSION=1.1.463
  R_BASE_VERSION=3.5.1
  LC_ALL=en_US.UTF-8
  LANG=en_US.UTF-8

%post
  export RSTUDIO_VERSION=1.1.463
  apt-get update
  apt-get install -y \
    wget \
    gdebi-core \
    libxslt1-dev \
    qt5-default \
    mesa-utils \
    libgl1-mesa-glx \
    libgl1-mesa-dev \
    libxt6 \
    openssh-client

  R -e "install.packages('caTools')" #needed in rstudio

  wget \
    --no-verbose \
     "https://download1.rstudio.org/rstudio-xenial-${RSTUDIO_VERSION}-amd64.deb"

  gdebi -n rstudio-xenial-${RSTUDIO_VERSION}-amd64.deb
  rm -f rstudio-xenial-${RSTUDIO_VERSION}-amd64.deb
  rm -rf /var/lib/apt/lists/*

%apprun R
  exec R "${@}"

%apprun Rscript
  exec Rscript "${@}"

%apprun rstudio
  exec rstudio "${@}"

%runscript
  exec "${@}"

%test
  exec R --version
