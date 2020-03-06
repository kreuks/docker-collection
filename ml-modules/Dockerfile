FROM ubuntu:xenial

ARG KAFKA_HOME=/opt/kafka

ENV PATH "/opt/spark/bin:/opt/conda/bin:$PATH"
ENV SPARK_VERSION=2.4.4
ENV HADOOP_VERSION=2.7
ENV LANG C.UTF-8

RUN apt-get update -yqq \
    && apt-get install -yqq \
        apt-utils \
        build-essential \
        zip \
        vim \
        wget \
        docker.io

RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.5.12-Linux-x86_64.sh -O ~/miniconda.sh \
    && /bin/bash ~/miniconda.sh -b -p /opt/conda \
    && rm ~/miniconda.sh \
    && /opt/conda/bin/conda clean -tipsy \
    && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh

RUN wget --quiet https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
    && tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
    && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark \
    && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

RUN mkdir $KAFKA_HOME \
    && wget --quiet https://downloads.apache.org/kafka/2.4.0/kafka_2.12-2.4.0.tgz -O $KAFKA_HOME/kafka.tgz \
    && tar xvf $KAFKA_HOME/kafka.tgz -C $KAFKA_HOME/ \
    && mv $KAFKA_HOME/kafka_2.12-2.4.0/* $KAFKA_HOME \
    && rm -r $KAFKA_HOME/kafka_2.12-2.4.0/

RUN apt-get install -yqq openjdk-8-jdk

