FROM bnxtipro/base-notebook:latest AS base
FROM bnxtipro/miniconda:latest AS build
# Minimal notebook for Jupyter
LABEL MAINTAINER="Manuel Gonzalez Blanco <manuel.gonzalez.freelancer@gmail.com>"
LABEL stage=base
ENV NB_USER="jovyan"
ENV NB_GROUP="conda"
ENV CONDA_DIR=/opt/conda
RUN conda config --system --prepend channels conda-forge && \
    conda config --system --set auto_update_conda true && \
    conda config --system --set show_channel_urls true && \
    conda install  --freeze-installed -c conda-forge --yes nomkl pypy3.6 \
    dask numpy \
    scipy matplotlib Ipython sympy pandas jupyterlab jupyterhub \
    ipywidgets ipyparallel  && \
    conda update --all && \
    conda clean -afyp && \
    jupyter notebook --generate-config \
    && ipcluster nbextension enable \
    && find ${CONDA_DIR} -follow -type f -name '*.a' -delete \
    && find ${CONDA_DIR} -follow -type f -name '*.pyc' -delete \
    && find ${CONDA_DIR} -follow -type f -name '*.js.map' -delete \
    && find /opt/conda/lib/python*/site-packages/bokeh/server/static -follow -type f -name '*.js' ! -name '*.min.js' -delete && \
    npm cache clean --force && \
    rm -rf ${CONDA_DIR}/share/jupyter/lab/staging && \
    rm -rf /home/${NB_USER}/.cache/yarn
# Copy local files as late as possible to avoid cache busting
EXPOSE 8888
CMD ["start-notebook.sh"]
COPY --from=base /usr/local/bin/start.sh /usr/local/bin/
COPY --from=base /usr/local/bin/start-notebook.sh /usr/local/bin/
COPY --from=base /usr/local/bin/start-singleuser.sh /usr/local/bin/
COPY --from=base /etc/jupyter/jupyter_notebook_config.py /etc/jupyter/
USER ${NB_USER}