## **2.3 Projet n°2 : Génération d’un signal de lumière codée**

### **Objectif**

Le but de ce projet est de concevoir un système analogique permettant d’émettre un signal lumineux codé, qui pourra être reçu et traité par un récepteur optique. L’objectif est d’assurer une transmission fiable de l’information en utilisant la modulation lumineuse, ce qui permet également de réduire l’influence des lumières parasites présentes dans l’environnement.

### **Principe du codage lumineux**

L’information est transmise sous forme de signal **binaire** en utilisant une LED infrarouge :

- **Bit à 1** → La LED est allumée.
    
- **Bit à 0** → La LED est éteinte.
    

Ce codage temporel permet au récepteur de distinguer clairement les transitions entre les états ON et OFF, garantissant ainsi une détection précise.

Le signal doit être **modulé en fréquence** afin d’être facilement différentiable des sources lumineuses ambiantes (soleil, lampes, etc.). Une fréquence de **2 kHz** a été choisie pour l’émission, ce qui signifie que la LED clignote à cette fréquence pour représenter un bit.

### **Mise en œuvre technique**

L’émission du signal lumineux est réalisée grâce à un circuit analogique composé de :

- Un **oscillateur** basé sur un circuit **NE555** (ou un oscillateur RC) permettant de générer un signal carré périodique.
    
- Une **LED infrarouge** qui émet la lumière selon le signal de l’oscillateur.
    
- Une **résistance de limitation de courant** pour protéger la LED et assurer un fonctionnement stable.
    

Le **circuit oscillateur** est conçu de manière à produire un signal carré ayant :

- Une **tension de sortie oscillante entre 0V et 9V** (valeurs définies par l’alimentation du circuit).
    
- Un **rapport cyclique de 50 %**, garantissant un temps d’allumage et d’extinction égaux.
    
- Une **fréquence de 2 kHz**, assurant une bonne séparation entre les impulsions.
    

### **Schéma fonctionnel**

Le montage peut être représenté par le schéma fonctionnel suivant :

`Oscillateur (NE555 ou circuit RC) → Résistance (150 Ω) → LED IR → Transmission lumineuse`

### **Calculs des composants**

La fréquence d’oscillation d’un NE555 en mode astable est donnée par la formule :

$f=1.44(R1+2R2)×Cf = \frac{1.44}{(R1 + 2R2) \times C}f=(R1+2R2)×C1.44​$

Avec :

- R1 et R2 des résistances en ohms.
    
- C un condensateur en farads.
    

En choisissant :

- R1=1kΩ 
    
- R2=680kΩ
    
- C=1nF
    

On obtient une fréquence de **2 kHz**, conforme aux spécifications du projet.

### **Conclusion du projet**

Ce projet a permis de concevoir un émetteur optique fonctionnant uniquement en **analogique**, sans microcontrôleur. L’utilisation d’un **oscillateur autonome** garantit un fonctionnement stable et répétitif. La modulation à **2 kHz** permet une détection facile par un récepteur, tout en limitant les interférences dues à la lumière ambiante.

---

## **2.4 Séance n°2 : Réalisation pratique de l’émetteur**

### **Câblage et mise en place du montage**

Le montage a été assemblé sur une **plaque d’expérimentation (breadboard)**. Les connexions suivantes ont été réalisées :

1. **Alimentation du circuit oscillateur** en 9V.
    
2. **Connexion du circuit NE555** en mode astable avec les composants passifs calculés précédemment.
    
3. **Branchement de la LED infrarouge** avec une **résistance série de 150 Ω** pour limiter le courant à environ **50 mA**.
    
4. Vérification du bon fonctionnement du circuit avec un **oscilloscope** en sortie de l’oscillateur.
    

### **Mesures et observations**

#### **1. Vérification du signal généré**

Le signal en sortie du circuit oscillateur a été mesuré à l’aide d’un oscilloscope :

- **Forme d’onde :** signal carré propre et stable.
    
- **Tension maximale :** 9V.
    
- **Tension minimale :** 0V.
    
- **Fréquence mesurée :** environ **2 kHz**, conforme aux calculs théoriques.
    

#### **2. Observation du fonctionnement de la LED**

- Avec un téléphone, la LED infrarouge semble allumée en continu, car la fréquence de 2 kHz est trop rapide pour être perçue.
    
- Avec l'oscilloscope, on observe que la LED clignote bien à la fréquence attendue.
    

### **Tests et validation du fonctionnement**

Des tests ont été effectués en utilisant un **récepteur optique** pour vérifier la bonne transmission du signal :

- Le **capteur infrarouge (phototransistor)** détecte bien les impulsions lumineuses émises.
    
- Avec l'**oscilloscope**, on retrouve un signal modulé correspondant à celui envoyé par l’oscillateur.
    

### **Chronogrammes observés**

1. **Signal de l’oscillateur** (sortie NE555) :
    
    - Signal carré propre.
        
    - Fréquence stable à 2 kHz.
        
2. **Signal lumineux détecté par la photodiode** :
    
    - Même fréquence de 2 kHz.
        
    - Amplitude variable en fonction de la distance et de l’alignement du capteur.
        

### **Difficultés rencontrées et solutions apportées**

- **Problème :** LED infrarouge trop faible dans certains cas.
    
    - **Solution :** Augmentation du courant en ajustant la résistance de limitation (passage de 150Ω à 100Ω).
        
- **Problème :** Interférences lumineuses.
    
    - **Solution :** Vérification dans un environnement sombre et orientation optimale du capteur.
        

### **Conclusion de la séance**

L’émission du signal lumineux codé a été validée par des mesures expérimentales.

- Le circuit oscillateur produit un **signal carré propre**.
    
- La LED infrarouge **suit précisément le signal généré**.
    
- Un récepteur optique permet de **détecter les impulsions lumineuses correctement**.