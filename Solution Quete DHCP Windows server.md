---
# **DHCP avec Windows Server**
---

## **Avant de commencer la configuration DHCP :**    

**Voici l'apparence de windows server 2022 venant d'être installé :**   
image1  
1. **Se placer sur le réseau local du groupe :**   
Demande de l'exercice :    
> Configure la carte réseau de ta machine virtuelle en Réseau Interne  
Pour cela dans proxmox :
Se positionner sur **"matériel"** (dans le menu gauche de ma VM   
a   
double cliquer sur **"Carte réseau"**   
Puis dans **"Pont"** choisir le groupe auquel on appartient.   
Dans notre cas, c'est le groupe 1 (G1)
b   
Il faut faire exactement la même chose sur la VM qui fera office de client.    

2. **Renommer Système si necéssaire sous windows server 2022 :**
Cliquer sur le logo windows en bas à gauche de l'écran.   
d    
Choisir **"System"**   
e   
Cliquer sur **"rename this PC"**   
Taper le nom désirer, ici ce sera comme suggéré en exemple, **"SRV-DHCP"**.   
g   
Cliquer sur le bouton **"Next"**   
h    
Puis cliquer sur **"Restart now"**    


## **<ins>Première étape :</ins>**   

## **<ins>1. Donner une addresse IP au serveur**</ins>   
Taper Network dans la zone de recherche ou une loupe se trouve :
1   
Choisir **Network status**
La fenêtre suivante s'affiche :   
2a      
Cliquer sur **Ethernet** dans le menu sur la gauche    
2b   
Cliquer sur **Network2** (im3):
La fenêtre suivante s'affiche :     
4   
Défiler vers le bas et cliquer sur **Edit** dans la section "IP settings" im5 :
La fenêtre suivante s'affiche :     
6   
Le challenge indique :
> Configure le service DHCP pour qu'il fournisse des adresses IP de la plage 172.20.0.100 - 172.20.0.200 sur le réseau 172.20.0.0/24   
Le CIDR indique bien un sous masque 255.255.255.0 (\24). On peut choisir comme adresse IP : **172.20.0.1**.   
Effacer les cases **Gateway** et **Preferred DNS** puis remplacer IP address par **172.20.0.1**.   
On obtient cette fenêtre :   
7   
Cliquer maintenant sur **Save**
Fermer la fenêtre en cours en cliquant sur la croix :x: en haut à droite.
8
On revient sur la fenêtre **"Server Manager"**   


---


## **<ins>Deuxième étape :</ins>**
## <ins>**2. Ajouter la fonctionnalité DHCP au serveur**</ins>

**Ajouter la fonctionnalité DHCP au serveur**
  
**Voici l'apparence d'un windows server venant d'être installé :**     
image1  
Cliquer sur ** 2 Add roles and features** qui est en n°2 en bleu sur l'image ci-dessus  
La fenêtre suivante s'affiche :  
image2  
Cliquer sur **Next**   
La fenêtre suivante s'affiche :   
image3   
Cliquer sur **Next**   
La fenêtre suivante s'affiche :  
image4
Cliquer sur **Next**   
La fenêtre suivante s'affiche :  
image5
Cliquer sur la case de **DHCP Server** (en bleu sur l'image ci dessous).  
La fenêtre suivante s'affiche :  
image6   
Cliquer sur le bouton **Add features**
La fenêtre ou on a coché **DHCP Server** avec :heavy_check_mark:dans la case :  
image7
Cliquer sur **Next**   
La fenêtre suivante s'affiche :   
image8   
Cliquer sur **Next**   
La fenêtre suivante s'affiche :   
image9   
Cliquer sur **Next**   
La fenêtre suivante s'affiche :   
image10   
 Cocher la case de l'option :
 image11
 Cliquer sur **Install**
L'installation débute :
 image13   
 Une fois l'installation effectuée, cliquer sur le bouton **Close** pour fermer la fenêtre.   
 On revient sur la fenêtre **"Server Manager"**   
 On aperçoit en haut de cette fenêtre 9 :    
 Quand ce symbole :warning: apparait, il y a un problème donc allons voir de quoi il s'agit.   
 Cliquer sur le drapeau :
 10   
 On aperçoit "Post-deployment Configuration" à côté du logo :warning: puis en bas en bleu **"complete DHCP configuration"**   
 Il faut donc configurer la fonctionnalité DHCP qu'on a installé.
 Donc cliquer sur **"complete DHCP configuration"**.    

La fenêtre suivante s'affiche :  
11    
Cliquer sur le bouton **Commit** en bas de la fenêtre.   
La fenêtre suivante s'affiche :  
12    
Cliquer sur le bouton **Close** en bas de la fenêtre.   
13   
 On revient sur la fenêtre **"Server Manager"**   
 On constate qu'il n'y a plus de symbole :warning: a côté du drapeau.
 
 ## **<ins>Deuxième étape :</ins>**
## <ins>**3. Configuration du service DHCP**</ins>
Revenons sur l'énoncé du challenge :   
> Configure le service DHCP pour qu'il fournisse des adresses IP de la plage 172.20.0.100 - 172.20.0.200 sur le réseau 172.20.0.0/24   

**a. Configuration d'une plage D'IP pour fournir des adresses IP de la plage 172.20.0.100 - 172.20.0.200**   

Aller dans le menu **Tools** en haut à droite puis cliquer sur **DHCP** :
15    
La fenêtre suivante s'affiche :    
16     
Agrandir cette fenêtre en cliquant sue le rectange d'agrandissement 17 en haut à droite.   
Cliquer sur la flèche à gauche de **"winserv"** 18:
apparait alors IPV4 et IPV6
19
Cliquer sur la flèche à gauche de **"IPV4"** 20:
La fenêtre suivante est affichée :    
21     
Cliquer avec le bouton droit sur IPV4.
Puis choisir **"New Scope"**
 22
 La fenêtre suivante s'affiche :   
 23
Cliquer sur **Next**   
La fenêtre suivante s'affiche :   
24       
Donner le nom dans **"Name"**   
DHCP Service
Puis dans description
fournir des adresses IP de la plage 172.20.0.100 - 172.20.0.200 
Cliquer sur **Next**   
La fenêtre suivante s'affiche :   
25    
Remplir comme l'image en dessous :
26  
Cliquer sur **Next**   
La fenêtre suivante s'affiche :   
27      
Cliquer sur **Next**
La fenêtre suivante s'affiche :   
28      
Cliquer sur **Next**
La fenêtre suivante s'affiche :   
29      
Cliquer sur **Next**
La fenêtre suivante s'affiche :   
30    
Cliquer sur **Next**
La fenêtre suivante s'affiche :   
32    
Cliquer sur **Next**
La fenêtre suivante s'affiche :   
33    
Cliquer sur **Next**
La fenêtre suivante s'affiche :   
34     
Cliquer sur **Next**
La fenêtre suivante s'affiche :   
35  
Cliquer sur **Finish**     
On revient à la fenêtre suivante :
36
Pour vérifier que le serveur fonctionne à cette étape, il faut configurer une machine cliente en DHCP.  
On va se servir d'une VM Debian déjà installée.  
Voici la configuration du fichier /etc/network/interfaces :    
39    
Le fichier est configuré pour obtenir une adresse ip automatiquement.    
ligne : `iface ens18 inet DHCP`
Voici les résultats d'une commande `ip a`   :
40    
On peut constater que l'adresse IP de la vm est **172.20.0.100** ce qui corresspond à la première adresse de la plage d'adresse IP configurée sur windows server 2002.   
la première étape a bien foncionné, on a bien une adresse IP comprise dans la plage demandée.  
:+1: :+1: :+1: :muscle: :grin:    

**b. Configuration d'une IP spécique pour VM cliente :    
Grâce à la commande `ip a`, on en profite pour récupérer l'adresse MAC de la VM cliente qui est :   
**bc:24:11:28:9e:f2**   

Retourner dans la **VM Windows Server 2022**, à l'endroit ou on est resté.   
36  
Cliquer avec le bouton droit sur Reservations.   
puis cliquer sur **"new reservation"**    
37   
La fenêtre suivante s'affiche :   
38    
Voici ce qui est demandé dan sle challenge :   
>Mettre en place une attribution statique pour une machine cliente particulière dont l'adresse MAC permet d'obtenir l'adresse 172.20.0.10   
Remplir les cases comme suit :    
41    
Valider en cliquant sur le bouton **Add**     
Maintenant que l'adresse IP de réservation est configurée pour le client DHCP, on va vérifier le résultat sur la VM cliente :
Il faut d'abord renouveler le bail DHCP de la VM cliente avec les commandes :   
`dhclient -r` : permet de libérer l'adresse actuelle puis taper :    
`dhclient` : pour renouveler et obtenir une nouvelle adresse IP.    
`ìp a` :  donne les paramètres des interfaces réseaux    
43    
La nouvelle adresse IP de ma VM est bien 172.20.0.10 :+1: :+1: :+1: 
un des critères d'acceptationb est le suivant : 
> Le client qui possède la réservation n'obtient pas une autre IPv4, même si il demande un renouvellement.  
On a vu juste avant comment effectuer un renouvellement d'adresse IP. Retaper les commandes dans le terminal.   

- `dhclient -r` : permet de libérer l'adresse actuelle puis taper   
- `dhclient` : pour renouveler et obtenir une nouvelle adresse IP.    
- `ìp a` :  donne les paramètres des interfaces réseaux   
 
 44
 La nouvelle adresse IP de ma VM est bien 172.20.0.10 :+1: :+1: :+1: :muscle: :grin:  
 

