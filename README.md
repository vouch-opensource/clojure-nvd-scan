# Clojure NVD Scan Github Action

Github action to run an NVD scan on Clojure deps.edn projects. Uses [rm-hull/nvd-clojure](https://github.com/rm-hull/nvd-clojure).

This product uses the NVD API but is not endorsed or certified by the NVD.

## Usage

Before being able to use the action you have to 
[request an NVD API key](https://nvd.nist.gov/developers/request-an-api-key). 
It is a good idea to store it as a 
[Github Actions Secret](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions).

```yml
name: Example workflow

on: [push]

jobs:

  nvd-scan:

    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Prepare java
        uses: actions/setup-java@v4
        with:
          distribution: 'adopt'
          java-version: '11'
      
      - name: NVD Scan
        uses: vouch-opensource/clojure-nvd-scan@master # To pin the version you can also refer to a specific git sha here.
        with:
          nvd-api-key: ${{ secrets.NVD_API_KEY }}
          config-filename: '.nvd/config.json'
          aliases: 'dev:main'
          clojure-version: '1.10.3.1040'
          nvd-clojure-version: 'RELEASE'
          java-opts: '-Xmx1g'
```

### Configuration

Refer to [nvd-clojure configuration options](https://github.com/rm-hull/nvd-clojure#configuration-options). This github action uses the json configuration format.

### Working directory

In case you want to run the NVD scan in a different directory than the default GITHUB_WORKSPACE, you can specify the
`working-directory` option

```yml
      - name: NVD Scan
        uses: vouch-opensource/clojure-nvd-scan@master
        with:
          working-directory: './cljs'
          config-filename: '../.nvd/config.json'
```

Note that in case you also want to specify a config file, you have to provide a relative path from the working-directory.
