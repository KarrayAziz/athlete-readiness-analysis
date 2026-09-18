# Raw data

The raw dataset is not included in this repository.

Place the participant folders directly inside this directory:

```text
data/
├── p01/
├── p03/
└── p05/
```

The original internal folder structure should be preserved.

For example:

```text
data/
└── p01/
    ├── fitbit/
    ├── pmsys/
    ├── googledocs/
    └── food-images/
```

The same structure should be preserved for the other participants.

By default, the notebook reads the raw participant folders from:

```text
data/
```

If the data is stored elsewhere, set the `PMDATA_RAW_DIR` environment variable to the directory containing the participant folders.

For example:

```bash
export PMDATA_RAW_DIR=/path/to/data
```

The raw data should remain unchanged. The notebook only reads these files and writes the processed output to the project root and `outputs/` directory.
