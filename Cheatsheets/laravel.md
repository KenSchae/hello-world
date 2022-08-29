
# Create a Laravel site

```
composer create-project laravel/laravel {site-directory}
```

Note: If you are doing this on a dev server where the directory group defaults to your ID, then you may need to change the group so that Apache2 can write to the log files in the folder.

```
sudo chgrp -R www-data /var/www/site.local
sudo find /var/www/site.local -type d -exec chmod g+rx {​​​​​​​}​​​​​​​ +
sudo find /var/www/site.local -type f -exec chmod g+r {​​​​​​​}​​​​​​​ +
```