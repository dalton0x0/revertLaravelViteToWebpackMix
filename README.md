# Installation et Configuration de Laravel avec Webpack Mix au lieu de Vite

### 1. Supprimer Vite
```sh
npm remove vite laravel-vite-plugin
rm vite.config.js
```

### 2. Installer Webpack Mix
```sh
npm i --save-dev webpack webpack-cli webpack-dev-server html-webpack-plugin
```

### 3. Installer Laravel Mix
```sh
npm install laravel-mix --save-dev
```

### 4. Créer un fichier `webpack.mix.js` à la racine du projet
Mettez le contenu suivant :
```js
const mix = require('laravel-mix');

mix.js('resources/js/app.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css')
    .setPublicPath('public');
```

### 5. Modifier `package.json`
Ajouter les scripts suivants :
```json
{
    "private": true,
    "scripts": {
        "dev": "npm run development",
        "development": "mix",
        "watch": "mix watch",
        "watch-poll": "mix watch -- --watch-options-poll=1000",
        "hot": "mix watch --hot",
        "prod": "npm run production",
        "production": "mix --production"
    }
}
```

Enlever la ligne :
```json
{
    "type": "module"
}
```

## 6. Utiliser Mix dans vos templates Blade
Remplacer :
```html
@vite('resources/js/app.js')
@vite('resources/css/app.css')
```
Par :
```html
<link rel="stylesheet" href="{{ mix('css/app.css') }}">
<script src="{{ mix('js/app.js') }}"></script>
```

### 7. Compiler les assets
```sh
npm run dev
```
Pour une version optimisée :
```sh
npm run prod
```

## 8. Lancer le projet Laravel
```sh
php artisan serve
```
Le projet est accessible sur `http://127.0.0.1:8000`

---
🎉 Le projet Laravel est maintenant configuré avec Webpack Mix
