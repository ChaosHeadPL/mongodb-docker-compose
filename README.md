# MongoDB

## docker-compose

```yaml
version: "3"

services:
  mongo:
    image: mongo
    environment:
      - MONGO_INITDB_DATABASE=nabu
      - MONGODB_USERNAME=myuser
      - MONGODB_PASSWORD=mypass
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=admin
    ports:
      - "27017:27017"
    volumes:
      - ./mongo/data:/bitnami/mongodb/data
  express:
    image: mongo-express
    ports:
      - 8888:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=root
      - ME_CONFIG_MONGODB_ADMINPASSWORD=admin
      - ME_CONFIG_MONGODB_SERVER=mongo
      - ME_CONFIG_MONGODB_PORT=27017
      - ME_CONFIG_MONGODB_ENABLE_ADMIN=false
      - ME_CONFIG_MONGODB_AUTH_USERNAME=me_user
      - ME_CONFIG_MONGODB_AUTH_PASSWORD=me_pass
    depends_on:
      - mongo
    restart: always
```

---

### Run

```bash
docker compose up
```

---

### mongo

Image: https://hub.docker.com/_/mongo

Cretes user in the admin authentication database with root role:

- MONGO_INITDB_ROOT_USERNAME
- MONGO_INITDB_ROOT_PASSWORD

Crete db by cretion scripts in /docker-entrypoint-initdb.d/\*js

- MONGO_INITDB_DATABASE

---

### mongo-express

image: https://hub.docker.com/_/mongo-express

| Name                            | Default         | Description                                                                                                                  |
| ------------------------------- | --------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| ME_CONFIG_BASICAUTH_USERNAME    | ''              | mongo-express web username                                                                                                   |
| ME_CONFIG_BASICAUTH_PASSWORD    | ''              | mongo-express web password                                                                                                   |
| ME_CONFIG_MONGODB_ENABLE_ADMIN  | 'true'          | Enable admin access to all databases. Send strings: `"true"` or `"false"`                                                    |
| ME_CONFIG_MONGODB_ADMINUSERNAME | ''              | MongoDB admin username                                                                                                       |
| ME_CONFIG_MONGODB_ADMINPASSWORD | ''              | MongoDB admin password                                                                                                       |
| ME_CONFIG_MONGODB_PORT          | 27017           | MongoDB port                                                                                                                 |
| ME_CONFIG_MONGODB_SERVER        | 'mongo'         | MongoDB container name. Use comma delimited list of host names for replica sets.                                             |
| ME_CONFIG_OPTIONS_EDITORTHEME   | 'default'       | mongo-express editor color theme, [more here](http://codemirror.net/demo/theme.html)                                         |
| ME_CONFIG_REQUEST_SIZE          | '100kb'         | Maximum payload size. CRUD operations above this size will fail in [body-parser](https://www.npmjs.com/package/body-parser). |
| ME_CONFIG_SITE_BASEURL          | '/'             | Set the baseUrl to ease mounting at a subdirectory. Remember to include a leading and trailing slash.                        |
| ME_CONFIG_SITE_COOKIESECRET     | 'cookiesecret'  | String used by [cookie-parser middleware](https://www.npmjs.com/package/cookie-parser) to sign cookies.                      |
| ME_CONFIG_SITE_SESSIONSECRET    | 'sessionsecret' | String used to sign the session ID cookie by [express-session middleware](https://www.npmjs.com/package/express-session).    |
| ME_CONFIG_SITE_SSL_ENABLED      | 'false'         | Enable SSL.                                                                                                                  |
| ME_CONFIG_SITE_SSL_CRT_PATH     | ''              | SSL certificate file.                                                                                                        |
| ME_CONFIG_SITE_SSL_KEY_PATH     | ''              | SSL key file.                                                                                                                |

---

## Dockerfile

### Run:

```bash
docker run --name mongo bitnami/mongodb:latest
```
