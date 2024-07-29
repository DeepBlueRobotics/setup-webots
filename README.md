# setup-webots

This GitHub action can be used in a [GitHub workflow](https://docs.github.com/en/free-pro-team@latest/actions) to setup a version of [Webots](https://cyberbotics.com/) on ubuntu-latest, windows-latest, or macos-latest GitHub-hosted runner. Usage:

## Installing Webots

### Install a Stable Webots Release
``` YAML
    - name: Setup Webots
      id: setupWebots
      uses: DeepBlueRobotics/setup-webots@main
      with:
        webotsVersion: R2023b # Set this to your Webots version
```

### Install a Nightly Prerelease from the Official Webots Repository
``` YAML
    - name: Setup Webots
      id: setupWebots
      uses: DeepBlueRobotics/setup-webots@main
      with:
        webotsVersion: R2024a # Set this to your Webots version
        webotsTag: nightly_26_7_2024
```

### Install a Custom Release from a Webots Fork
``` YAML
    - name: Setup Webots
      id: setupWebots
      uses: DeepBlueRobotics/setup-webots@main
      with:
        webotsVersion: R2024a # Set this to your Webots version
        webotsTag: R2024a_DeepBlueSim_2024_07_28
        webotsRepository: DeepBlueRobotics/webots
```

### Install a Custom Release from an Arbitrary URL
Note that if you use the `webotsBaseUrl` option, the `webotsTag` and `webotsRepository` options
will be ignored, so the URL should contain any needed tag information.

``` YAML
    - name: Setup Webots
      id: setupWebots
      uses: DeepBlueRobotics/setup-webots@main
      with:
        webotsVersion: R2024a # Set this to your Webots version
        webotsBaseUrl: https://github.com/DeepBlueRobotics/webots/releases/download/R2024a_DeepBlueSim_2024_07_28
```

## Running Webots

``` YAML
    - name: Run Webots
      run: $RUN_WEBOTS /path/to/worlds/MyWorld.wbt
      shell: bash
```

In a step that uses the `bash` shell, `$RUN_WEBOTS` will expand to the start of a command line that will start Webots on any of the aforementioned runners with the `--no-rendering --stdout --stderr --minimize --batch` options. Those options allow Webots to run in a headless environment and redirect the controller's output/error to stdout/stderr.

Note:
 - On the macos-latest runner, Webots can take **10-15 minutes** to start, so be patient if using that runner.
 - This action has a few outputs that can be used to set environment variables like `WEBOTS_HOME` or `PATH` if desired. See [action.yml](action.yml) for details. You don't need to do that if you are just running Webots. `$RUN_WEBOTS` should be sufficient for that purpose.
