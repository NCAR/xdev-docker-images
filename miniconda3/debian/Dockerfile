FROM debian:buster-slim

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8 \
    PATH=/opt/conda/bin:$PATH \
    CONDA_DIR=/opt/conda

ARG PYTHON_VERSION=3.7

RUN echo $PYTHON_VERSION
RUN echo "Installing Apt-get packages..." && \
    apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates libglib2.0-0 libxext6 libsm6 libxrender1 git mercurial nano vim subversion && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN echo "Installing Miniconda..." && \
    wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo ". ${CONDA_DIR}/etc/profile.d/conda.sh ; conda activate base" > /etc/profile.d/init_conda.sh && \
    echo "conda activate base" >> ~/.bashrc && \
    conda init bash && \
    find /opt/conda/ -follow -type f -name '*.a' -delete && \
    find /opt/conda/ -follow -type f -name '*.js.map' -delete && \
    /opt/conda/bin/conda config --set always_yes true --set changeps1 false && \
    /opt/conda/bin/conda config --add channels conda-forge && \
    /opt/conda/bin/conda update --all

RUN conda update -n base -c conda-forge conda

RUN echo "Installing Packages..." && \
    conda install -c conda-forge python=${PYTHON_VERSION} dask xarray netcdf4 zarr matplotlib pytest pytest-xdist pytest-cov scipy pooch numba intake && \
    conda clean -aftipsy

RUN conda list

CMD [ "/bin/bash" ]
