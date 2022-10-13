## Configuración del agente en una máquina virtual distinta al server de glpi

#### Descargar el fichero de instalación .perl

```shell
wget https://github.com/glpi-project/glpi-agent/releases/download/1.4/glpi-agent-1.4-linux-installer.pl
```

#### Ver las opciones de instalación disponibles

```shell
perl glpi-agent-1.4-linux-installer.pl --help
```

#### Lanzar la instalación con las opciones elegidas

```shell
perl glpi-agent-1.4-linux-installer.pl -s http://192.168.46.214/marketplace/glpiinventory/ --type=all --service --install
```


