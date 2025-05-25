# PAwChO_Lab11_BK
Sprawozdanie z laboratorium 11, Programowanie aplikacji w chmurze obliczeniowej, autor: Bartosz Klimiuk

## Utworzenie sieci
docker network create --driver=bridge --subnet=10.0.1.0/24 lab11net

## Sprawdzenie sieci
docker network inspect lab11net

## Uruchomienie kontenera web1
docker run -dt --name web1 --network=lab11net --ip=10.0.1.3 -p 8001:80 --mount type=bind,source='/c/Users/barte/OneDrive/Pulpit/VI semestr/6.SE.4 Programowanie aplikacji w chmurze obliczeniowej/Laboratorium/lab11',target=/usr/share/nginx/html --mount type=bind,source='/c/Users/barte/OneDrive/Pulpit/VI semestr/6.SE.4 Programowanie aplikacji w chmurze obliczeniowej/Laboratorium/lab11/web1log',target=/var/log/nginx nginx

## Uruchomienie kontenera web2
docker run -dt --name web2 --network=lab11net --ip=10.0.1.4 -p 8002:80 --mount type=bind,source='/c/Users/barte/OneDrive/Pulpit/VI semestr/6.SE.4 Programowanie aplikacji w chmurze obliczeniowej/Laboratorium/lab11',target=/usr/share/nginx/html --mount type=bind,source='/c/Users/barte/OneDrive/Pulpit/VI semestr/6.SE.4 Programowanie aplikacji w chmurze obliczeniowej/Laboratorium/lab11/web2log',target=/var/log/nginx nginx

## Uruchomienie kontenera web3
docker run -dt --name web3 --network=lab11net --ip=10.0.1.5 -p 8003:80 --mount type=bind,source='/c/Users/barte/OneDrive/Pulpit/VI semestr/6.SE.4 Programowanie aplikacji w chmurze obliczeniowej/Laboratorium/lab11',target=/usr/share/nginx/html --mount type=bind,source='/c/Users/barte/OneDrive/Pulpit/VI semestr/6.SE.4 Programowanie aplikacji w chmurze obliczeniowej/Laboratorium/lab11/web3log',target=/var/log/nginx nginx

## Sprawdzenie działania z maszyny macierzystej
web1: http://localhost:8001

web2: http://localhost:8002

web3: http://localhost:8003

## Instalacja narzędzia sprawdzającego w każdym z kontenerów
docker exec -it web{X} /bin/bash (X - numer kontenera - 1, 2 lub 3)

apt update

apt install curl -y

## Sprawdzenie działania pozostałych kontenerów
web1: curl http://10.0.1.4, curl http://10.0.1.5

web2: curl http://10.0.1.3, curl http://10.0.1.5

web3: curl http://10.0.1.3, curl http://10.0.1.4
