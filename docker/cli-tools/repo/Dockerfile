FROM debian:sid-slim
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y \
        && apt-get install --yes --no-install-recommends shellcheck \
                           make \
                           python3-minimal \
                           python3-pip \
                           python3-setuptools \
                           npm

RUN mkdir -p /opt/workspace  && pip3 install yamllint
COPY . /opt/workspace
RUN cd /opt/workspace/cluster/pulumi && npm install --only=dev
WORKDIR /opt/workspace

