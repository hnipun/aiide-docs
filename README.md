# notbadaiide v0.9.4

## Download

Use the link below to download the app:

[notbadaiide v0.9.4](https://drive.google.com/file/d/1BDY5TyOPOtnuMeiB0C535q3O3aGcmTiB/view?usp=sharing)

After downloading, unzip the file and run the following command in your terminal (replace the path with the actual
location of the app file):

```bash
xattr -dr com.apple.quarantine /path/to/ai-editor-v0.9.4app
```

## Code Editor

The code editor supports shortcuts similar to VS
Code. [Here](https://github.com/hnipun/aiide-docs/blob/main/code_editing_shortcuts.md)’s a list of the popular
ones.

## Terminal

To reset the terminal (clearing both the display and back-scroll history), click the `Reset` button.

## Extensions

Extensions are Python scripts that enable interactions with LLMs, such as chat, code apply, autocomplete, gray
completions etc. You can also create your own extensions, which the editor will manage and execute (explained in a later
section).

### Setup

<img src="https://github.com/hnipun/aiide-docs/blob/main/images/image.001.png" alt=""/>

- When you launch the editor for the first time, the default extensions are downloaded to `~
  /.notbadaiide/extensions/.`
- This can be verified by navigating to `Extensions` (left side pane) → `Management` and checking the
  `Extensions Repository`. It should display the downloaded.
- Make sure to set your `Python Path` and `API Key` under `Extensions` → `Management`.

Once these steps are complete, the editor is ready for use.

### Default Extensions

#### 1. Chat

Lets you talk to your LLM directly from the editor. You can ask for code
explanations, code suggestions, and edits.

You can access this from the left-side pane.

<img src="https://github.com/hnipun/aiide-docs/blob/main/images/image.005.png" alt=""/>

- You can select a Chat extension to run from the dropdown menu.
- In the `default` chat extension, the context sent to the LLM includes only the currently open tabs.
- You can manually add more context, such as additional files or folders using the `+ context` option.
- The `files` extension automatically determines the relevant context to include, ignoring open tabs and any manually
  added context.
- In both extensions, the last 1,000 lines of Terminal output are also included in the context sent to the LLM.

#### 2. Apply

Lets you review and apply code suggestions from the LLM. You can see a diff, accept the changes, or discard them with a
click.

<img src="https://github.com/hnipun/aiide-docs/blob/main/images/image.006.png" alt=""/>

When the chat provides a code suggestion, it appears inside a code block.
Each code block includes an `Apply` button:

- Click `Apply` to review a diff between your current file and the suggested code.
- Click `Accept` to apply the changes (the file will be updated) or `Reject` to discard the suggestion (in the diff
  view).
- If the file doesn’t exist, you’ll be prompted to create it.

#### 3. Autocomplete

Provides smart single-line suggestions as you type.

Works like most code editors: as you type, a suggestion popup appears, allowing you to pick from a list of
options. Open tabs are automatically used as context to provide more accurate suggestions. Press `Shift+Cmd+Space`
trigger autocomplete suggestions manually.

#### 4. Gray Code Completions

Shows inline ghost-text suggestions, single or multi-line, to help you complete code quickly.

Press `Ctrl + M` to trigger Gray Code completion in the editor.

- Press `Tab` to accept the suggestion.
- Press `Esc` to dismiss it.

### Extension Errors

<img src="https://github.com/hnipun/aiide-docs/blob/main/images/image.002.png" alt=""/>

If an extension encounters any errors during execution, they will appear under `Extensions` → `Errors`. It will
provide details such as error messages and stack traces to help you debug and resolve the issue.

### Running Extensions

<img src="https://github.com/hnipun/aiide-docs/blob/main/images/image.003.png" alt=""/>

Extensions that are currently running will be listed under `Extensions` → `Running`.
From this tab, you can:

- Terminate any active extension.
- Monitor progress, as extensions that send progress updates will display a progress bar here.
-

### Extension Updates and Notifications

If an extension sends an update, it will appear under `Extensions` → `Updates`.
If an extension sends a notification, it will be shown under `Extensions` → `Notifications`.

### Developing Your Own Extensions

To use your own set of extensions, create a directory named `extensions` at the root level of your project.
This will override all the default extensions, as the editor will use this directory as the extension path when
executing extensions.

The easiest way to get started is to copy
the [default extensions directory](https://github.com/hnipun/extensions/tree/main) into your project (top level) and
customize it as needed.

#### 1. config.yaml

All extension-related settings are defined in [config.yaml](https://github.com/hnipun/extensions/blob/main/config.yaml).
From this file, you can configure the main entry file and other settings for each extension.

<img src="https://github.com/hnipun/aiide-docs/blob/main/images/image.004.png" alt=""/>

Any errors in the `config.yaml` file will be displayed in the `Extensions` tab.

#### 2. Extension API

The [ExtensionAPI](https://github.com/hnipun/extensions/blob/main/common/api.py)
defines:

- The data passed from the editor to the extension.
- The utility functions available for extensions to interact with the editor.

Every extension’s main file must include a function with the following definition:

```python
def extension(api: ExtensionAPI):
    pass
``` 

This function is executed by the editor when the extension runs.

#### 3. `extensions/common` directory

The `extensions/common` directory is automatically added to the Python path when running an extension.
This allows you to import shared utilities, or settings directly into your extensions without needing relative
paths.

example:

```python
from common.api import ExtensionAPI
from common.diff import get_matches
from common.settings import LLM_PROVIDERS
```

#### 4. Debug Logs

During extension development, you can add debug logs using the [
`log`](https://github.com/hnipun/extensions/blob/32a86209fb968d1b157d72ef73e43d2a95452523/common/api.py#L234)  function
provided by the ExtensionAPI.

These logs are generated each time the extension runs.

To view the logs:

- Go to `View` → `Toggle Developer Tools`

- Or use the shortcut `Shift+Cmd+I` 
