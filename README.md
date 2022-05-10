<p align="center"><a href="#readme"><img src="https://gh.kaos.st/perfecto-action.svg"/></a></p>

<br/>

Action for checking RPM spec files with [_perfecto_](https://kaos.sh/perfecto).

### Usage

Create file `.github/workflows/perfecto.yml`.

Add next code to it:

```yml
name: CI

on:
  push:
    branches: [master, develop]
  pull_request:
    branches: [master]

jobs:
  Perfecto:
    name: Perfecto
    runs-on: ubuntu-latest

    steps:
      - name: Code checkout
        uses: actions/checkout@v3

      - name: Login to GitHub Container Registry
        uses: docker/login-action@v1
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Check specs with Perfecto
        uses: essentialkaos/perfecto-action@v2
        with:
          files: myapp.spec

```

### Options

| Option | Description | Value |
|--------|-------------|-------|
| `files` | One or more files to check | _Path to spec file_ |
| `format` | Output format | `github` (_Default_)<br/>`summary`<br/>`tiny`<br/>`short` |
| `error-level` | Return non-zero exit code if alert level greater than given | `notice`<br/>`warning`<br/>`error`<br/>`critical` |
| `absolve` | Disable some checks by their ID | [Check ID](https://kaos.sh/perfecto/w/Home) |
| `image` | Docker image with perfecto | `ghcr.io/essentialkaos/perfecto:micro` (_Default_) |

### License

[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)

<p align="center"><a href="https://essentialkaos.com"><img src="https://gh.kaos.st/ekgh.svg"/></a></p>
