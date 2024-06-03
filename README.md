# tk-mari

`tk-mari` is a ShotGrid Toolkit engine for Mari, providing seamless integration with ShotGrid. 

This engine allows artists and technical directors to access ShotGrid functionality directly within Mari.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Environments](#environments)
- [Configuration](#configuration)
- [Contributing](#contributing)

## Introduction

`tk-mari` integrates ShotGrid with Mari, enabling a streamlined workflow for visual effects and animation production. 

By using this toolkit, users can easily manage assets, publish work, and track project progress within the mari environment.

## Environments
`tk-mari` has been tested in this environment:
- CentOS 7
- Shotgrid Desktop App 1.8.0
- Mari 6.0v2

## Features

- Asset Management: Browse and load assets directly from ShotGrid.
- Publishing: Publish your work to ShotGrid with metadata and version control.
- Task Management: View and manage your ShotGrid tasks within Mari.
- Customizable UI: Tailor the toolkit interface to fit your pipeline needs.

## Installation

#### You must be prepared for [Shotgrid](https://shotgrid.autodesk.com/)  and Advanced Project Settings in Shotgrid Desktop App to use `tk-mari`!

The official [ShotGrid Developer Help Center](https://help.autodesk.com/view/SGDEV/ENU/) and [Shotgrid Community](https://community.shotgridsoftware.com/) can be helpful.


## Configuration
To configure `tk-mari`, edit the environment yml files located in the `config` directory.
After adding the `tk-mari` engine, you can add various apps to `tk-mari`.


#### 1. Locate where you installed Pipeline Configuration

#### 2. Add `MARI_SCRIPT_PATH` to recognition of `init.py` in `tk-mari` within mari

```sh
export MARI_SCRIPT_PATH="$MARI_SCRIPT_PATH:/tk-mari/startup"
```

#### 2. Add engine descriptor section to `config/env/includes/engine_locations.yml`:

```yaml
engines.tk-mari.location:
  type: git
  name: tk-mari
  version: v1.4.1
  path: "github.com/junopark00/tk-mari.git"
```

#### 3. Then, create `config/env/includes/settings/tk-mari.yml`:

```yaml
includes:
#- ../app_locations.yml
- ../engine_locations.yml
- ./tk-multi-loader2.yml
- ./tk-multi-publish2.yml
#- ./tk-multi-screeningroom.yml
#- ./tk-multi-shotgunpanel.yml
#- ./tk-multi-snapshot.yml
- ./tk-multi-workfiles2.yml
- ./tk-mari-project-manager.yml

# asset_step
settings.mari.asset_step:
  apps:
    tk-multi-loader2: "@apps.tk-multi-loader2"
    tk-multi-publish2: "@apps.tk-multi-publish2"
    tk-multi-workfiles2: "@settings.tk-multi-workfiles2.mari"
    tk-mari-projectmanager: "@settings.tk-mari-projectmanager"
  menu_favourites:
  - {app_instance: tk-multi-workfiles2, name: File Open...}
  - {app_instance: tk-multi-workfiles2, name: File Save...}
  - {app_instance: tk-multi-loader2, name: Load}
  - {app_instance: tk-multi-publish2, name: Publish...}
  location: "@engines.tk-mari.location"
```

#### 4. Update the apps using the `tank` command in your Pipeline Configurations folder:

```sh
./tank cache_apps
```

## Contributing
Welcome contributions to tk-mari.

To contribute:
1. Fork the repository.
2. Create a new branch (git checkout -b feature/your-feature-name).
3. Make your changes.
4. Commit your changes (git commit -m 'Add some feature').
5. Push to the branch (git push origin feature/your-feature-name).
6. Open a pull request.
