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

3. 
