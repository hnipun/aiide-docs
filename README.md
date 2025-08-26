# notbadaiide v0.9.3

## Download

Use the link below to download the app:

[notbadaiide v0.9.3](https://drive.google.com/file/d/15y4yP5h8VkHg-PVIqQN9Tr3zKMpTOaip/view?usp=sharing)

After downloading, unzip the file and run the following command in your terminal (replace the path with the actual
location of the app file):

```bash
xattr -dr com.apple.quarantine /path/to/ai-editor-v0.9.3app
```

## Code Editor

The code editor supports shortcuts similar to VS
Code. [Here](https://github.com/hnipun/aiide-docs/blob/main/code_editing_shortcuts.md)’s a list of the most popular
ones.

## Terminal

To reset the terminal (clearing both the display and back-scroll history), click the Reset button.

## Extensions

### Default Extensions

Extensions are Python scripts that enable interactions with LLMs, such as chat, code apply, autocomplete, gray
completions etc. Users can create their own extensions, which the editor will manage and execute (explained in a later
section).

#### Setup

- When the editor is launched for the first time, the default extensions will be downloaded to `~
  /.notbadaiide/extensions/.`
- This can be verified by navigating to `Extensions` (left side pane) → `Management` and checking the
  `Extensions Repository`. It should display the downloaded.
- The user also needs to configure the `Python Path` and `API Key` under `Extensions` → `Management`.

Once these steps are complete, the editor is ready for use.

#### Types

##### Chat

The user can access this from the left-side pane.

- By default, the context sent to the LLM includes only the tabs that are currently open.
- However, the user can also select additional files or folders using the `+ context` option.
- Terminal content (last 1000 lines) is also included in the context sent to the LLM.

##### Apply

Whenever the chat provides a code suggestion, it appears inside a code block.
Each code block includes an Apply button:

- Click Apply to review a diff between your current file and the suggested code.
- If the file doesn’t exist, you’ll be prompted to create it.

##### Autocomplete

Works like most code editors: as user type, a suggestion popup appears, allowing user to pick from a list of
options. Open tabs are automatically used as context to provide more accurate suggestions.

##### Gray Code Completions

Press `Ctrl + M` to trigger Gray Code completion in the editor.

- Press `Tab` to accept the suggestion.
- Press `Esc` to dismiss it.

