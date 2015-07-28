# Html-Chat-SDK

### What is the BoldChat HTML Chat Window SDK?
The BoldChat HTML SDK allows businesses to create and host a fully customized chat window. The HTML Chat Window SDK is a collection of HTML, JavaScript and CSS files that allow you to create a completely customized chat user interface, facilitating communication between the visitor and operator.

## What does this repository contain?
The SDK is bundled with template themes that you can use as a base for further customization.

The zip file in this repository contains two versions of each included theme:
 - A non-minified and non-compressed version. The included HTML files reference the raw JavaScript and CSS files.
 - A production ready, minified and compressed version. The included HTML files are minified and reference the compressed, minified and consolidated JavaScript and CSS files.

### Examples of currently available themes

> ####Nightshade####
![nightshadelayout](http://logmein-boldchat.github.io/Html-Chat-Sdk/NightshadeLayout.jpg)

----------

> ####Hubris####
![hubrislayout](http://logmein-boldchat.github.io/Html-Chat-Sdk/HubrisLayout.gif)

----------

> ####Lovato####
![lovatolayout](http://logmein-boldchat.github.io/Html-Chat-Sdk/LovatoLayout.gif)

## Supported browsers/platforms:

 1. Chrome
 2. Internet Explorer 9 or newer
 3. Firefox
 4. iOS (current and previous version)
 5. Android (current and previous version)

## Getting Started
1) Clone or download this repository and add it to your web site.

2) Generate an API key in the Boldhat Client. For more information see [BoldChat Help](http://help.boldchat.com/help/BoldChat/c_bc_sdk_get_sdk.html)

3) Modify the scripts/bc-config.js file in the HTML SDK. Change the sessionApiKey value to the API key you generated in the BoldChat client.

4) Add 3 javascript tags to your page.
```html
<script type="text/javascript" src="scripts/bc-util.js"></script>
<script type="text/javascript" src="scripts/bc-config.js"></script>
<script type="text/javascript" src="scripts/bc-sdk-start.js"></script>
```

5) If you do not already have a BoldChat button on your page, you must generate one in the BoldChat client and add the HTML snippet to your web site. For detailed instructions on chat button setup please see [BoldChat Help](http://help.boldchat.com/help/current/BoldChat/c_bc_setupguide_header.html).

6) When the BoldChat button or invitation is clicked, the HTML SDK will be launched instead of the default BoldChat window.


## Changing Themes

Modify scripts/bc-config.js to change the theme of your chat window. The chatWindowUrl variable defines the theme used. Change the value to the theme path of your choice, for instance "themes/hubris".

## Building from source

These files are built using [NPM](https://nodejs.org/) & [Gulp](http://gulpjs.com/). You must install NodeJs as well as gulp. 

The SDK bundle comes with three files to get you started with the build process:
 - gulpfile.js
 - gulpfile.config.js
 - package.json:
 
The package.json file contains a scripts object that provides various build options. However, if this is your initial build, we suggest you run the following command to download everything necessary for your project:
```javascript
npm run build
```
This is the equivalent of running:
```javascript
npm install && gulp
```
####gulp Build Options

 - **build-requirements** :
	 - **fonts**: Copies all font files to their respective location in the output directory.
	 - **images**: Optimizes and copies all images to their respective location in the output directory.
	 - **videos**: Copies all videos to their respective location in the output directory.
	 - **sass**: Processes all scss files and generates the appropriate CSS in their respective theme, then places them in their respective location in the output directory.
	 - **minify-all-js**: See below.
 - **minify-all-js**: Depending on build arguments, this option minifies, uglifies or concatenates the JavaScript files according to their usage, then places them in their respective location.
	 - **minify-theme-js**: Theme js files are optional that serve to override existing functionality.
	 - **minify-boldchat-js**: Boldchat js files are the core HTML SDK files, used by both Popup and Layered Chat Windows. 
	 - **minify-start-js**: Place Start js files on your existing site/page where you want to use the HTML SDK Chat Window. These files include the utility functions used by the other files, the configuration files as well as a start-sdk file that handles the opening of the windows themselves.
	 - **minify-popup-js**: These files are used exclusively by Popup Windows. The minify-start-js files are included besides the necessary popup file.
 - **html-process-only**: Our gulp process uses gulp-inject as a means to build the appropriate output files. Each theme can be opened in either a layered or popup window mode. To prevent duplication of effort on developments part, the popup.html files (under each theme) are created at build time. The 'template' for each popup is the index.html file under each theme. For example, building html-process-only would take the themes/hubris/index.html file and extract the html to build the themes/hubris/popup.html file. 
	 - **inject-index-html**: Injects the necessary JavaScript and CSS files into their appropriate tag placeholders, depending on build arguments.
	 - **inject-popup-html**: Injects the necessary JavaScript and CSS files into their appropriate tag placeholders, depending on build arguments. It also copies the index.html and inserts into appropriate place in popup.html
 - Running the default gulp task executes 'build-requirements', 'html-process-only' and finally 'js-doc'. 
	 - **js-doc**: Creates a help document from the JavaScript files.

####There are various gulp arguments you can pass to the gulp build process:
- **--verbose**: Lists the files affected by each task.
- **--prod**: Creates concatenated versions of the JavaScript/CSS files and sets the proper reference in the HTML files.
	- For example, the index.html file includes various comment tags used by the build process, such as:
		- `<!-- inject:boldchat:js -->`
		- The HTML build processes (inject-index and inject-popup) check whether the --prod argument has been passed. If so, the getBoldchatJsSource function retrieves the source files (js_bc) to be used as the gulp source, and builds a final concatenated file named boldchat.js, resulting in a single JavaScript file instead of nine.
- **--min**: Used in conjuction with the --prod argument to further minify JavaScript and CSS files.
- **--minhtml**: Minifies the HTML file(s).


## Additional Info:

#### Technically Speaking...

 - While the bc-config.js file sets all the configuration information, it is also possible to override these settings on each page. For instance, you may need to use a different API key, theme and window type on different pages. To accomplish this, add the following snippet to each page to override bc-config options:
```javascript
<script type="text/javascript">
	window._bcChatWindowUrl = 'themes/{theme name here}';
	window._bcSessionApiKey = '{your api key here}';
	window._bcForcePopup = false; 
</script>
```

**Important**: The snippet must be placed before the bc.config.js file reference.

As an alternative method, you can also set up a different bc-config file for each page.

##### Layered vs Popup Windows
There is a certain hierarchy associated with how a window is opened. Window Definitions are determined by the API Key. Learn more about the Chat Window Definition on [our help site](http://help.boldchat.com/help/BoldChat/c_bc_chatwindow_about.html).
