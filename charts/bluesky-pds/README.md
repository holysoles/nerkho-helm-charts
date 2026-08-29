# bluesky-pds

A Helm chart to deploy a [Bluesky PDS](https://github.com/bluesky-social/pds) on Kubernetes.

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.4.5027](https://img.shields.io/badge/AppVersion-0.4.5027-informational?style=flat-square)

## Installing the Chart

See this [blog post](https://nerkho.ch/blog/self-hosted-pds-on-k8s/) for more details how to get the PDS running.

## Bluesky PDS configuration and account creation

Regarding configuration and account creation, refer to the [official PDS docs](https://github.com/bluesky-social/pds/blob/main/README.md).

### Generate invite code

```bash
export ADMINPW=your-admin-pw
export PDS_HOSTNAME=pds.example.com
curl --silent --show-error --request POST --header "Content-Type: application/json" "$@" \
    --user "admin:${ADMINPW}" \
    --data '{"useCount": 1}' \
    "https://pds.example.com/xrpc/com.atproto.server.createInviteCode" | jq --raw-output '.code'
```

### Create account

* Create the json input

```json
{
  "email": "user@example.com",
  "handle": "user.pds.example.com",
  "password": "my-password",
  "inviteCode": "invite-code"
}

```

* Create the account

```bash
curl --silent --show-error --request POST --header "Content-Type: application/json" -d @data.json "https://${PDS_HOSTNAME}/xrpc/com.atproto.server.createAccount"
```

Once this is done, you should be able to login on https://bsky.app/ using your PDS.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/bluesky-social/pds"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `""` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"pds.example.com"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"Prefix"` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.httpGet.path | string | `"/xrpc/_health"` |  |
| livenessProbe.httpGet.port | string | `"pds-port"` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| pds.config.blobstoreLocation | string | `"/pds/blocks"` |  |
| pds.config.bskyAppViewDid | string | `"did:web:api.bsky.app"` |  |
| pds.config.bskyAppViewUrl | string | `"https://api.bsky.app"` |  |
| pds.config.crawlers | string | `"https://bsky.network"` |  |
| pds.config.dataDir | string | `"/pds"` |  |
| pds.config.didPlcUrl | string | `"https://plc.directory"` |  |
| pds.config.hostname | string | `"pds.example.com"` | The public hostname of your PDS |
| pds.config.pdsEmailFromAddress | string | `""` | From address for emails sent |
| pds.config.reportSvcDid | string | `"did:plc:ar7c4by46qjdydhdevvrndac"` |  |
| pds.config.reportSvcUrl | string | `"https://mod.bsky.app"` |  |
| pds.config.secrets.adminPassword | string | `""` |  |
| pds.config.secrets.emailSmtpUrl | string | `""` | Example: `smtps://user:password@smtp.example.com:465/` |
| pds.config.secrets.jwtSecret | string | `""` |  |
| pds.config.secrets.plcRotationKey | string | `""` |  |
| pds.dataStorage | object | `{"mountPath":"/pds","selector":null,"size":"10Gi","storageClass":null}` | Persistent storage settings |
| pds.dataStorage.mountPath | string | `"/pds"` | Where to mount the PVC. Make sure it matches pds.config.dataDir! |
| pds.dataStorage.selector | string | `nil` | Selector for persistent disk |
| pds.dataStorage.size | string | `"10Gi"` | How large of a PVC to make |
| pds.dataStorage.storageClass | string | `nil` | Storage class to use. Defaults to the cluster default. |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.port | int | `3000` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| tolerations | list | `[]` |  |

