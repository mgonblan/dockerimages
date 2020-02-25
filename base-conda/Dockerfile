FROM --platform=$BUILDPLATFORM container-registry.oracle.com/os/oraclelinux:8-slim AS builder
LABEL MAINTAINER="Manuel Gonzalez Blanco <manuel.gonzalez.freelancer@gmail.com>"
LABEL stage=builder
ARG TARGETPLATFORM
ARG BUILDPLATFORM
ARG NB_USER="jovyan"
ARG NB_GROUP="conda"
ARG SHELL=/bin/zsh
ARG CONDA_DIR=/opt/conda
ENV PATH=$CONDA_DIR/bin:$PATH
RUN microdnf update -y --enablerepo ol8_baseos_latest && \
   microdnf install -y shadow-utils zsh && \
   microdnf clean all && \
   groupadd ${NB_GROUP} && \   
   useradd -G ${NB_GROUP} -s ${SHELL} ${NB_USER} && \
   cd /tmp && \
   curl -sSO https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
   chmod u+x /tmp/Miniconda3-latest-Linux-x86_64.sh && \
   /tmp/Miniconda3-latest-Linux-x86_64.sh -b -p ${CONDA_DIR} && \
   rm /tmp/Miniconda3-latest-Linux-x86_64.sh && \
   chgrp -R ${NB_GROUP} ${CONDA_DIR} && \
   chmod 770 -R ${CONDA_DIR}
USER ${NB_USER}
RUN  source ${CONDA_DIR}/bin/activate &>/dev/null && \
    conda init zsh