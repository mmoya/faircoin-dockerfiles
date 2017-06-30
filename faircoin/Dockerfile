FROM alpine:3.6

RUN apk --no-cache add \
      autoconf \
      automake \
      boost \
      boost-dev \
      boost-program_options \
      ca-certificates \
      db \
      db-dev \
      g++ \
      git \
      libevent \
      libevent-dev \
      libtool \
      make \
      openssl \
      openssl-dev \
      pkgconf \
      zeromq \
      zeromq-dev \
 && git clone --depth=1 https://github.com/faircoin/faircoin \
 && ( \
      cd faircoin \
 &&   ./autogen.sh \
 &&   ./configure \
         --disable-bench \
         --disable-tests \
         --disable-wallet \
         --with-incompatible-bdb \
         --without-fasito \
         --without-libs \
 &&   make -j2 \
 &&   make install \
 &&   strip /usr/local/bin/* \
    ) \
 && rm -fr faircoin \
 && apk --no-cache del \
      autoconf \
      automake \
      boost-dev \
      db-dev \
      g++ \
      git \
      libevent-dev \
      libtool \
      make \
      openssl-dev \
      pkgconf \
      zeromq-dev

RUN mkdir /root/.faircoin2
WORKDIR /root/.faircoin2

EXPOSE 40404
ENTRYPOINT ["faircoind", "-rpcallowip=0.0.0.0/0"]
