Cucumber PlayWright HTML Reporter
=================================
A reporting module for Cucumber called Cucumber PlayWright HTML Reporter parses JSON output to create stunning reports with HTML and Excel format. The following features set this reporting module apart from all the others on the market:

- an overview of all features and scenarios that have been tested.
- an overview of the features that can accommodate numerous instances of the same feature or instances of the same feature on several browsers and/or devices.

- a searchable, filterable, and sortable features overview
- a feature overview including information about the browsers and/or devices utilised.

## Install
Install this module locally with the following command:

``` bash
npm i cucumberjs-playwright-reporter
```

Save to dependencies or dev-dependencies:

``` bash
npm i cucumberjs-playwright-reporter --save
npm i cucumberjs-playwright-reporter --save-dev
```

## Compatibility
Cucumber HTML Reporter **now works with CucumberJS 4+**.

## 
```javascript
const report = require('cucumberjs-playwright-reporter');

report.generate({
	jsonDir: './path-to-your-json-output/',
	reportPath: './path-where-the-report-needs-to-be/',
	metadata:{
        browser: {
            name: 'chrome',
            version: '100'
        },
        device: 'Local test machine',
        platform: {
            name: 'windows',
            version: '10'
        }
    },
    customData: {
        title: 'Run info',
        data: [
            {label: 'Project', value: 'Custom project'},
            {label: 'Release', value: '1'},
            {label: 'Cycle', value: 'B11221'},
            {label: 'Execution Start Time', value: 'Nov 19th 2021, 02:31 PM EST'},
            {label: 'Execution End Time', value: 'Nov 19th 2021, 02:56 PM EST'}
        ]
    }
});
```

> **IMPORTANT:**

> Make sure that, when you generate the JSON files with Cucumber, each file will have a **UNIQUE** name. If you don't provide a unique name Cucumber will **override** the JSON files.

> **Advice** is to use for example the name of the feature, the name of the browser / device it is running on AND a unix timestamp with for example this `(new Date).getTime();`. This will result in something like this `name_of_feature.chrome.1495298685509.json`

## Options
### `jsonDir`
- **Type:** `String`
- **Mandatory:** Yes

The directory that will hold all the generated JSON files, relative from where the script is started.

**N.B.:** If you use a npm script from the command line, like for example `npm run generate-report` the `jsonDir` will be relative from the path where the script is executed. Executing it from the root of your project will also search for the `jsonDir` from the root of you project.

### `reportPath`
- **Type:** `String`
- **Mandatory:** Yes

The directory in which the report needs to be saved, relative from where the script is started.

**N.B.:** If you use a npm script from the command line, like for example `npm run generate-report` the `reportPath` will be relative from the path where the script is executed. Executing it from the root of your project will also save the report in the `reportPath` in the root of you project.

### `staticFilePath`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

If true each feature will get a static filename for the html. Use this feature only if you are not running multiple instances of the same tests.

### `openReportInBrowser`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

If true the report will automatically be opened in the default browser of the operating system.

### `saveCollectedJSON`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

This module will first merge all the JSON-files to 1 file and then enrich it with data that is used for the report. If `saveCollectedJSON :true` the merged JSON **AND** the enriched JSON will be saved in the `reportPath`. They will be saved as:

- `merged-output.json`
- `enriched-output.json`

### `disableLog`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

This will disable the log so will **NOT** see this.

```shell
=====================================================================================
    Multiple Cucumber HTML report generated in:

    /Users/cucumber-html-reporter/.tmp/index.html
========================================================================
```
### `pageTitle`
- **Type:** `string`
- **Mandatory:** No
- **Default:** Multiple Cucumber HTML Reporter

You can change the report title in the HTML head Tag

### `reportName`
- **Type:** `string`
- **Mandatory:** No

You can change the report name to a name you want

### `pageFooter`
- **Type:** `string`
- **Mandatory:** No

You can customise Page Footer if required. You just need to provide a html string like `<div><p>A custom footer in html</p></div>`

### `plainDescription`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

The feature description is assumed to be a simple string and the library formats it accordingly, by copying it inside a
paragraph tag. Since the description can be any free text, it can also be as complex as a full `div`, e.g.:

```html
<div>
    <p><strong>Test description  </strong> : The test implements comparisons using all our datatypes</p>
    <p><strong>Expected result   </strong> : Device does not reset</p>
    <p><strong>Feature type      </strong> : Robustness</p>
    <p><strong>Comments          </strong> : Test covers comparison operators</p>
</div>
```

If the description already include formatting tags you can include it _as is_ by setting `plainDescription` to `true`.

### `displayDuration`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

If set to `true` the duration of steps, scenarios and features is displayed on the Features overview and single feature page in an easily readable format.
This expects the durations in the report to be in **nanoseconds**, which might result in incorrect durations when using a version of Cucumber(JS 2 and 3) that does not report in nanoseconds but in milliseconds. This can be changed to milliseconds by adding the parameter `durationInMS: true`, see below

> **NOTE: Only the duration of a feature can be shown in the features overview. A total duration over all features CAN NOT be given because the module doesn't know if all features have been run in parallel**

### `durationInMS`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

If set to `true` the duration of steps will be expected to be in **milliseconds**, which might result in incorrect durations when using a version of Cucumber(JS 1 or 4) that does report in **nanoseconds**.
This parameter relies on `displayDuration: true`

### `hideMetadata`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

If set to `true` metadata Devicetype, Device, OS, App, Browser are not being displayed in the Features overview.

### `displayReportTime`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

If set to `true` the date and time at which the JSON-files were generated, is displayed on the Features overview.

### `useCDN`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

If you prefer, you can use CDN for assets.

### `customStyle`
- **Type:** `path`
- **Mandatory:** No

If you need to add some custom style to your report. Add it like this `customStyle: 'your-path-where/custom.css'`.
Please note that the doughnut charts uses the same colors as used by the status icons, i.e. the `.*-color` classes.
Refer to the `test` directory and the `embedded-array` test report for a complete color customization example.

### `overrideStyle`
- **Type:** `path`
- **Mandatory:** No

If you need to replace completely the default style for your report. Add it like this `overrideStyle: 'your-path-where/custom.css'`
Please refer to the `test` directory for an example.

### `metadata`
- **Type:** `JSON`
- **Mandatory:** No

Print more data to your report, such as browser name + version, platform name + version and your environment. The values need to meet some predefined data, see [Metadata](./README.MD#metadata) for more info.
Data can be passed like below.

> **If you already have metadata in your JSON then the metadata in the JSON will take precedence**

```js
metadata:{
    browser: {
        name: 'Chrome',
        version: '100'
    },
    device: 'Local test machine',
    platform: {
        name: 'Windows',
        version: '10'
    }
}
```

See [metadata](./README.MD#metadata-1) for more info

### `customMetadata`
- **Type:** `boolean`
- **Default:** `false`
- **Mandatory:** No

It is possible to provide custom metadata by setting this variable to `true`. Custom metadata will override the regular metadata completely and potentially have strange formatting bugs if too many (10+) variables are used.
The columns will be in the order defined by the order of the list.

Adding the metadata is done in the same way as with normal metadata. The metadata is formed as a list of key-value pairs to preserve order:

```js
metadata: [
        {name: 'Environment v.', value: '12.3'},
        {name: 'Plugin v.', value: '32.1'},
        {name: 'Variable set', value: 'Foo'}
    ]
```

On the features overview page the custom metadata is shown like:
![Snapshot - Features overview custom metadata](./docs/images/features-custom-metadata.jpg "Snapshot - Features overview custom metadata")

>**IMPORTANT:**
> This does not work correctly if features have different sets of metadata. Try to avoid this situation.

> **If you already have metadata in your JSON then the metadata in the JSON will take precedence**

### `customData`
- **Type:** `object`
- **Mandatory:** No

You can add a custom data block to the report like this

![Snapshot - Features overview custom data](./docs/images/custom-data.jpg "Snapshot - Features overview custom data")

```js
customData: {
    title: 'Run info',
    data: [
        {label: 'Project', value: 'Custom project'},
        {label: 'Release', value: '1'},
        {label: 'Cycle', value: 'B11221'},
        {label: 'Execution Start Time', value: 'Nov 19th 2021, 02:31 PM EST'},
        {label: 'Execution End Time', value: 'Nov 19th 2021, 02:56 PM EST'}
    ]
}
```

#### `customData.title`
- **Type:** `string`
- **Mandatory:** No
- **Default:** `Custom data title`

Select a title for the custom data block. If not provided it will be defaulted.

#### `customData.data`
- **Type:** `array`
- **Mandatory:** yes

The data you want to add. This needs to be in the format

```js
data: [
    {label: 'your label', value: 'the represented value'}
]
```

## Metadata
The report can also show on which browser / device a feature has been executed. It is shown on the features overview in the table as well as on the feature overview in a container.

### Adding metadata to the Cucumber JSON

To be able to see this you will need to add the following to the Cucumber JSON before you save it.


```javascript
// This represents the Cucumber JSON file that has be retrieved
const cucumberJSON;

const metadata = {
	"browser": {
		"name": "chrome",
		"version": "100"
	},
	"device": "string",
	"platform": {
		"name": "Windows",
		"version": "10.12"
	}
}

// Add it with for example
cucumberJSON[0].metadata = metadata;

// Now save the file to the disk
```

### `metadata.app.name`
- **Type:** `string`

**e.g.:** The name of the app.

### `metadata.app.version`
- **Type:** `string`

**e.g.:** The version of the app.

### `metadata.browser.name`
- **Type:** `string`
- **Possible values:** `internet explorer | edge | chrome | firefox | safari`

> If no correct value is provided the `?`-icon with the text `not known` is shown

### `metadata.browser.version`
- **Type:** `string`

**e.g.:** The version of the browser, this can be added manual or retrieved during the execution of the tests to get the exact version number.

>If no correct value is provided the `?`-icon with the text `not known` is shown

### `metadata.device`
- **Type:** `string`

**e.g.:** A name that represents the type of device. For example, if you run it on a virtual machine, you can place it here `Virtual Machine`, or the name of the mobile, like for example `iPhone 7 Plus`.

> If no correct value is provided the `?`-icon with the text `not known` is shown

### `metadata.platform.name`
- **Type:** `string`
- **Possible values:** `windows | osx | linux | ubuntu | android | ios`

> If no correct value is provided the `?`-icon with the text `not known` is shown

### `metadata.platform.version`
- **Type:** `string`

**e.g.:** The version of the platform

>If no correct value is provided the `?`-icon with the text `not known` is shown

### Metadata example features overview
![Snapshot - Features overview browser / device info](./docs/images/overview-metadata.jpg "Snapshot - Features overview browser / device info")

### Metadata example scenario with and without known data
![Snapshot - Scenario browser / device info](./docs/images/scenario-browser-metadata.jpg "Snapshot - Scenario browser / device info")
![Snapshot - Scenario app / device info](./docs/images/scenario-app-metadata.jpg "Snapshot - Scenario app / device info")
![Snapshot - Scenario browser / device info not known](./docs/images/scenario-no-metadata.jpg "Snapshot - Scenario browser / device info not known")

## FAQ
### Only 1 report is shown in the features overview table
It could be that the name of the Cucumber JSON file that has been saved is not unique (enough).

My advice is to use for example:

- the name of the feature
- the name of the browser / device it is running on
- a unix timestamp with for example this `(new Date).getTime();`

This will result in something like this `name_of_feature.chrome.1495298685509.json`.

The advantage of this is that when you look at the folder where the Cucumber JSON-files are saved you can see:

- the features that have been executed
- on which browser
- a timestamp to see which feature has been executed the last (if featurename and browser are the same)

### Metadata shows `not known` or not the correct icons
There could be 2 causes:

 1. The metadata has not (correctly) been added to the Cucumber JSON.
 2. The `metadata.browser.name` or `metadata.platform.name` can't be mapped to the right icon

To fix this see the part about **Metadata** and check the **possible values**.

### How to attach Screenshots to HTML report
You can attach screenshots at any time to a Cucumber JSON file. Just create a Cucumber `scenario`-hook that will handle this. You can add them during running or when a `scenario` failed.

> Check the framework you are using to attach screenshots to the JSON file.

### How to attach Plain Text to HTML report
You can attach plain-text / data at any time to a Cucumber JSON file to help debug / review the results. You can add them during running or when a `scenario` failed.

> Check the framework you are using to attach plain text to the JSON file. Please make sure to convert binary/non-readable data to a suitable textual representation, e.g. via Base64 encoding.

### How to attach pretty JSON to HTML report
You can attach JSON at any time to a Cucumber JSON file. You can add them during running or when a `scenario` failed.

> Check the framework you are using to attach JSON data to the JSON file.

## Changelog and Releases

## Contributing
How to contribute can be found [here](./docs/CONTRIBUTING.md)

## Credits
In the search for a reporting tools for Cucumber I found a few tools that helped me a lot:
(https://github.com/wswebcreation/multiple-cucumber-html-reporter/releases)
(https://github.com/LennDG)
