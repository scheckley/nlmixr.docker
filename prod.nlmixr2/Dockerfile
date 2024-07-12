FROM rocker/verse:latest

WORKDIR /usr/local/rstudio

RUN groupadd -g 1001 stephen && useradd -u 1001 -g stephen stephen
RUN mkdir /home/stephen

RUN apt-get clean all && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
      cmake \
      libbz2-dev \
      libcairo2-dev \
      libcurl4-openssl-dev \
      libgit2-dev \
      libglpk40 \
      libgmp-dev \
      libhdf5-dev \
      liblzma-dev \
      libmpc-dev \
      libmpfr-dev \
      libpng-dev \
      libssl-dev \
      libudunits2-dev \
      libxml2-dev \
      libxt-dev \
      xclip \
      zlib1g-dev \
   && \
   apt-get clean all && \
   apt-get purge && \
   rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER 1001

USER root

RUN mkdir -p /home/stephen/r-installation
RUN chown -R stephen:stephen /home/stephen/r-installation
COPY *.R *.sh /home/stephen/r-installation/

# Run all files ending with "sh"; then cleanup any apt installation remnants
RUN cd /home/stephen/r-installation/ && \
    chmod 755 *sh && \
    run-parts --exit-on-error --verbose --regex '.*sh' /home/stephen/r-installation && \
    apt-get clean all && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY examples /home/stephen/examples
