# Version test — carte arrosage 35 × 55 mm

Mise à jour du 25 novembre 2026, KiCad 10. La carte conserve deux couches,
une épaisseur de 1,6 mm et le quart supérieur de 35 × 13,75 mm réservé à
l'antenne A2. Les composants occupent les trois quarts restants.

## Modifications appliquées

- **U.FL sur le trajet RF** : U1.12 → R4 → pastille signal de J3 → R6 → A2.
  R4, J3 et R6 sont alignés sur la piste à Y = 68,725 mm. C6 reste une
  branche d'adaptation à la masse ; L1 est raccordée côté antenne. La ligne
  RF est entièrement sur F.Cu, sans via. La zone interdite sous le corps
  du connecteur U.FL est respectée. Le module radio est légèrement décalé
  vers le bas pour dégager cette ligne.
- **R4 doit être montée** : sa résistance de 0 Ω fait maintenant partie du
  chemin principal, son option DNP a donc été retirée. J3 reste un connecteur
  de test optionnel ; C6 et L1 conservent leur statut DNP. Pour un essai
  avec antenne externe sur J3, retirer R6 pour isoler l'antenne imprimée.
- **Repères de composants ajoutés en sérigraphie** : les 40 références sont
  visibles, 21 sur F.Silkscreen et 19 sur B.Silkscreen. Le verso est utilisé
  dans les zones denses afin de conserver une hauteur minimale de 0,8 mm.
  Le plan d'implantation et le tableau des composants ci-dessous facilitent
  le repérage avant soudure.
- **Bornier solaire J10 accessible** : son entrée de câble est orientée vers
  le bord gauche. Le cavalier J5 et des composants voisins ont été déplacés
  pour dégager son enveloppe mécanique et l'accès aux fils. Vérifier le
  dégagement correspondant dans le boîtier final.
- **Sept résistances alternatives supprimées du schéma et du PCB** :
  ROV1B1, ROV2B1, ROK1B1, ROK2B1, ROK3B1, ROUT1B1 et ROUT2B1.
  Les résistances principales et leurs valeurs sont conservées.
- Les pistes concernées par ces déplacements ont été reprises, avec des
  sorties réservées autour du BQ25570 et des raccordements des plans de masse.

## Vérifications

- Contour Edge.Cuts : **35 × 55 mm** ; épaisseur : **1,6 mm**.
- **40 empreintes**, 862 segments de piste et 64 vias.
- Largeur minimale de piste : 0,2 mm ; règles de fabrication initiales
  conservées, sans nouvelle exclusion DRC.
- **DRC : 0 violation, 0 connexion manquante, 0 écart avec le schéma**.
- **ERC : 0 erreur et 6 avertissements préexistants**, sans nouvel
  avertissement. Ils concernent un label isolé, la copie du symbole BQ25570,
  deux indicateurs de non-connexion et deux alias de noms sur le bus I²C.
- Les valeurs des composants conservés sont inchangées. La seule modification
  de statut de montage est R4, nécessaire au nouveau chemin RF.

Rapports et vues issus du PCB enregistré :

- [Rapport DRC](test/DRC_test.json)
- [Rapport ERC](test/ERC_test.json)
- [Vérifications de dimensions et de connectivité RF](test/verification_test.json)
- [Cuivre et sérigraphie dessus](test/cuivre_dessus_test.svg)
- [Cuivre et sérigraphie dessous, vue miroir](test/cuivre_dessous_test.svg)
- [Plan d'implantation dessus](test/implantation_test.svg)
- [Composants et positions des repères](test/composants_test.csv)

## Points restant à valider avant fabrication

Ces contrôles de continuité et d'isolement ne valident pas le fonctionnement
électrique ni l'accord radio. La géométrie de l'antenne CST reste inchangée ;
son calcul utilisait du FR-4 de 0,8 mm, alors que cette carte utilise 1,6 mm.
La piste RF de cette version a une largeur de 0,4 mm sur le trajet principal :
elle n'est pas certifiée à 50 Ω. Recalculer l'impédance avec l'empilage réel,
resimuler l'ensemble et mesurer le prototype à 868 MHz avant fabrication finale.
Voir aussi [les limites de l'import CST](A2_IFA_868MHz_CST.md).

**J19 conserve un problème électrique déjà présent** : fermer ce cavalier
relie le réseau nommé VOUT_EN, également connecté à VSTOR, à GND. Ne pas
fermer J19 sans corriger et valider cette commande. La commande `'EN` du
BQ25570 reste également à revoir. Ces points n'ont pas été modifiés dans
cette version test ; ils sont détaillés dans le
[rapport initial](ROUTAGE_35x55.md#points-a-valider-avant-fabrication).

La sauvegarde locale avant modification est conservée dans
`.history/avant_modifs_test/`, hors du dépôt Git.
