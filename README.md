# codeceptjs-cucumber-json-reporter

### CodeceptJS plugin to generate cucumber json output file to be consumed by cucumber-html-reporter or similar packages
---
## Requirements
- CodeceptJS v3.0.5 or higher
---

## Installation
```
npm i codeceptjs-cucumber-json-reporter
```

---
## Configuration

- Add plugin in your `codecept.conf.js`
```
plugins: {
    cucumberJsonReporter: {
      require: 'codeceptjs-cucumber-json-reporter',
      enabled: true,
    },
}
```

---
## Usage

When the plugin is enabled, run your test as you normally would (parallelized runs not tests).

The plugin parses the BDD feature file before the start of each feature and generates the report structure. Once the test starts, it uses event listeners to add runtime data such as step status (pass/fail), screenshot embeddings, comment embeddings, and errors.

- Attach screenshots to your report by using `I.saveScreenshot` method on the available helpers.
- Attach comments to your report by using `I.say` method in codeceptjs for logging comments.


`cucumber_output.json` generated in your output folder on run completion.

Some additional logging added when running `--verbose` to debug potential issues

---
## Html Report

Use `cucumber-html-reporter` or other similar html reporters to generate your pretty html report using the `cucumber_output.json` file.

---
## Limitations
- CodeceptJS treats BDD steps as metasteps. Therefore if your step definition does not contain any helper methods it only fires bddStep events which are limited in what information we can extract.
- Not tested with parallelized/multiple worker runs