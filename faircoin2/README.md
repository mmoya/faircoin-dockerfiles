# FairCoin2 Relay Node

This image runs a [FairCoin2][1] Relay Node (ie: no CVN or wallet support).

# Running

```shell
mkdir faircoin2
docker run --name faircoin2 -p 40404:40404 -v $PWD/faircoin2:/faircoin2 mmoya/faircoin2
```

# Querying the server

```shell
docker exec faircoin2 faircoin-cli -datadir=/faircoin2 getpeerinfo
```

# Building the image yourself

```shell
git clone https://gitlab.com/mmoya/dockerfiles
cd dockerfiles/faircoin2
make
```

[1]: https://chain.fair-coin.org/download/FairCoin2-white-paper-V1.1.pdf
