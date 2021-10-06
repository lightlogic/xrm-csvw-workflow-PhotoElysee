# Template for a Barnard59 pipeline running XRM mappings

Use this repo as template to set up a project-specific pipeline which transform CSVW into RDF using CSVW mapping files.

## Set up

The `mappings` directory contains an example XRM mappings which define how the input CSV files get transformed to RDF. See our [product page](https://zazuko.com/products/expressive-rdf-mapper/) and the [documentation](https://github.com/zazuko/expressive-rdf-mapper) for editing instructions.

The `input` directory contains said CSV file.

The files inside `src-gen` are generated by XRM. They should be committed to the repository.

## Parameters

The pipeline requires three parameters, which are set as environment variables:

| ENV variable | default | description |
| -- | -- | -- |
| MAPPINGS | `src-gen/*.json` | [glob pattern](https://www.npmjs.com/package/glob) for (XRM-generated) csvw mapping files |
| INPUT_DIR | `input` | location of input CSV files |
| OUTPUT | `output/transformed.nt` | path to write resulting n-triples |

They are stored in the `.env.defaults` file.

Note that if the `OUTPUT` is changed, then artifacts section of workflow yaml has to be updated so that the resulting file is picked up and stored as artifact.

## Running locally

It is possible to run locally with `npm start`.

Parameters can be changed locally by creating a `.env` file in the repo root with key/value pairs. For example to narrow down the input mappings:

```
MAPPINGS=src-gen/subset*.json
```

Diagnostic output it possible by running the command with a verbose switch

```
npm run start -- -v
```

or

```
yarn start -v
```
