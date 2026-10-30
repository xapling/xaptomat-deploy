# xaptomat-deploy

Wächter für das Ausrollen von [xapling/xaptomat](https://github.com/xapling/xaptomat) nach Azure.

## Regel

Ein Stand von `xaptomat` erreicht Azure nur, wenn er

1. über einen gemergten Pull Request nach `main` kam und
2. entweder von **Artur Kuksin** oder **Georg Dörgeloh** gemergt wurde (ihr Merge gilt als Freigabe)
   oder auf dem letzten Stand von einem der beiden freigegeben wurde – nicht von der Person, die ihn gestellt hat.

Direkte Pushes auf `main` in `xaptomat` landen zwar im Repo, werden aber nicht ausgerollt.

## Warum ein eigenes Repo

Im kostenlosen GitHub-Tarif lässt sich `main` in privaten Repos nicht schützen. Die Deploy-Identität in Azure (`gh-xaptomat-deploy`) vertraut deshalb nur Tokens aus [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) auf `main` dieses Repos (OIDC-Claim `job_workflow_ref`). Dieses Repo ist öffentlich, damit `main` kostenlos geschützt werden kann; es enthält keine Geheimnisse.

## Änderungen

Nur per Pull Request; mergen dürfen nur die in [`CODEOWNERS`](.github/CODEOWNERS) genannten Personen. Einrichtung der Azure-Seite: `scripts/bootstrap-deploy-identity.sh` in `xaptomat`.
