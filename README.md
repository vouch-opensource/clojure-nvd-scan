# Clojure NVD Scan Github Action

Github action to run an NVD scan on Clojure deps.edn projects. Uses [rm-hull/nvd-clojure](https://github.com/rm-hull/nvd-clojure).

## Usage

```yml
name: Example workflow

on: [push]

jobs:

  nvd-scan:

    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Prepare java
        uses: actions/setup-java@v2
        with:
          distribution: 'openjdk'
          java-version: '8'
      
      - name: NVD Scan
        uses: vouch-opensource/clojure-nvd-scan@v0.2
        with:
          config-filename: '.nvd/config.json'
          aliases: 'dev:main'
          clojure-version: '1.10.3.1040'
          nvd-clojure-version: 'RELEASE'
```

### Configuration

Refer to [nvd-clojure configuration options](https://github.com/rm-hull/nvd-clojure#configuration-options). This github action uses the json configuration format.

### Working directory

In case you want to run the NVD scan in a different directory than the default GITHUB_WORKSPACE, you can specify the
`working-directory` option

```yml
      - name: NVD Scan
        uses: vouch-opensource/clojure-nvd-scan@v0.2
        with:
          working-directory: './cljs'
          config-filename: '../.nvd/config.json'
```

Note that in case you also want to specify a config file, you have to provide a relative path from the working-directory.
