# GitHub Actions Reutilizáveis

[![actions-cool](https://img.shields.io/badge/using-actions--cool-blue?style=flat-square)](https://github.com/actions-cool)

Conjunto de fluxos de trabalho ou GitHub Actions reutilizáveis, conforme proposto nos seguintes vídeos do YouTube:

- [GitHub Actions Reusable Workflows FULL TUTORIAL with Examples: Templates on Steroids](https://www.youtube.com/watch?v=lRypYtmbKMs).
- [GitHub Actions - Calling Reusable Workflows](https://www.youtube.com/watch?v=2dxmvDL1gP8).

Quando um novo Github Actions reutilizável é criado, sua documentação deve ser adicionada abaixo, devendo as informações confidenciais (secrets) serem bem projetadas para evitar o erro ["invalid secret, is not defined in the referenced workflow"](https://github.com/orgs/community/discussions/26749).

A documentação incluída abaixo utiliza `@RELEASE_VERSION`. Para configurar a versão desejada basta incluir a mesma no lugar de `@RELEASE_VERSION` ou `@main` para utilizar a versão ainda não instável. **A versão mais atualizada publicada é a [v2.5](https://github.com/meadapt/github-actions-reutilizaveis/tree/v2.5)**. Todas as versões disponíveis podem ser consultadas nas [tags](https://github.com/meadapt/github-actions-reutilizaveis/tags) do repositório.

## Atualização de versões

- Atualização da documentação (principalmente versão) no arquivo `README.md`.
- Atualização arquivo `CHANGELOG.md` com um resumo das modificações da versão.
- Realiza um commit com o número da nova versão. Exemplo: `git commit -m 'v1.0' --allow-empty`[^1].
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

- Publicar uma nova [release](https://github.com/meadapt/github-actions-reutilizaveis/releases/new).

## Adicionar projeto em um novo issue

[Este GitHub Actions reutilizável](https://github.com/meadapt/github-actions-reutilizaveis/blob/main/.github/workflows/add_project_to_issue.yml) foi criado para automatizar o processo de vinculação [de um projeto a um novo issue](https://github.com/actions/add-to-project).

As seguintes configurações devem ser feitas no repositório que irá utilizar este processo:

- GitHub secrets:
  - GH_TOKEN, conforme explicado [aqui](https://github.com/actions/add-to-project#inputs).
  - PROJECT_NUMBER: número GitHub Project.
- Crie o arquivo `.github/workflows/add_project_to_issue.yml` com o seguinte conteúdo:

```
# This uses a reusable workflow
name: Add project to issue

on:
  issues:
    types: [opened]

jobs:
  add_project_to_issue:
    uses: meadapt/github-actions-reutilizaveis/.github/workflows/add_project_to_issue_reusable.yml@RELEASE_VERSION
    secrets:
        GH_TOKEN: ${{ secrets.GH_TOKEN }}
        PROJECT_NUMBER: ${{ secrets.PROJECT_NUMBER }}
```

## Adicionar closet at em issues fechados

[Este fluxo de trabalho reutilizável](https://github.com/meadapt/github-actions-reutilizaveis/blob/main/.github/workflows/set_closet_at_to_closed_issue_reusable.yml) foi criado para automatizar o processo de adicionar closet at em issues que foram fechados.

As seguintes configurações devem ser feitas no repositório que irá utilizar este processo:

- GitHub secrets:
  - GH_TOKEN, conforme explicado [aqui](https://github.com/actions/add-to-project#inputs).
  - PROJECT_NUMBER: número GitHub Project.
- Crie o arquivo `.github/workflows/set_closet_at_to_closed_issue.yml` com o seguinte conteúdo:

```
# This uses a reusable workflow
name: Set closet at to closed issue

on:
  issues:
    types: [closed]

jobs:
  set_closet_at_to_closed_issue:
    uses: meadapt/github-actions-reutilizaveis/.github/workflows/set_closet_at_to_closed_issue_reusable.yml@RELEASE_VERSION
    secrets:
        GH_TOKEN: ${{ secrets.GH_TOKEN }}
        PROJECT_NUMBER: ${{ secrets.PROJECT_NUMBER }}
```

## Adicionar assignee em issues fechados

[Este fluxo de trabalho reutilizável](https://github.com/meadapt/github-actions-reutilizaveis/blob/main/.github/workflows/add_assignee_to_closed_issue_reusable.yml) foi criado para automatizar o processo de informar assignee em issues que foram fechados.

As seguintes configurações devem ser feitas no repositório que irá utilizar este processo:

- GitHub secrets:
  - GH_TOKEN, conforme explicado [aqui](https://github.com/actions/add-to-project#inputs).
- Crie o arquivo `.github/workflows/add_assignee_to_closed_issue_reusable.yml` com o seguinte conteúdo:

```
# This uses a reusable workflow
name: Add assignee to closed issue

on:
  issues:
    types: [closed]

jobs:
  add_assignee_to_closed_issue:
    uses: meadapt/github-actions-reutilizaveis/.github/workflows/add_assignee_to_closed_issue_reusable.yml@RELEASE_VERSION
    secrets:
        GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

## Publica Mkdocs com Mike

[Este fluxo de trabalho reutilizável](https://github.com/meadapt/github-actions-reutilizaveis/blob/main/.github/workflows/publish_mkdocs_with_mike_version_reusable.yml) foi criado para automatizar o processo de publicação de sites estáticos utilizando Mkdocs e Mike e GitHub pages.

As seguintes configurações devem ser feitas no repositório que irá utilizar este processo:

- Crie o arquivo `.github/workflows/publish_mkdocs_with_mike_version.yml` com o seguinte conteúdo:
    - Não esqueça de incluir o número da versão (`my_doc_version` entre aspas) que se deseja publicar a documentação.

```
# This uses a reusable workflow
name: Publish mkdocs with mike version reusable

on:
  push:
    branches:
      - main
    paths:
      - 'docs/**'

jobs:
  publish_mkdocs_with_mike_version:
    uses: meadapt/github-actions-reutilizaveis/.github/workflows/publish_mkdocs_with_mike_version_reusable.yml@RELEASE_VERSION
    with:
      doc_version: 'my_doc_version'
```

## Referências

- [Issues helper](https://github.com/marketplace/actions/issues-helper).
- [Add to project](https://github.com/actions/add-to-project).

[^1]: Caso seja necessário apagar uma tag criada erroneamente utilizar `git tag -d <tag-name>` (localmente) e/ou `git push --delete origin <tag-name>` (GitHub), como sugerido [neste post](https://devconnected.com/how-to-delete-local-and-remote-tags-on-git/#:~:text=tag%20%2Dd%20%3Ctag_name%3E-,For%20example,-%2C%20if%20you%20wanted). Processo bastante similar ao delete de um branch (`git branch -d <branch-name>` ou `git branch -D <branch-name>` para branchs não mergiados na `main`.)
