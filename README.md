# Lecteur France Culture

Ce projet fournit une page HTML unique (`lecteur.html`) pour écouter France Culture en direct, ou avec un décalage temporel qui fonctionne jusqu'à un délai de 24h. L'interface expose plusieurs contrôles pour jouer le flux live, revenir à un horaire précis (par timestamp Unix ou date ISO), ou lancer automatiquement le journal de 19h calculé pour l'heure de Paris.
Il a été généré par ChatGPT à partir d'un développement "legacy", remontant à plusieurs années.
Utilisation première de ChatGPT pour générer le code via l'interface de chat (usage génératif classique), puis évolution via Codex.

## Pré-requis
- Navigateur moderne avec prise en charge de l'audio HTML5 et de l'API Web Audio.
- Pour une meilleure compatibilité HLS, l'application charge `hls.js` depuis un CDN ; veillez à disposer d'un accès réseau si vous ouvrez le fichier localement.

## Démarrage
1. Ouvrez directement `lecteur.html` dans votre navigateur **ou** servez le répertoire avec un serveur statique simple, par exemple :
   ```bash
   python -m http.server 8000
   ```
2. Cliquez sur le bouton désiré (lecture live, lecture par date, etc.). Si le navigateur bloque l'autoplay, utilisez le bouton Play du lecteur audio.

## Fonctionnalités principales
- **Lecture live** : lit l'URL HLS fournie dans le champ « direct hls ».
- **Lecture par retard** : calcule un paramètre `delay` à partir d'un timestamp Unix et joue le flux correspondant.
- **Lecture par date** : construit une URL `?date=` à partir d'une date ISO UTC saisie.
- **Journal de 19h** : calcule le dernier journal de 19h à Paris et lance automatiquement la lecture correspondante.
- **Générateur de timestamps** : convertit des champs date/heure locaux en timestamp Unix ou en chaîne ISO UTC.
- **Contrôles audio** : réglage du volume initial, gain logiciel (0–300 %) via Web Audio et vitesse de lecture (0.5x–2x).

## Paramètres d'URL utiles
- `?vol=` : fixe le volume initial (entre 0–1 ou 0–100 %).
- `?gain=` : définit le gain logiciel initial (0–300 %).
- `?delay=` ou `?date=` : utilisables sur les endpoints configurés pour lire un point précis du flux.

## Conseils
- Le bouton « journal 19h » se base sur le fuseau `Europe/Paris` pour déterminer le dernier journal disponible.
- Les champs de date utilisent l'heure locale du navigateur ; si une conversion UTC est nécessaire, utilisez le bouton « remplir iso (utc) depuis ces champs ».
