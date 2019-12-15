# docker-miniconda

Docker container with a bootstrapped installation of Miniconda that is ready to use.

The Miniconda distribution is installed into the `/opt/conda` folder and ensures that the default user has the conda command in their path.


## Usage

You can download and run this image using the following commands:

```bash
docker pull ncarxdev/miniconda
docker run -i -t ncarxdev/miniconda /bin/bash
```

or specify Python version

```bash
docker pull ncarxdev/miniconda:[TAG]
```

where `TAG` is one of `[3.6, 3.7, 3.8]`
