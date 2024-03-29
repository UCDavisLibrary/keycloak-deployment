# Keyloak Deployment

[Keycloak](https://www.keycloak.org/) is the Identity and Access Management system used by the UC Davis Library. It primarily acts as an identity broker for the UC Davis Central Authentication System (CAS).

After making any changes, you can deploy by following these steps:
1. Check `config.sh` to ensure that everything looks good. 
2. Run `./cmds/generate-deployment-files.sh`.
3. Check changes into github and tag the release.
4. ```ssh auth.library.ucdavis.edu```
5. `cd /opt` and then into the version you are deploying - currently `prod` or `sandbox`.
6. git pull either the tag or branch you need.
7. `docker compose pull`
8. If you made changes to the apache config, move it. `mv apache/keycloak.conf /etc/httpd/conf.d/prod.conf`
9. Verify that your env file is good.
10. `docker compose up -d`

## Env

| Variable | Description | Required? |
| -------- | ----------- | --------- |
| KC_DB_USERNAME | PG user | Y |
| KC_DB_PASSWORD | PG password | Y |
| POSTGRES_PASSWORD | Same as above | Y |
| KEYCLOAK_ADMIN | Creates KC admin user on start | Only use if setting up KC for first time |
| KEYCLOAK_ADMIN_PASSWORD | KC admin user password created on start | Only use if setting up KC for first time |

