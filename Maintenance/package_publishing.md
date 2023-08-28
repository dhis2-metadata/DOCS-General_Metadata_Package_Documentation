# Package Publishing

## Table of Contents

1. [Introduction](#introduction)

## Introduction

This guide is aimed at core team implementers that are responsible for exporting and publishing DHIS2 metadata packages.

The process of publishing DHIS2 metadata packages requires:

1. Admin access to DHIS2 development instances
2. Collaborator access to [dhis2-metadata organisation](https://github.com/dhis2-metadata)
3. Access to [Jenkins metadata exporter](https://ci.dhis2.org/job/metadata-exporter) and [Jenkins metadata export triggerer](https://ci.dhis2.org/job/metadata-export-triggerer)
4. Access to [DHIS2 metadata package index spreadsheet](https://docs.google.com/spreadsheets/d/1IIQL2IkGJqiIWLr6Bgg7p9fE78AwQYhHBNGoV-spGOM/edit?usp=sharing)
5. Access to [DHIS2 S3](https://s3.console.aws.amazon.com/s3/home) - optional
6. Basic knowledge of markdown syntax. [Markdown support and extensions guide](https://docs.dhis2.org/en/implement/support-and-documentation/dhis2-documentation-guide.html?h=markdown#markdown_support_and_extensions) provides an overview of supported functionality. The structure of markdown documents is addressed in the [Markdown File Structure](#markdown-file-structure) section 

