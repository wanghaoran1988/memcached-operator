FROM quay.io/app-sre/boilerplate:image-v2.2.0 AS builder

RUN mkdir -p /workdir
WORKDIR /workdir
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN make go-build



FROM registry.access.redhat.com/ubi8/ubi-minimal:latest

ENV USER_UID=1001 \
    USER_NAME=memcached-operator

WORKDIR /
COPY --from=builder /workdir/build/_output/bin/* /usr/local/bin/

USER 65532:65532

ENTRYPOINT ["/usr/local/bin/memcached-operator"]
