# DB

```bash
$ fly pg create
? Choose an app name (leave blank to generate one): mkh-hydra-demo
? Select Organization: Mohammad K. Hussain (personal)
? Select region: Mumbai, India (lhr)
? Select configuration: Development - Single node, 1x shared CPU, 256MB RAM, 1GB disk
? Scale single node pg to zero after one hour? Yes
Creating postgres cluster in organization personal
Creating app...
Setting secrets on app mkh-hydra-demo...
Provisioning 1 of 1 machines with image flyio/postgres-flex:17.2@sha256:f4301ae20d193ab3c3539eb9df9a8f8d3736dd331aeec1bfb2e34b539dc353c5
Waiting for machine to start...
Machine 6e822249be76e8 is created
==> Monitoring health checks
  Waiting for 6e822249be76e8 to become healthy (started, 3/3)

Postgres cluster mkh-hydra-demo created
  Username:    postgres
  Password:    ...
  Hostname:    mkh-hydra-demo.internal
  Flycast:     fdaa:a:1236:0:1::2
  Proxy port:  5432
  Postgres port:  5433
  Connection string: postgres://postgres:...@mkh-hydra-demo.flycast:5432

Save your credentials in a secure place -- you won't be able to see them again!

Connect to postgres
Any app within the Mohammad K. Hussain organization can connect to this Postgres using the above connection string

Now that you've set up Postgres, here's what you need to understand: https://fly.io/docs/postgres/getting-started/what-you-should-know/

$ fly config save 
? An existing configuration file has been found
Overwrite file '/Users/dylanjay/Projects/pretagovhydra/db/fly.toml' Yes
Wrote config file fly.toml
```
# api

```bash
$ cd api
# Need to setup api app first
$ fly launch
# Attach DB
$ fly pg attach mkh-hydra-demo -a mkh-hydra-demo-api --database-name=plone --database-user=plone
Checking for existing attachments
Registering attachment
Creating database
Creating user

Postgres cluster mkh-hydra-demo is now attached to mkh-hydra-demo-api
The following secret was added to mkh-hydra-demo-api:
  DATABASE_URL=postgres://plone:...@mkh-hydra-demo.flycast:5432/plone?sslmode=disable

$ fly secrets set RELSTORAGE_DSN="dbname='plone' user='plone' host='mkh-hydra-demo.flycast' password='...'"
$ fly launch

# Need to manually add VHM

```

# admin

```bash
$ cd admin
$ fly launch
```

# frontend

```bash
$ cd frontend
$ pnpm install
$ pnpm run dev --envName edit  # During development
$ pnpm run build --envName edit --preset netlify-static
$ netlify deploy  --prod
```

# hydraadmin

```bash
$ cd hydraadmin
$ fly launch
```



