# Cruise control system
Ce document comporte l'ensemble des travaux réalisés (modélisation, exigences, extraction et vérification des propriétés...) durant la modélisation d'un régulateur de vitesse en utilisant le logiciel UPPAAL. Les propriétés de ce cas d'étude ont été extrait du document nommé *casestudyABZ2020v1.17.pdf* au niveau de la section *5.4 Software Functions*.

Rédaction des différentes propriétés: 

### SCS-1 

previousDesiredSpeed == 0
setVehicleSpeed >0 and setVehicleSpeed <5
control.OFF --> setVehicleSpeed = 0
control.ON -->setVehicleSpeed >0 and setVehicleSpeed <5
Après le démarrge du moteur, aucune vitesse souhaitée.
La vitesse souhaitée est comprise entre: setVehicleSpeed >0 and setVehicleSpeed <5
(Echelle de la vitesse a été réduite plutôt qu'elle soit comprise entre 1km/h et 200km/h)

### SCS-2 

control.ON --> setVehicleSpeed == currentSpeed or setVehicleSpeed == previousDesiredSpeed (propriété non vérifiée)

Lorsqu'on appuie sur 1(Forward) au niveau du régulateur de vitesse , la vitesse souhaitée (desired speed) est soit égale à la vitesse actuelle (s'il n'y a pas de vitesse souhaitée précédente) ou la vitesse souhaitée précedente (previousDesiredSpeed).

### SCS-3 

control.ON --> currentSpeed<=2 and previousDesiredSpeed!=0 (propriété verifiée)

Si la vitesse actuelle (currentSpeed) est inferieure à 20km/h et sans aucune vitesse précedente enregistrée alors le régulateur de vitesse ne s'activera pas.

### SCS-4

control.ON --> setVehicleSpeed == previousDesiredSpeed + 1 (propriété verifiée)

Si le conducteur pousse le levier du régulateur de vitesse vers 2(up) et qu'en même temps ce dernier est activé, la vitesse souhaité(setVehiculeSpeed) est augmentée de 1km/h.

### SCS-5
control.ON --> setVehicleSpeed == previousDesiredSpeed + 10 (propriété verifiée)
Si le conducteur pousse le levier du régulateur de vitesse à un angle de 7 degree au-dessus du premier la vitesse augmentera de 10km/h. Pour cela nous avons ajouté un état supplémentaire identique à celui de l'état increase afin de pouvoir verifier la propriété.

### SCS-6

control.ON --> setVehicleSpeed == previousDesiredSpeed - 1 (propriété verifiée)
control.ON --> setVehicleSpeed == previousDesiredSpeed - 10 (propriété verifiée)

Pousser le levier du régulateur de vitesse vers le bas(3) réduit la vitesse souhaité (De -1km/h et -10km/h respectivement selon les propriétés Req. SCS-4 et Req. SCS-5).
Un état additonnel sera rajouté au modèle afin de reduire la vitesse souhaitée de -10km/h et satisfaire la propriété ci-dessous:


### SCS-7

La notion d'horloge est requise pour évaluer cette propriété:
Le levier du régulateur de vitesse déplacé d'un angle de 5 degrée vers le haut (2: up) et maintenu pour une durée de 2 secondes tout en ayant le régulateur de vitesse activé, augmentera à chaque seconde la vitesse de 1km/h jusqu'à ce que le conducteur puisse placer le levier dans une position neutre.

### SCS-8

La notion d'horloge est requise pour évaluer cette propriété:
Le levier du régulateur de vitesse déplacé d'un angle de 7 degrée vers le haut (2: up) et maintenu pour une durée de 2 secondes 
tout en ayant le régulateur de vitesse activé, augmentera à chaque 2 secondes la vitesse de 10km/h jusqu'à ce que le conducteur
puisse placer le levier dans une position neutre.

### SCS-9

La notion d'horloge est requise pour évaluer cette propriété:
Le levier du régulateur de vitesse déplacé d'un angle de 5 degrée vers le bas (3: down) et maintenu pour une durée de 2 secondes 
tout en ayant le régulateur de vitesse activé, augmentera à chaque  seconde la vitesse de 1km/h jusqu'à ce que le conducteur
puisse placer le levier dans une position neutre.

### SCS-10

La notion d'horloge est requise pour évaluer cette propriété:
Le levier du régulateur de vitesse déplacé d'un angle de 7 degrée vers le bas (3: down) et maintenu pour une durée de 2 secondes 
tout en ayant le régulateur de vitesse activé, augmentera à chaque 2 secondes la vitesse de 10km/h jusqu'à ce que le conducteur
puisse placer le levier dans une position neutre.

### SCS-11

La notion d'horloge est requise pour évaluer cette propriété:
Le levier du régulateur de vitesse déplacé d'un angle de 5 degrée vers le bas (3: down) et maintenu pour une durée de 2 secondes 
tout en ayant le régulateur de vitesse activé, augmentera à chaque  seconde la vitesse de 1km/h jusqu'à ce que le conducteur
puisse placer le levier dans une position neutre.

### SCS-12

control.OFF --> setVehicleSpeed == 0 (propriété verifiée)

Déplacer le levier du régulateur de vitesse vers la position 4 (Backward), désactive le régulateur de vitesse.


### SCS-13

Cette section regroupe l'ensemble des exigences dont les propriétés ont été effectuées précedemment. 
(Reqs. SCS-1 à SCS-12)

### SCS-14

Tant que le régulateur de vitesse est activé, le vehicule maintient la vitesse actuelle du véhicule au même niveau que la vitesse désirée sans que le conducteur ne puisse appuyer sur la pédale de frein.

### SCS-15

Cette manipulation est effectuée de façon autonome par le moteur.

### SCS-16

En appuyant sur le frein, le régulateur de vitesse est désactivée jusqu'à ce qu'il soit de nouveau activé.

### SCS-17

En poussant le levier de vitesse vers l'arrière, le régulateur de vitesse se désactive jusqu'à ce qu'il soit de nouveau réactivé.

