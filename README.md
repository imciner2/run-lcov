## run-lcov

This action runs the `lcov` tool with the specified options.

**Note:** This action only will run on Ubuntu-based runners (e.g. `ubuntu-latest` or equivalent).

## Inputs


### `input_directory`

**Required**

Base directory to search for the coverage files

### `output_file`

**Required**

The file to output the coverage information to.

Default: `coverage.info`

### `exclude`

Files/directories to exclude from the coverage report. Wildcards are supported. This should be passed in as a string, with each exclude pattern quoted inside it.

Default: empty string (no excludes)

### `display_coverage`

Display the coverage information in the action log.

Default: `true`


## Example usage

### Basic usage

Parse coverage information for the `build/` directory and save it to `coverage.info`.
```yaml
uses: imciner2/run-lcov@v1
with:
  input_directory: build/
```

### Excluding files

Remove the `test` folder and the `helpers.h` file.
```yaml
uses: imciner2/run-lcov@v1
with:
  input_directory: build/
  exclude: '"test/*" "*/helpers.h"'
```

### Complex usage

Parse the `build/` folder inside the runner workspace for the coverage information and save the resulting coverage inside `code_coverage.info` in that directory. Also remove the `tests/` and `examples/`folder contents from the coverage, along with system headers.
```yaml
uses: imciner2/run-lcov@v1
with:
  input_directory: '${{ runner.workspace }}/build'
  exclude: '"$GITHUB_WORKSPACE/tests/*" "$GITHUB_WORKSPACE/examples/*" "/usr/include/x86_64-linux-gnu/*"'
  output_file: '${{ runner.workspace }}/build/code_coverage.info'
```

## Author

Copyright (C) 2021 Ian McInerney

## License 

MIT
