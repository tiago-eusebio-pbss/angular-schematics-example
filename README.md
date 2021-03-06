# order-wizard

This repository is a basic Schematic implementation that serves as a starting point to create and publish Schematics to NPM.

The package is called `order-wizard` and contains a schematic with the same name: `order-wizard`.

For concepts regarding the schematics, refer to [CONCEPTS.md](https://github.com/tiago-eusebio-pbss/angular-schematics-example/blob/main/CONCEPTS.md "Concepts").
For a Pluralsight course about schematics, refer to [Building Reusable Angular Components Using Schematics](https://app.pluralsight.com/library/courses/building-reusable-angular-components-schematics/table-of-contents "Building Reusable Angular Components Using Schematics").

### Requirements

* **Node.js:** download installer [from the website](https://nodejs.org/en/ "Node.js")
* **Angular CLI:** `$ npm install -g @angular/cli`
* **Schematics CLI:** `$ npm install -g @angular-devkit/schematics-cli`

### Testing

To test locally, install `@angular-devkit/schematics-cli` globally and use the `schematics` command line tool. That tool acts the same as the `generate` command of the Angular CLI, but also has a debug mode.

Check the documentation with:
```bash
schematics --help
```

Run the schematic with:
```bash
rimraf -Force test-thing
npm run build
schematics .:order-wizard --name="testThing"
```

This will run the schematic without making changes to files (dry-run mode).
To run with dry-run disabled, pass the argument `--dry-run` as false:
```bash
schematics .:order-wizard --name=testThing --dry-run=false
```

### Unit Testing

`npm run test` will run the unit tests, using Jasmine as a runner and test framework.

### Making the package available locally

To make the package available globally on the local system so you can use it on an Angular app, simply do:
```bash
npm run build
npm link
```

### Linking the package

In order to use the package on an Angular app, you must link it with the package and then generate the schematic on the app.
Inside the Angular app folder, simply do:
```bash
npm link order-wizard-schematic
ng g order-wizard-schematic:order-wizard --name=checkout
```
Note that `order-wizard-schematic:order-wizard` follows the rule `package_name:schematics_name` and that `--name` is the required argument to run the schematic, that on this case will create on the app a component called `checkout`.

### Add route for component

The routing for the generated component must be added manually as it is not covered in this schematic.

On the target app, edit `src/app/app-routing.module.ts` and add:
```typescript
import { CheckoutComponent } from './checkout/checkout.component';

const routes: Routes = [
  {
    path: 'checkout', component: CheckoutComponent
  }
]
```

### Publishing

To publish, simply do:

```bash
npm run build
npm publish
```

That's it!
