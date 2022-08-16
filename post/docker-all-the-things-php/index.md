+++
author = "Fabian Meyer"
title = "Docker all the things - PHP Edition"
date = "2022-08-16"
description = "Wir dockern was das Zeug hält. Und zwar alles was man für die PHP Entwicklung braucht."
tags = [
    "php",
    "docker",
    "docker-compose",
    "composer",
]
categories = [
    "Tutorial",
]
+++

## Was ist Docker und warum sollte man das benutzen?

Docker ist eine Containerisierungsplattform die es uns ermöglicht unsere Entwicklungsumgebung in speziell auf den Zweck
zugeschnittene Container zu verpacken, die wir dann einfach wiederverwenden können. Dabei sparen wir auf unserem System
gegenüber normaler Virtualisierung ordentlich Ressourcen ein, denn Docker-Container teilen sich die wichtigsten
Komponenten des Linux-Kernels. Sollen nun mehrere Docker-Container miteinander kommunizieren wie z.B. PHP und eine
Datenbank kommt Docker-Compose ins Spiel. Mit Docker-Compose können wir mehrere Services verbinden, steuern und aufsetzen.

In der Welt von PHP können wir dank Docker ganz einfach mit verschiedenen PHP-Versionen, Composer-Versionen und mehr
arbeiten. Ich werde euch zeigen wie ihr mit Docker und Docker-Compose ein kleines Projekt containerisiert und wie ihr
PHP-Skripte lokal (in verschieden PHP-Versionen) ausführen könnt, ohne PHP überhaupt lokal installiert zu haben!

## Gedockertes PHP im Terminal

Normalerweise führen wir PHP Skripte lokal folgendermaßen aus:

```bash{linenos=false,.command}
php script.php
```

Hierbei sind wir aber immer auf die aktuell bei uns installierte Version beschränkt. Theoretisch könnten wir auch mehrere
PHP Installation auf dem System haben und zwischen denen wechseln, aber es gibt eine bessere Lösung:

```bash{linenos=false}
alias php8.1="docker run --rm -it -v $PWD:/app -w /app php:8.1-cli php"
```

Mit diesem alias können wir dann mit `php8.1 script.php` unser Skript in einem Docker-Container ausführen. Aber wie 
funktioniert das Ganze? Lasst und das alias mal genauer anschauen.

```bash{linenos=false}
docker 
    run            # Befehl run = starten.
    --rm           # --rm entfernt den Container nachdem er das Skript durchlaufen hat.
    -it            # -it erlaubt es uns eine interaktives Terminal zum Container zu öffnen.
    -v $PWD:/app   # -v steht für Volume, mit diesem Befehl wird unser aktuelles Verzeichnis in /app im Container kopiert
    -w /app        # -w setzt das aktuelle Arbeitsverzeichnis auf /app wo unser Skript nun liegt.
    php:8.1-cli    # php:8.1-cli ist das Docker-Image welches wir nutzen. Das könnt ihr euch wie eine Anleitung vorstellen.
    php            # Zuletzt rufen wir den Befehl php auf um unser Skript im Container zu starten.
```

```bash
alias composerd="docker run --rm -it -v $PWD:/app -v ${COMPOSER_HOME:-$HOME/.composer}:/tmp fmeyer:composer2"
alias composer1="docker run --rm -it -v $PWD:/app -v ${COMPOSER_HOME:-$HOME/.composer}:/tmp fmeyer:composer"
alias php8.1="docker run --rm -it -v $PWD:/app -w /app php:8.1-cli php"
alias php8.0="docker run --rm -it -v $PWD:/app -w /app php:8.0-cli php"
alias php7.4="docker run --rm -it -v $PWD:/app -w /app php:7.4-cli php"
```