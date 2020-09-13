# Lampe autocollante
Ceci est le répertoire de travail sur la lampe autocollante basée pour l'instant sur le [projet WLED](https://github.com/Aircoookie/WLED).
![alt text](https://github.com/ThotAlion/lampe-autocollante/edit/master/IMG_20200913_102709.jpg "Logo Title Text 1")

## Matériel

- [ESP8266](https://fr.aliexpress.com/item/33018645469.html?spm=a2g0w.search0302.3.37.732a40966f5qsy&ws_ab_test=searchweb0_0,searchweb201602_0,searchweb201603_0,ppcSwitch_0&algo_pvid=a749a424-0d00-4edc-b6e5-f7088eb65d1d&algo_expid=a749a424-0d00-4edc-b6e5-f7088eb65d1d-5)
- [Shield Neopixel](https://fr.aliexpress.com/item/32893389334.html?spm=a2g0o.detail.1000060.3.57587360zXjthO&gps-id=pcDetailBottomMoreThisSeller&scm=1007.13339.169870.0&scm_id=1007.13339.169870.0&scm-url=1007.13339.169870.0&pvid=6f3d81ff-2825-45ea-9e79-d6e2e9d8621b&_t=gps-id:pcDetailBottomMoreThisSeller,scm-url:1007.13339.169870.0,pvid:6f3d81ff-2825-45ea-9e79-d6e2e9d8621b,tpp_buckets:668%230%23131923%2398_668%23808%233772%2347_668%23888%233325%231_668%232846%238113%23622_668%232717%237566%23825_668%231000022185%231000066059%230_668%233468%2315608%23159)
- [Bandeau Neopixel](https://fr.aliexpress.com/item/32682015405.html?spm=a2g0o.productlist.0.0.5a3a4d1bF2Kfdi&algo_pvid=9974e75d-0c06-4ced-bee2-57134684c338&algo_expid=9974e75d-0c06-4ced-bee2-57134684c338-0&btsid=0b0a0ae215999883340953433eb612&ws_ab_test=searchweb0_0,searchweb201602_,searchweb201603_)
- [Alimentation 5V](https://fr.aliexpress.com/item/32916357952.html?spm=a2g0o.productlist.0.0.65eb190bpylV7p&algo_pvid=8b9f953c-4532-4622-be26-225b96bf5906&algo_expid=8b9f953c-4532-4622-be26-225b96bf5906-6&btsid=0b0a0ae215999883654585217eb612&ws_ab_test=searchweb0_0,searchweb201602_,searchweb201603_) (choisir l'alimentation en fonction du nombre de LED sachant que chaque LED a besoin de 60mA quand elle est à fond, 1A peut par exemple contrôler au maximum 16 LEDs)

La lampe autocollante est un bandeau LED Neopixel alimenté et contrôlé par un module ESP8266. Ce module héberge un mini site web qui permet de contrôler les LED comme on le souhaite.
Quand on branche le module sur le secteur, s'il n'y a pas de WIFI connu, le module créé son propre réseau wifi, ce qui permet de configurer le module sur le réseau de la box. Une fois configuré, le module éteint son wifi et se connecte sur le réseau. Pour accéder au contrôle, il suffit de taper l'adresse IP du module dans la barre de recherche du navigateur.

## Installation

### déterminer une adresse IP au futur module

La première étape est de trouver une adresse IP pour le futur module. Pour cela, il faut lister tous les appareils qui sont sur le réseau WIFI afin d'éviter de prendre une adresse déjà prise.

- Appuyez simultanément sur les touches [windows + R]
- Tapez "cmd" dans la ligne de texte puis Entrée
- Une console apparait
- Dans cette console, tapez 
  
```
arp -a
```

- une liste apparait avec toutes les adresses du réseau
```
Interface : 192.168.0.100 --- 0x9
    Adresse Internet      Adresse physique      Type
    192.168.0.1           b0-4e-26-45-6c-d3     dynamique
    192.168.0.255         ff-ff-ff-ff-ff-ff     statique
    192.168.0.22          01-00-5e-00-00-16     statique
    192.168.0.251         01-00-5e-00-00-fb     statique
    192.168.0.252         01-00-5e-00-00-fc     statique
```
La première ligne "Interface" correspond à l'adresse du PC sur lequel vous travaillez. Les autres sont les autres appareils sur le réseau.
Pour déterminer l'adresse du module, prenez l'adresse de votre PC (ici **192.168.0.100**) et ajoutez 1 au dernier chiffre (ça donne **192.168.0.101**). Si cette adresse n'est pas dans la liste, c'est qu'elle est disponible. Dans le cas contraire, on ajoute 1 jusqu'à trouver une adresse libre.
Une fois l'adresse définie, notez la sur un papier.

### Configurer le module

Prenez le module et branchez le sur le secteur. Attendez 1 minute, en cherchant les réseaux wifi, vous devriez voir apparaitre un nouveau réseau nommé "WLED-AP" avec le mot de passe "wled1234". L'explorateur Internet va s'ouvrir sur la page d'accueil du module. Cliquez sur "WIFI settings" et tapez le nom du réseau wifi que vous utilisez, son mot de passe et dans le champs "Static IP" l'adresse IP que nous avons déterminée au paragraphe précédent.
Appuyez ensuite sur "save and reboot"

Votre module est prêt et va se connecter sur le réseau.

### première connexion

Dans votre navigateur internet, tapez http://192.168.0.X en remplaçant avec l'adresse vue au premier paragraphe. Vous arrivez sur la page de contrôle. Amusez vous bien.

Vous pouvez vous connecter à votre lampe via smartphone en téléchargeant l'appli WLED (Androis et iOS)
