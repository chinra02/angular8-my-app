# Angular8MyApp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 8.0.3.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

## Custom-webpack

In order to use a custom webpack config, we’ll need the @angular-builders/custom-webpack dependency. Add it to your project as a devDependency like so:

$ npm i @angular-builders/custom-webpack -D
We can then install moment to our project and import this into our project:

$ npm i moment --save
Custom webpack Configuration
We can then create a custom webpack configuration that rips out any locales that we don’t specifically choose to keep.

Inside of the root of your project, create a new file named custom-webpack.config.js with the following:

const MomentLocalesPlugin = require('moment-locales-webpack-plugin');

module.exports = {
  plugins: [
    new MomentLocalesPlugin({
      localesToKeep: ['de']
    })
  ]
};

This requires us to install the moment-locales-webpack-plugin:

$ npm i moment-locales-webpack-plugin -D
Adding this to angular.json
Afterwards, we need to configure angular.json to use this new configuration. Inside of the architect/build object, update the builder from @angular-devkit/build-angular:browser to @angular-builders/custom-webpack:browser and add the customWebpackConfig key:

"architect": {
  "build": {
    "builder": "@angular-builders/custom-webpack:browser",
    "options": {
      "customWebpackConfig": {
        "path": "./custom-webpack.config.js",
        "replaceDuplicatePlugins": true
      }
    }
  }
}
Custom webpack Configuration When Using ng serve
This is all we need to do if we only want our final, built, application to use the webpack config. However, if we wanted to test this config while using ng serve, we have one more thing to do.

Install the @angular-builders/dev-server custom web server from within npm:

$ npm i @angular-builders/dev-server -D
We can then update this inside of serve/builder in the angular.json file:

"serve": {
  "builder": "@angular-builders/custom-webpack:dev-server"
}

## Github deployment

First install the angular-cli-ghpages globally:

$ npm install -g angular-cli-ghpages
Now use the Angular CLI with the --base-href flag to build your project and set the correct base href location:

$ ng build --prod --base-href "https://<user-name>.github.io/<repo>/"
Then it’s as simple as running angular-cli-ghpages. You can use the ngh shorthand:

$ ngh


