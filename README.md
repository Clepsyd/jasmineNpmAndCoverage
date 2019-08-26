- Install node.js (it comes with npm (Node Package Manager)): https://nodejs.org/en/
- Run `npm init`. It will ask you a few things (defaults between '()', press Enter if you're ok with it) and then create a package.json file for you (kind of a Gemfile but not only).
Type in `jasmine` (no quote marks) when asked for "test".
- Install jasmine for node: https://jasmine.github.io/setup/nodejs.html
    I personally installed it both globally and locally:
    `npm install jasmine --save-dev` (adds it to './node_modules' and to the devDependencies in './package.json')
    `npm install -g jasmine`
- Initialize jasmine: `jasmine init`
- Install nyc (command line client for Istanbul test coverage tool): `npm install --save-dev`.
- Install a pretty reporter for jasmine: `npm install jasmine-console-reporter --save-dev`
    - It displays all your test descriptions and gives you a summary. Does raise weird npm errors on failures though, on top of the actual failures.
    - Feel free to skip this and delete the "reporter" part for the test script below.
- Edit the scripts within package.json:

```javascript
"scripts": {
"test": "jasmine --reporter=jasmine-console-reporter", // only write "jasmine" as a value if you skipped the previous step.
"coverage": "nyc -x 'spec/' npm run test" // this runs your test suite and adds code coverage report(excluding your spec files).
}
```
- Run only your tests with `npm test` (no coverage).
- Check coverage with `npm run coverage`.

*N.B : Writing tests with the node version of jasmine is a bit different!*

You'll need to export/import between your source file and your spec file:
- my source file (./lib/frame.js)
```javascript
class Frame { // or function Frame() {};
    // blablabla
}

module.exports = Frame; //this makes the Frame class available outside of the file.
```

- my spec file (./spec/frameSpec.js):
```javascript
describe('Frame', () => {
    
  var Frame = require('../lib/frame'); // this makes the Frame class available in my tests...
  frame = new Frame();                 // ...and I can create a new Frame object.

  // rest of the tests...
}
```
