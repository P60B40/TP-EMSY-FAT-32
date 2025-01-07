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
### Question F représentation graphique de la FAT

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

## Calcule de l'adresse de départ des données des fichiers :
- TOTO : 512 * 8 * 6 = 24576 
- TITI : 512 * 8 * 7 = 28672
- TUTU : 512 * 8 * 10 = 40960

offset pas de corrélation !
![adresse des fichiers](https://github.com/user-attachments/assets/998eb368-b095-4d60-baaf-17f65f4a773b)

## Secteur utilisé :
- en vert TOTO
- en orange TITI
- en rouge TUTU
![secteur fichier](https://github.com/user-attachments/assets/e0f14b0e-e766-4c15-88ce-d8e6aa1655bf)

## Visualisation du contenue des fichier :
- Toto
 ![contenu toto](https://github.com/user-attachments/assets/9755bf21-394b-4474-8602-c04da39ba00c)
- Titi (début)
 ![contenu titi1](https://github.com/user-attachments/assets/9a28c57c-2855-4b4c-a59c-339e70b4f940)
- Titi (fin)
![contenu titi2](https://github.com/user-attachments/assets/7da72772-55bb-4e32-952e-565f53913c9b)
- Tutu (début)
![contenu tutu1](https://github.com/user-attachments/assets/3999469a-e5ea-4610-9955-1afedbc5a842)
- Tutu (fin)
![contenu tutu2](https://github.com/user-attachments/assets/99c0b5ab-6867-4c54-85f2-6ca87d23c697)

## Effacement d'un fichier :
Nous avons effacer le fichier Titi.txt

![effacement du fichier titi](https://github.com/user-attachments/assets/bb909172-534f-4e13-b7b0-52c9490202cb)

Dans la FAT nous ne voyons pas le fichier Titi on le voit avec les données 00 qui remplace les données FF, dans le Root directory Titi est toujours présent 

![root directory titi toujours présant](https://github.com/user-attachments/assets/5897e496-0896-47d4-bcf2-22e2d0738ec2)

Les données du fichier txt sont toujours présent :

![donée titi toujours présantes](https://github.com/user-attachments/assets/13edd308-8b33-466e-bb36-7a9fa249eebc)

## Restauration d'un fichier effacer :
pour la restauration du fichier nous pouvons remettre les secteurs utilisés dans la FAT
### Déscriptions de la manipulation :
- Appuyer sur Edit dans le menu en haut
- Nous allons réecrire le contenue précedent (avant effacement des données) dans la FAT)
- Sauvegarder les modification avec le boutton save (ne pas oublier de relancer Disk Editor)
![recovery titi](https://github.com/user-attachments/assets/7347b803-1fbb-4c6c-9443-7bcdaaa3d436)
- On peut voir que le fichier et de retour
![titi le retour](https://github.com/user-attachments/assets/c53db823-097d-4ad8-9f5f-15148a567c86)

### Effet de la fragmentation des fichiers :
- On constate que le fichier Titi prend plus de secteur.
![donée titi toujours présantes](https://github.com/user-attachments/assets/18d0065f-7ce7-4aa4-8136-8642bd8917c7)
- Par rapport au adresse nous remarquons que le fichier Titi se trouve dans un secteur plus loin après le fichier Tutu, les données sont donc fragmenter dans deux secteurs qui ne se suivent pas
![titi suite donnée frag](https://github.com/user-attachments/assets/f105d639-fa58-4389-a5aa-807ec74df0fb)

## Expérimentation des noms de fichiers longs :
### Visualistion de la FAT :
* les données souligner en jaune montre le fichier ajouté
![nom de fichier long fat](https://github.com/user-attachments/assets/25aeaee9-b922-4b01-bc54-4b6cf7058a66)

### Root directory :
* dans le root directory nous pouvons voir que le nom prend plus de place
![root directory nom long](https://github.com/user-attachments/assets/1172d252-4239-4502-b508-7eb1c85cf8f8)

### Donnée du fichier :
* nous pouvons remarquer que nous avons bien nos données dans le fichier (nom, classe et date )
![donnée nom long](https://github.com/user-attachments/assets/97359203-2876-4889-b345-62b2a7bccdfd)

## Expérimentation avec les sous-repertoires :
### Visualisation de FAT :
* nous avons un nouveau secteur réserver dans la FAT
![repertoire créé](https://github.com/user-attachments/assets/c1f33a80-2467-4db4-a291-add23b27e814)
* dans le Boot record nous avons bien un nouveau dossier avec le nom essai
![boot record essai](https://github.com/user-attachments/assets/25a9a5fa-6021-4eac-8c45-957b593b1b0c)

### Copie du fichier Toto : 
* nous pouvons voir qu'un nouveau secteurs est réserver dans la FAT
![copie toto](https://github.com/user-attachments/assets/45184513-647b-478c-9f1c-847a0156ca34)
* nous ne constatons pas de modification dans le Root directory, ce nous parrait n'est pas normal.

### Déplacement du fichier Titi dans le repertoire essai :
* Pas de modification dans la Fat
* Dans la root directory pas de changement non plus


