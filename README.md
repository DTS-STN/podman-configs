# Podman configs

`podman-configs` is a repository containing podman kube manifests
for deploying various applications and services locally.

See: <https://docs.podman.io/en/latest/markdown/podman-kube.1.html>

## Usage

``` shell
podman play kube --replace application.yaml
```

## JWT mock authentication

[mock-oauth2-server.yaml](mock-oauth2-server.yaml) runs
[NAV's mock OAuth2 server](https://github.com/navikt/mock-oauth2-server) with signed
JWT access tokens and passwordless login. **Local development only.**

```shell
podman play kube --replace mock-oauth2-server.yaml
```

| Setting | Value |
|---------|-------|
| Authority / issuer | `http://localhost:9400/default` |
| Discovery | `http://localhost:9400/default/.well-known/openid-configuration` |
| Debugger | `http://localhost:9400/default/debugger` |
| Client ID | `mock-oidc` (or your application's client ID) |
| Scopes | `openid profile email offline_access` |

Use the authorization-code flow with PKCE. No client registration or secret is
required. Allow HTTP metadata for local development. Tokens expire after one
hour; `offline_access` requests refresh tokens. Predefined accounts use the
client ID as their access-token audience.

Choose an account on the login page:

| Username | Roles |
|----------|-------|
| `mock-administrator` | Administrator |
| `mock-editor` | Editor |
| `mock-manager` | Manager |
| `mock-noaccess` | NoAccess |
| `mock-viewer` | Viewer |
