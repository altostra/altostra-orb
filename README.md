<p align="center">
  <img src="http://media.altostra.com/altostra-circleci-orb.png" alt="CircleCI + Altostra" width="390">
</p>
<br/>

<p align="center">
  <a href="https://altostra.com/blog/circle-ci-cd-altostra"><img alt="Learn More" src="https://media.altostra.com/buttons/learn-more.png" height="28" /></a>
  <a href="https://docs.altostra.com/"><img alt="View Docs" src="https://media.altostra.com/buttons/view-docs.png" height="28" /></a>
</p>
<br/>


[![Altostra](https://circleci.com/gh/altostra/altostra-orb.svg?style=svg)](https://app.circleci.com/pipelines/github/altostra/altostra-orb)

Easily integrate your Altostra deployment with your CircleCI

## Using

To deploy a project, use `altostra-orb` and provide the instance name and the environment:

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

      - altostra-orb/deploy:
          instance-name: "myInstance"
          env-name: "Production"
```

Or, you can push an image of the project:

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
          image-name: "v1.2.3-myVer"
          instance-name: "myInstance"
          env-name: "Production"
```
