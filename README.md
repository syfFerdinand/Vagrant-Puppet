# Projet Vagrant – Environnement Web & Base de Données

Ce projet fournit un **environnement de développement local** basé sur **Vagrant** et **VirtualBox**, comprenant deux machines virtuelles distinctes :

* 🖥️ **web** : serveur web Apache provisionné via Shell
* 🗄️ **db** : serveur base de données provisionné via **Puppet**

L’objectif est de disposer rapidement d’une infrastructure reproductible pour le développement et les tests.

---

## 📋 Prérequis

Avant de commencer, assure-toi d’avoir installé :

* [Vagrant](https://www.vagrantup.com/) ≥ 2.x
* [VirtualBox](https://www.virtualbox.org/)
* Un accès Internet (pour le provisionnement des paquets)

Vérification :

```bash
vagrant --version
virtualbox --version
```

---

## 📁 Structure du projet

```text
.
├── Vagrantfile
├── puppet/
│   ├── manifests/
│   │   └── default.pp
│   ├── modules/
│   └── hiera.yaml
└── README.md
```

---

## ⚙️ Configuration des machines

### 🖥️ Machine `web`

* **OS** : Ubuntu 14.04 (trusty64)
* **Hostname** : `web.vagrant.vm`
* **Provisionnement** : Shell
* **Services installés** :

  * Apache2

Provisionnement exécuté :

* `apt-get update`
* `apt-get install apache2`

---

### 🗄️ Machine `db`

* **OS** : Ubuntu 14.04 (trusty64)
* **Hostname** : `db.vagrant.vm`
* **Provisionnement** : Puppet

Configuration Puppet :

* `manifests_path` : `puppet/manifests`
* `manifest_file` : `default.pp`
* `module_path` : `puppet/modules`
* `hiera_config_path` : `puppet/hiera.yaml`

👉 Le fichier `default.pp` définit les ressources Puppet nécessaires à la configuration de la base de données.

---

## 🚀 Démarrage du projet

### Lancer toutes les machines

```bash
vagrant up
```

### Lancer une machine spécifique

```bash
vagrant up web
vagrant up db
```

---

## 🔑 Accès aux machines

```bash
vagrant ssh web
vagrant ssh db
```

### Tester Apache (machine web)

Depuis l’hôte :

```bash
curl http://localhost
```

Ou depuis la VM :

```bash
curl http://localhost
```

---

## 🛠️ Commandes utiles

| Commande            | Description                |
| ------------------- | -------------------------- |
| `vagrant status`    | État des machines          |
| `vagrant provision` | Rejouer le provisionnement |
| `vagrant halt`      | Arrêter les VM             |
| `vagrant destroy`   | Supprimer les VM           |

---
