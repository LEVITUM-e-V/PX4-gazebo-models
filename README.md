# PX4-gazebo-models (LevITum Fork)

This is a fork of [PX4/PX4-gazebo-models](https://github.com/PX4/PX4-gazebo-models) maintained by LevITum. We use this fork to develop and maintain custom Gazebo simulation models for our prototypes:

- **p2** — Prototype 2
- **p4_1** — Prototype 4.1
- **p5** — Prototype 5

These models can be found in the `models/` directory alongside the upstream PX4 models.

## Submodule in PX4-Autopilot

This repository is included as a **git submodule** in our PX4-Autopilot fork at:

```
Tools/simulation/gz
```

When you make changes to a model in this repository, the submodule reference in PX4-Autopilot must be updated to point to the new commit. Otherwise PX4-Autopilot will continue using the old version of the model.

To update the submodule in PX4-Autopilot:

```bash
cd PX4-Autopilot
git submodule update --remote Tools/simulation/gz
git add Tools/simulation/gz
git commit -m "Update PX4-gazebo-models submodule"
git push
```

---

## Upstream README

*The following is the original upstream documentation.*

# PX4-gazebo-models (Upstream)
Models and worlds to be used in local Fuel instances and kept up to date in [app.gazebosim.org/PX4](https://app.gazebosim.org/PX4).

## Starting GZ simulation
In addition to providing resource files for all models and worlds, this repo also contains a simulation-gazebo script that will start a world and works in conjunction with PX4.

In order for this script to work, you must have installed gz-garden beforehand. The way to do this can be found [here](https://gazebosim.org/docs/garden/install_ubuntu):

After setting up gazebo, navigate to the repo containing simulation-gazebo and script with

```shell
python simulation-gazebo
```

If you do not provide any arguments, this will download all models and worlds from the PX4-gazebo-models repo, save them to `/.simulation-gazebo` and start a default world. **In order for a model to load, you need to start PX4 as well**

The following arguments can be passed:

`--world` A string variable that names the sdf file which runs the simulation world. Default argument is "default", which links to the default world.

`--gz_partition` A string variable that sets the gazebo partition to run in (more information [here]([https://gazebosim.org/api/transport/13/envvars.html))

`--gz_ip` A string variable that sets the IP of the outgoing network interface (more information [here]([https://gazebosim.org/api/transport/13/envvars.html))

`--interactive` A boolean variable that requires the ability to run the code in interactive mode, allowing for custom paths for `--model_download_source`. If this is not set, `--model_download_source` will only download from the default Github repo.

`--model_download_source` A string variable setting the path to a directory from where models are to be imported. At the moment this can only be a local file directory or a http address. The source should end with the zipped resource file. (e.g. https://path/to/simulation/models/resource.zip)

`--model_store` A string variable setting the path to the model storage directory. This is where the zip file provided in `model_download_source` will be placed.

`--overwrite` A boolean variable providing the ability to overwrite existing directories with new data.

`--dryrun` A boolean variable that can be set when running testcases. It will not provide any interactivity and will not start Gazebo simulation.

`--headless` A boolean variable providing the ability to run in headless (server-only) mode. This is the [mode of operation in macOS](https://gazebosim.org/docs/harmonic/getstarted#macos), and is more suitable for container use.
