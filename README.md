
# font-loaded

This tool can be used to see if a font is loaded and returns a boolean.

## Usage

In this example this repository is placed in the same directory as the JS file that imports it. A font called Myfont is used.

CSS:
```css
@font-face {
  font-family: 'Myfont';
  font-style: normal;
  font-weight: 400;
  src: url(fonts/Myfont.woff) format('woff');
}
```
JS:
```js
import fontLoaded from './front-loaded';
const myfontLoaded = fontLoaded('Myfont'); //true
const otherfontLoaded = fontLoaded('Otherfont'); //false
```

## Logic

The code tests `monospace`, `sans-serif` and `serif` on a string containing some letters from [all writing systems](https://en.wikipedia.org/wiki/List_of_writing_systems#List_of_writing_scripts_by_adoption) and measures the width and height of the element. Next, it does the same using your font-face with those three as fallbacks and compares them to the initial measurements. If any of the three produces a different size, the code concludes that the font is loaded. If they're all identical to the initial measurements, it can be concluded that the font isn't loaded, as the broswer used the fallback each time.

## Notes

* The code only tests if the font is loaded at the time of execution. It will return `false` if the code is executed *before* the font has been downloaded and decoded.

* If you have a special font that only defines characters in a very specific range (such as emoji), you need to add those characters to the string being tested against. The code only tests using most common special characters and characters used for writing.

* This tool only supports ES6 module importing out of the box.
