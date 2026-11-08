# Dépôt APT d'Artysan

Ce dépôt sert le paquet `artysan-server` aux serveurs Debian 13 x86-64, par GitHub Pages.
La release d'[Artysan](https://github.com/acolyte-labs/artysan) le réécrit à chaque version : n'y poussez rien à la main.

## Ajouter la source

```bash
sudo install -d -m 0755 /etc/apt/keyrings
sudo curl -fsSLo /etc/apt/keyrings/artysan-archive-keyring.asc https://acolyte-labs.github.io/artysan-apt/artysan-archive-keyring.asc
gpg --show-keys --with-fingerprint /etc/apt/keyrings/artysan-archive-keyring.asc
```

Comparez l'empreinte affichée avec celle-ci, puis continuez seulement si elles sont identiques :

```text
155F 1872 9673 E7E0 4BD0  1C51 72AA 4B70 A60B 1944
```

```bash
sudo curl -fsSLo /etc/apt/sources.list.d/artysan.sources https://acolyte-labs.github.io/artysan-apt/artysan.sources
sudo apt update
sudo apt install artysan-server
```

Sans `/etc/artysan/artysan.env`, le paquet affiche la commande qui termine l'installation :

```bash
sudo artysan install --domain <nom> --acme-email <adresse>
```

## Sortir d'une installation en échec

Avec `/etc/artysan/artysan.env` et PostgreSQL 18 déjà installé, chaque `apt install` et `apt upgrade` relance `artysan install`.
Quand cette installation échoue, par exemple sur un volume de données non monté, dpkg laisse `artysan-server` à moitié configuré.
Corrigez le prérequis signalé, puis terminez la configuration :

```bash
sudo dpkg --configure -a
```
