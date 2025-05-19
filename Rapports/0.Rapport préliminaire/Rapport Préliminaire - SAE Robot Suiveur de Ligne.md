>RUIZ Evan Gr 3A
# **Introduction**

Le robot à pour but de se **diriger en autonomie** en **suivant une ligne marquée sur le sol**.

# **Cahier des charges**

L'objectif est de concevoir un robot capable de **suivre une ligne** de manière **autonome**. Le robot doit *démarrer et s'arrêter* à la suite d’un *claquement de mains.*

# **Spécifications**

## Environnement

Le robot sera en **intérieur**.

Des **sons** tels que les *claquements de mains* et des *sons parasites* vont réagir avec le robot

Ensuite, de la **lumière** *reflèteras sur la piste* ainsi que des *lumières parasites*

## Spécifications fonctionnelles

Il doit **réagir aux claquements de mains**. Cependant, des **sons parasites**, résonné par les murs de la pièce par exemple, peuvent interférer avec le robot.

De plus, il doit **indiquer sont état** (veille / allumé) avec *une LED*

Ensuite, le robot doit pouvoir se déplacer en **suivant** une *ligne blanche sur fond noir*. On va faire **reflétée de la lumière sur la piste blanche** pour qu’*il détecte sa présence* et *la suivre*. Cependant, des **lumières parasites** peuvent venir gêner le robot et le faire dévier de sa trajectoire.

Enfin, il doit **être autonome**, c’est-à-dire qu’il doit être *alimenté avec des piles*.

## spécifications opérationnelles

Le robot devra **suivre une ligne blanche** qui comporte des *virages*, parfois des *absences de piste* mettront le robot à l’épreuve. Il devra **aller tout droit**.

Lors d’un croisement de piste le robot s’arrêtera et en ligne droite il atteindra sa vitesse maximale.

Il sera **commandé par claquement de main**, au premier claquement de main il *s’allumera* et au second il* s’arrêtera*. Le claquement de main serait au plus loin à 10m.

Une LED affichera son état, s’il est en **veille**, la LED sera *allumée* et si il est en **marche**, une *LED blanche s’allumera* et *son intensité variera* en fonction de la lumière reçu par le capteur.

**Par défaut le robot sera en veille.**

## Spécifications technologiques

Le robot sera conçu à partir d’**électronique analogique**, les composants que nous allons utiliser seront : CNY70, SG3524, NE555, CD4017, BD438, capteur à électrets, moteurs à courant continu. 

De plus il sera alimenté par des piles : **1 pile de 9V** pour la *partie commande* et **4 piles de 1.5V** en série pour *la partie puissance*.

Les circuits imprimés conçu par nous-même seront reliée ensemble par une **carte fond de panier** *fournis*.

Les logiciels mis à notre disposition sont *Micro-Cap et Eagle*.

Le supports que l’on va nous fournir est constitué de 2 roues motorisées, d’une carte des yeux, d’une carte fond de panier et d’emplacements des piles, elles aussi fournis.

# Fonctionnement

Le robot se **repère** grâce à des *capteurs infrarouge*s placés à l'avant sous le robot.

 Il **suit une ligne blanche** qu’il détecte grâce à la lumière réfléchis par la piste, s’il **ne détecte pas la ligne**, il ira *tout droit*.

De plus, **ajuste sa trajectoire** en fonction des informations captées, comme des intersections.

Le **capteur gauche** contrôle le *moteur gauche* et le **capteur droit** contrôle le *moteur droit*.

Si le **capteur gauche** ne détecte *plus de lumière* et que le **capteur droit** détecte encore la *lumière* alors le **moteur droit** iras *plus vite* que le moteur gauche pour **tourner à droit**, et inversement.

# Conception Fonctionnelle

## Ordre 1

![[schéma ordre 1 - seance 0.png]]
## Ordre 2

![[schéma ordre 2 -  seance 0.png]]

## F1 : Détection du claquement de mains

- Le robot détecte le **claquement de mains** à une distance comprise entre *5m et 10m* grâce à un *micro à électret* placé sur le haut de la carte et le **transforme** en un *ordre de marche/arrêt*.

 - Une *LED de 5mm* sur le haut de la carte **affiche son état** de veille (allumé = veille) et l’intensité lumineuse reçu par la piste (par une LED blanche).

- La tension de sortie passe à **9V** s’il est à l’*arrêt* et à **0V** s’il est en *marche*.

## F2 : Repérage par rapport à la piste

- Le robot se repère par rapport à la piste, il **émet** *des infrarouges* pour sonder le sol et **capter** *les infrarouges réfléchis*. Il doit être capable de **différencier** les lumière réfléchis par la piste par rapport aux *lumières parasites*.

- Chaque capteur va recevoir un signal, il sera de **6V** s’il détecte la *piste blanche* et il sera de **0V** s’il ne détecte *rien*.

- Ensuite il va émettre de la lumière avec une **LED blanche**, son *intensité varie* en fonction de la quantité de lumière capté. S’il est **au-dessus de la piste blanche** son intensité sera *maximal* et inversement s’il ne capte rien.

- La carte comportant les capteurs sera fournie. On utilise le *CNY70* comme composant et l’**alimentation** se fait par une *pile 9V*.

## F3 : Commande du déplacement

- **Chaque moteur** est*indépendant*, donc l**eur vitesse peut varier** afin de faire *tourner le robot*. Ainsi le robot peut **s’adapter au parcours**.

- En fonction de sa position sur la piste il pourra **adapter la vitesse d’un de ses moteurs** pour par exemple suivre un virage. Pour cela, il y à **un capteur par moteur**, le *capteur de droite commande le moteur de droite* et *inversement pour le moteur de gauche*.

- Si on reçoit un signal de **0V** on sait que le moteur est à sa *vitesse maximal*, inversement s’il on reçois un signal de **6V**, le moteur est à la *vitesse minimum*.

- On doit pouvoir **récupérer les signaux de commandes** des *moteurs* ainsi que **contrôler le courant** dès les *moteurs*. Le courant d’un moteur est **limité à 1A**.

- La **marche/arrêt** sera gérer en fonction du *signal d’autorisation de déplacement*, c’est-à-dire le claquement de main.

- Si le signal est à **9V** alors il est *à l’arrêt* et *inversement* s’il est à **0V**.

- La **partie commande** (capteurs et SG 3524 [contrôleur PWM]) seront *alimenté par une pile 9V* tandis que la **partie puissance**  (moteurs [à courant continu de 6V et courant nominal de 600mA] et transistor BD 438) seront alimenté par *4 piles en 6V*. Attention il faut **prévoir un découplage** **pour chaque partie** de *100µF*