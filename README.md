# drbergman-lab QuPath catalog

A QuPath [extension catalog](https://github.com/qupath/extension-catalog-model)
listing the QuPath extensions published by drbergman-lab.

## Use this catalog in QuPath

Paste the following URL into QuPath's **Extensions → Manage extension catalogs**
form (the exact menu wording varies by QuPath version):

```
https://raw.githubusercontent.com/drbergman-lab/qupath-catalog/main/catalog.json
```

After that, **Extensions → Manage extensions** lists every extension in this
catalog with an Install button. QuPath downloads the jars straight from the
authors' GitHub releases.

## Currently listed

| Extension | Repository | Description |
|-----------|------------|-------------|
| **BIWT** | [`drbergman-lab/biwt-jvm`](https://github.com/drbergman-lab/biwt-jvm) | Sample QuPath digital pathology images on a regular grid and export substrate initial conditions for PhysiCell-style ABMs. |

## Adding a new release of an existing extension

Each release is a separate entry in the `releases` array under its
extension. Newer first by convention.

```json
{
    "name": "v0.4.0",
    "main_url": "https://github.com/<owner>/<repo>/releases/download/v0.4.0/<jar-name>.jar",
    "version_range": { "min": "v0.7.0" }
}
```

The `main_url` must return HTTP 200; the consumer validates this at parse time.

## Adding a new extension

Append a new entry to the `extensions` array with `name`, `description`,
`author`, `homepage`, and a first release.

## Validating before pushing

```sh
# Optional, but catches typos before the catalog goes live.
pip install git+https://github.com/qupath/extension-catalog-model
python -c "from extension_catalog_model.model import Catalog; \
           Catalog.parse_file('catalog.json'); print('valid')"
```

Plain `jq . catalog.json` confirms JSON validity but not schema conformance.
