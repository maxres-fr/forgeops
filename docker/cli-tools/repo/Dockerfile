FROM outillage/commitsar:latest
FROM debian:sid-slim
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y \
        && apt-get install --yes --no-install-recommends shellcheck \
                           make \
                           python3-minimal \
                           python3-pip \
                           python3-setuptools \
                           npm
COPY --from=0 /usr/local/bin/commitsar /usr/local/bin/commitsar
RUN mkdir -p /opt/workspace  && pip3 install yamllint
COPY . /opt/workspace
# TODO this should really only have tslint installed...
RUN cd /opt/workspace/cluster/pulumi && npm install --only=dev && rm -rf /opt/workspace/*
WORKDIR /opt/workspace
