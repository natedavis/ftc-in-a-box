FROM ubuntu:16.04
LABEL Description="This image is a build of the FTC explorer"

RUN apt-get update
RUN apt-get install --yes software-properties-common
RUN add-apt-repository --yes ppa:bitcoin/bitcoin

RUN apt-get update && \
    apt-get install -y curl sudo nano net-tools build-essential git-core python telnet iputils-ping libkrb5-dev && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash - && \
	apt-get install -y nodejs

RUN git clone https://github.com/iquidus/explorer.git /opt/iquidus

RUN cd /opt/iquidus && \
    git checkout master && \
    npm install --production

COPY settings.json /opt/iquidus/settings.json

USER root
EXPOSE 3001
CMD ["/bin/bash"]