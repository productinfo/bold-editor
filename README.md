# Bold Editor

The Bold Editor is a Standard Notes derived editor that offers text formatting and FileSafe integration.

![Over 21 different text formatting features are available.](editor_bar.png)

## Quickstart

Quickly see the editor in action via the browser. Note that FileSafe integration is not supported.  

1. Clone the [bold-editor](https://github.com/standardnotes/bold-editor) repository from GitHub.
   
2. Run `npm install` to install required dependencies.
   
3. Edit `app/index.html` for use locally:
   - comment out lines under 'Production'
   - uncomment lines under 'Development'

    ```html
    <!-- Development -->
    <script type="text/javascript" src="redactor.min.js"></script>
    <script type="text/javascript" src="app.min.js"></script>

    <!-- Production -->
    <!--<script type="text/javascript" src="dist.min.js"></script>-->
    ```

5. Use the webpack-dev-server via `npm run start` and open the browser to visit `localhost:8080` where the app will be running.

## Local Installation

Get a full working copy of the editor (with FileSafe) for development. 

1. Clone the [bold-editor](https://github.com/standardnotes/bold-editor) and [filesafe-embed](https://github.com/standardnotes/filesafe-embed) repositories from GitHub.

2. Ensure that either the Standard Notes desktop app is available for use or the web app is accessible. Use both locally or with an Extended account (or the extension will not load).

3. In the `bold-editor` folder, edit the `package.json` file under `devDependencies` to use the local `filesafe-embed`:
    ```json
    "filesafe-embed": "~/folder_with_both_repositories/filesafe-embed",
    ```

4. Run `npm install` in both the `bold-editor` and `filesafe-embed` folders to install the required dependencies. 
   - If there are errors, delete the `package-lock.json` file and `node_modules` folder. Then run `npm install` again. This is equivalent to "turning it off and on again" for npm. ([source](https://stackoverflow.com/questions/48298361/npm-install-failed-at-the-node-sass4-5-0-postinstall-script))

5. Edit `index.html` for use locally:
   - comment out lines under 'Production'
   - uncomment lines under 'Development'

6. Run `npm install -g http-server` to install a simple local server to host the extension.
7. Choose between webpack Watch Mode and webpack-dev-server for development and follow the corresponding instructions.

## Development with webpack Watch Mode

Start by following the instructions here: https://docs.standardnotes.org/extensions/local-setup

This will setup a local server from which the bold-editor can be imported via the desktop app or the web app. You should be able to use the bold-editor now.

However, this will not allow for easy development because the app will not automatically build to the dist folder. We will use webpack for this.

1. In the `package.json` file, under `scripts`, add the following line:

    ```json
    "watch": "webpack --watch"
    ```
    (Additional webpack documentation can be found [here](https://webpack.js.org/guides/development/#using-watch-mode))

2. Use `npm run watch` to automatically build files.
   - There should be an existing console open that is running  `http-server`
   - Open a new console for `npm run watch`

3. Disable the cache on the desktop app/web app.
   - We want to ensure that the latest build is always loaded when the app is refreshed
   - Open devtools (`Ctrl+Shift+i`) and go to `Network`
   - Check `Disable cache`
   - On some systems, devtools must be kept open for this to work

4. Make some changes to `Editor.js`, reload the desktop or web app, and your changes will show up.

## Development with webpack-dev-server

*Note that this method only actively builds `app.min.js`.*

The steps are similar to the webpack Watch Mode, differences are listed below:

- The `ext.json` file belongs in the `dist` folder
- Update the url to `http://localhost:8080`
- `npm run start` to use the webpack-dev-server.

Disable the cache as in the webpack Watch Mode. Reload may be required to see changes in action.

## Production

In production environments, check that the `index.html` file is configured as follows: 

```html
<!-- Development -->
<!-- <script type="text/javascript" src="redactor.min.js"></script>
<script type="text/javascript" src="app.min.js"></script> -->

<!-- Production -->
<script type="text/javascript" src="dist.min.js"></script>
```

`dist.min.js` is built via `grunt`.

The CSS is also built with grunt, so webpack-dev-server will not be able to reload it. You must run `npm run build` anytime you change the CSS.

## Support

Please open a new issue and the Standard Notes team will take a look as soon as we can. For more information on editors, refer to the following link:

- Standard Notes Help: [What are editors?](https://standardnotes.org/help/77/what-are-editors)

Known issue: ordered lists, unordered lists, and tables seem to ignore any font preference you apply to it.

## License

[GNU AGPL v3.0](https://choosealicense.com/licenses/agpl-3.0/)