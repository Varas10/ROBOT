## **Séance 5 – Étude théorique et conception d’un détecteur de crête**

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
    

### Calculs :

- La fréquence maximale du signal est f=2 kHz.
    
- On fixe la constante de temps $τ=1fmod=5 ms$ pour un bon compromis entre réactivité et lissage.
    
- Choix de :
    
    - C=100 nF
        
    - $R=τC=5×10−3100×10−9=50 kΩ$
        

### Simulation :

- Réalisée sous MicroCap.
    
- Signal en entrée : onde sinusoïdale à 2 kHz.
    
- Résultat attendu : signal de sortie continue ≈ 9 V pour le signal modulé à 9 V crête.
    

---

## **Séance 6 – Réalisation du montage de démodulation et validation**

### Objectif :

Implémenter le montage détecteur de crête sur plaque d’expérimentation et valider sa capacité à générer Vsuivi à partir de Vout filtrée amplifiée.

### Étapes :

1. Câblage du montage détecteur de crête.
    
2. Connexion de l’entrée à la sortie de l’amplificateur de la séance précédente.
    
3. Mesures à l’oscilloscope :
    
    - Entrée : Vout filtrée amplifiée
        
    - Sortie : Vsuivi (tension démodulée)
        

### Observations :

- **Surface blanche** :
    
    - Entrée : ≈ 9 V crête
        
    - Vsuivi : ≈ 9 V (tension stable)
        
- **Surface noire** :
    
    - Entrée : ≈ 0 V
        
    - Vsuivi : ≈ 0 V (tension quasi nulle)
        
- Comportement du montage conforme aux attentes.
    
- Aucun effet de ripple significatif, la constante de temps choisie est bien adaptée.
    

### Conclusion :

Le démodulateur fonctionne parfaitement. Il convertit efficacement le signal sinusoïdal amplifié en une tension continue proportionnelle à l’intensité lumineuse perçue. Cette tension (Vsuivi) pourra ensuite être utilisée pour allumer des LED ou piloter des moteurs.