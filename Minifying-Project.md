### Minifying HTML
* Install [html-minifier](https://github.com/kangax/html-minifier) with `npm install html-minifier -g`
* `html-minifier --collapse-whitespace --remove-comments --remove-optional-tags --remove-redundant-attributes --remove-script-type-attributes --remove-tag-whitespace --use-short-doctype --minify-css true --minify-js true -o <outputFile.html> <inputFile.html>`

### Minifying CSS
* Install [csso](https://github.com/css/csso-cli) with `npm install -g csso-cli`
* `csso <inputFile.css> --output <outputFile.css>`

### Minify Javascript
* Install [uglifyjs](https://github.com/mishoo/UglifyJS2) with `npm install uglify-js -g`
* `uglifyjs <inputFile.js> -c -m -o <outputFile.js>`
