FROM golang:1.9-alpine as hub-builder

RUN apk add --no-cache make bash git
RUN git clone https://github.com/github/hub.git -b v2.3.0-pre10 && \
    cd hub && ./script/build

FROM docker:17.05.0-ce-git


RUN apk add --no-cache nodejs make jq wget ca-certificates && \
    npm install -g @commitlint/cli @commitlint/config-conventional conventional-commits-parser semver && \
    wget -q https://storage.googleapis.com/kubernetes-helm/helm-v2.8.1-linux-amd64.tar.gz && \
    tar -xvf helm-v2.8.1-linux-amd64.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/ && \
    wget -q https://storage.googleapis.com/kubernetes-release/release/v1.9.0/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl

COPY --from=hub-builder /go/hub/bin/hub  /usr/local/bin/hub

ENV RUN_DOCKER=0
ARG WORKDIR=/workdir
RUN mkdir -p "${WORKDIR}"
WORKDIR /workdir
