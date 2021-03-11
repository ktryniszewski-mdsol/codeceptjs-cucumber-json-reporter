# codeceptjs-cucumber-json-reporter
## Description

A [CodeceptJS](https://codecept.io) plugin to generate a cucumber json output file that can be consumed by [cucumber-html-reporter](https://www.npmjs.com/package/cucumber-html-reporter) or similar packages

---
## Requirements
- CodeceptJS v3 or higher (tested with 3.0.5)
---

## Installation
```
npm i codeceptjs-cucumber-json-reporter
```

---
## Configuration

- Add plugin to your `codecept.conf.js`
```
...
plugins: {
    cucumberJsonReporter: {
      require: 'codeceptjs-cucumber-json-reporter',
      enabled: true,
      attachScreenshots: true,       // true by default
      attachComments: true,          // true by default
      outputFile: file.json,         // cucumber_output.json by default
    },
}
...
```

---
## Usage

When the plugin is enabled, run your test as you normally would (parallelized runs not tested).

The plugin parses the BDD feature file before the start of each feature and generates the report structure. Once the test starts, it uses event listeners to add runtime data such as step status (pass/fail), screenshot embeddings, comment embeddings, and errors.

- Attach screenshots to your report by using `I.saveScreenshot` method in your steps
- Attach comments to your report by using `I.say` method in your steps


`cucumber_output.json` generated in your output folder on run completion.

Some additional logging added when running `--verbose` to debug potential issues

---
## Html Report

Use [cucumber-html-reporter](https://www.npmjs.com/package/cucumber-html-reporter) or other similar html reporters to generate your pretty html report passing the `cucumber_output.json` file as your source file.

---
## Limitations
- CodeceptJS treats BDD steps as metasteps. Therefore if your step definition does not contain any helper methods it only fires bddStep events which are limited in what information we can extract.
- Not tested with parallelized/multiple worker runs