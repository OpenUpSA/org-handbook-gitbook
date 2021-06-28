# Hosting on dokku

Multiple apps are deployed to each [dokku](https://dokku.com/) server. Examples of our dokku servers are dokku9.code4sa.org and hetzner1.openup.org.za.

## Deploying new apps, app environments, and config changes

Add required secrets to the [secrets_store](https://github.com/OpenUpSA/secrets_store), for example:

```shell
pass git pull
pass generate --no-symbols apps/app-name/prod/DJANGO_SECRET_KEY 40
pass insert --multiline apps/app-name/prod/ANOTHER_SECRET

# Enter:

actual-secret
someKey: someValue
and: soOn
# Ctrl-D to save

pass git push
```

Maintain a playbook for the app at e.g. `apps/app-name/backend.yml` in [ansible-config](https://github.com/OpenUpSA/ansible-config). Secrets as added above can be accessed using e.g. `"{{ lookup('passwordstore', 'apps/app-name/{{ env_name }}/DJANGO_SECRET_KEY')}}"`, and deploy it:

```shell
pass git pull
export PASSWORD_STORE_DIR=~/.pass/openup

# Deploy environment for the first time:
ansible-playbook --inventory inventory/prod.yml apps/app-name/backend.yml # Check first using `--check --diff`

# Deploy app playbook changes:
ansible-playbook --inventory inventory/prod.yml apps/app-name/backend.yml --start-at-task "Dokku app exists" --tags app # Check first using `--check --diff`
```

## Deploying app code changes

We usually deploy app updates using the [`git push` approach ](http://dokku.viewdocs.io/dokku/deployment/application-deployment/)from a clone of the repository on our development machines, for example:

```shell
git remote add dokku dokku@hetzner1.openup.org.za:app-name
git push dokku master
```

## Managing URLs, domains, and TLS certificates

[Cloudflare](https://www.cloudflare.com) is used to manage DNS records. To have https://some-name.nice-domain.com resolve to the app `app-name` on dokku server `hetzner1.openup.org.za`, create a `CNAME` record `some-name` for nice-domain.com pointing to hetzner1.openup.org.za.

[dokku-letsencrypt](https://github.com/dokku/dokku-letsencrypt) is used to manage TLS certificates. To allow proper handshakes for the above, add the domain and generate the certificates:

```shell
ansible hetzner1.openup.org.za -a 'dokku domains:add app-name some-name.nice-domain.com'
ansible hetzner1.openup.org.za -a 'dokku letsencrypt app-name'
```
