## **Mise en forme du signal Vout** - Théorie

### **Objectif**

Le signal Vout, issu du capteur optique (phototransistor), est un signal analogique modulé à la fréquence de la lumière codée (2 kHz). Ce signal comporte deux composantes :

- Une **composante alternative (AC)**, qui est l’image de la lumière codée (modulation de 2 kHz).
    
- Une **composante continue (DC)**, due à la lumière ambiante et aux caractéristiques propres du capteur.
    

L’objectif de ce projet est de **supprimer la composante continue** pour ne conserver que la **composante alternative**, représentative du signal lumineux codé reçu.

---

### **Analyse du problème**

Le signal Vout capté contient une **valeur moyenne non nulle** (décalage DC), qui varie selon la luminosité ambiante ou la surface réfléchissante.  
Ce décalage peut masquer ou fausser la détection de la modulation 2 kHz.

---

### **Solution technique : le filtre passe-haut**

On utilise un **filtre passe-haut analogique** (filtre RC) pour supprimer la composante continue et ne laisser passer que les signaux alternatifs de fréquence suffisante.

#### **Schéma de principe :**

![[Pasted image 20250508102008.png]]

#### **Calcul de la fréquence de coupure**

La **fréquence de coupure Fc** du filtre est choisie telle que :

$Fc=12πRC$ 
$Fc = \frac{1}{2 \pi R C}$
$Fc=2πRC1​$

Objectif : que **$Flum = 2 kHz$** soit **dans la bande passante**, donc $Fc < Flum$. On choisit :

- **Fc = 200 Hz**, soit$ $Flum / 10.$
    

#### **Choix des composants :**

- **C = 100 nF**
    
- **R = 1 / (2π × 100 nF × 200 Hz) ≈ 7957 Ω**
    
- **Valeur normalisée de R choisie : 6,8 kΩ**
    

Ce filtre permet d’atténuer fortement les composantes inférieures à 200 Hz (dont le continu), tout en laissant passer efficacement la modulation de 2 kHz.

---

### **Conclusion du projet**

Le montage permet de :

- Supprimer la composante continue de Vout (liée aux conditions d’éclairage ambiant).
    
- Conserver uniquement le signal modulé à 2 kHz, qui représente l’information utile.
    
- Faciliter le traitement ultérieur du signal (amplification, démodulation).
    

---

## **Réalisation pratique du filtre de Vout**

### **Montage et câblage**

- Le filtre RC a été câblé selon les valeurs théoriques :
    
    - **Condensateur de 100 nF**
        
    - **Résistance de 6,8 kΩ** à la masse
        
- Signal d’entrée : Vout du capteur.
    
- Mesures effectuées à l’aide d’un **GBF (générateur basse fréquence)** et d’un **oscilloscope**.
    

---

### **Tests et chronogrammes**

#### **1. Signal sinusoïdal appliqué (test de fréquence)**

- Signal d’entrée Ve : sinusoïdal, amplitude 8 V, fréquence variable (Ve en bleu).
    
- Signal de sortie Vs : réponse du filtre (Vs en jaune).
	
- ![[Pasted image 20250508102211.png]]

On a testé trois cas :

|**Fréquence (f)**|**Vs (amplitude crête-à-crête)**|**Atténuation**|**Bande passante**|
|---|---|---|---|
|**Fc / 10 = 20 Hz**|0,7 V|Forte|Non|
|**Fc = 200 Hz**|5,4 V|Moyenne|Non (limite)|
|**10 Fc = 2 kHz**|8 V|Aucune|Oui|

#### **Calcul de l’atténuation (A = Vs / Ve)**

|Fréquence|A|
|---|---|
|20 Hz|0,088|
|200 Hz|0,675|
|2 kHz|1|

**Conclusion :** Le filtre laisse bien passer la composante 2 kHz tout en atténuant fortement les basses fréquences et le continu.

---

### **2. Application avec Vout réel**

- **Signal Vout** (brut) connecté à l’entrée du filtre.
    
- **Sortie filtrée** observée à l’oscilloscope.
    

#### **Résultats observés :**

- **Surface noire** : pas de signal modulé, donc Vs ≈ 0.
	
- ![[Pasted image 20250508102237.png]]
- **Surface blanche** : modulation claire à 2 kHz visible sur Vs.
	
-  ![[Pasted image 20250508102252.png]]

Le filtre a bien supprimé le décalage continu et a laissé passer uniquement la modulation utile.

---

### **Conclusion de la séance**

Le filtre RC mis en œuvre permet efficacement de :

- Éliminer la composante continue indésirable.
    
- Préparer le signal pour les étapes suivantes (amplification et démodulation).
    
- Améliorer la lisibilité et la fiabilité du signal de suivi lumineux.
    

Cette étape est indispensable pour garantir un **traitement précis et robuste** du signal optique.