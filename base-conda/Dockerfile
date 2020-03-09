FROM  --platform=$BUILDPLATFORM bnxtipro/alpine-glibc:latest AS builder
LABEL MAINTAINER="Manuel Gonzalez Blanco <manuel.gonzalez.freelancer@gmail.com>"
LABEL stage=builder
ARG TARGETPLATFORM
ARG BUILDPLATFORM
ARG NB_GROUP=conda
ARG NB_USER=jovyan
ARG CONDA_DIR=/opt/conda
ENV PATH=${CONDA_DIR}/bin:$PATH
RUN set -ex; \
   cd /tmp && \
case $BUILDPLATFORM in \
 linux/amd64) bp=Linux-x86_64 ;; \
 linux/ppc64le) bp=Linux-ppc64le ;; \
 esac && \
 wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-$bp.sh && \
 chmod u+x /tmp/Miniconda3-latest-$bp.sh && \
 /tmp/Miniconda3-latest-$bp.sh -b -p ${CONDA_DIR} && \
 rm -rf /tmp/* && \
     apk add --no-cache --upgrade xz xz-dev && \
    addgroup -S ${NB_GROUP} && \
    adduser -S ${NB_USER} --ingroup ${NB_GROUP} && \
    chgrp -R ${NB_GROUP} ${CONDA_DIR} && \
    chmod 770 -R ${CONDA_DIR}
USER ${NB_USER}