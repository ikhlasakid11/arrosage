# Empreinte A2 — antenne IFA du fichier CST

L'antenne du schema radio porte maintenant la reference **A2**. Son empreinte
est `Arrosage_RF:A2_IFA_868MHz_CST`, incluse dans les bibliotheques du projet.
L'instance est placee et raccordee dans `arrosage.kicad_pcb`, a l'origine
X = 82,9 mm, Y = 63,15 mm, dans le quart superieur de la carte 35 x 55 mm.
Voir [le rapport du routage](ROUTAGE_35x55.md) pour le placement final,
les controles et les points restant a valider avant fabrication.

## Geometrie et raccordement

Le cuivre est repris du modele final `antenne_IFA_868MHz.cst`, sans changement
d'echelle : `Lretour = 23 mm`, `Ltip = 8 mm`, `Xfeed = -14,6 mm`.
Les sept rectangles de cuivre de l'antenne sont conserves. Leur enveloppe
mesure **33 x 13 mm**. La zone libre de cuivre du support est de
**35 x 13,75 mm**. Le substrat CST complet mesure **35 x 55 x 0,8 mm**.

L'origine de l'empreinte est le point CST (-14,6 ; 14,35), cote antenne du
port discret. La conversion est : X_KiCad = X_CST + 14,6 ;
Y_KiCad = 14,35 - Y_CST. L'inversion de Y correspond aux axes KiCad.

- Pad **1** : RF, reseau `Net-(A2-VIN)`, relie dans le schema a R6 et L1.
- Pad **2** : masse GND et branche de court-circuit de l'IFA.
- Un raccord intentionnel entre les pads 1 et 2 est declare par un net tie.
- La liaison des deux masses du modele CST est reprise par un pad traverse
  numero 2 : diametre cuivre 0,6 mm, percage 0,3 mm. Il doit etre relie aux
  plans de masse lors du routage, comme dans le modele CST.
- Le radiateur est sur F.Cu, sans depot de pate a braser. Le cuivre de
  l'antenne est ouvert dans F.Mask pour ne pas ajouter de vernis au radiateur.

Une zone d'exclusion couvre la bande rayonnante sur toutes les couches de
cuivre. Elle interdit les remplissages, vias, autres empreintes et pistes,
avec une petite entree reservee a l'alimentation RF. Les pads de l'antenne
elle-meme restent autorises. Les plans de masse du PCB doivent s'arreter
aux limites prevues par le modele CST : Y_CST = 13,75 mm sur le dessus,
11,15 mm sur le dessous. Ils ne sont pas inclus dans cette empreinte.

## Limites a conserver lors de l'integration

Le port discret CST est une excitation ideale, pas une piste de PCB.
Le routage d'alimentation et son isolation dans la masse doivent etre
dessines puis resimules. Le gap de port CST de 0,6 mm ne doit pas etre
remplace par un pont entre RF et GND.

Le modele CST utilise un substrat de **0,8 mm**, alors que le projet KiCad
est configure a **1,6 mm**. L'importation conserve la geometrie du cuivre,
mais ne valide donc pas la frequence sur le PCB actuel. La simulation source
indiquait S11 = -13,74 dB a 868 MHz et un minimum a 869 MHz ; la convergence
du maillage n'etait pas demontree. Ces chiffres ne sont pas une mesure
ni une validation de l'antenne apres son integration dans KiCad.

L'ancien A1 du schema a ete renomme A2, en conservant son UUID et ses fils.
Le PCB utilise le meme chemin hierarchique que le symbole, afin de conserver
le lien lors d'une mise a jour du PCB depuis le schema.
L'ancienne empreinte SmartPot reste disponible dans la bibliotheque historique.

## Verification

- Chargement et sauvegarde avec l'API officielle pcbnew de KiCad 10.
- Dimensions et positions des sept rectangles verifiees a 1 micrometre pres.
- Connexions des pads verifiees contre la netlist exportee par KiCad.
- Zone d'exclusion et net tie reconnus par KiCad.
- Apres placement et routage : 0 violation DRC, 0 liaison manquante.

Une sauvegarde avant import est conservee dans `.history/avant_import_A2_2824d5d2/`.
Une copie du fichier CST source, sans ses resultats de calcul externes, est
incluse dans `docs/cst/antenne_IFA_868MHz.cst`.
