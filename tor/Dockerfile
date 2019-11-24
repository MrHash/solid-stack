FROM alpine:latest

RUN apk update
RUN apk add tor

RUN echo "Log notice stdout" >> /etc/torrc
RUN echo "SocksPort 172.72.1.10:9250" >> /etc/torrc
RUN echo "HiddenServiceDir /var/lib/tor/bitcoin-service/" >> /etc/torrc
RUN echo "HiddenServiceVersion 2" >> /etc/torrc
RUN echo "HiddenServicePort 18888 172.72.1.20:18888" >> /etc/torrc

CMD tor -f /etc/torrc