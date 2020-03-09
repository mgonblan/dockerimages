FROM buildpack-deps:latest AS gitter
LABEL stage="gitter"
RUN set ex; git clone https://github.com/PAIR-code/facets.git
FROM bnxtipro/minimal-notebook:latest AS minimal
LABEL MAINTAINER="Manuel Gonzalez Blanco <manuel.gonzalez.freelancer@gmail.com>"
LABEL stage="minimal"
RUN set ex; \
    conda install --freeze-installed --quiet --yes \
    nomkl dask \
    beautifulsoup4 bokeh \
    numpy scipy matplotlib pandas sympy nose && \
    jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    pip install dask_labextension && \
    jupyter labextension install --no-build install dask-labextension && \
    jupyter lab build --minimize=False --debug=true && \
    conda clean -afyp && \
    npm cache clean --force && \
    rm -rf /opt/conda/share/jupyter/lab/staging && \
    rm -rf $HOME/.cache/yarn && \
    rm -rf $HOME/.node-gyp    