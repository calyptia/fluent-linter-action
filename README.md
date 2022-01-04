<p align="center">
    <a href="https://github.com/marketplace/actions/fluent-linter-action">
      <img src="https://img.shields.io/badge/Marketplace-v2-undefined.svg?logo=github&logoColor=white&style=flat" alt="GitHub Marketplace" />
    </a>
    <a href="https://github.com/calyptia/fluent-lint-action/actions/workflows/unit-tests.yml">
      <img src="https://github.com/calyptia/fluent-linter-action/actions/workflows/unit-tests.yml/badge.svg" alt="unit-tests" />
    </a>
    <a href="https://codecov.io/gh/calyptia/fluent-linter-action">
      <img src="https://codecov.io/gh/calyptia/fluent-linter-action/branch/main/graph/badge.svg?token=48gHuQl8zV" alt="codecov" />
    </a>
  <a href="https://github.com/calyptia/fluent-linter-action/blob/main/LICENSE">
      <img src="https://img.shields.io/github/license/calyptia/fluent-linter-action" alt="APACHE 2.0 license" />
    </a>
</p>

<p align="center">
  <a href="https://github.com/calyptia/fluent-linter-action">
    <img src="logo.svg" alt="Logo" width="95" height="105">
  </a>

  </p>

## Table of Contents

- [Getting Started](#getting-started)
- [Installation](#installation)
  - [Add workflow to your repository](#add-workflow-to-your-repository)
    - [Using GitHub UI](#using-github-ui)
    - [Manual](#manual)
  - [Get Calyptia API Key](#get-calyptia-api-key)
  - [Configure secret in your repository](#configure-secret-in-your-repository)
- [Limitations](#limitations)
- [Contributing](#contributing)
- [License](#license)

# Getting started

fluent-bit and fluentd configurations are simple to use. But over time, use will grows and with that, complexity as well. This action will help stay away from common pitfalls. It will add linting to your development process through workflows.

# Installation

The next steps will help set up fluent linter action in your repository.

## Add workflow to your repository

The first step is to create the workflow in your repository. We describe two ways: via [ Github UI ](#using-github-ui) or [manually](#manually).

### Manual

1. Create the following directory in your repository `.github/workflows/`
1. Under `.github/workflows/` create a file called `fluent-linter.yml`
1. Open `.github/workflows/fluent-linter.yml`
1. paste the following content:

   ```yml
   on: pull_request

   name: Fluent-linter
   jobs:
     lint:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@master
         - id: fluent_linter_action
           uses: calyptia/fluent-linter-action@gg/use-example
           with:
             CALYPTIA_API_KEY: ${{ secrets.CALYPTIA_API_KEY }}
             CONFIG_LOCATION_GLOB: '*.conf'
   ```

1. Make sure to change `CONFIG_LOCATION_GLOB` to a [glob](<https://en.wikipedia.org/wiki/Glob_(programming)>) that points to your fluentd and/or fluent-bit configuration within the repository.

_If you want to see it in action, take a look at the [example here](https://github.com/calyptia/fluent-linter-action/pull/9)_

### Using GitHub UI

1. Go to the repository you wish to add the fluent-linter-action workflow.
1. Under the tab _Actions_ look for a button called _New workflow_.
1. Under _Choose workflow_, you will find a text box, please type "fluent-linter".
1. You will find Fluent-linter-action by Calyptia, look for a button called "Configure".
1. Make sure to change `CONFIG_LOCATION_GLOB` to a [glob](<https://en.wikipedia.org/wiki/Glob_(programming)>) that points to your fluentd and/or fluent-bit configuration within the repository.

If everything goes well, you will have an editor that will let you change anything on the workflow before committing. Keep in mind that the version could be changed to a specific version instead of `main` (current version `v0.0.10`).

_Make sure to commit the workflow to your repository._

_For more information about using workflows, take a look at\ [github documentation](https://docs.github.com/en/actions/learn-github-actions/using-starter-workflows)_

If the options we have just described are not working out for you try the [Manual approach](###Manual)

## Get Calyptia API Key

In order to get the full linting capabilities from this action, you will need to get a Calyptia token. The token is easy to get, just head over to [Calyptia Cloud](https://cloud.calyptia.com/) and login (you can use your github account). On the Left panel you can find _Account > settings > Generate API key_. Give it a distinct name for safe keeping (for instance you could name it _linter_). please copy this token.

## Configure secret in your repository

The last step will make use of the API Key we generated in Calyptia Cloud.

In order to add a new secret to your repository find _Settings > Secrets > New repository secret_. the name for this secret should be `CALYPTIA_API_KEY`. Paste the secret you obtained in the step before.

> note: Settings is often next to the insights tab. If is missing, you might need administrator permissions to add secrets to the repo.

# Limitations

- The current `fluent-linter-action` only works with `fluent-bit` configurations. `fluentd` configurations will be available shortly.
- The current `fluent-linter-action` doesn't support `@includes` yet. These if found in your configurations, will be ignored. Please follow [this issue](https://github.com/calyptia/fluent-bit-config-parser/issues/9) for updates.

<!-- CONTRIBUTING -->

## Contributing

Contributions are what makes the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<!-- LICENSE -->

## License

Distributed under the Apache-2.0 License. See `LICENSE` for more information.
