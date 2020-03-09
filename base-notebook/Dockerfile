FROM --platform=$BUILDPLATFORM bnxtipro/base-conda AS base
LABEL MAINTAINER="Manuel Gonzalez Blanco <manuel.gonzalez.freelancer@gmail.com>"
LABEL stage=base
ARG TARGETPLATFORM
ARG BUILDPLATFORM
ENV NB_USER=jovyan
ENV HOME=/home/${NB_USER}
ENV PYTHONDONTWRITEBYTECODE=true
ENV CONDA_DIR=/opt/conda
WORKDIR ${HOME}/labs
RUN set ex; \
    mkdir -p ${HOME}/labs && \
    sh -c "source ${CONDA_DIR}/bin/activate >> /dev/null " && conda init && \
    sh -c "source ${HOME}/.bashrc" && \
    conda config --system --prepend channels conda-forge && \
    conda config --system --set auto_update_conda true && \
    conda config --system --set show_channel_urls true &&  \
    conda install --freeze-installed -c conda-forge --yes nodejs nomkl pypy3.6 jupyterlab \
    ipykernel ipywidgets ipympl jupyterhub  && \
    conda update --all && \
    conda clean -afyp && \
    jupyter lab --generate-config  \
    && find ${CONDA_DIR} -follow -type f -name '*.a' -delete \
    && find ${CONDA_DIR} -follow -type f -name '*.pyc' -delete \
    && find ${CONDA_DIR} -follow -type f -name '*.js.map' -delete && \
    npm cache clean --force && \
    rm -rf ${CONDA_DIR}/share/jupyter/lab/staging && \
    rm -rf ${HOME}/.cache/yarn
CMD ["jupyter","lab"]
COPY start.sh start-notebook.sh start-singleuser.sh /usr/local/bin/
COPY jupyter_notebook_config.py /etc/jupyter/ 
COPY nbimport.py /etc/jupyter/  
EXPOSE 8888