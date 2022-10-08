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

3. Partitionnez ce disque en utilisant fdisk : créez une première partition de 2 Go de type Linux (n°83), et une seconde partition de 3 Go en NTFS (n°7)

Grace a la commande `fdisk /dev/sdb -l` qui nous indique le type de chaque partion on peut voir qu'on a bien les deux paritions demandés :

![image](https://user-images.githubusercontent.com/80455696/194697648-df8bb0f3-ed46-41f3-a3ab-9975bec7f094.png)

4. A ce stade, les partitions ont été créées, mais elles n’ont pas été formatées avec leur système de fichiers.A l’aide de la commande mkfs, formatez vos deux partitions 

Pour formater la première partition on tappe la commande suivante `mkfs.ext4 /dev/sdb1`

![image](https://user-images.githubusercontent.com/80455696/194264149-aed64855-95e3-4b6c-a2ac-1f5a2814e47c.png)

Et pour formater la seconde partition on tappe la commande suivante `mkfs.ntfs /dev/sdb2`

![image](https://user-images.githubusercontent.com/80455696/194265417-013c2108-6121-4d66-9f47-a8f698e8b22c.png)

5. Pourquoi la commande df -T, qui affiche le type de système de fichier des partitions, ne fonctionne-telle pas sur notre disque ?

La commande `df -T` ne marche pas car nos disques ne sont pas encores montés .

6. Faites en sorte que les deux partitions créées soient montées automatiquement au démarrage de la machine, respectivement dans les points de montage /data et /win (vous pourrez vous passer des UUID en raison de l’impossibilité d’effectuer des copier-coller)

Pour ce faire j' ajoute a la fin du fichier /etc/fstab `/dev/sdc1 ext4 defaults 0 0` et `/dev/sdc2 ntfs defaults 0 0`

![image](https://user-images.githubusercontent.com/80455696/194697881-477ca0d5-8258-485c-8931-b7d84fef6506.png)

7. Utilisez la commande mount puis redémarrez votre VM pour valider la configuration

            sudo mount /dev/sdb1 /data
            sudo mount /dev/sdb2 /win
      
8. Montez votre clé USB dans la VM

            sudo mount /dev/usb  /data1
      
9.       


## Exercice 2. Partitionnement LVM


1. On va réutiliser le disque de 5 Gio de l’exercice précédent. Commencez par démonter les systèmes de
fichiers montés dans /data et /win s’ils sont encore montés, et supprimez les lignes correspondantes
du fichier /etc/fstab

Pour demonter les sytèmes fichiers montés dans /data et /win on tappe la commande suivante ` sudo umount /win ` et ` sudo umount /data`

![image](https://user-images.githubusercontent.com/80455696/194698212-07777576-78d2-456a-95b7-1ec3f009c3d2.png)

Apres avoir fait ca on va supprimer les les lignes correspondantes u fichier /etc/fstab.

2. Supprimez les deux partitions du disque, et créez une partition unique de type LVM

Pour supprimer les deux partitions on tappe la commande suivante `sudo fdisk /dev/sdb`

![image](https://user-images.githubusercontent.com/80455696/194698431-cb84a20c-c31d-40e5-999e-7b40fae3b474.png)

On créer ensuite une nouvelle partition :

![image](https://user-images.githubusercontent.com/80455696/194701726-628e435f-0fa0-4897-b5aa-4b1bade3535d.png)

3. A l’aide de la commande pvcreate, créez un volume physique LVM. Validez qu’il est bien créé, en
utilisant la commande pvdisplay.

La commande `pvcreate` permet de créez un volume physique LVM.

![image](https://user-images.githubusercontent.com/80455696/194699067-30c856ea-cd8e-43e9-bb6b-8aab23305213.png)

La commande `pvdispaly` permet de validez que le volume physique LVM a bien été créer.

![image](https://user-images.githubusercontent.com/80455696/194699078-413ee36f-2f6f-4234-95fe-f3aa343bb8d1.png)

4. A l’aide de la commande vgcreate, créez un groupe de volumes, qui pour l’instant ne contiendra que
le volume physique créé à l’étape précédente. Vérifiez à l’aide de la commande vgdisplay.

![image](https://user-images.githubusercontent.com/80455696/194699306-a06623cc-b544-4c6a-947f-d69bb3d723fe.png)

5. Créez un volume logique appelé lvData occupant l’intégralité de l’espace disque disponible

![image](https://user-images.githubusercontent.com/80455696/194699501-9b234c72-fbe6-4ecf-9491-eede725b9031.png)

6. Dans ce volume logique, créez une partition que vous formaterez en ext4, puis procédez comme dans
l’exercice 1 pour qu’elle soit montée automatiquement, au démarrage de la machine, dans /data.

![image](https://user-images.githubusercontent.com/80455696/194699866-c2b53a20-19a2-44d9-9326-add772ef345c.png)

![image](https://user-images.githubusercontent.com/80455696/194699997-6ce91d70-08dc-4ef5-a40b-6388c68a4007.png)

7. Eteignez la VM pour ajouter un second disque (peu importe la taille pour cet exercice). Redémarrez
la VM, vérifiez que le disque est bien présent. Puis, répétez les questions 2 et 3 sur ce nouveau disque.

