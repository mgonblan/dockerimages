FROM bnxtipro/base-notebook:latest AS base
# Minimal notebook for Jupyter
LABEL MAINTAINER="Manuel Gonzalez Blanco <manuel.gonzalez.freelancer@gmail.com>"
LABEL stage="base"
# Installs additional extensions to jupyter notebook
RUN set ex; \
    conda install --yes --freeze-installed dask nomkl nbcommands \
    ipympl && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
jupyter labextension install jupyter-matplotlib --no-build && \
jupyter lab build --dev-build=False --minimize=False && \
conda clean -afyp  \
&& find /opt/conda -follow -type f -name '*.a' -delete \
    && find /opt/conda -follow -type f -name '*.pyc' -delete \
    && find /opt/conda -follow -type f -name '*.js.map' -delete && \
    find /opt/conda/lib/python*/site-packages/bokeh/server/static -follow -type f -name '*.js' ! -name '*.min.js' -delete && \
    npm cache clean --force && \
    rm -rf /opt/conda/share/jupyter/lab/staging && \
    rm -rf ${HOME}/.cache/yarn