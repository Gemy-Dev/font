# fontname

> 🅰️ Parse font file (TTF, OTF) metadata like font family name.

[![](https://img.shields.io/npm/v/fontname.svg)](https://www.npmjs.com/package/fontname)

## Demo

Upload a font and see the results at: https://danbovey.uk/fontname

## Install

`npm install fontname`

`yarn add fontname`

## Usage

`FontName.parse(ArrayBuffer)`

Parses an ArrayBuffer (binary data of the font from a FileReader) and returns an object with font meta. Throws on failure.

### Example (browser)

```js
import FontName from 'fontname';

const fontFile = e.target.files[0]; // File
const reader = new FileReader();
reader.onload = e => {
  const buffer = e.target.result; // ArrayBuffer
  try {
    const fontMeta = FontName.parse(e.target.result)[0];
    console.log(fontMeta);
  } catch (e) {
    // FontName may throw an Error
  }
};
reader.readAsArrayBuffer(fontFile);
```

### Example (node)

```js
const fs = require('fs');
const FontName = require('fontname');

try {
  const fontMeta = FontName.parse(fs.readFileSync('font.tff'))[0];
  console.log(fontMeta);
} catch (e) {
  // FontName may throw an Error
}
```

### Returns

```json
{
  "copyright": "Copyright 2011 Google Inc. All Rights Reserved.",
  "_lang": 0,
  "fontFamily": "Roboto",
  "fontSubfamily": "Regular",
  "ID": "Roboto",
  "fullName": "Roboto",
  "version": "Version 2.137; 2017",
  "postScriptName": "Roboto-Regular",
  "trademark": "Roboto is a trademark of Google.",
  "designer": "Google",
  "urlVendor": "Google.com",
  "urlDesigner": "Christian Robertson",
  "licence": "Licensed under the Apache License, Version 2.0",
  "licenceURL": "http://www.apache.org/licenses/LICENSE-2.0"
}
```

## License

File parsing logic from [Typr.js](https://github.com/photopea/Typr.js).
