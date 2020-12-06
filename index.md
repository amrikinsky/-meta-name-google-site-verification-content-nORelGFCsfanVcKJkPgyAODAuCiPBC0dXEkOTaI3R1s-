## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/amrikinsky/.github-stale.yml/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/amrikinsky/.github-stale.yml/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
<!DOCTYPE html>

<html>

<head>

  <meta charset="utf-8">

  <title>App Shell</title>

  <link rel="manifest" href="/manifest.json">

  <meta http-equiv="X-UA-Compatible" content="IE=edge">

  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <link rel="stylesheet" type="text/css" href="styles/inline.css">

</head>

<body>

  <header class="header">

    <h1 class="header__title">App Shell</h1>

  </header>

  <nav class="nav">

  ...

  </nav>

  <main class="main">

  ...

  </main>

  <div class="dialog-container">

  ...

  </div>

  <div class="loader">

    <!-- Show a spinner or placeholders for content -->

  </div>

  <script src="app.js" async></script>

  <script>

  if ('serviceWorker' in navigator) {

    navigator.serviceWorker.register('/sw.js').then(function(registration) {

      // Registration was successful

      console.log('ServiceWorker registration successful with scope: ', registration.scope);

    }).catch(function(err) {

      // registration failed :(

      console.log('ServiceWorker registration failed: ', err);

    });

  }

  </script>

</body>


</html>
var cacheName = 'shell-content';

var filesToCache = [

  '/css/styles.css',

  '/js/scripts.js',

  '/images/logo.svg',

  '/offline.html',

  '/',

];

self.addEventListener('install', function(e) {

  console.log('[ServiceWorker] Install');

  e.waitUntil(

    caches.open(cacheName).then(function(cache) {

      console.log('[ServiceWorker] Caching app shell');

      return cache.addAll(filesToCache);

    })

  );

});
gulp.task('generate-service-worker', function(callback) {

  var path = require('path');

  var swPrecache = require('sw-precache');

  var rootDir = 'app';

  swPrecache.write(path.join(rootDir, 'service-worker.js'), {

    staticFileGlobs: [rootDir + '/**/*.{js,html,css,png,jpg,gif}'],

    stripPrefix: rootDir

  }, callback);

});
