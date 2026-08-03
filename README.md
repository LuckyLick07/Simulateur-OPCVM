# Simulateur OPCVM

Simulateur d'épargne en fonds communs de placement de l'UMOA, destiné au grand
public. Page statique unique, sans dépendance : tout le calcul s'exécute dans le
navigateur.

Site publié : https://luckylick07.github.io/Simulateur-OPCVM/

## Principe

Pour chaque fonds, le simulateur calcule le rendement annualisé constaté sur
l'historique de ses valeurs liquidatives, puis projette à taux constant. Trois
scénarios : épargne par capitalisation, rente tirée d'un capital (montant fixé →
durée calculée, ou durée fixée → montant calculé, avec cas « à vie »), et plan
retraite combinant épargne mensuelle jusqu'à la retraite puis rente jusqu'à
épuisement. Un parcours guidé propose fonds et scénario d'après les réponses du
visiteur, en expliquant ses critères (horizon, régularité observée des VL,
frais). Chaque simulation s'exporte en rapport PDF d'un clic. Les frais de
gestion étant déjà reflétés dans les VL, seuls les droits d'entrée (sur chaque
versement) et de sortie (sur chaque retrait ou la valeur finale) s'ajoutent.

## Structure du dépôt

- `index.html` — le simulateur, engendré à partir du gabarit (ne pas éditer à la main)
- `donnees-vl/` — un fichier d'historique de VL par fonds (CSV `date;vl`, dates `JJ/MM/AAAA` ou `AAAA-MM-JJ`, décimales avec virgule ou point)
- `outil/gabarit.html` — le gabarit de la page (mise en forme, moteurs de calcul, parcours guidé, rapport PDF)
- `outil/integrer_vl.py` — engendre `index.html` depuis le gabarit et les fichiers de `donnees-vl/` (rendement, volatilité et pire variation calculés par fonds)
- `vendeur/jspdf.umd.min.js` — bibliothèque de génération PDF, embarquée pour que le site reste sans dépendance externe

## Mettre à jour les valeurs liquidatives

1. Remplacer ou compléter les fichiers de `donnees-vl/` (mêmes noms, ou nouveaux fichiers pour de nouveaux fonds).
2. Exécuter `python3 outil/integrer_vl.py` à la racine du dépôt.
3. Vérifier la sortie du script (nombre de VL, période, rendement annualisé par fonds), puis valider et pousser.

Les droits d'entrée et de sortie proposés par défaut pour chaque fonds se
règlent dans le dictionnaire `REGLAGES` en tête de `outil/integrer_vl.py`.

## Envoi du résumé par e-mail

Le bouton « Recevoir par e-mail » fonctionne dans deux modes. Tant que le
dictionnaire `EMAILJS` en tête de `outil/integrer_vl.py` est vide, il ouvre la
messagerie du visiteur avec le résumé prérédigé (aucun service tiers). Une fois
les trois clés renseignées (`service`, `template`, `publicKey` d'un compte
EmailJS) et `index.html` régénéré, l'envoi devient automatique depuis la page.
Dans le compte EmailJS, restreindre les origines autorisées à
`luckylick07.github.io` pour éviter tout usage du quota par un tiers.

## Avertissement

Outil pédagogique. Il ne constitue ni un conseil en investissement, ni une offre
de souscription, ni une promesse de rendement. Les performances passées ne
préjugent pas des performances futures.
