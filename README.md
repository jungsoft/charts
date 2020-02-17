# Helm Charts

* Create chart package

```bash
helm package charts/traefik --destination .deploy
```

* Create new release and upload package

```bash
cr upload -o jungsoft -r charts -p .deploy --token $CH_TOKEN
```

* Update `index.yaml`

```bash
cr index -i ./index.yaml -o jungsoft -r charts -p .deploy --token $CH_TOKEN -c https://jungsoft.github.io/charts/
```

* Commit `index.yaml` to `gh-pages` branch

```bash
git add index.yaml
git commit -m "Release Traefik v2.0.1"
git push origin gh-pages
```

* Add `jungsoft` to your repositories:

```bash
helm repo add jungsoft https://jungsoft.github.io/charts/
```

* Install an application:

```bash
helm install jungsoft/traefik --version 2.0.1
```
