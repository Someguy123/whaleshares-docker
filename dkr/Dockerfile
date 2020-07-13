FROM ubuntu:bionic


ARG steemd_version="e87e96053066136ae83831be91d390a7/whaled_lm-0.4.1-x86_64-linux.tar.gz"
ENV steemd_version ${steemd_version}

ARG STEEM_SOURCE="https://gitlab.com/beyondbitcoin/whaleshares-chain/uploads/"
ENV STEEM_SOURCE ${STEEM_SOURCE}

RUN apt-get update && \
    apt-get install -y unzip wget libbz2-dev libsnappy-dev libncurses5-dev libreadline-dev && \
    apt-get clean -qy

RUN cd /tmp && \
    echo " >>> Downloading whaleshares binary: ${STEEM_SOURCE}${steemd_version} ..." && \
    wget -O whaled.tar.gz "${STEEM_SOURCE}${steemd_version}" && \
    echo " >>> Untarring whaled.tar.gz ..." && \
    tar xvf whaled.tar.gz && \
    echo " >>> Installing whaled ..." && \
    cp -v whaled /usr/bin/whaled && \
    echo "Cleaning up ..." && \
    rm -rvf whaled whaled.tar.gz

# P2P (seed) port
EXPOSE 1776
# RPC ports
EXPOSE 5000
EXPOSE 8090
EXPOSE 8091

VOLUME /steem
WORKDIR /steem

ARG STEEMD_BIN="/usr/bin/whaled"
ENV STEEMD_BIN ${STEEMD_BIN}

RUN echo "Please configure me! You need to mount a data directory onto /steem of this container to it to function correctly. (if you're using Steem-in-a-box most of this is handled automatically)"
CMD ["sh", "-c", "${STEEMD_BIN}"]


