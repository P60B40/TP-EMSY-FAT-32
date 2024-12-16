# TP-EMSY-FAT-32

## Consigne 
* Le travail se fait par groupe de 2 élèves.
* Un rapport par groupe de 2 élèves ; chacun maîtrise son contenu.
* Votre rapport doit expliquer et commenter votre démarche, les difficultés rencontrées, 
les solutions, et répondre aux questions posées. Les commandes exécutées doivent être 
expliquées.
* Toutes les étapes doivent figurer et être documentées dans votre rapport.
* Pour faciliter la lecture, merci d'organiser votre rapport selon l'ordre et la numérotation 
de la donnée.

## Formatage de la clé
Selon c'est paramètre (VM widows 7 ou windows 10, même resultat)
### Manipulation dans la VM  
Nous avons ouvert windows 7 sur machine virtuelle pour une question de sécurité.
pour que la VM lise notre clé usb il faut aller dans l'option de la VM player ->Removable device -> et selctionner la clé usb.
Nous avons été chercher diskeditor sur notre disque K: pour le copier et l'ouvrir sur notre VM.

![image](https://github.com/user-attachments/assets/11c6cc74-0e47-4904-9691-9923d2e55827)

Nous avons rélever le nombre de secteur du disque physique (voir capture) nous avons un disque de 3915776 secteurs.
log du contenue du secteur 0 : voir fichier hdd_info.xml
dans ma partition primaire dans l'option navigate l 'adresse de ma partition 1 débute à l'adresse F8.

## Question A
Il y'a 4 partition primaire, les partitions 2, 3, 4 ont 0 secteur.
## Question B
Voici les adresses des débuts des partitions.

![nombre partition](https://github.com/user-attachments/assets/0e9c6cad-0fc2-4bf9-89cc-c7fc13c8bb9d)
* Partition 1 : 1BE
* Partition 2 : 1CE
* Partition 3 : 1DE
* Partition 4 : 1EE

### Décodage des données
* nombre de secteurs (partition logique) ?
Le nombre de secteurs est de 3915713
disque de 3915776 secteurs : 66 secteurs utilisé par la partie disque.

* nombre secteurs par cluster?
le nobre est de 8 secteur par cluster.

* Le "Boot record" se situe dans la zone "reserved sectors" du début de la partition. Quel espace cette zone occupe-t-elle ?
elle occupe 560 secteurs.

* Combien y a-t-il de FAT et quel espace occupent-elles chacune ?
secteurs par FAT est de 3816 / nombre de FAT est de 2

## Question C


