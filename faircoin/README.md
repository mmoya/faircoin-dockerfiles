# FairCoin Relay Node

This image runs a [FairCoin][1] Relay Node (ie: without CVN or wallet support).

# Running

```shell
mkdir faircoin2
docker run --name faircoin -p 40404:40404 -v $PWD/faircoin2:/faircoin2 mmoya/faircoin
```

# Querying the server

```shell
docker exec faircoin faircoin-cli -datadir=/faircoin2 getpeerinfo
```

# Building the image yourself

```shell
git clone https://gitlab.com/mmoya/dockerfiles
cd dockerfiles/faircoin
make
```

[1]: https://chain.fair-coin.org/download/FairCoin2-white-paper-V1.1.pdf
