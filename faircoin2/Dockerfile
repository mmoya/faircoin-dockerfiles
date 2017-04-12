FROM debian:9

COPY dpkg-no-doc /etc/dpkg/dpkg.cfg.d/01_nodoc

RUN apt-get update \
 && apt-get -Vy --no-install-recommends install \
      autoconf \
      automake \
      build-essential \
      ca-certificates \
      libboost-filesystem-dev \
      libboost-program-options-dev \
      libboost-system-dev \
      libboost-thread-dev \
      libdb++-dev \
      libevent-dev \
      libssl-dev \
      pkg-config \
      libtool \
      wget \
 && wget -c https://github.com/faircoin/faircoin2/archive/master.tar.gz \
 && tar xfz master.tar.gz \
 && ( \
      cd /faircoin2-master \
 &&   ./autogen.sh \
 &&   ./configure \
         --disable-bench \
         --disable-tests \
         --disable-wallet \
         --disable-zmq \
         --without-fasito \
 &&   make -j`nproc` \
 &&   make install \
 &&   strip /usr/local/bin/* \
    ) \
 && rm -fr master.tar.gz faircoin2-master \
 && apt-mark manual \
      libevent-2.0-5 \
      libevent-pthreads-2.0-5 \
      libboost-chrono1.62.0 \
      libboost-filesystem1.62.0 \
      libboost-program-options1.62.0 \
      libboost-system1.62.0 \
      libboost-thread1.62.0 \
 && apt-get -Vy purge \
      autoconf \
      automake \
      build-essential \
      libboost-filesystem-dev \
      libboost-program-options-dev \
      libboost-system-dev \
      libboost-thread-dev \
      libdb++-dev \
      libevent-dev \
      libssl-dev \
      pkg-config \
      libtool \
      wget \
 && apt-get -y --purge autoremove \
 && rm -fr /var/lib/apt/lists

RUN mkdir /faircoin2
WORKDIR /faircoin2

EXPOSE 40404
ENTRYPOINT ["faircoind", "-datadir=/faircoin2", "-rpcallowip=0.0.0.0/0"]
