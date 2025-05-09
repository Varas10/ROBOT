## Étude théorique

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
    

### Fonctionnement du montage transistor

- Choix du montage : **Montage collecteur commun** pour obtenir une **tension Vout** qui augmente avec l’intensité lumineuse reçue.
    
- Relations utilisées :
    
    Vcc=Vce+Ic×ReVcc = Vce + Ic \times ReVcc=Vce+Ic×Re
- Calculs :
    
    - **Re** :
        
        Re=9V−0V0,001A=9000 ΩRe = \frac{9V - 0V}{0,001A} = 9000\, \OmegaRe=0,001A9V−0V​=9000Ω
    - **Vce** pour 50mA d’émission : ≈ 0,3V.
        
    - **Vout** correspondant :
        
        Vout=9V−0,3V=8,7VVout = 9V - 0,3V = 8,7VVout=9V−0,3V=8,7V

### Limitation du courant LED

- Calcul de la résistance RD pour limiter le courant LED à 50 mA sous 9V :
    
    RD=9V−1,25V0,05A=155 ΩRD = \frac{9V - 1,25V}{0,05A} = 155\, \OmegaRD=0,05A9V−1,25V​=155Ω
- **Valeur normalisée** utilisée : **150 Ω**.
    

### Conclusion de l'étude théorique

Grâce à cette étude, la conception de la carte "yeux" permet d’assurer :

- La bonne émission de lumière infrarouge.
    
- La détection fiable des surfaces via un phototransistor.
    
- La protection des composants par le choix adapté des résistances.
    

---

## Étude pratique

### Câblage de la carte

- **Entrée du signal générant la lumière codée** : 9V.
    
- **RLeds** : 150 Ω installée (protection des LEDs).
    
- **Re** : montage ajustable pour limiter le courant dans les phototransistors.
    

### Mesures réalisées

- **Mesure du courant LED** :
    
    ILED=5,37V150 Ω=35 mAI_{LED} = \frac{5,37V}{150\,\Omega} = 35\, mAILED​=150Ω5,37V​=35mA
- **Mesures de Vout** :
    
    - **Surface blanche** : 0,1 V.
        
    - **Surface noire** : 0 V.
        

### Rejet des lumières parasites

- Pour éviter l'influence de l'éclairage ambiant, la lumière émise est modulée :
    
    - **Signal carré** appliqué : 0-9V, **fréquence = 2kHz**.
        
- Relevés :
    
    - Chronogrammes du signal d'entrée (générant la lumière codée).
        
    - Chronogrammes de la sortie Vout sur surface blanche et noire.
        

### Résultats observés

- Lorsque la surface est blanche, Vout présente une réponse claire et modulée.
    
- Lorsque la surface est noire, Vout est quasiment nul, ce qui permet une détection fiable du changement de surface.
    

### Conclusion de l'étude pratique

L'étude pratique a permis de :

- Vérifier le fonctionnement du montage théorique.
    
- Valider la modulation comme méthode efficace pour rejeter les interférences lumineuses.
    
- S'assurer que le robot pourra différencier correctement les pistes claires et sombres lors de son suivi de ligne.