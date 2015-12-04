# Copyright (c) Jupyter Development Team.
FROM jupyter/minimal-notebook

MAINTAINER Jupyter Project <jupyter@googlegroups.com>

USER jovyan

# Install Python 3 packages
RUN conda install --yes \
    'ipywidgets=4.0*' \
    'pandas=0.16*' \
    'matplotlib=1.4*' \
    'scipy=0.15*' \
    'seaborn=0.6*' \
    'scikit-learn=0.16*' \
    'scikit-image=0.11*' \
    'sympy=0.7*' \
    'cython=0.22*' \
    'patsy=0.3*' \
    'statsmodels=0.6*' \
    'cloudpickle=0.1*' \
    'dill=0.2*' \
    'numba=0.20*' \
    'bokeh=0.9*' \
    && conda clean -yt

# Install Python 2 packages
RUN conda create -p $CONDA_DIR/envs/python2 python=2.7 \
    'ipython=4.0*' \
    'ipywidgets=4.0*' \
    'pandas=0.16*' \
    'matplotlib=1.4*' \
    'scipy=0.15*' \
    'seaborn=0.6*' \
    'scikit-learn=0.16*' \
    'scikit-image=0.11*' \
    'sympy=0.7*' \
    'cython=0.22*' \
    'patsy=0.3*' \
    'statsmodels=0.6*' \
    'cloudpickle=0.1*' \
    'dill=0.2*' \
    'numba=0.20*' \
    'bokeh=0.9*' \
    pyzmq \
    && conda clean -yt

RUN pip install xlrd bash_kernel elasticsearch arrow pyyaml py-dateutil
RUN python -c "import bokeh.sampledata; bokeh.sampledata.download()"

RUN pip install bash_kernel
RUN python -m bash_kernel.install

USER root

# Migu 1M
RUN wget "http://sourceforge.jp/frs/redir.php?m=iij&f=%2Fmix-mplus-ipa%2F59022%2Fmigu-1m-20130617.zip" -P /tmp \
    && unzip "/tmp/redir.php?m=iij&f=%2Fmix-mplus-ipa%2F59022%2Fmigu-1m-20130617.zip" -d /tmp \
    && mkdir -p /usr/share/fonts/truetype/migu \
    && mv /tmp/migu-1m-20130617/*ttf /usr/share/fonts/truetype/migu \
    && rm -r /tmp/*

# IPA
RUN wget http://dl.ipafont.ipa.go.jp/IPAexfont/ipaexg00301.zip -P /tmp \
    && unzip /tmp/ipaexg00301.zip -d /tmp \
    && mkdir -p /usr/share/fonts/truetype/ipa \
    && mv /tmp/ipaexg00301/ipaexg.ttf /usr/share/fonts/truetype/ipa \
    && rm -r /tmp/*
    
# Install Python 2 kernel spec globally to avoid permission problems when NB_UID
# switching at runtime.
RUN $CONDA_DIR/envs/python2/bin/python \
    $CONDA_DIR/envs/python2/bin/ipython \
    kernelspec install-self
