# resources

## Project setup
```
npm install
```

## Project Setup 2
```
Buat folder baru dengan nama resources dan pindah kan semua file kedalam folder resources, kecuali folder "config" dan file api.php
```

## Project Setup 3
```
Buka folder config > Database.php silahkan ubah settinggan didalamnya seperti nama database dan nama kolom, sesuaikan dengan file api.php
```

### Create .htaccess and Copy This
```
RewriteEngine On

RewriteRule ^note/create/?$ api.php?f=CREATE [NC,L]

RewriteRule ^note/update/?$ api.php?f=UPDATE [NC,L]

RewriteRule ^note/delete/?$ api.php?f=DELETE [NC,L]

RewriteRule ^note?$ api.php [NC,L]

RewriteRule ^note/([0-9]+)/?$ api.php?id=$1 [NC,L]
```

### Run
```
npm run serve atau install vue ui
```

### Create By 
```
  Celvine Adi Putra
```

### Status
 ```
 Development
 ```
