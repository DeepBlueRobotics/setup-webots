# setup-webots

This GitHub action can be used in a [GitHub workflow](https://docs.github.com/en/free-pro-team@latest/actions) to setup [Webots](https://cyberbotics.com/) version 2021a on ubuntu-latest, windows-latest, or macos-latest GitHub-hosted runner. Usage:

```
    steps:
    - name: Setup Webots
      uses: DeepBlueRobotics/setup-webots@v0.0.1

    - name: Run Webots
      run: $RUN_WEBOTS /path/to/worlds/MyWorld.wbt
      shell: bash

```

In a step that uses the `bash` shell, `$RUN_WEBOTS` will expand to the start of a command line that will start Webots on any of the aforementioned runners with the `--no-rendering --stdout --stderr --minimize --batch` options. Those options allow Webots to run in a headless environment and redirect the controller's output/error to stdout/stderr.

Note:
 - On the macos-latest runner, Webots takes over **8 minutes** to start, so be patient if using that runner.
 - This action has a few outputs that can be used to set environment variables like `WEBOTS_HOME` or `PATH` if desired. See [action.yml](action.yml) for details. You don't need to do that if you are just running Webots. `$RUN_WEBOTS` should be sufficient for that purpose.
 

