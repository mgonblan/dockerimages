FROM bnxtipro/minimal-notebook:latest AS minimal
LABEL MAINTAINER="Manuel Gonzalez Blanco <manuel.gonzalez.freelancer@gmail.com>"
LABEL stage="minimal"
RUN conda install --yes --freeze-installed -c r r-pbdzmq r r-irkernel && \
    conda clean -afyp