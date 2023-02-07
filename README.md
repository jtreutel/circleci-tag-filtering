# circleci-tag-filtering
Example showing how to run certain jobs only when git tags are matched.

In this repo, `build` and `test` will run on (1) all branches and (2) all commits with a tag prefixed with `v`, due to the following filters ([example](https://app.circleci.com/pipelines/github/jtreutel/circleci-tag-filtering/2/workflows/f36cde51-5149-4d8f-a4c7-e096937aa4be)):

```yml
  filters:
    tags:
      only: /^v.*/ #Run on tags that start with "v", but don't run for any other tags
    #Run on all branches because there is no "branches" filter
```

The `deploy` and `type: approval` jobs will only run on commits with a tag prefixed with `v` due to the following filters (example: [workflow1](https://app.circleci.com/pipelines/github/jtreutel/circleci-tag-filtering/3/workflows/d35bbd2e-d36a-4add-a26d-cb29eb532f81), [workflow2](https://app.circleci.com/pipelines/github/jtreutel/circleci-tag-filtering/3/workflows/35bdf468-8b20-48ce-bb74-8dde28c262bb)):

```yaml
  filters:
    tags:
      only: /^v.*/ #Only run on tags that start with "v"
    branches:
      ignore: /.*/ #Don't run on any branches unless they are tagged
```

