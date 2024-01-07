# OpenTTDLab

Python framework for running reproducible experiments using OpenTTD.

Based on [TrueBrain's OpenTTD Savegame Reader](https://github.com/TrueBrain/OpenTTD-savegame-reader).

> Work in progress. This README serves as a rough design spec.


## Installation

```shell
pip install OpenTTDLab
```


## Concepts

OpenTTDLab is based around the concept of an _experiment_, which encapsulates:

- Exact version of OpenTTD
- OpenTTD and command line arguments
- Versions of any AIs used
- Number of runs of OpenTTD
- Random seed used for each run
- Version of OpenTTDLab itself

This information is generated an available for each experiment, allowing it to be extracted in either machine or human readable forms, for use in code or publishing respectively.


## Usage

The core function of OpenTTD is the `setup_experiment` function.

```python
from openttdlab import setup_experiment

# If necessary, this will download the latest OpenTTD
run_experiment, get_experimental_config = setup_experiment()

# Run the experiment and get results. This may take time
results = run_experiment()
print(results)

# The information needed to reproduce the experiment
config = get_experiment_config()
print(config)
```


## Reproducing an experiment

If you have the `config` from a previous experiment, you can pass it into `setup_experiment` to exactly reproduce

```python
from openttdlab import setup_experiment

# allow_platform_difference=True will allow experiments from a platform other than the one
# the original experiments were performed on. Otherwise, setup_experiment may error because
# the exact same OpenTTD will not be able to be run on this platform
run_experiment, get_experimental_config = setup_experiment(config=config, allow_platform_difference=True)

# Run the experiment and get results
results = run_experiment()
print(results)
```


## API design considerations

- Mutability is avoided
- Impure functions are avoided
- Designed so if type checking were in place and passes, API misuse should be close to impossible
