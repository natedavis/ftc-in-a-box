FROM ubuntu:16.04
LABEL Description="This image is a clean build of feathercoind from a github branch"

RUN apt-get update
RUN apt-get install --yes software-properties-common
RUN add-apt-repository --yes ppa:bitcoin/bitcoin

RUN apt-get update && \
    apt-get install -y build-essential libtool autotools-dev autoconf libssl-dev git-core libboost-all-dev libdb4.8-dev libdb4.8++-dev libminiupnpc-dev nano pkg-config && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git clone https://github.com/FeatherCoin/Feathercoin.git /opt/feathercoin

RUN cd /opt/feathercoin && \
    git checkout 0.9.6.2 && \
    ./autogen.sh && \
    ./configure --with-miniupnpc --enable-upnp-default --disable-tests --without-gui --without-qrcode
    
RUN cd /opt/feathercoin && \
    make -j2

RUN cp /opt/feathercoin/src/feathercoind /usr/local/bin/ && \
    cp /opt/feathercoin/src/feathercoin-cli /usr/local/bin/

RUN groupadd -r feathercoin && useradd -r -m -g feathercoin feathercoin
ENV FEATHERCOIN_DATA /data
RUN mkdir $FEATHERCOIN_DATA
ADD . /data
RUN chown -R feathercoin:feathercoin $FEATHERCOIN_DATA
RUN ln -s $FEATHERCOIN_DATA /home/feathercoin/.feathercoin
USER root
VOLUME /data
WORKDIR /data
EXPOSE 19001 19011
CMD ["make start"]