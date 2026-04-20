

## Mini-projet 2 – Optimisation
Mines Paris – PSL
https://moodle.psl.eu2025-2026
Ce mini-projet, à effectuer en binôme au sein du même groupe de PC (inscription sur Moodle), fera
l’objet d’une soutenance orale, incluant la présentation des résultats obtenus et une séance de questions. La
présentation comportera obligatoirement un Jupyter Notebook, avec les réponses aux questions demandées
dans le sujet, le code Python réalisé et les graphiques obtenus par des simulations sous Python.Ce Jupyter
Notebook sera à déposer au plus tard le mercredi 22 avril à 9hsur Moodle.
Le code rendu devra être fonctionnel, et le notebook exécutable en direct durant la soutenance, dans l’ordre
des cellules, avec un "Run All Cells". Tout code non-exécutable pourra donner lieu à une pénalisation sur
la note obtenue. Il est également demandé à ce que les paramètres d’entrée du cas d’étude soient modifiables
à la volée dans le code le jour de la soutenance. Il est nécessaire d’apporter un ordinateur le jour de la
soutenance.
Effacement de consommation.
On s’intéresse dans ce sujet au chauffage d’un bâtiment résiden-
tiel. On souhaite piloter ce chauffage de sorte à minimiser la facture
électrique du consommateur, tout en garantissant le confort des oc-
cupants.
Pour ce faire, on considère un horizon de temps[t
## 0
, t
f
], que l’on
partitionne enNintervalles de temps[t
i
, t
i+1
](i= 0, . . . , N−1) de
longueur uniforme∆t, avec∆t=  (t
f
## −t
## 0
)/N, de sorte quet
## N
## =
t
f
. On suppose que le bâtiment est équipé de convecteurs, dont on
contrôle la puissance totale de chauffage, supposée constante sur
chaque intervalle de temps[t
i
, t
i+1
]et notéeP
i
. Cette puissance de chauffage est limitée
## 0≤P
i
## ≤P
## M
,   i= 0, . . . , N(1)
La température moyenne du bâtiment évolue entre les tempst
i
ett
i+1
en fonction de la puissance de
chauffage et de la température extérieure (supposé également constante sur l’intervalle de temps[t
i
, t
i+1
## ])
suivant l’équation
## T
i+1
## =e
## −(k+h)∆t
## T
i
## +
## 1−e
## −(k+h)∆t
k+h
(bP
i
+hT
e
i
),   i= 0, . . . , N−1(2)
oùb,kethsont trois constantes positives. Les conditions initiale/terminale correspondantes sont
## T
## 0
## =T
in
etP
## N
## = 0(3)
Pour le confort des habitants, cette température doit rester bornée entre une température min et une tem-
pérature max données aux horaires de présence des occupants, soit
## T
m
## ≤T
i
## ≤T
## M
,   i∈I
occ
## ⊂{0, . . . , N}(4)
Enfin, on suppose l’existence d’un tarif heure pleine/heure creuse pour ce bâtiment, correspondant à un tarif
d’électricitéc
i
variant dans le temps et à la facture d’énergie
## ∆t
## N
## ∑
i=0
c
i
## P
i
## (5)
## 1

1  Etude du problème d’optimisation
- Justifier que la facture d’énergie s’écrit bien (5).
- Interpréter l’équation (2). Quels échanges thermiques incorpore-t-elle ? Cette modélisation vous semble-
t-elle raisonnable ?
- Formuler le problème d’optimisation à résoudre sous la forme
min
x
f(x)
tel quec
eq
## (x) = 0,
c
in
## (x)≤0
## (6)
On précisera les variables de décisionx, leur nombren, les contraintesc
eq
etc
in
ainsi que la fonction
objectiffà minimiser.
- Etudier la convexité de ce problème. Appartient-il à une famille particulière de problèmes d’optimisa-
tion ?
2  Etude et résolution numérique du problème individuel
- Quelles méthodes de résolution peuvent être envisagées pour ce problème ?
- Développer un algorithme de résolution dans le cas d’un horizon de temps de 24h (t
## 0
## = 23h,∆t= 0.5h),
avec :
•un tarif d’heure creuse (c
i
## =c
cr
constant) entre d’une part minuit et6h, et d’autre part12het14h
et un tarif d’heure pleine (c
i
## =c
pl
constant) le reste du temps ;
•les horaires de "présence" des occupants[7h,9h]et[18h,23h].
On prendra les valeurs numériques suivantes :
c
cr
= 1,   c
pl
## = 3/2,   T
m
## = 18
## ◦
## C ,   T
## M
## = 30
## ◦
## C,   T
in
## =T
m
## (7)
h=0.05h
## −1
,   k= 0.01h
## −1
,   b= 1/500C/W h ,   P
## M
## = 5000W(8)
et l’on supposera que la température extérieure varie suivant la fonctionT
e
i
## = 4 + 8e
## −(t
i
## −12)
## 2
## /40
## (avec
t
i
modulo 24). On veillera à afficher au minimum les graphiques suivants :
(a) l’évolution de la température du bâtiment au cours du temps ainsi que la puissance de chauffage
(normalisée) fournie. On prendra soin d’indiquer les plages d’occupation, ainsi que les bornes de
température correspondantes.
(b) l’évolution de la puissance de chauffage (normalisée) comparée à celle du tarif électrique.
Commenter les résultats obtenus.
- Observer les résultats obtenus pour différents prix d’heure pleine (c
pl
## = 7/4etc
pl
= 2). Commenter le
profil optimal obtenu et l’effet incitatif du tarif.
3  Régulation collective
On considère maintenant que un logement mitoyen avecn
l
−1autres (copropriété, immeuble...) et que l’on
est en mesure de piloter l’ensemble de ces logements dont on noteT
j
i
etP
j
i
(j= 1, . . . , n
l
) les températures
et puissances respectives au tempst
i
. Des échanges thermiques ayant lieu entre les logements, ceci modifie
la dynamique de la température de la maisonj= 1, . . . , n
l
suivant l’équation
## T
j
i+1
## =e
## −(k+h+
## ∑
k6=j
h
jk
## )∆t
## T
i
## +
## 1−e
## −(k+h+
## ∑
k6=j
h
jk
## )∆t
k+h+
## ∑
k6=j
h
jk
(bP
i
+hT
e
i
## +
## ∑
k6=j
h
jk
## T
k
i
),   i= 0, . . . , N−1(9)
oùh
jk
## =h
kj
## ≥0.
## 2

- On souhaite concevoir un pilotage centralisé du chauffage de ces logements. Ecrire le nouveau problème
d’optimisation à résoudre.
- Quels inconvénients/avantages cette solution de pilotage vous semble-t-elle présenter (on pourra penser
aux informations qu’il est nécessaire de connaître à l’optimiseur centralisé) ?
- Développer un algorithme de résolution dans le casn
l
= 2. On prendrah
## 12
## =h
## 21
=het les mêmes
paramètres pour les deux maisons (avec les valeurs données en (7)–(8)), à l’exception de la température
minimale pour le second logement qui estT
## 2
m
## = 20
## ◦
C, contreT
## 1
m
## = 18
## ◦
Cpour le premier. On prendra
soin de tracer les mêmes graphiques que précédemment, mais pour chaque logement. Commenter les
résultats obtenus.
## 3