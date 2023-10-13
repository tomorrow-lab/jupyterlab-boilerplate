# Jupyter analytics boilerplate

## Purpose

Inspired by [http://drivendata.github.io/cookiecutter-data-science/](Cookiecutter Data Science), this directory represents a platonic ideal from which I begin new data analysis tasks.

### Principles
- By default everything in the `/data` directory is gitignored. Don't manually place data there, but rather include the code necessary to reproduce the data from scratch when run.
- A properly documented notebook has enoguh markdown that it can be used as a self-contained report when the code is hidden. When in doubt, hide your code and see if the notebook still makes sense.

## Structure
```
├── sql                         <- Templated SQL files
│   └── example_query.sql
├── data                        <- Cached data sets
│   ├── example_query.parquet
│   └── example_query.tsv
├── notebook.ipynb              <- Main analysis
└── README.md                   <- When completed, write a summary
```

# Build a docker image using pixi
This project shows how to build a docker image with pixi installed into it.

To show the strength of pixi in docker, we're going to use an installed pixi to build pixi in a docker image.
Steps of the docker build:
- Install the latest `pixi` from our prebuild binaries.
- Use `pixi` to install the build dependencies for the source project of `pixi`.
- Use `pixi` to run the cargo build of the source `pixi`.

NOTE: Please [install docker](https://docs.docker.com/engine/install/) manually as it is not available through conda.
To start the `docker build` use pixi:
```shell
pixi run start
```

To optimize build time of the docker image, we use a cache for the pixi environment.
The mount is a docker specific cache location, so the first it will be slow but the second time the cache will be reused.
More info in their docs: https://docs.docker.com/build/guide/mounts/
```dockerfile
RUN --mount=type=cache,target=/root/.cache/rattler pixi install
```
