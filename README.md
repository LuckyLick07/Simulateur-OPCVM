# Simulateur OPCVM

Simulateur d'épargne en fonds communs de placement de l'UMOA, destiné au grand
public. Page statique unique, sans dépendance : tout le calcul s'exécute dans le
navigateur.

Site publié : https://luckylick07.github.io/Simulateur-OPCVM/

## Principe

Pour chaque fonds, le simulateur calcule le rendement annualisé constaté sur
l'historique de ses valeurs liquidatives, puis projette à taux constant le plan
d'épargne saisi (mise de départ, versements réguliers, durée, droits d'entrée et
de sortie). Le graphique confronte deux courbes : le montant cumulé déposé et
l'évolution du capital. Les frais de gestion étant déjà reflétés dans les VL,
seuls les droits d'entrée et de sortie s'ajoutent au calcul.

## Structure du dépôt

- `index.html` — le simulateur, engendré à partir du gabarit (ne pas éditer à la main)
- `donnees-vl/` — un fichier d'historique de VL par fonds (CSV `date;vl`, dates `JJ/MM/AAAA` ou `AAAA-MM-JJ`, décimales avec virgule ou point)
- `outil/gabarit.html` — le gabarit de la page (mise en forme, moteur de calcul)
- `outil/integrer_vl.py` — engendre `index.html` depuis le gabarit et les fichiers de `donnees-vl/`

## Mettre à jour les valeurs liquidatives

1. Remplacer ou compléter les fichiers de `donnees-vl/` (mêmes noms, ou nouveaux fichiers pour de nouveaux fonds).
2. Exécuter `python3 outil/integrer_vl.py` à la racine du dépôt.
3. Vérifier la sortie du script (nombre de VL, période, rendement annualisé par fonds), puis valider et pousser.

Les droits d'entrée et de sortie proposés par défaut pour chaque fonds se
règlent dans le dictionnaire `REGLAGES` en tête de `outil/integrer_vl.py`.

## Avertissement

Outil pédagogique. Il ne constitue ni un conseil en investissement, ni une offre
de souscription, ni une promesse de rendement. Les performances passées ne
préjugent pas des performances futures.
