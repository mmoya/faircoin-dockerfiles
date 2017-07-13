FROM alpine:3.6

ENV FAIRCOIN_REV=a2ac75a1
ENV FAIRCOIN_SUM=5e000e86136ed530e67d738aff9d77941fafd8a263e904b3e035c034f925dd7b

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
