FROM alpine:3.6

ENV FAIRCOIN_REV=2ce78b76
ENV FAIRCOIN_SUM=ff1d7bf569d1eadf4cc27c8d5aac6f03dd9857e8afbeabba9ab5e320a8f48e82

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
      libevent \
      libevent-dev \
      libtool \
      make \
      openssl \
      openssl-dev \
      pkgconf \
      zeromq \
      zeromq-dev \
 && export FAIRCOIN_TGZ=${FAIRCOIN_REV}.tar.gz FAIRCOIN_SRC=faircoin-faircoin-${FAIRCOIN_REV:0:7} \
 && wget -t 0 -O $FAIRCOIN_TGZ https://api.github.com/repos/faircoin/faircoin/tarball/$FAIRCOIN_REV \
 && sha256sum $FAIRCOIN_TGZ | grep -Eq $FAIRCOIN_SUM \
 && tar -xz -f $FAIRCOIN_TGZ \
 && ( \
      cd $FAIRCOIN_SRC \
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
 && rm -fr $FAIRCOIN_TGZ $FAIRCOIN_SRC \
 && apk --no-cache del \
      autoconf \
      automake \
      boost-dev \
      db-dev \
      g++ \
      libevent-dev \
      libtool \
      make \
      openssl-dev \
      pkgconf \
      zeromq-dev

RUN mkdir /root/.faircoin-beta
WORKDIR /root/.faircoin-beta

EXPOSE 40404
ENTRYPOINT ["faircoind", "-rpcallowip=0.0.0.0/0"]
