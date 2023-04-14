230414vueTesting

## `vue create vuetest`, `npm run test:unit`

``` console
$ npm init vue@latest

Vue.js - The Progressive JavaScript Framework

√ Project name: ... vue-test
√ Add TypeScript? ... No / Yes
√ Add JSX Support? ... No / Yes
√ Add Vue Router for Single Page Application development? ... No / Yes
√ Add Pinia for state management? ... No / Yes
√ Add Vitest for Unit Testing? ... No / Yes
√ Add an End-to-End Testing Solution? » No
√ Add ESLint for code quality? ... No / Yes

Scaffolding project in C:\Users\AlvinNg\zero1Wk31\vue-test...

Done. Now run:

  cd vue-test
  npm install
  npm run dev

AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk31
$ cd vue-test
```

``` console
$ vue add unit-jest

📦  Installing @vue/cli-plugin-unit-jest...

added 611 packages, and audited 644 packages in 23s

50 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
✔  Successfully installed plugin: @vue/cli-plugin-unit-jest

🚀  Invoking generator for @vue/cli-plugin-unit-jest...
📦  Installing additional dependencies...

added 14 packages, and audited 658 packages in 6s

50 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
✔  Successfully invoked generator for plugin: @vue/cli-plugin-unit-jest
```

``` console
$ npm install -g @vue/cli
npm WARN deprecated source-map-url@0.4.1: See https://github.com/lydell/source-map-url#deprecated
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
...
```

``` console
$ vue create vuetest

Vue CLI v5.0.8
? Target directory C:\Users\AlvinNg\zero1Wk31\vuetest already exists. Pick an action: Merge

Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, Linter
? Choose a version of Vue.js that you want to start the project with 3.x
? Pick a linter / formatter config: Basic
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, ESLint, etc.? In dedicated config files
? Save this as a preset for future projects? No

Vue CLI v5.0.8
✨  Creating project in C:\Users\AlvinNg\zero1Wk31\vuetest.
🗃  Initializing git repository...
⚙️  Installing CLI plugins. This might take a while...

added 616 packages, and audited 1274 packages in 39s

106 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
🚀  Invoking generators...
📦  Installing additional dependencies...

added 75 packages, and audited 1349 packages in 5s

118 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
⚓  Running completion hooks...

C:\Users\AlvinNg\zero1Wk31\vuetest\tests\unit\example.spec.js
   4:1  error  'describe' is not defined  no-undef
   5:3  error  'it' is not defined        no-undef
  10:5  error  'expect' is not defined    no-undef

✖ 3 problems (3 errors, 0 warnings)
```
update with the latest vue (from vue@latest)
``` console
$ npm run test:unit

> vuetest@0.0.0 test:unit
> vue-cli-service test:unit

 PASS  tests/unit/example.spec.js
  HelloWorld.vue
    √ renders props.msg when passed (36 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        3.155 s
Ran all test suites.

AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk31/vuetest (master)
```
