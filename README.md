# Site vitrine SoCraTes Lille

Repo du site vitrine de la non conférence SoCraTes 2027.

## Prévisualisation locale

Le site est statique, sans build ni installation de dépendances. `package.json`
n'intervient pas dans la publication ou sa vérification.

Depuis la racine du dépôt :

```sh
mkdir -p _site
cp index.html styles.css _site/
cp -R assets _site/
python3 -m http.server 5173 --bind 127.0.0.1 --directory _site
```

Ouvrir <http://127.0.0.1:5173/> et vérifier le titre
« SoCraTes Lille — 16 avril 2027 », les styles, le logo, les photos après
défilement, le lien « Infos pratiques » et l'ouverture d'une réponse FAQ.
Dans « L’organisation », vérifier le titre au-dessus d’une grille à quatre cases :
HoppR et Shodo sur la première ligne, Epitech et les remerciements sur la seconde.
À 640 pixels de largeur ou moins, les cases s’empilent dans cet ordre, sans
débordement horizontal. Au-delà, les deux colonnes ont la même largeur et les
cases de chaque ligne la même hauteur, sans déformer les logos.
Vérifier que HoppR et Shodo ouvrent chacun leur site dans un nouvel onglet,
sans quitter le site SoCraTes Lille ; Epitech conserve la navigation dans
l’onglet courant. Contrôler le texte de remerciement, le lien Software Craft
Lille, le contact et la visibilité du focus lors du parcours clavier.
Après vérification, arrêter le serveur et supprimer le répertoire généré `_site` ;
ne pas l'ajouter au dépôt.

## Publication GitHub Pages

Le workflow `.github/workflows/deploy-pages.yml` publie uniquement `index.html`,
`styles.css` et `assets/`, via un artefact `_site`. Il se déclenche sur les pushs
vers `main` ou manuellement depuis `main`, jamais sur les pull requests.
Il utilise les actions officielles, le `GITHUB_TOKEN` et OIDC, sans secret personnel.

Première publication, avec un compte administrateur autorisé :

1. Ouvrir <https://github.com/swcraftLille/SoCraTesLille2027/settings/pages>
   et choisir **Build and deployment → Source → GitHub Actions**, sans générer
   un autre workflow.
2. Intégrer le workflow sur `main` par le circuit habituel. Aucun commit ni push
   n'est effectué automatiquement par cette configuration locale.
3. Le push déclenche **Deploy to GitHub Pages**. Si le workflow était déjà intégré
   lors de l'activation, ouvrir
   <https://github.com/swcraftLille/SoCraTesLille2027/actions/workflows/deploy-pages.yml>
   puis **Run workflow**, sélectionner `main` et lancer.
4. Conserver les protections existantes ; si l'environnement demande une
   approbation, la faire donner par un administrateur autorisé.
5. Vérifier le succès du job `deploy`, notamment l'upload et le déploiement, puis
   ouvrir l'URL de l'environnement `github-pages`. L'URL standard attendue est
   <https://swcraftlille.github.io/SoCraTesLille2027/>, à confirmer par le workflow.
   Refaire les contrôles visuels et interactifs ci-dessus et vérifier l'absence
   de 404 pour les ressources locales sous le sous-chemin du dépôt.

La prévisualisation locale ne prouve pas une publication en ligne. L'activation
et le premier déploiement nécessitent encore une vérification depuis un compte
GitHub autorisé. Si Pages est indisponible pour l'offre ou la politique de
l'organisation, faire résoudre ce prérequis sans modifier automatiquement la
visibilité du dépôt, l'offre ou les protections.
