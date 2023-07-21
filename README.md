# Dev container configuration for Tauri (Rust)

## Introduction
This configuration allows for Tauri (Rust) development inside a Dev Container without having to manually install all the neeeded dependencies and extensions, and wire up all launch and debugging commands.

## Usage
Clone the configuration and start a new project using `cargo create-tauri-app` inside the container: this will create a new folder in your workspace with your `<app-name>`. 
Copy all the content of your `<app-name>`'s folded to the root folder: all configuration assumes your files are in the root directory (at the same level as the `.devcontainer` folder).

Then run `npm install` to fetch all Node dependencies.

## Content
The content of the `.devcontainer` folder contains:
- a `Dockerfile` for starting a container using Debian 12 with a Rust and Node development environment
- a `devcontainer.json` for setting up all needed extensions for Rust and Tauri development and all VSCode tasks and launch configuration needed for running and debugging the Tauri application without additionnal configuration.

## Tasks and launch configuration
The `devcontainer.json` contains 3 launch configurations:
- `Tauri Run Dev` which is equivalent to typing `npm run tauri dev` in the terminal and allows for HTML, CSS, JS and Rust hot reloading ==> This configuration is the default when launching with `Ctrl + F5`
- `Tauri Development Debug` and `Tauri Production Debug` which are the Rust debugging profiles recommended by Tauri's documentation : please be sure to select the launch config manually before running it with `F5` (or you will launch `Tauri Run Dev` by default)

It also contains 3 tasks:
- `tauri:dev` which is used by the `Tauri Run Dev` launch configuration: it executes `npm run tauri dev`
- `ui:dev` which is used by the `Tauri Development Debug` and starts the UI before allowing debugging the Rust code through LLDB: a custom `problemMatcher` has been setup in order for VSCode to understand when the UI has been correctly started. Whithout it the debugger would hang and VSCode would prompt you to override the start manually each time you run the debugger.
- `ui:build` same but for `Tauri Production Debug`

## Warning
I have noticed the CodeLLDB debugger sometimes cannot be installed directly by the Rust image because of a `PROXY ERROR`. I have added the extension as a `vsix` file in the repository, which can be installed manually inside VSCode running the dev container with `Ctrl + Maj + P` and choosing `Extensions: Install from VSIX...`.
