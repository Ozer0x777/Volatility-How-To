Volatility est un outil open source permettant d'analyser des images de mémoire pour la recherche de malwares et d'autres types de données.

Voici une documentation d'installation et d'utilisation de Volatility:




## Installation

Volatility est un outil en ligne de commande et nécessite Python pour fonctionner. Les étapes ci-dessous vous aideront à installer Volatility sur votre machine.
Étape 1: Installation de Python

Si Python n'est pas déjà installé sur votre machine, vous pouvez le télécharger et l'installer à partir du site officiel de Python (https://www.python.org/downloads/). Assurez-vous de télécharger la version 3.x de Python.
Étape 2: Téléchargement de Volatility

Le code source de Volatility est disponible sur GitHub. Vous pouvez télécharger la dernière version de Volatility en exécutant la commande suivante dans votre terminal:

```
git clone https://github.com/volatilityfoundation/volatility.git
```

Cette commande téléchargera Volatility dans un dossier nommé "volatility".
Étape 3: Installation de Volatility

Après avoir téléchargé le code source de Volatility, vous pouvez l'installer en exécutant les commandes suivantes à partir de votre terminal:


```
cd volatility
python setup.py install
```
Cette commande installera Volatility sur votre machine.





## Utilisation

Maintenant que Volatility est installé sur votre machine, vous pouvez commencer à l'utiliser pour analyser des images de mémoire. Voici quelques exemples de commandes que vous pouvez exécuter.
Analyse de l'image de mémoire

Pour analyser une image de mémoire, vous devez d'abord spécifier le profil de l'image. Le profil est une description de la version du système d'exploitation et de l'architecture du processeur utilisés dans l'image de mémoire.

Vous pouvez trouver le profil en utilisant la commande suivante:

```
volatility imageinfo -f <path-to-image>
```
Remplacez <path-to-image> par le chemin d'accès à votre image de mémoire.

Une fois que vous avez identifié le profil de l'image, vous pouvez utiliser la commande suivante pour lister les processus en cours d'exécution dans l'image de mémoire:

```
volatility pslist -f <path-to-image> --profile=<profile>
```

Cette commande listera les processus en cours d'exécution dans l'image de mémoire, ainsi que leur identifiant de processus (PID), leur nom et leur statut.
Recherche de malwares

Volatility peut être utilisé pour rechercher des malwares dans une image de mémoire. Vous pouvez utiliser la commande suivante pour identifier les processus suspects dans l'image de mémoire:

```
volatility pslist -f <path-to-image> --profile=<profile> --show-hidden
```

Cette commande listera tous les processus en cours d'exécution, y compris les processus cachés, dans l'image de mémoire.

Vous pouvez également utiliser la commande suivante pour rechercher des connexions réseau suspectes dans l'image de mémoire:

```
volatility netscan -f <path-to-image> --profile=<profile>
```
Cette commande listera toutes les connexions réseau établies dans l'image de mémoire, y compris les adresses IP locales et distantes, ainsi que les ports utilisés.

 ## Acquisition de l'image

La première étape pour utiliser Volatility est d'acquérir une image de la mémoire volatile du système cible. Il existe plusieurs outils pour réaliser cette étape, notamment :

    FTK Imager (https://accessdata.com/product-download/ftk-imager-version-4-6-0)
    DumpIt (https://download.nirsoft.net/utils/dumpit.zip)
    Volatility (https://github.com/volatilityfoundation/volatility)

Voici un exemple d'utilisation de Volatility pour acquérir une image de la mémoire volatile :


```
$ python vol.py -f /dev/mem imagecopy -O image.raw
```
  
  
Ce commandement crée une copie de l'image de mémoire volatile dans un fichier nommé "image.raw".
 
Identification du profil

Après avoir acquis l'image de la mémoire volatile, la prochaine étape consiste à identifier le profil du système cible. Le profil correspond à la configuration matérielle et logicielle du système. Cette étape est essentielle car elle permet à Volatility de comprendre la structure de la mémoire et de récupérer les informations nécessaires pour l'analyse.

Volatility fournit une liste de profils pour différents systèmes d'exploitation. Pour identifier le profil, il suffit d'exécuter la commande suivante :

```
$ python vol.py -f image.raw imageinfo
```
  
  
Voici un exemple de sortie pour un système Windows 7 :


```  
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...

          Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win7SP1x86, Win7SP0x86 (Instantiated with Win7SP1x64)
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/root/image.raw)
                      PAE type : PAE
                           DTB : 0x185000L
                          KDBG : 0x828e3018L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0x828e4018L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2022-02-03 19:33:13 UTC+0000
     Image
```
  
## Analyse des processus

Une fois le profil identifié, il est possible de commencer à analyser la mémoire volatile. L'une des analyses les plus courantes est l'analyse des processus en cours d'exécution. Pour lister les processus, il suffit d'exécuter la commande suivante :

```
$ python vol.py -f image.raw --profile=<nom du profil> pslist
```
  
Cette commande affichera une liste des processus en cours d'exécution, ainsi que leurs PID et leurs propriétaires.

Voici un exemple de sortie pour une image Windows 10 :

```
Volatility Foundation Volatility Framework 2.6.1
Offset(P)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0x0000000005a6a040 System                    4      0    109     1976 ------      0 2023-03-29 20:30:56 UTC+0000                                  
0x0000000005b38d40 Registry                 96      4     12      531 ------      0 2023-03-29 20:31:12 UTC+0000                                  
0x0000000005a1b040 smss.exe                628      4      2       29 ------      0 2023-03-29 20:30:47 UTC+0000                                  
0x0000000005b22660 wininit.exe             768      4      3       73 ------      0 2023-03-29 20:30:51 UTC+0000                                  
0x0000000005a42040 csrss.exe               868    844      9      419      0      0 2023-03-29 20:30:53 UTC+0000                                  
0x0000000005b32220 csrss.exe               900    884      8      369      1      0 2023-03-29 20:30:53 UTC+0000                                  
0x0000000005bfa040 winlogon.exe            936    884      3      119      1      0 2023-03-29 20:30:54 UTC+0000                                  
0x0000000005a38d40 services.exe            992    768      8      252      0      0 2023-03-29 20:30:55 UTC+0000                                  
0x0000000005a9c040 lsass.exe              1004    768      7      674      0      0 2023-03-29 20:30:56 UTC+0000                                  
0x0000000005b3ed40 svchost.exe            1068    992     22      550      0      0 2023-03-29 20:30:56 UTC+0000                                  
0x0000000005b30040 svchost.exe            1104    992     20      482      0      0 2023-03-29 20:30:56 UTC+0000                                  
0x0000000005a98840 svchost.exe            1172    992     40     1204      0      0 2023-03-29 20:30:56 UTC+0000     
```
  
## Analyse réseau

En plus de l'analyse des processus, l'analyse réseau est une autre tâche courante dans l'analyse de la mémoire volatile. Volatility fournit plusieurs plugins pour analyser les connexions réseau, les sockets, les connexions UDP et TCP, etc.

Pour lister les connexions réseau actives, vous pouvez utiliser le plugin netscan :

```
$ python vol.py -f image.raw --profile=<nom du profil> netscan
```
  
Cette commande affichera une liste des connexions réseau actives, ainsi que les PID correspondants et les adresses IP et ports distants et locaux.

Voici un exemple de sortie pour une image Windows 10 :

```
Volatility Foundation Volatility Framework 2.6.1
Offset(P)          Local Address             Remote Address            Pid
------------------ ------------------------ ------------------------ ---
0xffff9c029a4f6c00 192.168.0.100:51756       13.107.4.50:443           2004
0xffff9c0298c7b800 192.168.0.100:51757       216.58.207.46:443         2004
0xffff9c0298b6d200 192.168.0.100:51758       216.58.207.46:443         2004
0xffff9c02a0a18a00 192.168.0.100:51759       192.0.78.25:443           2004
0xffff9c02a0a18a00 192.168.0.100:51760       192.0.78.25:443           2004
```
  
Vous pouvez également utiliser d'autres plugins pour analyser les connexions UDP et TCP, tels que connscan et sockets. Voici un exemple de commande pour analyser les connexions TCP :

```
$ python vol.py -f image.raw --profile=<nom du profil> connscan
```
  
Cette commande affichera une liste de toutes les connexions TCP actives, ainsi que les PID correspondants, les adresses IP et ports distants et locaux, et l'état de la connexion (ouvert, fermé, etc.).

Voici un exemple de sortie pour une image Windows 10 :


```
Volatility Foundation Volatility Framework 2.6.1
Offset(P)          Local Address             Remote Address            State          Pid
------------------ ------------------------ ------------------------ -------------- ---
0xffff9c029a4f6c00 192.168.0.100:51756       13.107.4.50:443           ESTABLISHED    2004
0xffff9c0298c7b800 192.168.0.100:51757       216.58.207.46:443         ESTABLISHED    2004
0xffff9c0298b6d200 192.168.0.100:51758       216.58.207.46:443         ESTABLISHED    2004
0xffff9c02a0a18a00 192.168.0.100:51759       192.0.78.25:443           ESTABLISHED    2004
0xffff9c02a0a18a00 192.168.0.100:51760       192.0.78.25:443           ESTABLISHED    2004
```
  
