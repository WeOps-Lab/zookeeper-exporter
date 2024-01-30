#
# build container
#
FROM --platform=linux/amd64 golang:1.19-alpine as builder
WORKDIR /

COPY zookeeper_exporter_linux_amd64 /zookeeper_exporter_linux_amd64

RUN chmod +x /zookeeper_exporter_linux_amd64

EXPOSE     9141
ENTRYPOINT [ "/zookeeper_exporter_linux_amd64" ]
