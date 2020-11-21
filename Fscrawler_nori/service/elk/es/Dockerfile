ARG ELK_VERSION

FROM docker.elastic.co/elasticsearch/elasticsearch-oss:${ELK_VERSION}
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install --batch analysis-nori