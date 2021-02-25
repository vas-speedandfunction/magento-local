# Magento local setup

## Setup DDEV

https://www.ddev.com/get-started/

We need more memory then default.
Docker Desktop for Mac has a number of settings that you'll want to pay attention to. Under "Advanced" in the "Resources" section in "Preferences", you can adjust the amount of memory, disk, and CPUs allocated to Docker. While the defaults work well for a small project or two, you may want to adjust these upward based on your experience. The default memory allocation is 2GB, but many people raise it to 4-5GB or even higher. 
see https://github.com/vas-speedandfunction/magento-local/blob/main/Settings%2B2021-02-24%2B22-20-27.png

## DDEV for Magento

For the reference: https://ddev.readthedocs.io/en/stable/users/cli-usage/#magento-2-quickstart

```
mkdir magento2 && cd magento2
ddev config --project-type=magento2 --docroot=pub --create-docroot
```
Attention! Copy docker-compose.elasticsearch.yaml to local .ddev directory.

fix in .ddev/config.yaml

```
php_version: "7.4"

router_http_port: "8000"
router_https_port: "8443"
```

Please do ```ddev poweroff``` and then ```ddev start```.

Attention! Get Developer Access Keys: https://devdocs.magento.com/guides/v2.3/install-gde/prereq/connect-auth.html

## Setup Magento with Composer

The most resent version:
```
ddev composer create --repository=https://repo.magento.com/ magento/project-community-edition -vvv
```
The version without elastic search:
```
ddev composer create --repository=https://repo.magento.com/ magento/project-community-edition=2.3.6 -vvv
```
but there we need 
```
php_version: "7.3"
```
Also, we need to turn off all stuff like browsers, messagers and so on,
because it can cause 
```
Failed to create project:exit status 137, stderr=
```
Due to the lack of physical memory. 

```
Authentication required (repo.magento.com):
      Username: [Your Public Key]
      Password: [Your Private Key]
```

## Setup Magento

```
$ bin/magento setup:install --base-url=https://magento2.ddev.site:8443/ --db-host=db --db-name=db --db-user=db --db-password=db --admin-firstname=Magento --admin-lastname=User --admin-email=test@test.com --admin-user=admin --admin-password=admin123 --language=en_US
```
Make some commands inside docket shell:

```
$ bin/magento deploy:mode:set developer
$ bin/magento module:disable Magento_TwoFactorAuth
$ bin/magento cache:flush
```
or the same outside:
```
$ ddev magento deploy:mode:set developer
$ ddev magento module:disable Magento_TwoFactorAuth
$ ddev magento cache:flush
```

If you need Magento 2 Sample Data (https://devdocs.magento.com/guides/v2.4/install-gde/install/sample-data-after-composer.html):

```
$ bin/magento sampledata:deploy
$ bin/magento setup:upgrade
```

