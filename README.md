# Jellyfin Media Server (`jellyfin-app`)

Manifestos GitOps (ArgoCD + Kustomize) para o **Jellyfin Media Server** no cluster K3s (`h89-1` e `h89-2`) com armazenamento compartilhado OCFS2 (`/data/jellyfin-app/config`), mídia via OneDrive Rclone (`/onedrive-glaucio-media-root`) e exposição via Cloudflare Tunnel + Traefik (`https://media.glauciolabs.work`).

### Configuração SSO (Referência com variáveis de ambiente)

Plugin: `https://github.com/9p4/jellyfin-plugin-sso`

```bash
curl -v -X POST -H "Content-Type: application/json" -d '{
  "oidEndpoint": "https://login.microsoftonline.com/<TENANT_ID>/v2.0/.well-known/openid-configuration",
  "oidClientId": "<AZURE_CLIENT_ID>",
  "oidSecret": "<AZURE_CLIENT_SECRET>",
  "enabled": false,
  "doNotValidateEndpoints": true,
  "enableAuthorization": false,
  "enableAllFolders": true,
  "enabledFolders": [],
  "schemeOverride": "https"
}' "https://media.glauciolabs.work/sso/OID/Add/jellyfin-media-app?api_key=<JELLYFIN_API_KEY>"
```