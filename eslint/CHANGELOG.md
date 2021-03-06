### 1.2.6

#### Fixes:

- [Do not always run eslint from the project's root directory](https://github.com/Microsoft/vscode-eslint/issues/196)
- [baseDir should be an absolute path](https://github.com/Microsoft/vscode-eslint/issues/202)


### <a name="RN125"></a>1.2.5

- Validdating a single file (no workspace folder open) will set the working directory to the directory containing the file.
- Added support for working directories. ESLint resolves configuration files relative to a working directory. This new settings allows users to control which working directory is used for which files. Consider the following setups:

```
client/
  .eslintignore
  .eslintrc.json
  client.js
server/
  .eslintignore
  .eslintrc.json
  server.js
```

Then using the setting:
```json
  "eslint.workingDirectories": [
    "./client", "./server"
  ]
```
will validate files inside the server directory with the server directory as the current working directory. Same for files in the client directory. If the setting is omitted the working directory is the workspace folder.


### 1.2.4

- fixes [.eslintignore is completely ignored](https://github.com/Microsoft/vscode-eslint/issues/198)
- reverted fix for [Does not respect nested eslintignore files](https://github.com/Microsoft/vscode-eslint/issues/111) since it broke the use case of a single global .eslintrc file

### 1.2.3

- Bug fixes:
  - [Does not respect nested eslintignore files](https://github.com/Microsoft/vscode-eslint/issues/111)
  - [eslintrc configuration cascading not being honored ](https://github.com/Microsoft/vscode-eslint/issues/97)
  - [autoFixOnSave not working with eslint.run=onSave](https://github.com/Microsoft/vscode-eslint/issues/158)
  - [autoFixOnSave not listed under Settings Options in Readme](https://github.com/Microsoft/vscode-eslint/issues/188)

### 1.2.2

- Added configuration options to enable code actions and auto fix on save selectively per language. In release 1.2.1 code actions and auto fix on save very still only
available for JavaScript. In 1.2.2 you can now enable this selectively per language. For compatibility it is enabled by default for JavaScript and disabled by default for all
other languages. The reason is that I encounter cases for non JavaScript file types where the computed fixes had wrong positions resulting in 'broken' documents. To enable it simply
provide an object literal in the validate setting with the properties `language` and `autoFix` instead of a simple `string`. An example is:
```json
"eslint.validate": [ "javascript", "javascriptreact", { "language": "html", "autoFix": true } ]
```

### <a name="RN121"></a>1.2.1

- Added support to validate file types other than JavaScript. To enable this, you need to do the following:
  - Configure ESLint with an additional plugin to do the actual validation. For example, to validate HTML files install
`eslint-plugin-html` using `npm install eslint-plugin-html --save-dev` and update the eslint configuration (e.g. .eslintrc.json file)
with `"plugin": [ "html" ]`.
  - Add the corresponding language identifier to the `eslint.validate` setting. Something like `"eslint.validate": [ "javascript", "javascriptreact", "html" ]`.
If the setting is missing, it defaults to `["javascript", "javascriptreact"]`

Please note that code actions and auto fix on save is still only available for JavaScript. The reason is that I detected position problems with fixes contributed by plugins
resulting in broken source code when applied.

### 1.1.0

- Supports more than one ESLint module installation in a workspace. This eases working with typical client / server setups where ESLint is installed
in a `node_modules` folder in the `server` and the `client` directory.
- Improved error handling if a plugin can't be loaded.
- Added commands to enable and disable ESLint.

### 1.0.8

- Supports auto fix on save. Needs to be enabled via `"eslint.autoFixOnSave": true`. Please note that auto fix on save will only happen
if the save happened manually or via focus lost. This is consistent with VS Code's format on save behaviour. Auto fix on save requires
VS Code version 1.6 or newer.

### 1.0.7

- Fixed problem with validating package.json when editing .eslintrc.* files.

### 1.0.5

- Moving to official 2.5.0 language server libraries.

### 1.0.4

- Bug fixing: eslint is validating package.json files

### 1.0.3

- Errors in configuration files are only shown in a status message if the file is not open in the editor. Otherwise message are shown in the output channel only.

### 1.0.2

- Added a status bar item to inform the user about problems with ESLint. A message box only appears if the user attention is required.
- Improved handling of missing corrupted configuration files.
- The ESLint package is now loaded from parent folders as well.
- Added an action to create a .eslintrc.json file.
