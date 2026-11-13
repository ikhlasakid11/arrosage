# Arrosage

Projet electronique KiCad 10. Ouvrir `arrosage.kicad_pro`.

Le schema principal `arrosage.kicad_sch` utilise trois sous-feuilles :
`untitled.kicad_sch` (radio), `BQ25570.kicad_sch` (alimentation) et
`capteur.kicad_sch`. `mic.kicad_sch` est conserve comme feuille de travail.

Les symboles et empreintes personnalises sont inclus dans `symbols/` et
`footprints/`. Les tables de bibliotheques utilisent `${KIPRJMOD}` : aucune
dependance au dossier externe `pot_fleur` n'est necessaire pour ces empreintes.
Les bibliotheques standard de KiCad doivent etre installees.

Les empreintes de l'antenne `SmartPot_RF:CST_IFA_868MHz_SmartPot` et de la
bobine `LPS4018-223MRC:IND_LPS4018-223MRC` ont ete recuperees dans la copie
locale de `SmartPot_RAK3172/old/pot_fleur`, sans modification de leur geometrie.
Le modele 3D optionnel `3dmodels/LPS4018-223MRC.step` n'etait pas fourni ;
son absence n'empeche pas l'utilisation de l'empreinte PCB.

La bibliotheque SHT40 provient du pack local SHT40_KiCad. Ses instructions
et attributions sont conservees dans `docs/SHT40_LIRE_MOI.txt`
(bibliotheques KiCad, CC-BY-SA 4.0 avec exception KiCad).
Les autres fichiers conservent leurs attributions et conditions d'origine ;
aucune nouvelle licence generale n'est attribuee.

Les sauvegardes `.history/` et preferences personnelles sont ignorees par Git.
Le projet est en cours : cette preparation pour GitHub ne valide pas la
conception electrique ni l'aptitude du PCB a la fabrication.

L'antenne CST du projet est importee sous la reference **A2**, dans la
bibliotheque `Arrosage_RF`. Voir [les cotes, raccords et limites de l'import](docs/A2_IFA_868MHz_CST.md).

La carte est maintenant placee et routee en **35 x 55 mm, deux couches,
epaisseur 1,6 mm**, avec 25 % de la surface reservee a l'antenne.
Le [rapport de routage](docs/ROUTAGE_35x55.md) indique les verifications et
les points du schema et de la liaison RF a revoir avant fabrication.
