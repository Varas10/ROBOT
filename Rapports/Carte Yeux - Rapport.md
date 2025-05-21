# 0. Introduction

Le robot à pour but de se **diriger en autonomie** en **suivant une ligne marquée sur le sol**.

## Cahier des charges

L'objectif est de concevoir un robot capable de **suivre une ligne** de manière **autonome**. Le robot doit *démarrer et s'arrêter* à la suite d’un *claquement de mains.*

## Spécifications

### Environnement

Le robot sera en **intérieur**.

Des **sons** tels que les *claquements de mains* et des *sons parasites* vont réagir avec le robot

Ensuite, de la **lumière** *reflèteras sur la piste* ainsi que des *lumières parasites*

### Fonction principale

Le robot doit :

- Être **commandé par des claquements de mains** (allumage/extinction).
    
- **Suivre une ligne blanche sur fond noir** de manière autonome.
    
- **Afficher son état de fonctionnement à l’aide de deux LEDs** distinctes.
    
- Être **alimenté uniquement par piles**.
    

---

### Spécifications Fonctionnelles

- Réagit **aux claquements de mains**, tout en filtrant les **sons parasites** (bruits d’ambiance ou réverbération).
    
- **Affichage de l’état par deux LEDs** :
    
    - Une **LED rouge** : _allumée en mode veille_.
        
    - Une **LED blanche** : _allumée en mode actif_, avec **intensité variable** en fonction de la lumière détectée par les capteurs IR.
        
- Détection de piste basée sur la **réflexion de lumière infrarouge** sur la **ligne blanche**.
    
- Intégration de filtres et d’amplification pour éviter les **interférences lumineuses extérieures**.
    

---

### Spécifications Opérationnell**

- Le robot suit une **ligne blanche sinueuse**, même en cas de **virages ou interruptions temporaires**.
    
- Il doit :
    
    - **Aller tout droit** par défaut.
        
    - **S’arrêter** automatiquement en cas de **croisement de piste**.
        
    - Atteindre sa **vitesse maximale** sur ligne droite.
        
- Commande sonore par claquements :
    
    - 1er claquement → **activation** du robot.
        
    - 2e claquement → **arrêt** du robot.
        
    - Portée maximale : **10 mètres**.
        
- Par défaut, le robot est en **mode veille**.
    

---

### Spécifications Technologiques

- Technologie : **électronique analogique uniquement**.
    
- Composants principaux :
    
    - **CNY70** (capteurs IR),
        
    - **NE555**, **SG3524**, **CD4017**, **BD438**,
        
    - **Capteur à électret**,
        
    - **Moteurs à courant continu**.
        
- **Alimentation** :
    
    - **1 pile 9V** → pour la **commande**.
        
    - **4 piles de 1,5V (6V)** → pour la **puissance moteur**.
        
- Connexions assurées par une **carte fond de panier fournie**.
    
- Logiciels utilisés :
    
    - **Micro-Cap** (simulation analogique),
        
    - **Eagle** (routage des circuits imprimés).
        
- Support matériel fourni :
    
    - Châssis avec **2 roues motorisées**,
        
    - **Carte des yeux** (détection IR),
        
    - **Support de piles** intégré.
        

---

### Fonctionnement général

- Deux capteurs **infrarouges CNY70** situés à l’avant détectent la **réflexion de lumière** sur la ligne blanche.
    
- Le robot ajuste sa trajectoire en temps réel :
    
    - Le **capteur gauche** contrôle le **moteur gauche**,
        
    - Le **capteur droit** contrôle le **moteur droit**.
        
- Logique de suivi :
    
    - Si le capteur gauche **perd la piste** et le droit la détecte → le robot **tourne à droite**.
        
    - Inversement pour un virage à gauche.
        
- Si **aucune piste n’est détectée**, il **avance en ligne droite**.


## Conception Fonctionnelle

### Ordre 1

![[schéma ordre 1 - seance 0.png]]
### Ordre 2

![[schéma ordre 2 -  seance 0.png]]

### F1 : Détection du claquement de mains

- Détection du **claquement de mains** entre **5 et 10 m** via un **micro à électret**.
    
- Sert à **passer de l’état de veille à la marche** (et inversement).
    
- Une **LED 5 mm** indique l’état de **veille** (allumée = en veille).
    
- **Signal de sortie** :
    
    - **9V** = robot **à l’arrêt**
        
    - **0V** = robot **en marche**
        

---

### F2 : Suivi de piste (capteurs IR)

- Utilise des capteurs **CNY70** pour **émettre et capter** des infrarouges réfléchis par le sol.
    
- Objectif : **différencier la piste blanche** des autres surfaces ou lumières parasites.
    
- **Sortie capteurs** :
    
    - **6V** = piste blanche détectée
        
    - **0V** = rien détecté
        
- Une **LED blanche** ajuste son **intensité** selon la lumière reçue :
    
    - Forte intensité = piste bien détectée
        
    - Faible intensité = hors piste
        
- **Alimentation capteurs** : **pile 9V**
    

---

### F3 : Commande et contrôle des moteurs

- Deux moteurs **indépendants**, chacun commandé par un capteur :
    
    - Capteur droit → moteur droit
    - Capteur gauche → moteur gauche

- **Signal reçu par chaque moteur** :
    
    - **0V** = moteur à **vitesse maximale**
    - **6V** = moteur à **vitesse minimale**

- Permet au robot de **s’adapter au parcours** (virages, corrections de trajectoire).
    
- On peut :
    
    - **Récupérer les signaux de commande** des moteurs
    - **Contrôler le courant** fourni à chaque moteur

- **Courant moteur limité à 1A**

- **Alimentations séparées** :
    
    - Partie **commande** (capteurs, SG3524) : **pile 9V**
    - Partie **puissance** (moteurs, BD438) : **4 piles = 6V**

- Nécessité d’un **découplage avec condensateurs 100µF** pour **chaque partie**

# 1. Émettre et Recevoir de la lumière
## **Étude théorique**

### Présentation du capteur CNY70

- **Type de lumière émise** : Infrarouge (λ = 950 nm).
    
- **Spectre** : Non visible à l'œil nu.
    
- **Constitution** du capteur :
    
    - **Diode émettrice** : Cathode et anode identifiées sur le schéma.
    - **Phototransistor récepteur** : Collecteur (C) et émetteur (E) également identifiés.

### Schéma de routage

- Le schéma fourni montre la carte "yeux" avec :
    
    - **Entrée** : Signal générant la lumière codée.
    - **Sorties** :
        - Capteur 1 : Broche 4.
        - Capteur 2 : Broche 3.
		
    - **Alimentation** : 9V.
    - **Masse**.

- **Trajet du courant** : Surligné en rouge sur le schéma pour visualiser le chemin de l’émission lumineuse.
    
	![[Routage, chemin du courant entre les deux capteurs - Seance 1.jpg]]
### Fonctionnement du montage transistor

- Choix du montage : **Montage collecteur commun** pour obtenir une **tension Vout** qui augmente avec l’intensité lumineuse reçue.
    
- Relations utilisées : $Vcc = Vce + Ic \times Re$
	
- Calculs :
    
    - **Re** :$Re=\frac{V_{cc}-V_{ce}}{I_{c}}=\frac{9V−0V}{0,001A}=9000 Ω$
    - **Vce** pour 50mA d’émission : ≈ 0,3V.
    - **Vout** correspondant : $Vout=9V−0,3V=8,7V$

### Limitation du courant LED

- On fait donc varier RE pour ne pas dépassé $I_c=2mA$ 
	Avec $I_{C_{max}}$: $R_{E}=\frac{Vcc-V_{CE}}{I_{C}}=\frac{9-0.1}{0.002}=4,450k\ohm$
	Avec $I_{C_{tres petit}}:RE=\frac{9-0.1}{0,00001}=89k\ohm$
- Calcul de la résistance RLed pour limiter le courant LED à 50 mA sous 9V :
    $RLed=\frac{Vcc-V_{D}}{I_{D}}=\frac{9−1,25}{0.05}=155 Ω$ (150$\ohm$ en valeur normalisée E12)
	
- Schéma lorsque le capteur est sur du blanc :
	![[Sortie module avec lumière - seance 1.png]]
	On constate que la sortie ne dépasse pas les 9V
	
- Schéma lorsque le capteur est entre le blanc et le noir :
	![[sortie module avec lumière entre blanc et noir - seance 1.png]]
	La sortie est bien à 4,5V.
	
## Résultats attendu :
- Lorsque la lumière est très forte (10) :
	![[Lumière a 10 - seance 1.png]]
- Lorsque la lumière est moyenne (5) :
	![[lumière à 5 - seance 1.png]]
- Lorsque la lumière est très faible (1) :
	![[lumière à 1 - seance 1.png]]

## **Étude pratique**

### Câblage de la carte

- **Entrée du signal générant la lumière codée** : 9V.
- **RLeds** : 150 Ω installée (protection des LEDs).
- **Re** : montage ajustable pour limiter le courant dans les phototransistors.

### Mesures réalisées

- **Mesure du courant LED** :
    $I_{LED} =\frac{Vled}{Rled} \frac{5,37V}{150\,\Omega} = 35\, mA$

- **Mesures de Vout** :
    - **Surface blanche** : 0,1 V.
    - **Surface noire** : 0 V.

### Rejet des lumières parasites

- Pour éviter l'influence de l'éclairage ambiant, la lumière émise est modulée :
    
    - **Signal carré** appliqué : 0-9V, **fréquence = 2kHz**.

- Relevés :
    
    - Signal codé généré pour la lumière (en bleu) et signal de sortie en jaune:
		- Surface blanche :
		![[fond blanc seance 2.jpg]]
		- Surface noir :
		![[fond noir seance 2.jpg]]
### Résultats observés

- Lorsque la surface est blanche, Vout présente une réponse claire et modulée.
    
- Lorsque la surface est noire, Vout est quasiment nul, ce qui permet une détection fiable du changement de surface.
    

### Conclusion 

Grâce à cette étude, la conception de la carte "yeux" permet d’assurer :

- La bonne émission de lumière infrarouge.
- La détection fiable des surfaces via un phototransistor.
- La protection des composants par le choix adapté des résistances.

L'étude pratique a permis de :

- Vérifier le fonctionnement du montage théorique.
- Valider la modulation comme méthode efficace pour rejeter les interférences lumineuses.
- S'assurer que le robot pourra différencier correctement les pistes claires et sombres lors de son suivi de ligne.
---
# 2. Génération d’un signal de lumière codée
## Analyse Théorique :

### **Objectif**

Le but de ce projet est de concevoir un système analogique permettant d’émettre un signal lumineux codé, qui pourra être reçu et traité par un récepteur optique. L’objectif est d’assurer une transmission fiable de l’information en utilisant la modulation lumineuse, ce qui permet également de réduire l’influence des lumières parasites présentes dans l’environnement.

### **Principe du codage lumineux**

L’information est envoyée sous forme binaire avec une LED infrarouge :

- **1** → La LED s’allume
    
- **0** → La LED s’éteint

Pour éviter les interférences avec la lumière ambiante (comme le soleil ou les lampes), le signal est **modulé** : la LED clignote à une fréquence de **2 kHz** pour chaque bit transmis. Cela permet au récepteur de mieux reconnaître le signal.

### Technique :

L’émission du signal lumineux est réalisée grâce à un circuit analogique composé de :

- Un **oscillateur** avec un **NE555** permettant de générer un signal carré périodique.
- Une **LED infrarouge** qui émet la lumière selon le signal de l’oscillateur.
- Une **résistance de limitation de courant** pour protéger la LED et assurer un fonctionnement stable.


Le **circuit oscillateur** est conçu de manière à produire un signal carré ayant :

- Une **tension de sortie oscillante entre 0V et 9V** (valeurs définies par l’alimentation du circuit).
- Un **rapport cyclique de 50 %**, garantissant un temps d’allumage et d’extinction égaux.
- Une **fréquence de 2 kHz**, assurant une bonne séparation entre les impulsions.

### **Schéma fonctionnel**

Le montage peut être représenté par le schéma fonctionnel suivant :

![[Pasted image 20250519182410.png]]

### **Calculs des composants**

La fréquence d’oscillation d’un NE555 en mode astable est donnée par la formule :
$f=\frac{1.44}{(R1+2R2)×C}$

En choisissant :
- $R9=R8=33kΩ$
- $C7=1nF$.

On obtient une fréquence de **2 kHz**, conforme aux spécifications du projet.

## **Réalisation pratique**

### Mesures et observations

#### 1. Vérification du signal généré

Le signal en sortie du circuit oscillateur a été mesuré à l’aide d’un oscilloscope :

- **Forme d’onde :** signal carré propre et stable.
- **Tension maximale :** 9V.
- **Tension minimale :** 0V.
- **Fréquence mesurée :** environ **2 kHz**, conforme aux calculs théoriques.

#### 2. Observation du fonctionnement de la LED

- Avec l'oscilloscope, on observe que la LED clignote bien à la fréquence attendue.

### Tests et validation du fonctionnement

Des tests ont été effectués en utilisant un oscilloscope branché a la sortie des capteurs pour vérifier la bonne transmission du signal :

- Le **capteur infrarouge (phototransistor)** détecte bien les impulsions lumineuses émises.
    
- Avec l'**oscilloscope**, on retrouve un signal modulé correspondant à celui envoyé par l’oscillateur.

### Chronogrammes observés

1. **Signal de l’oscillateur** (sortie NE555) :
    
    - Signal carré propre.
        
    - Fréquence stable à 2 kHz.
		
	- Vlumière est en jaune et Vcondensateur est en bleu.
	 ![[Vlum (jaune) et Vc (bleu).jpg]]
	
2. **Signal lumineux détecté par la photodiode** :
    
    - Même fréquence de 2 kHz.
    - Amplitude variable en fonction de la distance et de l’alignement du capteur.
    - Fond blanc :![[fond blanc seance 2.jpg]]
	- Fond noir :![[fond noir seance 2.jpg]]
	
### Difficultés rencontrées et solutions apportées

- **Problème :** LED infrarouge trop faible dans certains cas.
    - **Solution :** Augmentation du courant en ajustant la résistance de limitation (passage de 150Ω à 100Ω).

### Conclusion de la séance

L’émission du signal lumineux codé a été validée par des mesures expérimentales.

- Le circuit oscillateur produit un **signal carré propre**.
    
- La LED infrarouge **suit précisément le signal généré**.
    
- Un récepteur optique permet de **détecter les impulsions lumineuses correctement**.

# 3. Mise en forme du signal Vout

### Objectif

Le signal Vout, issu du capteur optique (phototransistor), est un signal analogique modulé à la fréquence de la lumière codée (2 kHz). Ce signal comporte deux composantes :

- Une **composante alternative (AC)**, qui est l’image de la lumière codée (modulation de 2 kHz).
    
- Une **composante continue (DC)**, due à la lumière ambiante et aux caractéristiques propres du capteur.

L’objectif de ce projet est de **supprimer la composante continue** pour ne conserver que la **composante alternative**, représentative du signal lumineux codé reçu.

### Solution technique : le filtre passe-haut

On utilise un **filtre passe-haut** (filtre RC) pour supprimer la composante continue et ne laisser passer que les signaux alternatifs de fréquence suffisante.

#### Schéma de principe :

![[Filtre passa haut.png]]

#### Calcul de la fréquence de coupure

La **fréquence de coupure Fc** du filtre est choisie telle que :

$Fc=12πRC$ 
$Fc = \frac{1}{2 \pi R C}$
$Fc=2πRC1​$

Objectif : que **$Flum = 2 kHz$** soit **dans la bande passante**, donc $Fc < Flum$. On choisit :

- **Fc = 200 Hz**, soit $Flum / 10.$
    

#### Choix des composants :

- **C = 100 nF**
    
- **R = 1 / (2π × 100 nF × 200 Hz) ≈ 7957 Ω**, (valeur normalisé E12 = 6,8k$\ohm$)

Ce filtre permet d’atténuer fortement les composantes inférieures à 200 Hz (dont le continu), tout en laissant passer efficacement la modulation de 2 kHz.

### Conclusion du projet

Le montage permet de :

- Supprimer la composante continue de Vout (liée aux conditions d’éclairage ambiant).
    
- Conserver uniquement le signal modulé à 2 kHz, qui représente l’information utile.
    
- Faciliter le traitement ultérieur du signal (amplification, démodulation).

## Réalisation du filtre de Vout

### Tests et chronogrammes

#### 1) Signal sinusoïdal appliqué (test de fréquence)

- Signal d’entrée Ve : sinusoïdal, amplitude 8 V, fréquence variable (Ve en bleu).
    
- Signal de sortie Vs : réponse du filtre (Vs en jaune).
	
- ![[filtrage ve.png]]

On a testé trois cas :

|**Fréquence (f)**|**Vs (amplitude crête-à-crête)**|**Atténuation**|**Bande passante**|
|---|---|---|---|
|**Fc / 10 = 20 Hz**|0,7 V|Forte|Non|
|**Fc = 200 Hz**|5,4 V|Moyenne|Non (limite)|
|**10 Fc = 2 kHz**|8 V|Aucune|Oui|

#### Calcul de l’atténuation (A = Vs / Ve)

|Fréquence|A|
|---|---|
|20 Hz|0,088|
|200 Hz|0,675|
|2 kHz|1|

**Conclusion :** Le filtre laisse bien passer la composante 2 kHz tout en atténuant fortement les basses fréquences et le continu.

---

### b) Application avec Vout réel

- **Signal Vout** (brut) connecté à l’entrée du filtre.
    
- **Sortie filtrée** observée à l’oscilloscope.
    

#### **Résultats observés :**

- **Surface noire** : pas de signal modulé, donc Vs ≈ 0.
	![[vout modulé surface noir.png]]
- **Surface blanche** : modulation claire à 2 kHz visible sur Vs.
	![[Vout modulé surface blanche.png]]

Le filtre a bien supprimé le décalage continu et a laissé passer uniquement la modulation utile.

---

### Conclusion de la séance

Le filtre RC mis en œuvre permet efficacement de :

- Éliminer la composante continue indésirable.
    
- Préparer le signal pour les étapes suivantes (amplification et démodulation).
    
- Améliorer la lisibilité et la fiabilité du signal de suivi lumineux.

# 4. Amplifier Vout filtrée :

### Objectif :

Cette séance vise à concevoir un amplificateur qui augmente l’amplitude du signal filtré sans en altérer la forme, pour préparer la démodulation.
### Analyse du besoin :

- Le signal **Vout filtrée** correspond à une modulation d’amplitude liée à l’intensité lumineuse réfléchie par le sol (blanc ou noir).
    
- D’après les mesures expérimentales :
    
    - Pour une surface **blanche**, Vout filtrée ≈ **1,5 V crête**
        
    - Pour une surface **noire**, Vout filtrée ≈ **0 V**
        
- Le cahier des charges impose une **tension de sortie amplifiée d’environ 9 V** pour une surface blanche.

### Choix de la solution :

Un **amplificateur opérationnel non-inverseur** est retenu car il permet :

- Une **impédance d’entrée élevée**, évitant de charger le montage précédent.
    
- Une **conservation de la phase du signal** (pas d’inversion).
    
- Un gain ajustable selon la formule :
    
    $A_v = 1 + \frac{R_2}{R_1}$

### Calculs :

Pour obtenir un gain de 6 (objectif : 1,5 V → 9 V) :

- Choix de $R_1 = 680\ \Omega$ (valeur normalisée)
    
- Calcul de $R2=(Av−1)×R1=5×680=3400 Ω$
    
- Choix de $R_2 = 3.3\ k\Omega$ (valeur normalisée proche)
    

### Simulation :

-  ![[v out amplifié.png]]
    
- Entrée : signal sinusoïdal de 1,5 V crête à 2 kHz.
    
- Résultat : signal amplifié à 9 V crête, sans distorsion notable.

## Réalisation pratique et tests expérimentaux

### Procédure :

1. Alimentation de l’AOP en ±12 V pour éviter toute saturation.
    
2. Branchement de l’entrée du montage sur la sortie **Vout filtrée**.
    
3. Observation des signaux à l’oscilloscope :
    
    - Jaune : signal d’entrée (Vout filtrée)
        
    - Bleu : signal amplifié (Vout filtrée amplifiée)
        
### Problème rencontré :

- **Saturation négative** du signal en cas de petites variations négatives du signal d’entrée.
    
- Solution : insertion d’une **diode de redressement** en sortie de l’amplificateur pour éliminer la partie négative.
    

### Résultats :

- **Surface blanche** :
    
    - Entrée ≈ 1,5 V crête
        
    - Sortie ≈ 9 V crête (conforme au cahier des charges)
	![[fond blanc amplifier et non amplifier - Seance 4.jpg]]
- **Surface noire** :
    
    - Entrée ≈ 0 V
        
    - Sortie ≈ 0 V
    ![[fond noir vout filitré, ampli et non ampli - seance 4.jpg]]
### Conclusion :

Le montage est fonctionnel et conforme aux exigences. Le signal est propre, amplifié et prêt pour l’étape de **démodulation**.

# 5. Démoduler Vout filtrée et amplifié

### Objectif :

Réaliser un montage de **démodulation d’enveloppe** afin d’extraire la valeur moyenne (ou crête) du signal amplifié. Ce signal appelé **Vsuivi** est utilisé pour la commande du robot suiveur.

### Analyse du signal :

- Signal entrant (Vout filtrée amplifiée) : sinusoïdal à 2 kHz, amplitude ≈ 9 V crête (surface blanche), ≈ 0 V (surface noire).
    
- But : obtenir une tension continue (ou lentement variable) qui suit les crêtes positives du signal.

### Choix de la solution :

Un **détecteur de crête** est utilisé, composé de :

- Une **diode** pour bloquer les alternances négatives.
    
- Un **condensateur** pour stocker la tension maximale.
    
- Une **résistance** pour assurer la décharge progressive du condensateur (temps de réponse).
![[Detecteur crête.png]]

### Calculs :

- La fréquence maximale du signal est f=2 kHz.
    
- On fixe la constante de temps $τ=1fmod=5 ms$ pour un bon compromis entre réactivité et lissage.
    
- Choix de :
    
    - C6=100 nF
        
    - $R7=τC=5×10−3100×10−9=50 kΩ$
        

### Simulation :

- Réalisée sous MicroCap.
    
- Signal en entrée : onde sinusoïdale à 2 kHz.
    
- Résultat attendu : signal de sortie continue ≈ 9 V pour le signal modulé à 9 V crête.
	
- Ve en jaune et Vout démodulé en bleu.
	![[ve et vs seance5.jpg]]
## Réalisation du montage de démodulation et validation:

### Étapes :

1. Connexion de l’entrée à la sortie de l’amplificateur de la séance précédente.
    
2. Mesures à l’oscilloscope :
    
    - Entrée : Vout filtrée amplifiée
        
    - Sortie : Vsuivi (tension démodulée)

### Observations :

- **Surface blanche** :
    
    - Entrée : ≈ 9 V crête
        
    - Vsuivi : ≈ 9 V (tension stable)
    ![[surface blanche- seance 6.jpg]]
- **Surface noire** :
    
    - Entrée : ≈ 0 V
        
    - Vsuivi : ≈ 0 V (tension quasi nulle)
    ![[surface noir - séance 6.jpg]]
- Comportement du montage conforme aux attentes.

### Conclusion :

Le démodulateur fonctionne parfaitement. Il convertit efficacement le signal sinusoïdal amplifié en une tension continue proportionnelle à l’intensité lumineuse perçue. Cette tension (Vsuivi) pourra ensuite être utilisée pour allumer des LED ou piloter des moteurs.


# 6. Visualiser :

### Objectif :

Mettre en œuvre un système d’indication visuelle permettant de traduire l’état logique de la sortie **Vsuivi** (obtenue après démodulation du signal optique) en allumage ou extinction d’une **LED**. Ce retour visuel est essentiel pour valider la détection d’une piste claire (blanche) ou sombre (noire) par le robot suiveur.

### Données initiales (extrait du cahier des charges) :

|Surface|Vsuivi (V)|LED allumée|
|---|---|---|
|Blanche|≈ 6 V|Oui|
|Noire|≈ 0 V|Non|

### Solution proposée :

L’objectif est de commander une **diode électroluminescente (LED)** à partir de la tension **Vsuivi**. Pour cela, on utilise un montage de **comparateur à seuil** à base d’amplificateur opérationnel, qui :

- compare Vsuivi à une tension de référence (**Vref**, par exemple 3 V),
    
- commande la LED via un transistor de puissance (ex : **NPN** ou **MOSFET**),
    
- protège la LED par une résistance série adaptée.
    

### Calculs :

- Tension seuil choisie : **Vref = 3 V**
    
- Si Vsuivi>Vref, alors la LED s’allume (surface blanche détectée).
    
- Si Vsuivi<Vref, la LED reste éteinte (surface noire détectée).
    
- Résistance série pour la LED 
	$R_{LED}=V_{suivi}−V_{D}*I_{LED}=6V−2V*20mA=200 Ω$(valeur normalise E12 : 220 Ω) où $V_D$​ est la chute de tension dans la LED rouge ≈ 2V).

### Simulation :

- Simulation effectuée dans **MicroCap** ou environnement similaire.
    
- Résultat attendu : la sortie bascule rapidement en fonction du dépassement du seuil Vref, et commande proprement l’allumage de la LED.
	
- ![[Led.png]]

## Implémentation du montage et validation expérimentale

### Montage réalisé :

- Comparateur avec AOP ou comparateur dédié (type LM393).
    
- Entrée non-inverseuse connectée à Vsuivi.
    
- Entrée inverseuse connectée à Vref fixée par pont diviseur de tension.
    
- Sortie du comparateur connectée à une LED + résistance via un **transistor de commutation NPN**.
    

### Expériences menées :

- Cas 1 – **Surface blanche** :
    
    - Vsuivi mesuré ≈ 6 V
        
    - Vsuivi > Vref → LED **allumée** 
		
	- ![[surface blanche- seance 6.jpg]]
- Cas 2 – **Surface noire** :
    
    - Vsuivi mesuré ≈ 0 V
        
    - Vsuivi < Vref → LED **éteinte** 
        
	- ![[surface noir - séance 6.jpg]]
### Ajustements :

- Si besoin, Vref peut être modifiée pour affiner la sensibilité du déclenchement.
    
- La résistance série peut être recalculée selon la couleur de la LED utilisée (chute de tension différente pour LED bleue, verte, etc.).
    

### Conclusion :

Le circuit de visualisation est opérationnel et conforme aux exigences. Il permet de **traduire visuellement l’état du capteur IR** après amplification et démodulation, ce qui est essentiel pour la vérification manuelle ou le débogage du système. Ce montage constitue la dernière étape de la chaîne de traitement du signal sur la carte SUIVI.****