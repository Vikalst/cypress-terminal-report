# Cypress terminal report

[![Build Status](https://travis-ci.com/archfz/cypress-terminal-report.svg?branch=master)](https://travis-ci.com/archfz/cypress-terminal-report)

Plugin for cypress that adds better terminal output __when tests fail__
on the terminal for better debugging. Prints cy commands, console.warn, 
console.error and request response data captured with cy.route. 

> Note: If you want to display the logs when test succeed as well then check the
[options](#options) for the support install.

> Note: Currently logs do not appear in the dashboard. If you want to see them go
to your CI runner and check the pipeline logs there.

![demo](https://raw.githubusercontent.com/archfz/cypress-terminal-report/master/demo.png)

## Install

1. Install npm package.
    ```bash
    npm i --save-dev cypress-terminal-report
    ```
2. Register the output plugin in `cypress/plugins/index.js`
    ```js
    module.exports = (on) => {
       require('cypress-terminal-report').installPlugin(on);
    };
    ```
3. Register the log collector support in `cypress/support/index.js`
    ```js
    require('cypress-terminal-report').installSupport();
    ```

## Options

Options for the plugin install: `.installPlugin(on, options)`:
- `options.defaultTrimLength` - default: 200; max length of cy.log and console.warn/console.error.
- `options.commandTrimLength` - default: 600; max length of cy commands.
- `options.routeTrimLength` - default: 5000; max length of cy.route request data.
- `options.logToFile` - default: false; log output to a file instead of console.
- `options.logFile` - default: 'cypress-terminal-report.log'; name for log file.

Options for the support install: `.installSupport(options)`:
- `options.printLogs` - default: null; possible values: null, 'always' - When set to always
logs will be printed for successful test as well as failing ones.
- `printConsoleInfo` - default: null; possible values: null, true - When true `console.log()` 
and `console.info()` logs will also be printed to the terminal, besides warn and error.
    
## Release notes

#### 1.1.0

- Added notice for logs not appearing in dashboard. from [issue](https://github.com/archfz/cypress-terminal-report/issues/8)
- Added [support for logging](#options) console.info and console.log. in [issue](https://github.com/archfz/cypress-terminal-report/issues/12) 
- Added better logging of cy.requests. in [issue](https://github.com/archfz/cypress-terminal-report/issues/12) by [@zhex900](https://github.com/zhex900)

#### 1.0.0

- Added tests and CI to repository.
- Added support for showing logs even for successful tests. in [issue](https://github.com/archfz/cypress-terminal-report/issues/3) by [@zhex900](https://github.com/zhex900)
- Fixed issue with incorrectly labeled failed commands. in [issue](https://github.com/archfz/cypress-terminal-report/issues/3) by [@zhex900](https://github.com/zhex900)
- Fixed issue with logs from cy.route breaking tests on XHR API type of requests. [merge-request](https://github.com/archfz/cypress-terminal-report/pull/1) by [@zhex900](https://github.com/zhex900)
