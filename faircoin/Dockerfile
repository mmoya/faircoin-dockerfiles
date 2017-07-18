FROM alpine:3.6

ENV FAIRCOIN_VER=2.0.0
ENV FAIRCOIN_SUM=aa1cacf9f489d8f136e6b3d4350a34706c54cd4f16c1468abf6b85147af0b7e2

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
 && export FAIRCOIN_TGZ=v${FAIRCOIN_VER}.tar.gz FAIRCOIN_SRC=faircoin-${FAIRCOIN_VER} \
 && wget -t 0 https://github.com/faircoin/faircoin/archive/$FAIRCOIN_TGZ \
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

RUN mkdir /root/.faircoin2
WORKDIR /root/.faircoin2

EXPOSE 40404
ENTRYPOINT ["faircoind", "-rpcallowip=0.0.0.0/0"]
