FROM bnxtipro/miniconda:latest AS base
LABEL MAINTAINER="Manuel Gonzalez Blanco <manuel.gonzalez.freelancer@gmail.com>"
LABEL stage=base
RUN conda config --system --prepend channels conda-forge && \
    conda config --system --set auto_update_conda true && \
    conda config --system --set show_channel_urls true && \
    conda install  --freeze-installed -c conda-forge --yes nomkl pypy3.6 jupyterlab jupyterhub  && \
    conda update --all && \
    conda clean -afyp \
    && find /opt/conda/ -follow -type f -name '*.a' -delete \
    && find /opt/conda/ -follow -type f -name '*.pyc' -delete \
    && find /opt/conda/ -follow -type f -name '*.js.map' -delete && \
    npm cache clean --force && \
    jupyter notebook --generate-config && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf /home/$NB_USER/.cache/yarn 
# Copy local files as late as possible to avoid cache busting
EXPOSE 8888
CMD ["start-notebook.sh"]
COPY start.sh /usr/local/bin/
COPY start-notebook.sh /usr/local/bin/
COPY start-singleuser.sh /usr/local/bin/
COPY jupyter_notebook_config.py /etc/jupyter/
