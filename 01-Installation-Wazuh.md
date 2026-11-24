# Installation Wazuh

Nous allons installer Wazuh (Indexer/Server/Dashboard) sur notre machine, pour cela nous allons utiliser une machine virtuel avec 16Go de ram 4vCPU et 100 Go de Stockage.

![Capture Spec](img/Capture%20d'écran_20261124_112402.png)

Nous allons utiliser Debian 13 pour le serveur.

## Installation de Wazuh Indexer

Dans un premier temps, nous allons généré les fichiers pour l'installation de Wazuh sur notre machine maitre

```
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
curl -sO https://packages.wazuh.com/4.14/config.yml
```

![Capture téléchargement Wazuh creation config](img/Capture%20d'écran_20261124_122730.png)

Modifier le fichier config.yml en remplacant avec vos adresse IP

![Capture config.yml](img/Capture%20d'écran_20261124_123055.png)

Vous pouvez maintenant généré tout les fichiers que nous aurons besoin pour installer Wazuh dans notre infra automatiquement grace a la commande :

```
bash wazuh-install.sh --generate-config-files
```

![Capture Generation fichier .tar](img/Capture%20d'écran_20261124_123301.png)

Vous pouvez maintenant transféré en SFTP le fichier .tar et le fichier .sh sur votre serveur Wazuh

![Caputre Présence fichier sur le srv](img/Capture%20d'écran_20261124_123935.png)

Nous pouvons maintenant lancer l'installation, node-1 est le nom de mon node

```
bash wazuh-install.sh --wazuh-indexer node-1
```

![](img/Capture%20d'écran_20261124_124421.png)

Et voila l'Indexer est bien installé

On peut maintenant démarré l'Indexer

```
bash wazuh-install.sh --start-cluster
```

![](img/Capture%20d'écran_20261124_140936.png)

Vous pouvez récuper vos identifiant via la commande

```
tar -axf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt -O | grep -P "\'admin\'" -A 1
```

Vous pouvez tester si votre indexeur fonctionne en tentant de le joindre (vous aurez besoin de votre mot de passe admin)

```
curl -k -u admin https://<WAZUH_INDEXER_IP_ADDRESS>:9200
curl -k -u admin https://<WAZUH_INDEXER_IP_ADDRESS>:9200/_cat/nodes?v
```

![](img/Capture%20d'écran_20261124_142306.png)

![](img/Capture%20d'écran_20261124_142703.png)

## Installation Wazuh Server

Vous avez simplement à executer la commande

```
bash wazuh-install.sh --wazuh-server wazuh-1
```

![](img/Capture%20d'écran_20261124_143311.png)

## Installation Wazuh Dashboard