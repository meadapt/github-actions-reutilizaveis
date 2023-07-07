# GitHub Actions Reutilizáveis

Conjunto de fluxos de trabalho ou GitHub Actions reutilizáveis, conforme proposto nos seguintes vídeos do YouTube:

- [GitHub Actions Reusable Workflows FULL TUTORIAL with Examples: Templates on Steroids](https://www.youtube.com/watch?v=lRypYtmbKMs).
- [GitHub Actions - Calling Reusable Workflows](https://www.youtube.com/watch?v=2dxmvDL1gP8).

Quando um novo Github Actions reutilizável é criado, sua documentação deve ser adicionada abaixo, devendo as informações confidenciais (secrets) serem bem projetadas para evitar o erro ["invalid secret, is not defined in the referenced workflow"](https://github.com/orgs/community/discussions/26749).

## Adicionar projeto em um novo issue

[Este GitHub Actions reutilizável](https://github.com/o-futuro-ja-comecou/github-actions-reutilizaveis/blob/main/.github/workflows/add_project_to_issue_reusable.yml) foi criado para automatizar o processo de vinculação [de um projeto a um novo issue](https://github.com/actions/add-to-project).

As seguintes configurações devem ser feitas no repositório que irá utilizar este processo:

- GitHub secrets:
  - GH_TOKEN, conforme explicado [aqui](https://github.com/actions/add-to-project#inputs).
  - USER;
  - TYPE - `users` ou `orgs`.
  - PROJECT_NUMBER.
- Crie o arquivo `.github/workflow/add_project_to_issue.yml` com o seguinte conteúdo:

```
# This uses a reusable workflow
name: Reusable Workflow to add a project to issues

on:
  issues:
    types: [opened]

jobs:
  do-it:
    uses: o-futuro-ja-comecou/github-actions-reutilizaveis/.github/workflows/add_project_to_issue_reusable.yml@main
    secrets:
        GH_TOKEN: ${{ secrets.GH_TOKEN }}
        USER: ${{ secrets.USER }}
        TYPE: ${{ secrets.TYPE }}
        PROJECT_NUMBER: ${{ secrets.PROJECT_NUMBER }}
```
