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
