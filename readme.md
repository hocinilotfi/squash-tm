# Squash-TM **docker-compose.yml** file 
- Creer un fichier docker-compose.yml et le mettre dans un dossier Squash-tm
- Dans ce dossier:

```sh
docker compose up -d
```

```yml
version: '3.7'
services:
  squash-tm-md:
    image: mariadb:10.6
    environment:
      MARIADB_ROOT_PASSWORD: squash
      MARIADB_USER: squash
      MARIADB_PASSWORD: squash
      MARIADB_DATABASE: squash
    ports:
      - "3308:3306"  # Port changé ici
    volumes:
      - "/var/lib/mysql-db:/var/lib/mysql"

  squash-tm:
    image: squashtest/squash-tm
    depends_on:
      - squash-tm-md
    environment:
      SQTM_DB_TYPE: mariadb
      SQTM_DB_USERNAME: squash
      SQTM_DB_PASSWORD: squash
      SQTM_DB_NAME: squash
      SQTM_DB_HOST: squash-tm-md
      SQTM_DB_PORT: 3306  # Reste 3306 car on se connecte au port interne du conteneur
    ports:
      - "8090:8080"
    volumes:
      - squash-tm-logs:/opt/squash-tm/logs
      - squash-tm-plugins:/opt/squash-tm/plugins

volumes:
  squash-tm-logs:
  squash-tm-plugins:
```

## Cridentials pour entrer dans squash-tm
- **Endpoint**: localhost:8090/squash
- **Username**: squash
- **Password**: squash
