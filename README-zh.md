
# opencrud chinese

## Pre-requisites

* Node.js (v8.9+)
* Docker && docker-compose

## How to Run(local)

* install deps

```code
yarn
```

* build chinese version

```code
yarn build-zh
```

* local watch result (with live-server)

```code
yarn live
```

## How to Run (with docker)

* build webpage

```code
yarn build-zh
```

* build image && up

```code
docker-compose build && docker-compose up -d
```