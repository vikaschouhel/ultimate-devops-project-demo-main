# Copyright The OpenTelemetry Authors
# SPDX-License-Identifier: Apache-2.0

FROM bitnami/kafka:3.7.0

USER root

ARG OTEL_JAVA_AGENT_VERSION

RUN curl -L -o /tmp/opentelemetry-javaagent.jar https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v${OTEL_JAVA_AGENT_VERSION}/opentelemetry-javaagent.jar

ENV KAFKA_CFG_NODE_ID=1
ENV KAFKA_CFG_PROCESS_ROLES=controller,broker
ENV KAFKA_CFG_CONTROLLER_QUORUM_VOTERS=1@localhost:9093
ENV KAFKA_CFG_LISTENERS=PLAINTEXT://:9092,CONTROLLER://:9093
ENV KAFKA_CFG_CONTROLLER_LISTENER_NAMES=CONTROLLER
ENV KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP=PLAINTEXT:PLAINTEXT,CONTROLLER:PLAINTEXT
ENV KAFKA_KRAFT_CLUSTER_ID=ckjPoprWQzOf0-FuNkGfFQ
ENV KAFKA_CFG_AUTO_CREATE_TOPICS_ENABLE=true
ENV KAFKA_CFG_OFFSETS_TOPIC_REPLICATION_FACTOR=1
ENV KAFKA_CFG_TRANSACTION_STATE_LOG_REPLICATION_FACTOR=1
ENV KAFKA_OPTS="-javaagent:/tmp/opentelemetry-javaagent.jar -Dotel.jmx.target.system=kafka-broker"

# Kafka starts automatically in this image
