# Carte arrosage routee — 35 x 55 mm

Version du 13 novembre 2026, KiCad 10.

## Dimensions et repartition

- Contour reel sur Edge.Cuts : **35 x 55 mm**, de X=80 a 115 et Y=50 a 105 mm.
- Deux couches de cuivre ; epaisseur conservee : **1,6 mm**.
- Bande d'antenne en haut : **35 x 13,75 mm**, soit 25 % de la surface.
- Zone composants : **35 x 41,25 mm**, soit 75 % de la surface.
- 47 empreintes positionnees, dont A2 ; les valeurs, nets, liens au schema
  et options de non-montage sont conserves.

Les pistes et vias des autres circuits sont exclus de la bande rayonnante,
avec une entree limitee a la liaison d'alimentation de l'antenne. Le plan
de masse dessus commence a Y=63,75 mm ; le plan dessous a Y=66,35 mm,
pour conserver le decalage entre les deux masses du modele CST source.

## Routage et verification

- 580 segments de piste et 55 vias.
- Largeur minimale de piste : **0,2 mm** ; isolement de la classe par defaut : **0,2 mm**.
- Vias traversants de diametre cuivre 0,6 mm et percage 0,3 mm.
- Connexions RF principales sur le dessus ; pistes courtes de puissance
  autour des inductances et du BQ25570, plans de masse sur les deux faces.
- Les pastilles de masse sont raccordees directement aux plans. Le capteur
  dispose d'un raccord de masse vers le dessous, hors de son corps.
- Les references detaillees sont sur F.Fab pour garder une serigraphie lisible.
  Les principaux connecteurs et le nom de la carte sont indiques sur F.Silkscreen.
- Controle KiCad final : **0 violation DRC et 0 liaison manquante**.
- Le circuit de toutes les empreintes a ete compare au fichier avant routage :
  aucune valeur, affectation de broche, option DNP ou liaison au schema modifiee.

Le routage combine des liaisons locales prioritaires, Freerouting en execution
locale et une finition verifiee par le DRC KiCad. Aucun fichier du projet
n'a ete envoye a un service de routage en ligne.

La sauvegarde avant routage est dans `.history/avant_routage_35x55/`.
Les rapports de controle sont conserves avec cette documentation.

## Points a valider avant fabrication

Le DRC verifie les contraintes de cuivre et la continuite ; il ne valide pas
le fonctionnement du schema ni l'accord radio.

**J19 :** son pad 1 est GND et son pad 2 est le reseau `VOUT_EN`, qui est
aussi relie a **VSTOR, U3.19**, CBYP1 et CSTOR1. Poser un cavalier sur J19
relie donc VSTOR directement a la masse. Cette connexion existait dans le
schema et a ete conservee ; revoir son intention avant de monter un cavalier.
La broche U3.5 (`'EN`) est sur un reseau a une seule broche : verifier aussi
la commande attendue avec la [notice du BQ25570](https://www.ti.com/lit/ds/symlink/bq25570.pdf).

**RF :** l'antenne source CST a ete calculee sur FR-4 de 0,8 mm, avec une
convergence de maillage non demontree. La carte routee utilise 1,6 mm,
conformement au choix de fabrication. Le cuivre de son radiateur est conserve
a l'echelle 1:1, mais les resultats CST ne sont pas ceux de cette carte routee.
Les largeurs de la liaison RF varient avec ses raccords de pastilles ; elles
ne constituent pas une certification d'impedance a 50 ohms. Recalculer cette
liaison avec l'empilage du fabricant et resimuler l'ensemble, puis mesurer
un prototype au VNA. Le [fabricant du RAK3172](https://docs.rakwireless.com/product-categories/wisduo/rak3172-module/datasheet/)
demande une liaison RF d'impedance 50 ohms.

Les composants DNP, dont le reseau d'adaptation et les variantes de resistances,
gardent leur statut initial. Ne pas les peupler automatiquement tous ensemble.
