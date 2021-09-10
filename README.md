# @vscode/test-web

![Test Status Badge](https://github.com/microsoft/vscode-test-web/workflows/Tests/badge.svg)

This module helps testing [VS Code web extensions](https://code.visualstudio.com/api/extension-guides/web-extensions) locally.

The node module runs a local web server that serves VS Code for the browser including the extensions located at the given local path. Additionally the extension tests are automatically run.

The node module providers a command line as well as an API.

## Usage

Via command line:

Test a web extension in a browser:

```sh
vscode-test-web --browserType=chromium --extensionDevelopmentPath=$extensionLocation
```

Run web extension tests:

```sh
vscode-test-web --browserType=chromium --extensionDevelopmentPath=$extensionLocation --extensionTestsPath=$extensionLocation/dist/web/test/suite/index.js
```


Via API:

```ts
async function go() {
	try {
		// The folder containing the Extension Manifest package.json
		const extensionDevelopmentPath = path.resolve(__dirname, '../../../');

		// The path to module with the test runner and tests
		const extensionTestsPath = path.resolve(__dirname, './suite/index');

		// Start a web server that serves VSCode in a browser, run the tests
		await runTests({ browserType: 'chromium', extensionDevelopmentPath, extensionTestsPath });
	} catch (err) {
		console.error('Failed to run tests');
		process.exit(1);
	}
}

go()
```

CLI options:
```
  --browserType 'chromium' | 'firefox' | 'webkit': The browser to launch
  --extensionDevelopmentPath path. [Optional]: A path pointing to a extension to include.
  --extensionTestsPath path.  [Optional]: A path to a test module to run
  --version. 'insiders' (Default) | 'stable' | 'sources' [Optional]
  --open-devtools. Opens the dev tools  [Optional]
  --headless. Whether to show the browser. Defaults to true when an extensionTestsPath is provided, otherwise false. [Optional]
  folderPath. A local folder to open VS Code on. The folder content will be available as a virtual file system`

```

Corrsponding options are available in the API.


The `folderPath` argument allows to work on existing files.
VS Code for the browser will open an a virtual file system ('vscode-test-web://mount') where the files of the local folder will served.
The file system is read/write, but modifications are stored in memory and not written back to disk.

```sh
vscode-test-web --browserType=chromium --extensionDevelopmentPath=$extensionLocation --extensionTestsPath=$extensionLocation/dist/web/test/suite/index.js $testWorkspaceFolder
```


## Development

- `yarn install`
- Make necessary changes in [`src`](./src)
- `yarn compile` (or `yarn watch`)

- run `yarn sample` to launch VS Code Browser with the `sample` extension bundled in this repo.

- run `yarn sample-tests` to launch VS Code Browser running the extension tests of the  `sample` extension bundled in this repo.


## License

[MIT](LICENSE)

## Contributing

This project welcomes contributions and suggestions. Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
