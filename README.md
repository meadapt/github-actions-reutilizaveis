# GitHub Actions Reutilizáveis

Conjunto de fluxos de trabalho ou GitHub Actions reutilizáveis, conforme proposto nos seguintes vídeos do YouTube:

- [GitHub Actions Reusable Workflows FULL TUTORIAL with Examples: Templates on Steroids](https://www.youtube.com/watch?v=lRypYtmbKMs).
- [GitHub Actions - Calling Reusable Workflows](https://www.youtube.com/watch?v=2dxmvDL1gP8).

Quando um novo Github Actions reutilizável é criado, sua documentação deve ser adicionada abaixo, devendo as informações confidenciais (secrets) serem bem projetadas para evitar o erro ["invalid secret, is not defined in the referenced workflow"](https://github.com/orgs/community/discussions/26749).
A documentação incluída abaixo sempre sugerirá a utilização da versão mais atual do Github Actions reutilizável na propriedade `uses` do `job` `do-it`.
Para utilização de versões anteriores basta incluir a versão desejada após o `@`, na propriedade `uses` do `job` `do-it`.
Todas as versões disponíveis podem ser consultadas nas [tags](https://github.com/o-futuro-ja-comecou/github-actions-reutilizaveis/tags) do repositório.

## Atualização de versões

- Atualização da documentação (principalmente versão) no arquivo `READEME.md`.
- Atualização arquivo `CHANGELOG.md` com um resumo das modificações da versão.
- Realiza um commit com o número da nova versão. Exemplo: `git commit -m 'v1.0'`.
- Criação de tag e vinculação da mesma com o último commit:

```
# Exemplo
$ git tag v1.0 HEAD
```

- Push tag para repo online:

```
# Exemplo
$ git push origin v1.0
```

## Adicionar projeto em um novo issue

[Este GitHub Actions reutilizável](https://github.com/o-futuro-ja-comecou/github-actions-reutilizaveis/blob/main/.github/workflows/reusable/add_project_to_issue.yml) foi criado para automatizar o processo de vinculação [de um projeto a um novo issue](https://github.com/actions/add-to-project).

As seguintes configurações devem ser feitas no repositório que irá utilizar este processo:

- GitHub secrets:
  - GH_TOKEN, conforme explicado [aqui](https://github.com/actions/add-to-project#inputs).
  - ACCOUNT_TYPE: `users` ou `orgs`.
  - ACCOUNT: usuário ou organização.
  - PROJECT_NUMBER: número GitHub Project.
- Crie o arquivo `.github/workflow/add_project_to_issue.yml` com o seguinte conteúdo:

```
# This uses a reusable workflow
name: Reusable Workflow to add a project to issues

on:
  issues:
    types: [opened]

jobs:
  do-it:
    uses: o-futuro-ja-comecou/github-actions-reutilizaveis/.github/workflows/add_project_to_issue_reusable.yml@v1.0
    secrets:
        GH_TOKEN: ${{ secrets.GH_TOKEN }}
        ACCOUNT_TYPE: ${{ secrets.ACCOUNT_TYPE }}
        ACCOUNT: ${{ secrets.ACCOUNT }}
        PROJECT_NUMBER: ${{ secrets.PROJECT_NUMBER }}
```
