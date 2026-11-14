# Forgejo on Tinkr

[Forgejo](https://forgejo.org) (self-hosted Git forge) with PostgreSQL, packaged for Tinkr.

## Install

Install **Forgejo** from the Tinkr catalog, or add this repository as an app.
Forgejo is served over HTTPS at the hostname Tinkr assigns; `ROOT_URL` and
`DOMAIN` are set from it automatically.

## First login

The setup wizard is skipped (`INSTALL_LOCK=true`). **The first account registered
becomes the site administrator** — open the app and register right after install.

Then, if the instance should not be open to sign-ups, set the secret
`FORGEJO__service__DISABLE_REGISTRATION` to `true` and restart the app.

## Database password

The database password defaults to `forgejo`. The database is private to the app
(never exposed outside its namespace). To change it before the first install,
add two secrets with the same value:

- `POSTGRES_PASSWORD`
- `FORGEJO__database__PASSWD`

## Git access

Clone and push over HTTPS. SSH is disabled.

## Configuration

Any Forgejo setting can be added as a secret named `FORGEJO__<section>__<KEY>`,
e.g. `FORGEJO__mailer__ENABLED=true`. See the
[configuration cheat sheet](https://forgejo.org/docs/latest/admin/config-cheat-sheet/).

## Data

| Volume | Contents |
|--------|----------|
| `forgejo_data` | Repositories, attachments, `app.ini`, generated secrets |
| `db_data` | PostgreSQL data |

Both are kept when the app is destroyed.

## Run locally

```
docker compose up
```

Then open http://localhost:3000.
