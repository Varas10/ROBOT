## Théorie

Une diode émettrice CNY70 doit émettre une lumière d'une longueur d'onde de 950nm dans le domaine de l'infrarouge.

Le courant responsable de l'émission de la lumière vas de la borne 1 à la borne 5 du connecteur en passant par les deux capteurs.

La sortie du Capteur 1 se trouve sur la broche 4 et la sortie du Capteur 2 se trouve sur la broche 3.

On choisi un montage Common-Collector Amplifier pour faire augmenter Vout lorsque la lumière augmente.

Le courant va du Collecteur à l’émetteur et Vce sort par Vout.

La relation entre Vce, ic, Vcc et RE est : 
$Vcc=Vce + Ic * RE$

![[Courbe charge f(Ic et Vce).png]]
La courbe rouge représente la charge.

#### Dans le cas de la charge représenté par la courbe rouge :

$RE = \frac{Vcc-Vce}{Ic} =\frac{9-0}{0,001}=9k\ohm$

Si on envoie 50mA dans la diode émettrice on recoit une tension Vce de 0,3V

Vout vaut donc $Vout = 9-0,3=8,7V$


