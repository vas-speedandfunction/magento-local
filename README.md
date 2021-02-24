# Magento local setup

## Setup DDEV

https://www.ddev.com/get-started/

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

## Setup Magento with Composer

```
ddev composer create --repository=https://repo.magento.com/ magento/project-community-edition -vvv
```
