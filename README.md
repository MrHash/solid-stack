# Solid Federation (TESTING ONLY)

## Docker install
```
root$ curl -sSL https://get.docker.com/ | sh
root$ apt-get install libffi-dev libssl-dev
root$ apt-get install -y python3 python3-pip
root$ python3 -m pip install docker-compose
root$ usermod -aG docker <your user> # eg. pi, odroid etc.
```

## Clone Repo
```
$ git clone https://github.com/MrHash/solid-stack.git
$ cd solid-stack
```

## Solid Tor
```
$ docker-compose up -d tor

# wait for bootstrap completion
$ docker-compose logs -f #(ctrl-c to exit logs)

# Test the Tor connection
$ curl --socks5 127.0.0.1:9250 --socks5-hostname 127.0.0.1:9250 -s https://check.torproject.org/ | cat | grep -m 1 Congratulations | xargs

# get your onion address
$ docker-compose exec tor cat /var/lib/tor/bitcoin-service/hostname
```

## Solid Bitcoin Regtest
```
$ docker-compose up -d bitcoin

# wait for chain sync

$ bin/solid bitcoin getnetworkinfo
```

## Destroy the stack
```
$ docker-compose down -v
```
