<div align="center">

# 🌍 Atlas du Ciel

**Les avions du monde entier, tous les objets spatiaux depuis 1957 et la météo en direct, sur un globe 3D dans votre navigateur.**

[**▶ Voir le site en ligne**](https://damballah.github.io/atlas/) · [Tutoriel d'installation](#-installer-votre-propre-atlas-du-ciel-tutoriel) · [Licence MIT](LICENSE)

<!-- IMAGE PRINCIPALE : remplacez le fichier docs/images/apercu.png par une capture du globe (1600×900 conseillé) -->
![Aperçu d'Atlas du Ciel](docs/images/apercu.png)

</div>

<!-- GALERIE : déposez vos captures dans docs/images/ avec ces noms (ou changez les noms ci-dessous) -->
| Avions en temps réel | Satellites et débris | Voyage dans le temps |
|:---:|:---:|:---:|
| ![Avions](docs/images/avions.png) | ![Satellites](docs/images/satellites.png) | ![Frise 1900 → aujourd'hui](docs/images/frise.png) |
| **Recherche d'un vol** | **Passages au-dessus de chez vous** | **Fiche d'un objet** |
| ![Recherche](docs/images/recherche.png) | ![Visibilité](docs/images/visibilite.png) | ![Fiche](docs/images/fiche.png) |
| **Nuages et pluie** | **Vents animés** | **Météo d'un lieu** |
| ![Nuages et pluie](docs/images/meteo.png) | ![Vents](docs/images/vents.png) | ![Météo au clic](docs/images/meteo-clic.png) |

---

## ✨ Ce que ça fait

- 🌐 **Globe 3D** à manipuler dans tous les sens : tourner, zoomer du ras du sol jusqu'à l'orbite géostationnaire, jour et nuit réalistes.
- 🔎 **Zoom net jusqu'aux villes** : en s'approchant, le globe se couvre d'images satellites de plus en plus détaillées, comme Google Earth (Sentinel-2 à 10 m, ou Esri jusqu'à 1 m, au choix dans ⚙).
- ✈️ **Avions du monde entier**, orientés selon leur vrai cap, avec leur traînée des 30 dernières minutes. Ils sont relevés toutes les 5 minutes, et entre deux relevés chaque avion avance selon sa vitesse et son cap réels.
- 🛰️ **Satellites, étages de fusée et débris** : plus de 30 000 objets, avec les orbites précises des satellites actifs.
- ⏳ **Voyage dans le temps de 1900 à aujourd'hui** : le ciel vide, le premier vol des frères Wright, Spoutnik, la Lune, l'explosion de Starlink… avec les grandes dates sur une frise.
- 🔍 **Recherche** d'un vol (`AFR1234`), d'une compagnie (« air france ») ou d'un satellite (« ISS »). Un clic n'affiche plus que cet objet.
- 👁️ **Visibilité** : à partir d'une adresse, les prochains passages de l'ISS (ou d'un autre satellite) visibles à l'œil nu, avec l'heure et la direction où regarder.
- ☁️ **Météo en direct** : les vrais nuages vus par les satellites météo, la pluie et les orages, et les vents animés, sur les 3 derniers jours (la frise les fait défiler heure par heure).
- 📍 **Météo d'un lieu** : un clic n'importe où sur la Terre affiche la température, le ciel, le vent et les prochaines heures. Pour une date passée choisie sur la frise, la météo de ce jour-là, jusqu'en 1940.
- 🆕 **Nouveaux lancements** ajoutés automatiquement, avec une liste des nouveautés.
- 🆓 **100 % gratuit et 100 % GitHub** : aucun serveur à louer, aucun ordinateur à laisser allumé.

---

## 🧭 Comment ça marche (en une image)

```
            ┌──────────────── GitHub (gratuit) ────────────────┐
 OpenSky ──►│ tâche « Atlas - avions »      toutes les 5 min   │──► branche atlas-avions ─┐
CelesTrak ─►│ tâche « Atlas - satellites »  toutes les 3 h     │──► branche atlas-donnees ┤
 EUMETSAT,  │                                                  │                          │
 NASA, NOAA►│ tâche « Atlas - météo »       toutes les heures  │──► branche atlas-meteo ──┤
            └──────────────────────────────────────────────────┘                          │
                                                                                          ▼
                              votre navigateur  ◄──  site damballah.github.io/atlas (GitHub Pages)
```

Le site ne peut pas interroger OpenSky lui-même : OpenSky refuse les appels qui viennent directement d'une page web. Ce sont donc trois tâches automatiques de GitHub (GitHub Actions) qui vont chercher les données et les déposent sur trois branches du dépôt (pour la météo, la tâche assemble les images des satellites en une carte du monde, ce qu'un navigateur ne peut pas faire seul). Le site les lit ensuite. Chaque branche ne garde qu'un seul commit, remplacé à chaque relevé : le dépôt ne grossit pas.

---

## 🚀 Installer votre propre Atlas du Ciel (tutoriel)

> Il vous faut seulement **un compte GitHub** (gratuit). Comptez **10 minutes**. Aucune ligne de commande.

### Étape 1 — Avoir un site GitHub Pages

Si vous avez déjà un dépôt nommé **`votre-pseudo.github.io`**, passez à l'étape 2.

Sinon, sur GitHub : bouton **＋** en haut à droite › **New repository**. Nom : **`votre-pseudo.github.io`** (avec votre vrai pseudo). Cochez **Public**, puis **Create repository**. GitHub publiera ce dépôt à l'adresse `https://votre-pseudo.github.io`.

### Étape 2 — Télécharger Atlas du Ciel

Sur cette page : bouton vert **Code** › **Download ZIP**. Dézippez-le sur votre ordinateur.

### Étape 3 — Mettre votre pseudo dans le site

Ouvrez le fichier **`atlas/index.html`** avec le Bloc-notes. Cherchez les trois lignes qui contiennent **`damballah/damballah.github.io`**, et remplacez **`damballah`** par **votre pseudo** partout (six fois en tout). Enregistrez.

```html
window.ATLAS_DONNEES = 'https://raw.githubusercontent.com/VOTRE-PSEUDO/VOTRE-PSEUDO.github.io/atlas-donnees/';
window.ATLAS_AVIONS  = 'https://raw.githubusercontent.com/VOTRE-PSEUDO/VOTRE-PSEUDO.github.io/atlas-avions/';
window.ATLAS_METEO   = 'https://raw.githubusercontent.com/VOTRE-PSEUDO/VOTRE-PSEUDO.github.io/atlas-meteo/';
```

### Étape 4 — Envoyer les fichiers

Ouvrez votre dépôt **`votre-pseudo.github.io`** sur GitHub › **Add file** › **Upload files**. Glissez-déposez le dossier **`atlas`** et le dossier **`.github`**, puis cliquez **Commit changes**.

> 💡 Vous ne voyez pas le dossier `.github` ? Dans l'explorateur Windows : **Affichage › Éléments masqués**.

### Étape 5 — Autoriser les tâches automatiques

Dans votre dépôt : **Settings** › **Actions** › **General**.
1. En haut, choisissez **Allow all actions and reusable workflows**.
2. En bas, dans **Workflow permissions**, cochez **Read and write permissions**.
3. Cliquez **Save**.

### Étape 6 — Ajouter un compte OpenSky (conseillé, gratuit)

Sans compte, OpenSky peut limiter les relevés d'avions.
1. Créez un compte sur [opensky-network.org](https://opensky-network.org), puis allez dans **Account** › **API client** et créez un client. Notez le **client_id** et le **client_secret**.
2. Dans votre dépôt : **Settings** › **Secrets and variables** › **Actions** › **New repository secret**.
3. Créez un premier secret nommé **`OPENSKY_CLIENT_ID`** contenant votre client_id, puis un second nommé **`OPENSKY_CLIENT_SECRET`** contenant votre client_secret.

> 🔒 Les secrets ne sont jamais visibles, ni dans le site ni dans le dépôt.

### Étape 7 — Lancer les trois tâches une première fois

Onglet **Actions** de votre dépôt :
1. À gauche, cliquez **Atlas - satellites** › **Run workflow** › **Run workflow**. Attendez la ✅ (1 à 3 minutes).
2. À gauche, cliquez **Atlas - avions** › **Run workflow** › **Run workflow**. Attendez la ✅ (moins d'une minute).
3. À gauche, cliquez **Atlas - météo** › **Run workflow** › **Run workflow**. Attendez la ✅ (2 à 5 minutes).

Ensuite, tout est automatique : les avions toutes les 5 minutes, la météo toutes les heures, les satellites toutes les 3 heures. L'historique météo se remplit tout seul : 3 jours après l'installation, la frise peut remonter 72 heures en arrière.

### Étape 8 — Profiter 🎉

Ouvrez **`https://votre-pseudo.github.io/atlas/`**. Le bouton **⚙** en haut à droite indique la date des derniers relevés.

---

## 🆘 Problèmes fréquents

| Ce que vous voyez | Solution |
|---|---|
| ❌ croix rouge sur une tâche, avec « 403 » ou « Permission denied » | Refaites l'**étape 5** (Read and write permissions). |
| Le site s'affiche mais sans avion ni satellite | Les tâches n'ont pas encore tourné : refaites l'**étape 7**, puis vérifiez l'**étape 3** (votre pseudo dans `index.html`). |
| « relevé il y a 40 min » | GitHub retarde parfois ses tâches quand ses serveurs sont chargés. Les relevés reprennent tout seuls. |
| Les tâches ne tournent plus après quelques semaines | GitHub met en pause les tâches d'un dépôt sans activité pendant 60 jours. Onglet **Actions** › la tâche › **Enable workflow**. |
| Pas de nuages sur le globe, message « Météo pas encore publiée » | Lancez la tâche **Atlas - météo** (étape 7) et vérifiez la ligne `ATLAS_METEO` de l'étape 3. |
| Croix rouge sur **Atlas - météo** | Un service météo était en panne pendant ce relevé : la tâche suivante, une heure plus tard, réessaie. Les relevés déjà publiés restent en ligne. |
| Message « CelesTrak en pause » | Normal : après un refus de CelesTrak, l'appli le laisse tranquille 24 h et utilise ses sources de secours. |

---

## 🎮 Utilisation

| Action | Souris / clavier |
|---|---|
| Tourner la Terre | clic gauche + glisser, ou flèches du clavier |
| Zoomer | molette, ou touches `+` / `-` |
| Déplacer la vue | clic droit + glisser |
| Plonger vers un point | double-clic |
| Voir la fiche d'un objet | clic sur l'objet |
| Météo d'un lieu | clic sur la Terre, là où il n'y a pas d'objet (case « Météo au clic » du panneau de gauche) |
| Nuages, pluie, vents | cases de la rubrique **Météo**, panneau de gauche |
| Suivre l'objet sélectionné | `F` |
| Pause / lecture du temps | `Espace` |
| Revenir au temps réel | `L` |
| Recentrer | `R` |
| Afficher / masquer une catégorie | clic sur les compteurs en haut à droite (Ctrl + clic : n'afficher que celle-ci) |

---

## 📁 Contenu du dépôt

```
atlas/
├── index.html            le site
├── main.js               le globe, les calculs d'orbite, l'interface
├── style.css             l'apparence
└── outils/
    ├── avions.py         relevé mondial des avions (utilisé par GitHub Actions)
    ├── donnees.py        catalogue et orbites des satellites (utilisé par GitHub Actions)
    └── meteo.py          cartes des nuages, de la pluie et des vents (utilisé par GitHub Actions)
.github/workflows/
├── atlas-avions.yml      tâche automatique : avions, toutes les 5 min
├── atlas-meteo.yml       tâche automatique : météo, toutes les heures
└── atlas-satellites.yml  tâche automatique : satellites, toutes les 3 h
```

Aucune installation et aucune compilation : le site est en HTML, CSS et JavaScript, avec [three.js](https://threejs.org) chargé depuis un CDN.

---

## 🤝 Respect des sources de données

- **CelesTrak** : un seul téléchargement par relevé, le catalogue au plus une fois par jour, et une **pause de 24 h après tout refus**. Les visiteurs du site ne contactent jamais CelesTrak.
- **Sources de secours** automatiques : catalogue **GCAT** et orbites **SatNOGS**, puis la dernière copie publiée.
- **OpenSky** : un relevé mondial toutes les 5 minutes, soit environ 1 150 crédits par jour sur les 4 000 d'un compte gratuit.
- **Météo** : une dizaine d'images par heure, téléchargées par GitHub et non par les visiteurs. Seule la météo au clic interroge Open-Meteo depuis le navigateur, une fois par lieu cliqué (bien en dessous des 10 000 appels par jour de l'offre gratuite non commerciale).

## 📚 Sources et crédits

- Avions : [OpenSky Network](https://opensky-network.org), données ADS-B de récepteurs bénévoles.
- Satellites : [CelesTrak](https://celestrak.org). Secours : data from GCAT (J. McDowell, [planet4589.org/space/gcat](https://planet4589.org/space/gcat)), licence CC BY, et [SatNOGS DB](https://db.satnogs.org), licence CC BY-SA 4.0.
- Fiches de vol : [adsbdb](https://www.adsbdb.com). Adresses : [OpenStreetMap / Nominatim](https://nominatim.org) et la Géoplateforme de l'IGN.
- Nuages : © EUMETSAT ([EUMETView](https://view.eumetsat.int), satellites Meteosat) et NASA GIBS (satellites GOES et Himawari). *We acknowledge the use of imagery provided by services from NASA's Global Imagery Browse Services (GIBS), part of NASA's Earth Science Data and Information System (ESDIS).*
- Pluie : NASA GPM IMERG, via [NASA GIBS](https://www.earthdata.nasa.gov/engage/open-data-services-software/earthdata-developer-portal/gibs-api). Il s'agit d'observations publiées avec environ 5 heures de décalage.
- Vents : modèle [NOAA GFS](https://www.nco.ncep.noaa.gov/pmb/products/gfs/) (vent à 10 m, grille de 1°), donc une prévision à quelques heures et non une mesure.
- Météo au clic : [Open-Meteo.com](https://open-meteo.com), licence CC BY 4.0. Archives : réanalyse ERA5 de Copernicus / ECMWF.
- Imagerie détaillée : Sentinel-2 cloudless 2024 – [s2maps.eu](https://s2maps.eu) by EOX IT Services GmbH (Contains modified Copernicus Sentinel data 2024), licence CC BY-NC-SA 4.0 (usage non commercial). Option : Esri World Imagery (© Esri, Maxar, Earthstar Geographics et la communauté des utilisateurs SIG).
- Moteur 3D : [three.js](https://threejs.org) (MIT). Textures de la Terre : NASA Blue Marble, via [three-globe](https://github.com/vasturiano/three-globe) (MIT).
- **Avions d'avant aujourd'hui** : il s'agit d'une **simulation** fondée sur des ordres de grandeur historiques, car aucune archive mondiale de tous les vols n'existe. C'est indiqué clairement dans le site.

---

## 📄 Licence

Le **code** d'Atlas du Ciel est distribué sous **licence MIT** : vous pouvez l'utiliser, le copier, le modifier et le redistribuer librement, y compris dans un projet commercial, à condition de conserver la mention de copyright et le texte de la licence. Voir le fichier [LICENSE](LICENSE).

Les **données** affichées (avions, satellites, météo, adresses) ne sont pas couvertes par cette licence : elles restent soumises aux conditions de leurs fournisseurs, listés ci-dessus.

<div align="center">

Fait avec ❤️ par [**Damballah**](https://github.com/damballah)

</div>
