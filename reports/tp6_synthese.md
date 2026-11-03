# Orchestrateur ou integration continue ? (TP06)

| Critere | Prefect (orchestrateur) | GitHub Actions (CI) |
|---|---|---|
| Ce qui declenche l'execution | Planification cron ou Quick run depuis l'interface | Push Git ou lancement manuel avec workflow_dispatch |
| Ou s'execute le traitement | Sur notre poste, via serve ou un worker process | Sur un runner Linux heberge par GitHub |
| Qui surveille, et ou | Prefect affiche les etats des taches, les durees et les journaux dans son interface | GitHub Actions affiche les etapes et leurs journaux dans l'onglet Actions |
| Ce qui se passe en cas d'echec | Le workflow s'arrete ; la validation refusee empeche la notification ; la tache pipeline dispose de deux reessais | Le job passe au rouge ; les rapports disponibles sont conserves avec if: always() |
| Type de tache adapte | Pipelines recurrents, preparation de donnees et reentrainement | Verification automatique du pipeline et de la qualite a chaque modification |
| Ce qui est versionne dans Git | flow_mlops.py, planifier.py et prefect.yaml | .github/workflows/ci.yml, verifier_qualite.py et requirements-ci.txt |

## Conclusion (5 lignes)

Prefect permet de planifier et de surveiller notre pipeline de detection de fraude.
Le work pool et le worker separent l'orchestration de l'execution des traitements.
La regle de qualite bloque le workflow lorsque le F1 est inferieur a 0.82.
GitHub Actions verifie le pipeline a chaque push et a retrouve un etat reussi apres git revert.
L'orchestrateur et l'integration continue sont complementaires : aucun ne remplace l'autre.