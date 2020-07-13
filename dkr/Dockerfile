FROM ubuntu:bionic

RUN apt-get update && \
    apt-get install -y unzip wget libbz2-dev libsnappy-dev libncurses5-dev libreadline-dev && \
    apt-get clean -qy

ARG steemd_version="e87e96053066136ae83831be91d390a7/whaled_lm-0.4.1-x86_64-linux.tar.gz"
ENV steemd_version ${steemd_version}

ARG STEEM_SOURCE="https://gitlab.com/beyondbitcoin/whaleshares-chain/uploads/"
ENV STEEM_SOURCE ${STEEM_SOURCE}

ARG WALLET_SOURCE="https://whaleshares.info/wls-download/cli_wallet-0.2.7-x86_64-linux.tar.gz"
ENV WALLET_SOURCE ${WALLET_SOURCE}

RUN cd /tmp && \
    echo " >>> Downloading whaleshares binary: ${STEEM_SOURCE}${steemd_version} ..." && \
    wget -O whaled.tar.gz "${STEEM_SOURCE}${steemd_version}" && \
    echo " >>> Untarring whaled.tar.gz ..." && \
    tar xvf whaled.tar.gz && \
    echo " >>> Installing whaled ..." && \
    cp -v whaled /usr/bin/whaled && \
    echo " >>> Downloading cli_wallet binary: ${WALLET_SOURCE} ..." && \
    wget -O wallet.tar.gz "${WALLET_SOURCE}" && \
    echo " >>> Untarring wallet.tar.gz ..." && \
    tar xvf wallet.tar.gz && \
    echo " >>> Installing cli_wallet ..." && \
    cp -v cli_wallet /usr/bin/cli_wallet && \
    echo "Cleaning up ..." && \
    rm -rvf whaled whaled.tar.gz cli_wallet wallet.tar.gz

RUN echo "Linking libreadline.so.7.0 to libreadline.so.6 and libreadline.so.6.0" && \
    ln -v /lib/x86_64-linux-gnu/libreadline.so.7.0 /lib/x86_64-linux-gnu/libreadline.so.6 && \
    ln -v /lib/x86_64-linux-gnu/libreadline.so.7.0 /lib/x86_64-linux-gnu/libreadline.so.6.0

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


