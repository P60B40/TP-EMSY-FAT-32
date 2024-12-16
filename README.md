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
