# Mawid – application Android (APK)

Application de prise de rendez-vous médicaux (français / English / عربي), emballée en application Android avec [Capacitor](https://capacitorjs.com). L'APK est construit automatiquement par GitHub Actions : aucun Android Studio n'est nécessaire.

## Obtenir l'APK avec GitHub (sans rien installer)

1. Créez un dépôt sur GitHub (ex. `mawid-android`, vide).
2. Dézippez ce projet et envoyez **tout son contenu** dans le dépôt (bouton *Add file → Upload files*, en glissant les dossiers `www`, `assets`, `.github` et les fichiers de la racine). Le dossier caché `.github` doit bien être envoyé.
3. Ouvrez l'onglet **Actions** : le workflow *Build Android APK* démarre tout seul (≈ 5 à 8 min). Sinon : *Build Android APK → Run workflow*.
4. Quand il est vert, ouvrez l'exécution et téléchargez **Mawid-apk** (section *Artifacts*) : décompressez, vous obtenez `Mawid.apk`.
5. Copiez `Mawid.apk` sur le téléphone et ouvrez-le (autorisez « Installer des applications inconnues »).

Pour publier l'APK dans *Releases* : créez un tag, par ex. `git tag v1.0.0 && git push --tags`.

## Contenu du projet

| Élément | Rôle |
|---|---|
| `www/index.html` | L'application (HTML/CSS/JS) |
| `www/jspdf.umd.min.js` | Génération des reçus PDF (embarqué, fonctionne hors ligne) |
| `capacitor.config.json` | Nom (`Mawid`) et identifiant (`com.mawid.app`) de l'application |
| `assets/` | Icône et écrans de démarrage (générés en toutes tailles pendant le build) |
| `.github/workflows/build-apk.yml` | Construction de l'APK |

## Personnaliser

- **Nom / identifiant** : `capacitor.config.json` (`appName`, `appId`). Changez `appId` avant de publier sur le Play Store.
- **Application** : modifiez `www/index.html`, puis poussez sur GitHub : un nouvel APK est construit.
- **Icône** : remplacez les PNG de `assets/` (1024×1024 pour les icônes, 2732×2732 pour les écrans de démarrage).

## Construire en local (optionnel)

Prérequis : Node 20, JDK 17, Android SDK.

```
npm install
npx cap add android
npm run assets
npx cap sync android
cd android && ./gradlew assembleDebug
```
L'APK se trouve dans `android/app/build/outputs/apk/debug/app-debug.apk`.

## À savoir

- C'est un APK **debug** (signé avec la clé de débogage) : parfait pour installer et tester. Pour le Play Store, il faut un APK/AAB **release** signé avec votre propre clé.
- Version de démonstration : les comptes et rendez-vous sont enregistrés **sur l'appareil** (stockage local), aucun SMS n'est envoyé.
- Les polices (Poppins, Inter) sont chargées depuis Google Fonts ; sans connexion, des polices système les remplacent.
- Les reçus PDF s'enregistrent/se partagent via la fenêtre de partage Android.
