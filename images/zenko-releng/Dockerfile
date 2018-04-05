FROM docker:17.05.0-ce-git

ENV GOPATH /go

RUN apk add --no-cache nodejs make jq wget ca-certificates go && \
    npm install -g @commitlint/cli @commitlint/config-conventional conventional-commits-parser semver && \
    go get -u github.com/aktau/github-release && \
    wget -q https://storage.googleapis.com/kubernetes-helm/helm-v2.8.1-linux-amd64.tar.gz && \
    tar -xvf helm-v2.8.1-linux-amd64.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/ && \
    wget -q https://storage.googleapis.com/kubernetes-release/release/v1.9.0/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl && \

ENV PATH $GOPATH/bin:$PATH

ENV RUN_DOCKER=0
ARG WORKDIR=/workdir
RUN mkdir -p "${WORKDIR}"
WORKDIR /workdir
