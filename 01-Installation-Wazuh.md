# Installation Wazuh

Nous allons installer Wazuh (Indexer/Server/Dashboard) sur notre machine, pour cela nous allons utiliser une machine virtuel avec 16Go de ram 4vCPU et 100 Go de Stockage.

![Capture Spec](img/Capture%20d'écran_20261124_112402.png)

Nous allons utiliser Debian 13 pour le serveur.

## Installation de Wazuh Indexer

Dans un premier temps, nous allons généré les fichiers pour l'installation de Wazuh Indexer sur notre machine maitre

```
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
curl -sO https://packages.wazuh.com/4.14/config.yml
```


