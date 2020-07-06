FROM ubuntu:xenial

ENV H2O_HOME=/opt/h2o
ENV LANG C.UTF-8

RUN apt-get update -yqq \
    && apt-get install -yqq \
        apt-utils \
        build-essential \
        vim \
        wget \
        zip

WORKDIR /opt

RUN apt-get update && \
    apt-get install -y openjdk-8-jdk && \
    apt-get clean;

RUN wget --quiet https://h2o-release.s3.amazonaws.com/h2o/rel-yu/2/h2o-3.30.0.4.zip -O /opt/h2o.zip \
    && unzip h2o.zip \
    && mv h2o-3.30.0.4 h2o \
    && rm -r h2o/bindings h2o/R
