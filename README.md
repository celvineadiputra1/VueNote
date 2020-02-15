# resources

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### Create .htaccess and Copy This
```
RewriteEngine On

RewriteRule ^note/create/?$ api.php?f=CREATE [NC,L]

RewriteRule ^note/update/?$ api.php?f=UPDATE [NC,L]

RewriteRule ^note/delete/?$ api.php?f=DELETE [NC,L]

RewriteRule ^note?$ api.php [NC,L]

RewriteRule ^note/([0-9]+)/?$ api.php?id=$1 [NC,L]
```

### Create By 
```
  Celvine Adi Putra
```

### Status
 ```
 Development
 ```
