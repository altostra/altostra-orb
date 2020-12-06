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

Integrate Altostra projects into your CircleCI workflows.
Use Altostra to accelerate serverless applications development in a no-code environment.

To use this orb, sign up for a free account at [Altostra](https://altostra.com/). 

Click to [learn more](https://docs.altostra.com/integrations/ci-cd/circleci-integration.html)


## Using

### Setting up

First, add an env variable named ALTO_API_KEY to your project environment and set it's value to your Altostra API Token.
The `altostra-orb/setup` step will use this variable to set up your connection to Altostra.

### Pushing and Deploying 
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
      - altostra-orb/setup
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
      - altostra-orb/setup
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

### Non Node projects
If you're using an image that doesn't contain NPM installed (like python images), 
use the `circleci/node` orb to install NPM:

```yaml
version: 2.1
orbs:
  altostra-orb: altostra/altostra-orb@x.y #enter latest version
  node: circleci/node@4.1.0

jobs:
  build:
    docker:
      - image: circleci/python:latest

    working_directory: ~/repo

    steps:
      - checkout
      - node/install #Installing node
      # setup the Altostra CLI with your api-token
      - altostra-orb/setup
      - run:
          name: NPM install
          command: npm install

      - altostra-orb/deploy:
          instance-name: "myInstance"
          env-name: "Production"
```

You can read more about using specific node versions and other settings at the `circleci/node` [documentation page](https://circleci.com/developer/orbs/orb/circleci/node)