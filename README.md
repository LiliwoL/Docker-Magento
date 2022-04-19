<p align="center">
    <img src="https://static.magento.com/sites/all/themes/magento/logo.svg" width="300px" alt="Magento Commerce" />
</p>

#  Magento 2 Docker

### Contenu

- Magento 2.4
- Apache
- PHP 7.4
- Xdebug 2.9.8
- MariaDB 10.4.13
- Elasticsearch 7.6
- Varnish 6.4
- Redis
- MailHog
- n98-magerun


### Avant de commencer

ElasticSearch DOIT disposer de 262144 de mémoire.

Vérifier sur la machine hôte:

```bash
more /proc/sys/vm/max_map_count
```

Pour définir de manière permanente, ouvrez le fichier `/etc/sysctl.conf` et ajoutez à la fin:

```
vm.max_map_count=262144
```

Enregistrez, puis activez la nouvelle configuration en tapant sur la machine hôte:

```bash
sudo sysctl -p
```

***


### Lancer les conteneurs


Lancer avec la commande

```bash
bin/start
```

ou

```bash
docker-compose up
```

### Installation de Magento 2

Connectez vous en terminal au container apache avec

```bash
bin/shell
install-magento2
```

Il faudra spécifier les identifiants du repo.magento.com pour pouvoir télécharger les sources.
L'installation prend du temps.
Il faut confirmer la confiance dans de nombreuses dépendances composer.


A la fin, on doit avoir:
** Magento was installer: Yes.**

## Setup de Magento

Tous les fichiers doivent appartenir à l'utlisateur **www-data**:

```bash
chown -R www-data:www-data .
```


A exécuter dans le container apache:

```bash
bin/shell
```

ou utilisez le script `bin/shell`

```bash
bin/magento setup:install --db-host=db --db-name=magento --db-user=admin --db-password=admin123  --base-url=http://localhost/  --backend-frontname=system  --admin-firstname=Administrateur  --admin-lastname=Magento  --admin-email=formation@liliwol.fr  --admin-user=administrateur  --admin-password=magento2022  --language=fr_FR  --currency=EUR  --timezone=Europe/Paris   --use-rewrites=1  --search-engine=elasticsearch7  --elasticsearch-host=elasticsearch  --elasticsearch-port=9200  --elasticsearch-index-prefix=magento
```



### Serveurs

**Web server:** http://localhost/

**Local emails:** http://localhost:8025

### Features commands

| Commands  | Description  | Options & Examples |
|---|---|---|
| `bin/init`  | If you didn't use the CURL setup command above, please use this command changing the name of the project.  | `./init MYMAGENTO2` |
| `bin/start`  | If you continuing not using the CURL you can start your container manually  | |
| `bin/stop`  | Stop your project containers  | |
| `bin/kill`  | Stops containers and removes containers, networks, volumes, and images created to the specific project  | |
| `bin/shell`  | Access your container  | `./shell root` | |
| `bin/magento`  | Use the power of the Magento CLI  | |
| `bin/magento-basic`  | All basic Magento CLI commands (setup:upgrade, setup:di:compile, setup:static-content:deploy -f, cache:clean, cache:flush)  | |
| `bin/n98`  | Use the Magerun commands as you want | |
| `bin/grunt-init`  | Prepare to use Grunt  | |
| `bin/grunt`  | Use Grunt specifically in your theme or completely, it'll do the deploy and the watcher.  | `./grunt luma` |
| `bin/xdebug`  |  Enable / Disable the XDebug | |
| `bin/composer`  |  Use Composer commands | `./composer update` |
