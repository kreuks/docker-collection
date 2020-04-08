FROM ubuntu:bionic
ARG AIRFLOW_HOME=/usr/local/airflow

ENV PATH "/opt/conda/envs/airflow/bin:/opt/conda/bin:$PATH"
ENV LANG C.UTF-8

RUN apt-get update -yqq \
    && apt-get install -yqq \
        apt-utils \
        build-essential \
        postgresql-client \
        curl \
        vim \
        wget \
        libpq-dev \
        docker.io

RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh \
    && /bin/bash ~/miniconda.sh -b -p /opt/conda \
    && rm ~/miniconda.sh \
    && /opt/conda/bin/conda clean -tipsy \
    && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh

COPY airflow/environment.yml ${AIRFLOW_HOME}/

RUN conda env update -f ${AIRFLOW_HOME}/environment.yml

RUN curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" \
    -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose
