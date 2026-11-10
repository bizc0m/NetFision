# NetFision

Éditeur visuel de pages web en un seul fichier HTML, inspiré du fonctionnement de NetObjects Fusion : canevas à positionnement absolu, interface compacte, aucune installation, aucune dépendance distante, aucune télémétrie.

**Application :** https://bizc0m.github.io/NetFision/ — ou ouvrir `index.html` directement dans un navigateur.

## Fonctions

- Menus déroulants Fichier / Templates / Édition / Aperçu / Affichage
- Canevas absolu 1100 px, X / Y / W / H éditables, glisser-déposer, grille, aimantation, redimensionnement
- Édition directe du texte au double-clic (Ctrl/⌘ Entrée valide, Échap annule)
- Calques : ordre, verrouillage, visibilité
- Badges GitHub éditables **manuellement** (aucune synchronisation automatique)
- Import d'images PNG / JPEG / WebP (2 Mio max par image, 12 Mio au total) et bibliothèque de ressources
- Plusieurs pages (catalogue, produit, documentation…)
- 13 langues éditables **manuellement** (pas de traduction automatique)
- Mode clair / sombre, accordéons imbriqués à deux niveaux
- Boutons de repli des colonnes gauche et droite (flèches sur les bords + boutons de la barre), avec `aria-expanded`, état restauré au rechargement et inclus dans le JSON

## Enregistrer, exporter, charger

| Action | Effet |
|---|---|
| Enregistrer dans le navigateur (Ctrl/⌘ S) | Écrit dans IndexedDB local. Aucun fichier téléchargé. |
| Exporter le projet JSON (Ctrl/⌘ Maj S) | Télécharge `NetFision-projet.json` : pages, objets, images, état de l'interface (thème, pliages, colonnes). |
| Charger un projet | Remplace le projet courant après confirmation. |
| Exporter la page comme template | Télécharge `<page>.template.json` : page courante + images utilisées. |
| Charger un template | Ajoute une **nouvelle page** sans écraser le projet (identifiants et noms de fichiers renumérotés). |
| Exporter la page HTML | Page publiable autonome (images embarquées), sans outils d'édition ni script. |

Le stockage navigateur ne remplace pas une sauvegarde : exporter régulièrement le projet JSON.

Si NetFision est ouvert **dans un cadre intégré** (aperçu d'un autre outil), l'hôte peut bloquer téléchargements et stockage ; un message l'indique au démarrage. Ouvrir alors le fichier directement.

## Aperçu

- Modale : affiche le HTML réellement exporté (iframe isolée), largeurs 1100 / 768 / 390.
- Fenêtre séparée : message explicite si le navigateur bloque la fenêtre.
- La largeur mobile simulée ne rend pas une page absolue responsive. Pour les longues documentations, le mode **Documentation en flux** exporte les blocs dans l'ordre vertical, sur une colonne fluide.

## Compatibilité des données

La base IndexedDB `plane-one-v9`, le format de projet `version: 9` (et import `version: 8`) et le format de template `plane-template` sont conservés : les projets créés avec Plane One restent lisibles.

## Tests (v1.2)

53 contrôles E2E Playwright, données synthétiques, profils navigateur neufs, exécutés sur Chromium et WebKit, en `http://` et `file://` — tous réussis : démarrage, repli/dépli des colonnes, boutons accessibles une fois repliés, gain d'espace du canevas, accordéons parent/enfant indépendants, restauration après rechargement, thème persistant, déplacement, redimensionnement, édition texte (validation / annulation), badge, import d'image (et refus d'un faux PNG), export/réimport projet, export/chargement template sans collision, aperçu modal, fenêtre séparée (et blocage signalé), export HTML (échappement, lien `javascript:` neutralisé, image embarquée, rendu du fichier).

Non testé : Firefox, Safari réel (WebKit Playwright seulement), appareils tactiles.
