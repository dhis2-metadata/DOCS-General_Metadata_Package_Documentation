# Package Publishing

## Table of Contents

1. [Introduction](#introduction)
2. [Process Overview](#process-overview)
3. [Preparing Package for Export](#preparing-package-for-export)
4. [Exporting Package to Github](#exporting-package-to-github)
5. [Setting Up Documentation Structure in Github](#setting-up-documentation-structure-in-github)
6. [Creating a Release](#creating-a-release-in-github)

## Introduction

This guide is aimed at core team implementers that are responsible for exporting and publishing DHIS2 metadata packages.

The process of publishing DHIS2 metadata packages requires:

1. Admin access to DHIS2 development instances
2. Collaborator access to [dhis2-metadata organisation](https://github.com/dhis2-metadata)
3. Access to [Jenkins metadata exporter](https://ci.dhis2.org/job/metadata-exporter) and [Jenkins metadata export triggerer](https://ci.dhis2.org/job/metadata-export-triggerer)
4. Access to [DHIS2 metadata package index spreadsheet](https://docs.google.com/spreadsheets/d/1IIQL2IkGJqiIWLr6Bgg7p9fE78AwQYhHBNGoV-spGOM/edit?usp=sharing)
5. Access to [DHIS2 S3](https://s3.console.aws.amazon.com/s3/home) - optional
6. Basic knowledge of markdown syntax. [Markdown support and extensions guide](https://docs.dhis2.org/en/implement/support-and-documentation/dhis2-documentation-guide.html?h=markdown#markdown_support_and_extensions) provides an overview of supported functionality. The structure of markdown documents is addressed in the [Markdown File Structure](#markdown-file-structure) section.

## Process Overview

``` mermaid
    %%{init: {'mirrorActors': false } }%%

    sequenceDiagram

        autonumber
        actor Implementer
        participant D as Package Development<br><br>Instance
        participant G as Github
        participant A as Amazon S3
        participant W as dhis2.org
        Implementer->>D: Configure package metadata
        note over Implementer: Update package overview spreadsheet
        note over Implementer: Follow package QA checklist

        note over G: Create/review the target repository<br>Add documentation to the master branch
        note over D: Apply required package coding to metadata
        D->>G: <br>1. Use Jenkins Metadata Exporter for single package export<br>2. Use Jenkins Metadata Exporter Triggerer for bulk export<br>3. Manually import package to github (optional, not recommended)
        G->>A: Create a package release
        note over A: Copy metadata reference file url and<br>add it to the overview.md file
        note over G: Merge pull request to generate index file<br>for the downloads page
        A->>W: New package file<br>is available for download
```

## Preparing Package for Export

## Exporting Package to Github

## Setting Up Documentation Structure in Github

## Creating a Release in Github

Package release is a process that includes:

- creating a release tag and name (manual)
- compiling the contents of a metadata package (automated)
- generating a metadata reference Excel file (automated)
- pushing the package to S3 (automated)
- updating package index file (automated, PR has to be reviewed and merged manually)

``` mermaid
    %%{init: {'mirrorActors': false } }%%

flowchart LR
    subgraph 1[Master branch - docs folder]
        direction LR
        left2[Installation guide] --- right1[Release note]
    end
    subgraph 2[feature brunch eg. 2.40]
        direction LR
        left1[Package folder/s with metadata.json file/s]
    end
    subgraph 3[feature brunch eg. 2.39]
        direction LR
        left3[Package folder/s with metadata.json file/s]
    end
    2 --> 4[package for DHIS2.40] --> 6[S3]
    1 --> 4
    6[S3] <--> 7[Metadata package index]
    1 --> 5[package for DHIS2.39] --> 6[S3]
    3 --> 5
    7 --> 8[Downloads section on dhis2.org]
   
```



The process has to be triggered manually
This action has to be done for each version of the package that is being released. Make sure that each feature branch contains the publish.yaml file located in `.github/workflows/publish.yaml` Otherwise create it. The content of the file can be found below:

``` yaml
name: Publish to S3

on:
  push:
    tags:
      - '**'

  workflow_dispatch:

jobs:
  call-workflow:
    uses: dhis2-metadata/gha-workflows/.github/workflows/publish.yaml@v1
    secrets:
      BOT_ACCESS_KEY: ${{ secrets.BOT_ACCESS_KEY }}
      BOT_SECRET_KEY: ${{ secrets.BOT_SECRET_KEY }}
      S3_BUCKET: ${{ secrets.S3_BUCKET }}
      AWS_REGION: ${{ secrets.AWS_REGION }}
      BOT_GITHUB_PAT: ${{ secrets.BOT_GITHUB_PAT }}
      BOT_GITHUB_EMAIL: ${{ secrets.BOT_GITHUB_EMAIL }}
```
