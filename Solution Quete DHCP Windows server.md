---
# **DHCP avec Windows Server**
---

## **Avant de commencer la configuration DHCP :**    

**Voici l'apparence de windows server 2022 venant d'être installé :**   


![](https://github.com/infokrim/DHCP-avec-Windows-Server/blob/main/capture_%20DHCP_winserv/DHCPwin1.PNG)     

1. **Se placer sur le réseau local du groupe :**

Demande de l'exercice :
   
> Configure la carte réseau de ta machine virtuelle en Réseau Interne


Pour cela dans proxmox :   

Se positionner sur **"matériel"** (dans le menu gauche de ma VM)     

![](https://github.com/infokrim/DHCP-avec-Windows-Server/blob/main/capture_%20DHCP_winserv/a.PNG)   

double cliquer sur **"Carte réseau"**   

Puis dans **"Pont"** choisir le groupe auquel on appartient.   

Dans notre cas, c'est le groupe 1 (G1)   

![](https://github.com/infokrim/DHCP-avec-Windows-Server/blob/main/capture_%20DHCP_winserv/b.PNG)     

Il faut faire exactement la même chose sur la VM qui fera office de client.    

2. **Renommer Système si necéssaire sous windows server 2022 :**


Cliquer sur le logo windows en bas à gauche de l'écran.    

![](https://github.com/infokrim/DHCP-avec-Windows-Server/blob/main/capture_%20DHCP_winserv/d.PNG)
 
Choisir **"System"**   

![](https://github.com/infokrim/DHCP-avec-Windows-Server/blob/main/capture_%20DHCP_winserv/e.PNG)   

Cliquer sur **"rename this PC"**   

Taper le nom désirer, ici ce sera comme suggéré en exemple, **"SRV-DHCP"**.   


![](https://github.com/infokrim/DHCP-avec-Windows-Server/blob/main/capture_%20DHCP_winserv/g.PNG)   

   
Cliquer sur le bouton **"Next"**   

![](https://github.com/infokrim/DHCP-avec-Windows-Server/blob/main/capture_%20DHCP_winserv/h.PNG)     

   
Puis cliquer sur **"Restart now"**    


## **<ins>Première étape :</ins>**   

## **<ins>1. Donner une addresse IP au serveur**</ins>   

Taper Network dans la zone de recherche ou une loupe se trouve :   

![1](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/4847f822-099a-4ef0-a135-b392b239519c)   
   
Choisir **Network status**   

La fenêtre suivante s'affiche :    

![2a](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/7eef6e84-bcd2-455b-a484-dd5ae6400276)    
     
Cliquer sur **Ethernet** dans le menu sur la gauche     
 
  
Cliquer sur **Network2**   

![3](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/0414cba7-f28e-4068-a1fb-442013a4b6bb)    

La fenêtre suivante s'affiche :     

![4](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/9e849768-ca4e-474e-a1fe-2e58873b7cc5)   
   
Défiler vers le bas et cliquer sur **Edit** dans la section "IP settings"   

![5](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/395ff5e7-6e4b-4309-bfa7-5e0254b0fdb3)   

La fenêtre suivante s'affiche :     

![6](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/acc7d812-ca07-4ac2-8c5c-f14e0faf6945)     
  
Le challenge indique :   

> Configure le service DHCP pour qu'il fournisse des adresses IP de la plage 172.20.0.100 - 172.20.0.200 sur le réseau 172.20.0.0/24
> 
Le CIDR indique bien un sous masque 255.255.255.0 (\24). On peut choisir comme adresse IP : **172.20.0.1**.   

Effacer les cases **Gateway** et **Preferred DNS** puis remplacer IP address par **172.20.0.1**.   

On obtient cette fenêtre :   

![7](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/c18c7c68-1a77-478a-8a5e-b618c8f3235f)     
   
Cliquer maintenant sur **Save**   

Fermer la fenêtre en cours en cliquant sur la croix :x: en haut à droite.   

![8](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/ce07b92f-242c-4b34-bb39-d5e25cab7876)     

On revient sur la fenêtre **"Server Manager"**   


---


## **<ins>Deuxième étape :</ins>**    

## <ins>**2. Ajouter la fonctionnalité DHCP au serveur**</ins>    

**Ajouter la fonctionnalité DHCP au serveur**    
  
**Voici l'apparence d'un windows server venant d'être installé :**   

![DHCPwin1](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/de5dc153-24df-4cab-8e24-d020cde2b57f)    


Cliquer sur ** 2 Add roles and features** qui est en n°2 en bleu sur l'image ci-dessus    

La fenêtre suivante s'affiche :    

![DHCPwin2](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/c77d6f8c-3567-4434-9094-678bb4786803)    



Cliquer sur **Next**   

La fenêtre suivante s'affiche :     

![DHCPwin3](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/4f5af323-01ca-4a92-9208-974a8e07836d)   
   
Cliquer sur **Next**   

La fenêtre suivante s'affiche :  

![DHCPwin4](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/70541076-1d20-41f0-a2c0-e6d38d35c17a)    

Cliquer sur **Next**   

La fenêtre suivante s'affiche :    

![DHCPwin5](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/31f52495-b40c-480c-aeab-fa64a6b7f2d6)    


Cliquer sur la case de **DHCP Server** (en bleu sur l'image ci dessous).    

La fenêtre suivante s'affiche :   

![DHCPwin6](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/a8474ace-ebdb-4c19-b914-a372e35c6f35)   

Cliquer sur le bouton **Add features**   

La fenêtre ou on a coché **DHCP Server** avec :heavy_check_mark:dans la case :   

![DHCPwin7](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/fd36e556-8ede-45e7-a4b3-84d55c91ce1c)   

Cliquer sur **Next**   

La fenêtre suivante s'affiche :   

![8](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/2bb32baf-fd36-47c8-83dc-632f4026b322)   


Cliquer sur **Next**   

La fenêtre suivante s'affiche :   

![DHCPwin9](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/24461550-c8b4-4103-a3d5-6fb06a545f5b)     

Cliquer sur **Next**   

La fenêtre suivante s'affiche :   

![DHCPwin10](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/e9d15f83-4ced-4ea8-b7e1-b557910cb6e1)   


Cocher la case de l'option :

![DHCPwin11](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/e3e17e0c-ee9a-4a4d-983e-36dfa6ad5d18)   
 
 
 Cliquer sur **Install**   
 
L'installation débute :   

![DHCPwin13](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/45df0961-a4c7-4959-9108-60e70148b3f9)    

 
Une fois l'installation effectuée, cliquer sur le bouton **Close** pour fermer la fenêtre.   

On revient sur la fenêtre **"Server Manager"**   

On aperçoit en haut de cette fenêtre 9 :    

![9](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/c859cf4f-e6d6-4bb9-bd6f-fccde153cfb5)     

Quand ce symbole :warning: apparait, il y a un problème donc allons voir de quoi il s'agit.   

Cliquer sur le drapeau :    

![10](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/feeb70cd-d1bf-4354-8c49-8300cc778a65)   


 
On aperçoit "Post-deployment Configuration" à côté du logo :warning: puis en bas en bleu **"complete DHCP configuration"**   

Il faut donc configurer la fonctionnalité DHCP qu'on a installé.   

Donc cliquer sur **"complete DHCP configuration"**.    

La fenêtre suivante s'affiche :   

![11](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/e95c0737-57b9-44af-a860-fc82a4a45b8c)    
    
Cliquer sur le bouton **Commit** en bas de la fenêtre.   

La fenêtre suivante s'affiche :  

![12](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/c6dcccd5-a0a0-41d7-9125-ca9be3c915d1)    

   
Cliquer sur le bouton **Close** en bas de la fenêtre.   

![DHCPwin13](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/a161ace0-261c-4d17-942e-4a536f2b090d)   

  
 On revient sur la fenêtre **"Server Manager"**   
 
 On constate qu'il n'y a plus de symbole :warning: a côté du drapeau.   
 
 ## **<ins>Deuxième étape :</ins>**   
 
## <ins>**3. Configuration du service DHCP**</ins>   

Revenons sur l'énoncé du challenge :    

> Configure le service DHCP pour qu'il fournisse des adresses IP de la plage 172.20.0.100 - 172.20.0.200 sur le réseau 172.20.0.0/24   

**a. Configuration d'une plage D'IP pour fournir des adresses IP de la plage 172.20.0.100 - 172.20.0.200**   

Aller dans le menu **Tools** en haut à droite puis cliquer sur **DHCP** :   

![15](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/c0d89ad3-d6bc-49f1-a0b8-68a932280dee)   

   
La fenêtre suivante s'affiche :     

![16](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/4ff5a4f8-a623-4bd1-88ce-e865ee311276)   
    
Agrandir cette fenêtre en cliquant sue le rectange d'agrandissement ![17](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/dd085b42-2b6f-424a-80ea-850670476eb9) en haut à droite.   

Cliquer sur la flèche à gauche de **"winserv"** ![18](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/d10467e6-66a1-44f6-9148-d3aada6111b2)
:    

Apparait alors IPV4 et IPV6 :    

![19](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/1e4a7631-f1bf-4bcc-9cd9-38ee82d9503f)    


Cliquer sur la flèche à gauche de **"IPV4"** 20:   

La fenêtre suivante est affichée :     

![21](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/63ecdd92-f9cd-4473-ad70-8c5872f9b557)    

 
Cliquer avec le bouton droit sur IPV4.   

Puis choisir **"New Scope"**    

 ![22](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/c419713d-cf19-496e-a023-804d3d192027)   
 

 La fenêtre suivante s'affiche :   
 
![23](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/3c1d7db8-4fc7-458c-b270-12315b5f97fa)   

Cliquer sur **Next**   

La fenêtre suivante s'affiche :   

![24](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/140d022d-ead7-4ec9-b55f-c6ab13c514f2)   

       
Donner le nom dans **"Name"**   

DHCP Service    

Puis dans description    

fournir des adresses IP de la plage 172.20.0.100 - 172.20.0.200   

Cliquer sur **Next**    

La fenêtre suivante s'affiche :   

![26](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/7ba2b395-fad9-43e3-9b7b-e916569c0435)    

   
Remplir comme l'image ci dessus, puis cliquer sur **Next** .    

La fenêtre suivante s'affiche :   

![27](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/83ac6134-d190-48dc-bf4f-b6298d5181ab)   

Cliquer sur **Next**      

La fenêtre suivante s'affiche :    

![28](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/ade60aa7-768b-4bf5-8744-f8247e5028e2)    
      
Cliquer sur **Next**    

La fenêtre suivante s'affiche :   

![29](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/f8d9565b-7a5d-4071-a644-6c0b98ff6c9d)   

    
Cliquer sur **Next**    

La fenêtre suivante s'affiche :   

![30](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/eb9127d7-390a-4a98-8cef-852d3b03ea0f)   


Cliquer sur **Next**    

La fenêtre suivante s'affiche :    

![32](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/5c8d49cd-be75-4a3f-a73b-c796c04d2c0d)   
    
Cliquer sur **Next**   

La fenêtre suivante s'affiche :   

![33](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/fe4fd046-f5e9-46f5-a96b-8f4d0b5ef8b0)   

Cliquer sur **Next**    

La fenêtre suivante s'affiche :     

![34](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/86814c74-56ac-4647-aa87-0b0e654e8704)

    
Cliquer sur **Next**    

La fenêtre suivante s'affiche :    

![35](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/14c98840-3bd0-4840-ab01-afdbe79e4800)   


Cliquer sur **Finish**     

On revient à la fenêtre suivante :   

![36](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/e6bbd8f4-2185-41df-ac2a-343f8d36bbaa)   



Pour vérifier que le serveur fonctionne à cette étape, il faut configurer une machine cliente en DHCP.   

On va se servir d'une VM Debian déjà installée.  

Voici la configuration du fichier /etc/network/interfaces :    

![39](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/eb0d8206-d180-43ee-9e82-bed6990ea977)   

   
Le fichier est configuré pour obtenir une adresse ip automatiquement.    

ligne : `iface ens18 inet DHCP`   

Voici les résultats d'une commande `ip a`   :   

![40](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/a0412a14-4a3b-47a5-9f3d-94378fa98f22)   
    
On peut constater que l'adresse IP de la vm est **172.20.0.100** ce qui corresspond à la première adresse de la plage d'adresse IP configurée sur windows server 2002.   

la première étape a bien foncionné, on a bien une adresse IP comprise dans la plage demandée.  

:+1: :+1: :+1: :muscle: :grin:    

**b. Configuration d'une IP spécique pour VM cliente :    

Grâce à la commande `ip a`, on en profite pour récupérer l'adresse MAC de la VM cliente qui est :   

**bc:24:11:28:9e:f2**   

Retourner dans la **VM Windows Server 2022**, à l'endroit ou on est resté.  

![36](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/7ddbc26b-7c29-4326-8cfb-14d0d1b6de81)   

  
Cliquer avec le bouton droit sur Reservations.   

puis cliquer sur **"new reservation"**    

![37](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/d95e09fe-0867-4788-961a-32c869695339)

  
La fenêtre suivante s'affiche :   

![38](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/ee990768-d68e-4ff0-8d5a-2f2c112b8648)   

  
Voici ce qui est demandé dan sle challenge :   

>Mettre en place une attribution statique pour une machine cliente particulière dont l'adresse MAC permet d'obtenir l'adresse 172.20.0.10

Remplir les cases comme suit :    

![41](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/b33bce6a-1c39-4237-b86e-ef71306ff348)   

   
Valider en cliquant sur le bouton **Add**     

Maintenant que l'adresse IP de réservation est configurée pour le client DHCP, on va vérifier le résultat sur la VM cliente :    

Il faut d'abord renouveler le bail DHCP de la VM cliente avec les commandes :    

`dhclient -r` : permet de libérer l'adresse actuelle puis taper :    

`dhclient` : pour renouveler et obtenir une nouvelle adresse IP.    

`ìp a` :  donne les paramètres des interfaces réseaux    


La nouvelle adresse IP de ma VM est bien 172.20.0.10 :+1: :+1: :+1:   

un des critères d'acceptationb est le suivant :    

> Le client qui possède la réservation n'obtient pas une autre IPv4, même si il demande un renouvellement.
> 
On a vu juste avant comment effectuer un renouvellement d'adresse IP.  

Retaper les commandes dans le terminal.   

- `dhclient -r` : permet de libérer l'adresse actuelle puis taper   
- `dhclient` : pour renouveler et obtenir une nouvelle adresse IP.    
- `ìp a` :  donne les paramètres des interfaces réseaux

 ![44](https://github.com/infokrim/DHCP-avec-Windows-Server/assets/169550534/f0a40a94-6215-4020-8d1a-ccedca2e13af)   

 
 La nouvelle adresse IP de ma VM est bien 172.20.0.10 :+1: :+1: :+1: :muscle: :grin:  
 

