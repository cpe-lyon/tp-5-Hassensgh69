# TP 5 - Systèmes de fichiers, partitions et disques

## Exercice 1. Disques et partitions

1. Dans l’interface de configuration de votre VM, créez un second disque dur, de 5 Go dynamiquement
alloués ; puis démarrez la VM

![image](https://user-images.githubusercontent.com/80455696/194237396-4d76149b-5857-4d96-9221-d9b9bb0be2fe.png)

2. Vérifiez que ce nouveau disque dur est bien détecté par le système

Avant l'ajout du nouveau dique dur nous avons qu'un seul disque dur; nous pouvons le voir grace a la commande `lshow -C disk`

![image](https://user-images.githubusercontent.com/80455696/194242744-069c0ad5-6970-436d-84eb-2b1a75a693f9.png)

Après l'ajout du nouveau disque on peut voir qu'un nouveau disque est apparue sur la liste et donc le disque dur a bien été detecter :

![image](https://user-images.githubusercontent.com/80455696/194242628-37375a12-194f-4b3d-af12-3b8608084828.png)

3. 3. Partitionnez ce disque en utilisant fdisk : créez une première partition de 2 Go de type Linux (n°83), et une seconde partition de 3 Go en NTFS (n°7)

Grace a la commande `fdisk /dev/sdc -l` qui nous indique le type de chaque partion on peut voir qu'on a bien les deux paritions demandés :

![image](https://user-images.githubusercontent.com/80455696/194247616-bc6d2880-605b-4898-9e08-e0ed6718cee7.png)

4. A ce stade, les partitions ont été créées, mais elles n’ont pas été formatées avec leur système de fichiers.A l’aide de la commande mkfs, formatez vos deux partitions 

Pour formater la première partition on tappe la commande suivante `mkfs.ext4 /dev/sdc1`

![image](https://user-images.githubusercontent.com/80455696/194264149-aed64855-95e3-4b6c-a2ac-1f5a2814e47c.png)

Et pour formater la seconde partition on tappe la commande suivante `mkfs.ntfs /dev/sdc2`

![image](https://user-images.githubusercontent.com/80455696/194265417-013c2108-6121-4d66-9f47-a8f698e8b22c.png)

5. Pourquoi la commande df -T, qui affiche le type de système de fichier des partitions, ne fonctionne-telle pas sur notre disque ?

La commande `df -T` ne marche pas car nos disques ne sont pas encores montés .

6. Faites en sorte que les deux partitions créées soient montées automatiquement au démarrage de la machine, respectivement dans les points de montage /data et /win (vous pourrez vous passer des UUID en raison de l’impossibilité d’effectuer des copier-coller)

Pour ce faire j' ajoute a la fin du fichier /etc/fstab `/dev/sdc1 ext4 defaults 0 0` et `/dev/sdc2 ntfs defaults 0 0`

![image](https://user-images.githubusercontent.com/80455696/194273645-b7ba75a9-f793-4476-bd84-c7045d15e9a0.png)

7. Utilisez la commande mount puis redémarrez votre VM pour valider la configuration

      sudo mount /dev/sdc1 /data
      sudo mount /dev/sdc2 /win
      
8. Montez votre clé USB dans la VM

      sudo mount /dev/usb  /data1
      
9.       


## Exercice 2. Partitionnement LVM
