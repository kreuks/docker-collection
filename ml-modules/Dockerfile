FROM ubuntu:xenial

ARG KAFKA_HOME=/opt/kafka
ARG SPARK_HOME=/opt/spark

ENV PATH "/opt/spark/bin:/opt/conda/bin:$PATH"
ENV SPARK_VERSION=3.0.0
ENV HADOOP_VERSION=2.7
ENV KAFKA_VERSION=2.4.0
ENV LANG C.UTF-8

RUN apt-get update -yqq \
    && apt-get install -yqq \
        apt-utils \
        build-essential \
        zip \
        vim \
        wget

RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.5.12-Linux-x86_64.sh -O ~/miniconda.sh \
    && /bin/bash ~/miniconda.sh -b -p /opt/conda \
    && rm ~/miniconda.sh \
    && /opt/conda/bin/conda clean -tipsy \
    && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh

WORKDIR /opt

RUN wget --quiet https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz -O spark.tgz \
    && tar -xvzf spark.tgz \
    && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark \
    && rm spark.tgz \
    && wget --quiet https://storage.googleapis.com/hadoop-lib/gcs/gcs-connector-hadoop2-latest.jar -O /opt/spark/jars/gcs-connector-hadoop2-latest.jar

RUN wget --quiet https://downloads.apache.org/kafka/${KAFKA_VERSION}/kafka_2.12-${KAFKA_VERSION}.tgz -O kafka.tgz \
    && tar -xzvf kafka.tgz \
    && mv kafka_2.12-${KAFKA_VERSION} kafka \
    && rm kafka.tgz

COPY ml-modules/connect-log4j.properties $KAFKA_HOME/config/

RUN conda install -y python==3.7.4 \
    && pip install confluent-kafka==1.3.0 \
    && pip install h2o==3.30.0.4 \
    && pip install numpy==1.17.0 \
    && pip install oss2==2.9.1 \
    && pip install --upgrade google-cloud-storage

RUN apt-get update -yqq && apt-get install -yqq openjdk-8-jdk
