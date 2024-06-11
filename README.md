# cloudflare-docker-proxy

![deploy](https://github.com/east4ming/cloudflare-docker-proxy/actions/workflows/deploy.yaml/badge.svg)

> If you're looking for proxy for helm, maybe you can try [cloudflare-helm-proxy](github.com/ciiiii/cloudflare-helm-proxy).

## Deploy
[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/zyywo/cloudflare-docker-proxy)

1. fork this project
2. modify the link of the above button to your fork url
3. click the button, you will be redirected to the deploy page

## Config tutorial

### OPTION 1: Use Cloudflare Worker Host

use cloudflare worker host: only support proxy one registry
```javascript
const routes = {
  "${workername}.${username}.workers.dev/": "https://registry-1.docker.io",
};
```

### OPTION 2: Use Custom Domain

use custom domain: support proxy multiple registries route by host

- host your domain DNS on cloudflare
- add more records and modify the config as you need
```javascript
const routes = {
  "docker.your-domain.com": "https://registry-1.docker.io",
  "quay.your-domain.com": "https://quay.io",
  "gcr.your-domain.com": "https://k8s.gcr.io",
  "k8s-gcr.your-domain.com": "https://k8s.gcr.io",
  "ghcr.your-domain.com": "https://ghcr.io",
};
```
- deploy this project to cloudflare workers
- add `CNAME` **DNS record** of xxx.your-domain.com to the workers.dev domain, like this: `${workername}.${username}.workers.dev`
- add `xxx.your-domain.com/*` to **HTTP routes of workers**. xxx is `docker` `quay` `gcr` ...


