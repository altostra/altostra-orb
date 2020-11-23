<p align="center">
  <img src="https://altostra.com/images/blog/circle-ci-cd-altostra.png" alt="CircleCI + Altostra" width="390">
</p>
<br/>

<!-- <p align="center">
  <a href="https://altostra.com/blog/circle-ci-cd-altostra"><img alt="Learn More" src="https://secrethub.io/img/buttons/github/learn-more.png?v2" height="28" /></a>
  <a href="https://secrethub.io/docs/guides/circleci/"><img alt="View Docs" src="https://secrethub.io/img/buttons/github/view-docs.png?v2" height="28" /></a>
</p>
<br/>

<h1>
  CircleCI Orb <img src="https://secrethub.io/img/integrations/circleci/partner-badge.png" alt="Partner badge" width="60" />
</h1> -->

[![Altostra](https://circleci.com/gh/altostra/altostra-orb.svg?style=svg)](https://app.circleci.com/pipelines/github/altostra/altostra-orb)


Easily integrate your Altostra deployoment with your CircleCI

## Usage

To deploy a project directly to one of your instances, you can run:

```yaml
version: 2.1
orbs:
  altostra-orb: altostra/altostra-orb@x.y #enter latest version

jobs:
  build:
    docker:
      - image: circleci/node:12.13

    working_directory: ~/repo

    steps:
      - checkout
      # setup the Altostra CLI with your api-token
      - altostra-orb/setup:
          api-token: "$ALTO_API_KEY"

      - run:
          name: NPM install
          command: npm install

      - altostra-orb/deploy:
          instance-name: "myInstance"
          env-name: "Production"
```

Or, you can just push your version to your repository:

```yaml
version: 2.1
orbs:
  altostra-orb: altostra/altostra-orb@x.y #enter latest version

jobs:
  build:
    docker:
      - image: circleci/node:12.13

    working_directory: ~/repo

    steps:
      - checkout
      # setup the Altostra CLI with your api-token
      - altostra-orb/setup:
          api-token: "$ALTO_API_KEY" # Set this in your project Environment variables

      - run:
          name: NPM install
          command: npm install

      - altostra-orb/push:
          version: "v1.2.3-myVer"
```

and then deploy it:
```yaml
      - altostra-orb/deploy-version:
          image-version: "v1.2.3-myVer"
          instance-name: "myInstance"
          env-name: "Production"
```
