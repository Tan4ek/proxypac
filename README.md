# YET ANOTHER ONE .pac GENERATOR

Основная цель - поднимать свою прокси (SOCKS5), автоматизировать сборку `.pac` для своей прокси и обхода блокировок. 
За основу взят проект [Russian PAC file generator, light version](https://bitbucket.org/anticensority/antizapret-pac-generator-light/src/master/) ([ПростоVPN.АнтиЗапрет](https://antizapret.prostovpn.org/)).

## Как запустить

Сначала поменять переменные среды в [docker-compose.yaml](docker-compose.yaml):
```
PACSOCKS5HOST - прокси которая будет использована в .pac, внимательно указывать порт, такой же, пример mysuper.proxy:443
PACFILE - название файла, точно такое же название файла будет использоваться в url для .pac, например, superfile.pac , значит <host ip/domain>:80/superfile.pac
PACFILE_NOSSL - аналогично PACFILE
```

Затем коммандой `docker-compose up --build -d` запусть сборку `.pac` и прокси

## Добавить/исключить хост в .pac 

Добавление хост для принудительного проксирования - добавить в файл [antizapret-pac-generator-light/config/include-hosts-dist.txt](antizapret-pac-generator-light/config/include-hosts-dist.txt) желаемый хост
Исключить хост из проксирования - добавить в файл [antizapret-pac-generator-light/config/exclude-hosts-dist.txt](antizapret-pac-generator-light/config/exclude-hosts-dist.txt)

## Добавить cronjob на хосте
Не забываем про время на хост машине
```
0 2 * * * /usr/bin/docker restart proxypac-pac-generator
```