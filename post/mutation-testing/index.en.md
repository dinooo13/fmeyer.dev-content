---
author: Fabian Meyer
title: Mutation Testing
description: Was Mutation Testing uns über unsere Testqualität verraten kann.
date: 2022-08-19
tags:
  - php
  - testing
  - composer
  - phpstorm
categories:
  - Tutorial
links:
  - title: Kein Docker?
    description: Hier findest du es!
    website: https://docs.docker.com/get-docker/
---

## Wenn Code Coverage einfach nicht genug ist...

Oft ist die Testqualität ein großes Fragezeichen in der Entwicklung, ob nun hohe oder niedrige Coverage im Endeffekt
kommt es darauf an wie aussagekräftig die Testsuite ist. Mutation Testing ist eine Vorgehensweise mit der wir einen 
tieferen Einblick in die Qualität unserer Tests bekommen. Aber wie schafft Mutation Testing das? Wie der Name schon 
vermuten lässt mit Mutationen am Code. Wenn ein Test trotz Mutation am Code grün ist, heißt das der Mutant ist entkommen,
schlägt der Test hingegen fehl, wurde der Mutant gefangen. Schauen wir uns doch beispielhaft ein paar der Mutationen an die 
vorgenommen werden.

Mutation 1

Mutation 2

Mutation 3

Im Mutation Testing werden noch viele weitere dieser Mutationen durchlaufen. Mithilfe von infectionPHP können wir
Mutation Testing in ein PHP Projekt einbauen und dessen Testqualität auf die Probe stellen. Wir installieren
infectionPHP via composer und legen eine Konfigurationsdatei an.

composer command

Konfigurationsdatei

Um uns den Befehl für das ganze nicht merken zu müssen legen wir einfach ein composer script an, damit können wir die 
Tests dann einfach ausführen. infectionPHP lässt PHPUnit mit Coverage selbst durchlaufen und benötigt dann natürlich 
eine Coverage Engine wie XDebug. Hier können wir zum Beispiel unser PHP-Docker Image für die Entwicklung aus meinem 
letzten Tutorial nutzen.

infectionPHP liefert uns mit unserer Konfiguration einen html Report und mehrere Kennzahlen in der Konsole. 
Was bedeuten diese Kennzahlen?

Kennzahl 1

Kennzahl 2

Kennzahl 3

Im html Report können wir uns das Ergebnis visuell aufbereitet anzeigen lassen, dabei sehen wir auch welche Mutationen 
nicht gefangen wurden. Das gibt uns einen guten Tipp wie wir diesen Mutanten in einem neuen Test abfangen können.
Schauen wir in den Report sehen wir Folgendes:

Screenshot

Um diesen Mutanten nun abzufangen, schreiben wir einen neuen Test.

Test

Lassen wir infectionPHP nun noch einmal laufen sehen wir haben 100 % MSI. Damit kommen wir auch zum Ende dieses 
Artikels ich hoffe, ihr konntet etwas für eure Softwareprojekte mitnehmen!

