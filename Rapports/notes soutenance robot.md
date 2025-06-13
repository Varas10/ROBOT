# chaier des charger
## 🔧 **Cahier des charges – SAE Robot suiveur de ligne**

### 🎯 **Objectif général**

Concevoir un **robot suiveur de ligne** capable de :

- **Suivre une ligne blanche sur fond noir** de manière **autonome**
- **Démarrer et s’arrêter par claquement de mains**
- **Indiquer son état** (veille ou en marche)
- Fonctionner **sur piles**
---
## 🧩 **Spécifications fonctionnelles**

- Le robot doit :
    - Suivre une ligne blanche sur fond noir
    - Démarrer au **1er claquement de mains**
    - S’arrêter au **2e claquement de mains**
    - Indiquer son état par LED (veille/marche)
    - Fonctionner **sans fil** (alimentation sur piles)

---

## ⚙️ **Spécifications opératoires**

- **Suivi de ligne** :
    
    - Gérer les **virages**
    - En cas d'**absence de piste**, continuer tout droit
    - En cas de **croisement**, s’arrêter
    - En **ligne droite**, atteindre la **vitesse maximale**

- **Détection sonore** :
    
    - Détecter les claquements à **5 m environ**
    - Générer un signal TOR :
        - 9V = arrêt
        - 0V = marche

    - LED de veille :
        - Allumée = robot en veille
        - Éteinte = robot en mouvement

---

## 🔌 **Spécifications technologiques**

- **Technologie** : électronique **analogique**
    
- **Alimentations** :
    
    - 9V (commande)
        
    - 6V (puissance – 4 piles 1,5V)
        
- **Composants à utiliser** :
    
    - CNY70 (capteurs)
        
    - SG3524 (PWM)
        
    - NE555, CD4017, BD438 (logique / commande)
        
    - Capteur à électret (micro)
        
    - Moteurs CC 6V / 600 mA
        
- **Cartes** :
    
    - Carte « yeux » et fond de panier **fournies**
        
    - Réalisation de **circuits imprimés**
        
- **Outils autorisés** :
    
    - Micro-Cap, Eagle

# analyse fonctionnel
