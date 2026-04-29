# TP ALU

L'unité arithmétique et logique (ALU) permet de choisir parmi un certain nombre d'opérations. Nous allons voir comment une ALU peut choisir entre différentes opérations (ET, OU, addition, soustraction) à l'aide d'un **multiplexeur**.

Nous allons découvrir comment des décalages et additions successives peuvent constituer une **multiplication** ou une **division**.

Finalement, un **registre** permet de mémoriser les opérandes du calcul. Un registre particulier appelé **accumulateur** permet de faire des additions successives et *accumuler* une somme courante.

## 1. Sélectionneur

L'entrée **sel** du sélectionneur permet de choisir entre deux signaux d'entrée :

* entrée 0 : signal lent (période de 2 s)
* entrée 1 : signal rapide (période de 250 ms)

<!-- diagramme interactif -->

Recréez un tel sélecteur avec des portes NON, ET, OU.

## 2. Multiplexeur

Le multiplexeur (MUX) permet de choisir entre deux signaux 4-bits nommés a et b.
Ajoutez les éléments qui manquent.

<!-- diagramme interactif -->

* Ajoutez une deuxième entrée 4-bits avec un affichage.
* Ajoutez un décodeur et affichage à 7 segments.

## 3. Sélection d'opérations

Complétez le circuit qui permet de sélectionner entre les deux opérations `a ET b` et `a OU b`.

<!-- diagramme interactif -->

* Connectez a et b aux entrées des 4 portes OU,
* Ajoutez une sorie 4-bits pour afficher le résultat des opérations logiques
* Ajoutez une entrée de sélection pour le multiplexeur.

Un clic droit sur la porte quadruple permet de choisir son type (AND, OR, XOR, NAND, NOR, XNOR).

## 4. ALU

L'unité arithmétique et logique, ALU (arithmetic and logic unit), est la partie de l'ordinateur qui effectue les différents calculs arithmétiques et logiques.

Ci-dessous vous pouvez voir les circuits logiques d'une ALU 4-bits très utilisée dans les années 60 et 70, le modèle 74181.

![ALU](https://upload.wikimedia.org/wikipedia/commons/c/c0/74181aluschematic.png)

L'ALU dont nous disposons peut effectuer 4 opérations :

* addition (00)
* soustraction (01)
* OU logique (10)
* ET logique (11)

Avec l'ALU ci-dessous, ajoutez

<!-- diagramme interactif -->

* la deuxième entrée (B) avec un bloc d'affichage 4 bits
* un bloc d'affichage 4 bits pour la sortie (S)
* les 3 entrées (Cin, Op0, Op1)
* les 3 sorties (Cout, V, Z)

Ensuite, testez les 4 opérations. Montrez une soustraction.

## 5. Addition signée

Interprétez les nombres binaires comme des nombres signés. Vous pouvez configurer l'afficheur 4 bits avec son menu contextuel. Complétez l'additionneur 4-bit et montrez que l'addition de -2 et -3 donne bien -5.

<!-- diagramme interactif -->

## 6. Addition 8 bits

Pour additionner un nombre à 8-bits, il faut combiner deux ALU 4-bits. Dans ce cas il faut connecter Cout de la première ALU avec Cin de la deuxième.

<!-- diagramme interactif -->

* Complétez le circuit pour afficher l'addition de deux nombres binaires 8-bits.
* Ajoutez une entrée pour soustraire deux nombres.
* Montrez une soustraction correcte, dont le résultat est plus grand que 30

## 7. Carry et Overflow (V)

L'ALU possède deux sorties pour indiquer un dépassement de plage de résultat. Le résultat affiché est alors décalé de 16. Ce cas est signalé par l'ALU à l'aide de deux signaux de sortie spéciaux.

* C (carry) signale un dépassement pour des nombres non signés,
* V (overflow) signale un dépassement pour des nombres signés.

L'addition de deux nombres naturels (0 à 15) peut produire un résultat de 0 à 30.
L'addition de deux nombres relatifs (-8 à 7) peut produire un résultat de -16 à 14.
Dans certains cas on aura donc besoin de 5 bits pour représenter correctement le résultat.

![4bits Integers](https://apprendre.modulo-info.ch/_images/4bits_Integers.svg)

Pour les nombres non signés (première ALU)

<!-- diagramme interactif -->

* Choisissez des valeurs a et b qui produisent un dépassement (C = 1), et donc un affichage incorrect sur une sortie de 4 bits.
* Ajoutez en plus un affichage 8 bits et connectez-y les 4 bits de S et C comme 5e bit, pour afficher le résultat correct.

Pour les nombres signés (deuxième ALU)

<!-- diagramme interactif -->

* Ajoutez 2 entrées 4 bits et 1 sortie 4 bits.
* Ajoutez 3 affichages 4 bits configurés (via menu contextuel) en nombres signés.
* Choisissez des valeurs a et b négatives qui produisent un dépassement (V = 1).
* Ajoutez un affichage 8 bits configuré (via le menu contextuel) en nombres signés, et connectez-y les 4 bits de S et C comme 5e bit.

**Attention** : Dans ce cas vous devez connecter C également avec les 3 autres bits (b5-b7) pour faire une propagation du bit de signe et traiter correctement le cas des nombres négatifs.

## 8. Multiplier 1x1 bit

Les règles de la multiplication 1-bit sont très simples. Voici la table de vérité.

| a | b | a x b |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

On voit tout de suite que ceci correspond à la porte ET.
Dans l'exemple si dessous vous voyez une porte ET pour multiplier a et b, les deux ayant juste 1 bit.

<!-- diagramme interactif -->

* Vérifiez le bon fonctionnement du multiplicateur 1-bit
* Ensuite, utilisez 4 portes ET pour créer un multiplicateur **a** (4-bits) fois **b** (1-bit).
* Basculez b entre 0 et 1 pour vérifier si votre circuit fonctionne correctement.

## 9. Multiplier par 2, 4, 8

La multiplication par une puissance de 2 est facile. Il suffit de décaler les bits.
Le circuit ci-dessous calcule 2a en décalant d'un bit en direction du poids fort.

<!-- diagramme interactif -->

* Complétez le circuit pour calculer et afficher 4a et 8a.
* Vérifiez avec a=5. Votre affichage devrait montrer 10, 20 et 40.

## 10. Multiplier 1x4 bit

Le circuit ci-dessous utilise un multiplexeur 8x4 pour faire la multiplication d'un nombre **a** (4 bits) avec un nombre **b** (1 bit), au lieu des 4 portes ET utilisées précédemment.

Nous pouvons représenter un nombre binaire **b** par une séquence de 4 chiffres binaires : $b_3 b_2 b_1 b_0$.
Chaque bit $b_i$ contrôle la multiplication de son poids ($2^i$) avec $a$.

* $b_0 \cdot 2^0 a$
* $b_1 \cdot 2^1 a$
* $b_2 \cdot 2^2 a$
* $b_3 \cdot 2^3 a$

Pour compléter l'opération de multiplication 4x4 bits, la dernière étape sera d'additionner les 4 nombres.

<!-- diagramme interactif -->

Complétez le circuit avec :

* deux entrées que vous appelez **b2** et **b3**
* un affichage 8 bits qui affiche 4a sous contrôle de b2
* un affichage 8 bits qui affiche 8a sous contrôle de b3

Essayer de multiplier deux nombres, par exemple a=5 et b=5 (0101). Vous trouvez le résultat de la multiplication en additionnant les 4 nombres affichés.

## 11. Multiplier 4x4 bits

La multiplication 4 x 4 bits nécessite:

* 4 multiplexeurs pour la multiplication 4 x 1 bit
* 3 additionneurs pour additionner les 4 opérandes décalés

<!-- diagramme interactif -->

Pour multiplier `0101` x `1001` = `00101101` (5 x 9 = 45) nous écrivons en colonnes ceci :

```
1     1001
0    0000
1   1001
0 +0000
----------
  00101101
```

Cet algorithme peut être exprimé mathématiquement comme

$$ produit = \sum^4_{i=0} (b_i \cdot a) \cdot 2^i $$

Modifiez a et b dans le circuit multiplicateur 4 x 4 bits ci-dessus vérifiez que vous obtenez bien le produit de a et b. Faites une capture d'écran avec la plus grande valeur possible.

## 12. Diviser par 2, 4 et 8

La division par une puissance de 2 est très simple. Il suffit de décaler le nombre binaire. Pour diviser par 2 nous décalons d'une unité, et nous obtenons :

* La division entière (`a // 2`)
* Le reste de la division, l'opération modulo (`a % 2`)

<!-- diagramme interactif -->

Ajoutez deux affichages 8 bits pour la division par 4 et 8
Ajoutez deux affichages 4 bits pour le modulo 4 et 8
Ajoutez les étiquettes (`a % 4`, `a // 4`, etc.)

Par exemple pour `43 // 8` vous devriez obtenir 5,
et pour `43 % 8` vous devriez obtenir 3.

## 13. Registre

Le registre que nous allons voir plus en détail dans le prochain chapitre permet de mémoriser une donnée.
Avec un coup d'horloge (clock), les 4-bits de données sont mémorisés.

<!-- diagramme interactif -->

Ajoutez un deuxième registre, décodeur et affichage à 7 segments, pour permettre d'afficher un nombre décimal de 00 à 99 ou un nombre hexadécimal de 00 à FF.

## 14. Accumulateur

Un accumulateur est un registre spécial qui *accumule* une somme. La sortie de l'accumulateur est reliée avec l'entrée A de l'ALU. À chaque coup d'horloge du registre, le calcul `acc + b` est effectué et affiché.

Par exemple dans le circuit ci-dessous, l'accumulateur contient 3. Au prochain coup d'horloge, l'entrée b qui est 2 y sera additionnée. Ceci permet de calculer une somme courante.

<!-- diagramme interactif -->

Voici un exemple typique, calculer la somme 1+3+7.
En Python ceci correspondrait à :

```python
acc = 0     # clear
acc += 1    # add
acc += 3    # add
acc += 7    # add
print(acc)
```

Avec le circuit ci-dessous ceci correspond à 4 étapes:

1. **clear**
2. b=1 et **add**
3. b=3 et **add**
4. b=7 et **add**

Connectez les entrées **clear** et **add** au bon endroit et calculez 1+3+7.

**Attention:** tenez le bouton suffisamment longtemps pour laisser propager les signaux jusqu'au bout.

## 15. Incrémenter/décrémenter

Certains appareils électroniques ont très peu de touches et on doit utiliser juste deux boutons.
C'est le cas pour régler la température ou le volume.

<!-- diagramme interactif -->

Compléter le circuit pour les boutons

* **up** pour incrémenter la valeur (clock)
* **down** pour décrémenter la valeur (clock + soustraction)
* **clear** pour mettre la valeur à zéro

Attention au délai de transmission par défaut de 100 ms. Il faut soit appuyer plus longtemps sur les boutons, ou diminuer ce délai.

## 16. Comparer

En Python nous disposons de 6 comparateurs pour comparer deux nombres a et b :

* `>` plus grand
* `>=` plus grand ou égal
* `==` égal
* `!=` non égal
* `<=` plus petit ou égal
* `<` plus petit

Nous pouvons créer ces 6 comparaisons en utilisant une ALU qui soustrait deux nombres a et b et quelques portes logiques.
Voici quelques astuces :

* quand a-b est zéro alors `Z=1`, donc **a égal b**
* quand a-b est négatif, alors `C=1`, donc **a plus petit que b**
* quand vous combinez les deux `Z=1` ou `C=1`, vous trouvez **a plus petit ou égal à b**

<!-- diagramme interactif -->

Utilisez les portes ET, OU et NON pour décoder les 6 types de comparaisons.
