# BP-traefik-keycloak

Ce projet permet de déployer une instance Keycloak en utilisant Docker Compose.

## Description

 Il inclut les fonctionnalités suivantes :

- Utilisation de PostgreSQL avec persistance des données.
- Configuration des mots de passe root et utilisateur via des fichiers de secrets.
- Traefik est utilisé comme proxy pour fournir une connexion sécurisée (HTTPS) avec des certificats TLS via Let's Encrypt.


## Prérequis

Assurez-vous d'avoir les éléments suivants installés sur votre machine avant de commencer :

- Docker
- Docker Compose
- [Le projet BP-traefik-v3-ssl-ovh-api](https://github.com/lgrdev/BP-traefik-v3-ssl-ovh-api)
- [Le projet BP-traefik-postgresql](https://github.com/lgrdev/BP-traefik-postgresql)


## Structure du projet

```
.
├── docker-compose.yaml
├── keycloak/
│   └── import      # répertoire poir importer des configutaions keycloak
└── .env.sample
```

## Installation

### 1. Créer le fichier .env par copie du fichier .env.sample

```bash
cp .env.sample .env
```

### 2. Configurer l'environnement

Modifiez le fichier `.env` à la racine du projet avec les variables nécessaires :

```env
# URL site: https://keycloak.example.com
URL_KEYCLOAK=https://keycloak.example.com

# nous utilisons traefik, donc pas de hostname
KC_HOSTNAME=

# administrateur et son mot de passe
KEYCLOAK_ADMIN=admin
KEYCLOAK_ADMIN_PASSWORD=MonPassWordAdmin

# base de données postgres
KC_DB=postgres

# base keycloak, créee par le docker-compose, n utilisant le service diocker : postgresql
KC_DB_URL=jdbc:postgresql://postgres:5432/keycloak
KC_DB_USERNAME=
KC_DB_PASSWORD=
```

### 3. Lancer le service

Une fois les secrets créés et les variables d'environnement configurées, vous pouvez lancer le service MariaDB avec Docker Compose :

```bash
docker-compose up -d
```

## Configuration de Traefik

Le fichier `docker-compose.yaml` inclut des labels pour Traefik afin de sécuriser les connexions à keycloak avec HTTPS. Traefik obtient automatiquement des certificats SSL/TLS via Let's Encrypt.

## Fichiers importants

- **`docker-compose.yaml`** : Définit le service MariaDB, sa persistance, les secrets et les labels Traefik.
- **`.env`** : Contient les variables d'environnement pour MariaDB et Traefik.

## Contributions

Les contributions sont les bienvenues ! Si vous trouvez des problèmes ou souhaitez ajouter des fonctionnalités, n'hésitez pas à ouvrir une issue ou une pull request.

## License

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

