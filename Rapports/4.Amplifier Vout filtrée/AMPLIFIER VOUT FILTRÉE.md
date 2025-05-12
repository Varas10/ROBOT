## **Séance 5 – Étude théorique, simulation et conception du circuit d’amplification**

### Objectif :

L’objectif de cette séance est de concevoir un amplificateur pour le signal **Vout filtrée**, issu de la détection optique, afin d’en augmenter l’amplitude sans en altérer la forme, de manière à rendre ce signal exploitable pour l’étape suivante de démodulation.

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
    
    Av=1+R2R1A_v = 1 + \frac{R_2}{R_1}Av​=1+R1​R2​​

### Calculs :

Pour obtenir un gain de 6 (objectif : 1,5 V → 9 V) :

- Choix de R1=680 ΩR_1 = 680\ \OmegaR1​=680 Ω (valeur normalisée)
    
- Calcul de R2=(Av−1)×R1=5×680=3400 ΩR_2 = (A_v - 1) \times R_1 = 5 \times 680 = 3400\ \OmegaR2​=(Av​−1)×R1​=5×680=3400 Ω
    
- Choix de R2=3.3 kΩR_2 = 3.3\ k\OmegaR2​=3.3 kΩ (valeur normalisée proche)
    

### Simulation :

- Simulation réalisée sous **MicroCap**.
    
- Entrée : signal sinusoïdal de 1,5 V crête à 2 kHz.
    
- Résultat : signal amplifié à 9 V crête, sans distorsion notable.
    

---

## **Séance 6 – Réalisation pratique et tests expérimentaux**

### Objectif :

Mettre en œuvre le montage d’amplification conçu précédemment sur une platine d’essai, le tester avec des signaux réels, et valider son comportement.

### Procédure :

1. Réalisation du circuit sur plaque d’essai.
    
2. Alimentation de l’AOP en ±12 V pour éviter toute saturation.
    
3. Branchement de l’entrée du montage sur la sortie **Vout filtrée**.
    
4. Observation des signaux à l’oscilloscope :
    
    - Jaune : signal d’entrée (Vout filtrée)
        
    - Bleu : signal amplifié (Vout filtrée amplifiée)
        

### Résultats :

- **Surface blanche** :
    
    - Entrée ≈ 1,5 V crête
        
    - Sortie ≈ 9 V crête (conforme au cahier des charges)
        
- **Surface noire** :
    
    - Entrée ≈ 0 V
        
    - Sortie ≈ 0 V
        

### Problème rencontré :

- **Saturation négative** du signal en cas de petites variations négatives du signal d’entrée.
    
- Solution : insertion d’une **diode de redressement** en sortie de l’amplificateur pour éliminer la partie négative.
    

### Conclusion :

Le montage est fonctionnel et conforme aux exigences. Le signal est propre, amplifié et prêt pour l’étape de **démodulation**.