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
* Selon c'est paramètre (VM widows 7 ou windows 10, même resultat)
### Manipulation dans la VM  
* Nous avons ouvert windows 7 sur machine virtuelle pour une question de sécurité.
pour que la VM lise notre clé usb il faut aller dans l'option de la VM player ->Removable device -> et selctionner la clé usb.
Nous avons été chercher diskeditor sur notre disque K: pour le copier et l'ouvrir sur notre VM.

![image](https://github.com/user-attachments/assets/11c6cc74-0e47-4904-9691-9923d2e55827)

![taille du disque physique](https://github.com/user-attachments/assets/e01e327c-bd77-4ccd-bed3-4cb5e093bde5)

* Nous avons rélever le nombre de secteur du disque physique (voir capture) nous avons un disque de 3915776 secteurs.
log du contenue du secteur 0 : voir fichier hdd_info.xml
dans ma partition primaire dans l'option navigate l 'adresse de ma partition 1 débute à l'adresse F8.

## Etude du MBR / FAT 32

### Question A
Repérez la zone des partitions. Combien y a-t-il de partitions ?
* Il y'a 4 partition primaire, les partitions 2, 3, 4 ont 0 secteur.
### Question B
Décodez les informations de(s) partition(s) en vous basant sur le support de cours ?
* Voici les adresses des débuts des partitions.

![nombre partition](https://github.com/user-attachments/assets/0e9c6cad-0fc2-4bf9-89cc-c7fc13c8bb9d)
* Partition 1 : 1BE
* Partition 2 : 1CE
* Partition 3 : 1DE
* Partition 4 : 1EE

![taille partition](https://github.com/user-attachments/assets/b879cef6-0595-49fb-a301-262e25fa0f22)

#### Décodage des données
nombre de secteurs (partition logique) ?
* Le nombre de secteurs est de 3915713
disque de 3915776 secteurs : 66 secteurs utilisé par la partie disque.


Le "Boot record" se situe dans la zone "reserved sectors" du début de la partition. Quel espace cette zone occupe-t-elle ?
* elle occupe 560 secteurs.

Combien y a-t-il de FAT et quel espace occupent-elles chacune ?
* secteurs par FAT est de 3816 / nombre de FAT est de 2

### Question C
Affichez le contenu du secteur de départ de la partition 1. Montrez en analysant le 
contenu qu'il s'agit bien du début de la partition ?

![MBR du taille réel du disque](https://github.com/user-attachments/assets/4e19a991-e571-4872-873a-793312dc2532)

* La valeur 80 en Hexadécimal correspond au début de la partition.


![disque logique](https://github.com/user-attachments/assets/11f6038b-8409-43f9-bbce-c89c79f12478)

## Etude du BOOT RECORD
### Question A
Comparez le nombre de secteurs total à la taille de la partition (disque logique). indiquée dans le MBR ?
* le nombre de secteurs total pour le disque physique 3915776
* nombre de secteurs total pour le disque logique 3915712
### Question B
nombre secteurs par cluster?
* le nombre est de 8 secteur par cluster.
### Question C
Le "Boot record" se situe dans la zone "reserved sectors" du début de la partition. Quel 
espace cette zone occupe-t-elle ?
* disque physique - disque logique = 3915776 - 3915712 = 64
### Question D
 Combien y a-t-il de FAT et quel espace occupent-elles chacune ?
 * Il y'a 2 FAT et le nombre de secteur par est de 3816 secteurs.
### Question E
 Calculez le secteur de début de la 1ère FAT, de la 2ème FAT (copie de sécurité de la 
1ère), et de la zone de stockage de données. 
![MBR du taille réel du disque](https://github.com/user-attachments/assets/f5ee3b5b-78ae-4d61-b60a-3d11242af5b2)

* la 1ère FAT commence après les secteur reservé (560) la 2ème FAT commence après les secteur reservé plus les secteurs utilisé par la FAT1 (560 +3816).
  Stokage des donnée sur les secteur restant (3915713 -(560 + 2*3816))=3907521.

## Localistion d'un fichier

Pour le fichier toto :
- à l'offset 20 nous obtenons  le numéro du premier cluster du fichier (high word - 16 nits de poid fort) là 00 00
- à l'offset 26 nous obtenons le numéro du premier cluster du fichier (low word - 16 bits de poids faible) là 00 06
- à l'offset 28 nous obtenons la taille du fichier ici 00 00 00 17

Pour le fichier titi :
- à l'offset 20 nous obtenons  le numéro du premier cluster du fichier (high word - 16 nits de poid fort) là 00 00
- à l'offset 26 nous obtenons le numéro du premier cluster du fichier (low word - 16 bits de poids faible) là 00 07
- à l'offset 28 nous obtenons la taille du fichier ici 00 00 26 13

Pour le fichier tutu :
- à l'offset 20 nous obtenons  le numéro du premier cluster du fichier (high word - 16 nits de poid fort) là 00 00
- à l'offset 26 nous obtenons le numéro du premier cluster du fichier (low word - 16 bits de poids faible) là 00 0A
- à l'offset 28 nous obtenons la taille du fichier ici 00 00 17 CA

* Calcule de l'adresse de départ des données des fichiers :
- TOTO : 512*8*6 = 24576 
- TITI : 512*8*7 = 28672
- TUTU : 512*8*10 = 40960

offset pas de corrélation !
![adresse des fichiers](https://github.com/user-attachments/assets/998eb368-b095-4d60-baaf-17f65f4a773b)

