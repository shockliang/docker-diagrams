<p align="center">
  <a href="https://hub.docker.com/r/shockwater/diagrams/tags/"><img height="20" alt="Docker Tags" src="https://img.shields.io/badge/dynamic/json.svg?style=for-the-badge&label=%F0%9F%90%B3%20tags&colorB=066da5&query=$.count&uri=https%3A%2F%2Fhub.docker.com%2Fv2%2Frepositories%2Fshockwater%2Fdiagrams%2Ftags"></a>
  <a href="https://hub.docker.com/r/shockwater/diagrams/tags/"><img height="20" alt="Docker Latest Tag" src="https://img.shields.io/badge/dynamic/json.svg?style=for-the-badge&label=%F0%9F%90%B3%20latest%20tag&colorB=066da5&query=$.results[0].name&uri=https%3A%2F%2Fhub.docker.com%2Fv2%2Frepositories%2Fshockwater%2Fdiagrams%2Ftags"></a>
  <a href="https://github.com/shockliang/docker-diagrams/actions"><img height="20" alt="Build" src="https://img.shields.io/github/actions/workflow/status/shockliang/docker-diagrams/build.yml"></a>
</p>

<p align="center">
  Docker image for <a href="https://github.com/mingrammer/diagrams"><code>diagrams</code></a>
</p>

---

#### _Running:_

```sh
$ cat <diagram-file>.py | docker run -i --rm -v $(pwd)/out:/out shockwater/diagrams:<version>
```

The `/out` directory is where `diagram` will generate your PNGs.

---

#### _Developing:_

```sh
$ make build    # Builds a new image
$ make test     # Runs/tests the image
$ make push     # Pushes the image up
$ make clean    # Removes any generated artifacts
$ make clobber  # Removes artifacts and generated images
```

Update the diagrams version:
* Run the container using python 3.11.1-alpine and mount the volume to mapping the source folder
```sh
docker run -it --rm -v ${PWD}:/home python:3.11.1-alpine ash
```
* install package in the packages
```sh
apk add --update --no-cache \
    curl\
    graphviz\
    gcc\
    libc-dev\
    libffi-dev\
    ttf-freefont \
    coreutils && \
    curl -sSL https://raw.githubusercontent.com/python-poetry/install.python-poetry.org/42a10434ed127a5986c3a9952c75d333ac3a1f8e/install-poetry.py > install-poetry.py && \
    echo "08a38ab8de719d4012af4d62c37ce09e84edce6e1c4da7c5ccbcade359312c8b install-poetry.py" | sha256sum -c && \
    python install-poetry.py --version 1.3.1 && \
    apk del \
    gcc \
    libc-dev \
    libffi-dev
```
* Run `export PATH="/root/.local/bin:$PATH"` after install package of `poetry`.
* Upgrading the  diagrams version of `pyproject.toml`
* Run `poetry install --no-root` for update poetry.lock
* Exit the container and the `poetry.lock` will be updated.
* Run `make test` to testing.
* Commit the `poetry.lock` and `pyproject.toml` and push.
* Wait the github action to run pipeline. :tada:


Thanks @gtramontina

---

<p align="right">🐳</p>
