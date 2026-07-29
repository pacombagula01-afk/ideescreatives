# Idées Créatives — Site + Administration

Ce dossier contient votre site **et** son interface d'administration. Aucun WordPress.

## Contenu du dossier
- `index.html` — le site (design + logo intégrés).
- `content.json` — **tous les textes du site** (c'est ce fichier que l'administration modifie).
- `admin/` — l'interface d'administration (Sveltia CMS) accessible à l'adresse `votre-site/admin`.
- `images/` — dossier où seront rangées les images téléversées depuis l'admin.

Le site lit `content.json` au chargement. Si vous modifiez un texte dans l'admin,
le site se met à jour tout seul. (Ouvert en local par double-clic, le site affiche
les textes par défaut : c'est normal, l'admin ne fonctionne qu'une fois en ligne.)

---

## PARTIE 1 — Mettre le site en ligne

Deux textes/images ne changent pas ici : c'est du gratuit, sécurisé (HTTPS automatique).

### Option recommandée : GitHub + Cloudflare Pages
L'admin a besoin que le site soit relié à un dépôt **GitHub** — autant le faire dès le départ.

1. Créez un compte gratuit sur **github.com**.
2. Créez un nouveau dépôt (**New repository**), par exemple `idees-creatives`, en **Public**.
3. Cliquez **Add file → Upload files**, glissez **tout le contenu de ce dossier**
   (`index.html`, `content.json`, les dossiers `admin/` et `images/`), puis **Commit**.
4. Créez un compte gratuit sur **dash.cloudflare.com** → **Workers & Pages → Create → Pages → Connect to Git**.
5. Sélectionnez votre dépôt. Laissez les réglages de build **vides** (c'est un site statique).
   Cliquez **Save and Deploy**.
6. En moins d'une minute, votre site est en ligne à une adresse `…​.pages.dev`, en HTTPS.

### Option la plus rapide (sans admin, pour tester) : Netlify Drop
1. Renommez ce dossier au besoin, allez sur **app.netlify.com/drop**.
2. Glissez le **dossier entier**. Le site est en ligne immédiatement.
   (Pour activer l'admin ensuite, il faudra tout de même relier un dépôt GitHub — voir Partie 2.)

---

## PARTIE 2 — Activer l'interface d'administration (`/admin`)

L'admin enregistre les modifications dans votre dépôt GitHub. Il faut donc l'autoriser
à s'y connecter **une seule fois**. C'est l'étape la plus technique — faites-la
tranquillement, ou demandez de l'aide (voir la note en bas).

1. Ouvrez `admin/config.yml` et remplacez la ligne
   `repo: VOTRE-COMPTE/VOTRE-DEPOT` par votre dépôt réel, ex. `pacom/idees-creatives`.
   Renvoyez le fichier sur GitHub (Upload files → Commit).
2. Sur GitHub : **Settings (du compte) → Developer settings → OAuth Apps → New OAuth App**.
   - Application name : `Admin Idées Créatives`
   - Homepage URL : l'adresse de votre site (ex. `https://idees-creatives.pages.dev`)
   - Authorization callback URL : l'adresse fournie par le service d'authentification
     Sveltia (voir étape 3).
3. Sveltia a besoin d'un petit « relais d'authentification ». Le plus simple est de
   déployer le relais officiel gratuit **sveltia-cms-auth** sur Cloudflare Workers
   (guide : https://github.com/sveltia/sveltia-cms-auth ). Il vous donne l'URL de
   callback à coller à l'étape 2, et vous y renseignez l'identifiant/secret de l'OAuth App.
4. C'est fini : allez sur `votre-site/admin`, cliquez **Se connecter avec GitHub**,
   autorisez, et l'interface s'ouvre.

> Astuce : si cette étape d'authentification vous semble trop technique, il existe des
> administrations « hébergées » qui se connectent au même dépôt GitHub sans rien déployer
> (ex. **Pages CMS**, **TinaCloud**). On peut adapter la configuration à l'une d'elles.

---

## PARTIE 3 — Utilisation au quotidien (pour Pacom)

1. Aller sur `votre-site/admin` et se connecter.
2. Cliquer sur **Contenu du site → Page d'accueil**.
3. Modifier les champs (titres, textes, domaines, coordonnées, réseaux sociaux…).
4. Cliquer **Enregistrer / Publier**. Le site se met à jour en une minute.

Pour **ajouter un domaine d'intervention** : dans la section *Domaines*, cliquer
« + » sous la liste, remplir la famille, l'étiquette, le titre et la description.

---

## PARTIE 4 — Nom de domaine & sécurité (optionnel mais conseillé)
- Achetez un domaine (`.com`, `.org`, ou `.cd`) chez un registrar sérieux
  (Cloudflare Registrar, Namecheap, Gandi) — environ 10–15 $/an.
- Dans Cloudflare Pages (ou Netlify), section **Custom domains**, reliez-le :
  le certificat HTTPS s'installe automatiquement.
- Activez la **double authentification (2FA)** sur vos comptes GitHub, Cloudflare et registrar.

---

*Site conçu pour Idées Créatives — Communication · Audiovisuel · Conseil · Formation · Événementiel.*
