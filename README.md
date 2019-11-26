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

## Solid Init
```
$ docker-compose up -d

# wait for bootstrap completion
$ docker-compose logs -f tor #(ctrl-c to exit logs)

# Test the Tor connection
$ curl --socks5 127.0.0.1:9250 --socks5-hostname 127.0.0.1:9250 -s https://check.torproject.org/ | cat | grep -m 1 Congratulations | xargs

# get your onion address and share
$ docker-compose exec -T tor onions
```

## Solid Bitcoin Regtest
```
$ bin/solid bitcoin addnode tahptyz5nigsxqse.onion:18888 add
$ docker-compose logs -f bitcoin #(ctrl-c to exit logs)
$ bin/solid bitcoin generate 1
$ bin/solid bitcoin getnetworkinfo
$ bin/solid bitcoin getpeerinfo
```

## Solid Elements Regtest
```
$ bin/solid elements addnode tahptyz5nigsxqse.onion:18887 add
$ docker-compose logs -f elements #(ctrl-c to exit logs)
$ bin/solid elements generate 1
$ bin/solid elements getnetworkinfo
$ bin/solid elements getpeerinfo
```

## Destroy the stack
```
$ docker-compose down -v
```
