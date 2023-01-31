FROM ubuntu:20.04


ENV CONFLUENT_CLOUD_EMAIL=<your-confluent-email>
ENV CONFLUENT_CLOUD_PASSWORD=<your-confluent-password>
ENV CONFLUENT_CLOUD_ENVIRONMENT_ID=<your-env-id>
ENV CONFLUENT_CLOUD_API_KEY=<your-cluster-key>
ENV CONFLUENT_CLOUD_API_SECRET=<your-cluster-key-password>
ENV CONFLUENT_CLOUD_CLUSTER_ID=<your-cluster-id>

RUN apt-get update \
    && apt-get install -y curl \
    && curl -sL --http1.1 https://cnfl.io/cli | sh -s -- v2.29.0 \
    && export PATH=$(pwd)/bin:$PATH \
    && confluent login --save \
    && confluent environment use $CONFLUENT_CLOUD_ENVIRONMENT_ID \
    && confluent api-key store $CONFLUENT_CLOUD_API_KEY $CONFLUENT_CLOUD_API_SECRET --resource $CONFLUENT_CLOUD_CLUSTER_ID \
    && confluent api-key use $CONFLUENT_CLOUD_API_KEY --resource $CONFLUENT_CLOUD_CLUSTER_ID \
    && confluent kafka cluster use $CONFLUENT_CLOUD_CLUSTER_ID
