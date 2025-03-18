# veille_minecraft_log4shell

Dans ce cours il nous est demandé de mettre en place un LAB et d'exploiter une CVE de niveau 7 minimum puis de trouver un moyen de mitigation de la faille.
Notre groupe a donc choisi la CVE Log4shell de criticité de niveau 10. Ce niveau de criticité a été établit par le Common Vulnerability Scoring System (CVSS). 

## Historique de la vulnérabilité

Log4shell est une vulnérabilité basée sur la librairie java intitulée "Log4j" que l'on retrouve dans de nombreuses application permettant la gestion des logs.
Cette vulnérabilité a tout d'abord été signalée de manière privée à Apache le 24 novembre 2021.
Le 9 décembre 2021, Log4Shell a été publiquement divulgué et a reçu un correctif initial avec la version 2.15.0 d’Apache Log4j.


## Fonctionnement
Log4Shell est une vulnérabilité d’injection Java Naming and Directory Interface (JNDI), et qui peut permettre l'exécution de code à distance (RCE).
Le principe est simple, sur un système affecté un attaquant peu exécuter du code malveillant et récupérer des informations ou faire en sorte que le code exécuté fasse ce que l'attaquant veut qu'il fasse.

## Exploit

## Mitigation 

## Bilan


## Sources utilisées 

https://www.trendmicro.com/fr_fr/what-is/apache-log4j-vulnerability.html
https://github.com/Justin-Garey/Minecraft-Log4j-Exploit
https://medium.com/@hackingvarangian/log4shell-vulnerability-part-1-minecraft-poc-ef770e5800de
