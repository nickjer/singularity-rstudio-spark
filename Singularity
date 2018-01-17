BootStrap: docker
From: ubuntu:16.04

%labels
  Maintainer Jeremy Nicklas
  R_Version 3.4.3
  RStudio_Version 1.1.383
  Spark_Version 2.2.1
  Hadoop_Version 2.7

%post
  # Software versions
  export R_VERSION=3.4.3
  export RSTUDIO_VERSION=1.1.383
  export SPARK_VERSION=2.2.1
  export HADOOP_VERSION=2.7

  # Get dependencies
  apt-get update
  apt-get install -y --no-install-recommends \
    apt-transport-https \
    wget \
    ca-certificates \
    locales

  # Configure default locale
  echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
  locale-gen en_US.utf8
  /usr/sbin/update-locale LANG=en_US.UTF-8
  export LC_ALL=en_US.UTF-8
  export LANG=en_US.UTF-8

  # Install R
  echo "deb http://cran.r-project.org/bin/linux/ubuntu xenial/" > /etc/apt/sources.list.d/r.list
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
  apt-get update
  apt-get install -y --no-install-recommends \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    r-base=${R_VERSION}* \
    r-base-dev=${R_VERSION}* \
    r-recommended=${R_VERSION}*

  # Install RStudio Server
  apt-get update
  apt-get install -y --no-install-recommends \
    gdebi-core
  wget --no-verbose "https://download2.rstudio.org/rstudio-server-${RSTUDIO_VERSION}-amd64.deb" -O rstudio-server.deb
  gdebi -n rstudio-server.deb
  rm -f rstudio-server.deb

  # Install Spark
  apt-get update
  apt-get install -y --no-install-recommends \
    openjdk-8-jre
  mkdir -p /opt/spark
  wget --no-verbose "http://mirror.cc.columbia.edu/pub/software/apache/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" -O - | tar xz --strip-components=1 -C /opt/spark

  # Install sparklyr: R interface for Apache Spark
  Rscript -e " \
    withCallingHandlers( \
      install.packages( \
        c('ggplot2','sparklyr'), \
        repo = 'https://cran.rstudio.com/' \
      ), \
      warning = function(w) stop(w) \
    ) \
  "

  # Clean up
  rm -rf /var/lib/apt/lists/*

%environment
  export SPARK_HOME=/opt/spark
  export PATH=${SPARK_HOME}/bin:/usr/lib/rstudio-server/bin${PATH:+:${PATH}}
