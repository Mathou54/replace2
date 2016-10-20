# replace
`replace2` is a command line utility for performing search-and-replace on files. It's similar to sed but there are a few differences:
It is a fork of https://github.com/harthur/replace with rename of the command from `replace` to `replace2`.

* Modifies files when matches are found
* Recursive search on directories with -r
* Uses [JavaScript syntax](https://developer.mozilla.org/en/JavaScript/Guide/Regular_Expressions#Using_Simple_Patterns) for regular expressions and [replacement strings](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String/replace#Specifying_a_string_as_a_parameter).

# Install
With [node.js](http://nodejs.org/) and [npm](http://github.com/isaacs/npm):

	npm install replace2 -g

You can now use `replace2` and `search2` from the command line.


## Examples

Replace all occurrences of "foo" with "bar" in files in the current directory:

```
replace2 'foo' 'bar' *
```

Replace in all files in a recursive search of the current directory:

```
replace2 'foo' 'bar' . -r
```

Replace only in test/file1.js and test/file2.js:

```
replace2 'foo' 'bar' test/file1.js test/file2.js
```

Replace all word pairs with "_" in middle with a "-":

```
replace2 '(\w+)_(\w+)' '$1-$2' *
```

Replace only in files with names matching *.js:

```
replace2 'foo' 'bar' . -r --include="*.js"
```

Don't replace in files with names matching *.min.js and *.py:

```
replace2 'foo' 'bar' . -r --exclude="*.min.js,*.py"
```

Preview the replacements without modifying any files:

```
replace2 'foo' 'bar' . -r --preview
```

See all the options:

```
replace2 -h
```

## Search
There's also a `search2` command. It's like `grep`, but with `replace2`'s syntax.

```
search2 "setTimeout" . -r
```

## Programmatic Usage
You can use replace from your JS program:

```javascript
var replace = require("replace2");

replace({
  regex: "foo",
  replacement: "bar",
  paths: ['.'],
  recursive: true,
  silent: true,
});
```

## More Details

### Excludes
By default, `replace2` and `search2` will exclude files (binaries, images, etc) that match patterns in the `"defaultignore"` located in this directory.

### On huge directories
If `replace2` is taking too long on a large directory, try turning on the quiet flag with `-q`, only including the necessary file types with `--include` or limiting the lines shown in a preview with `-n`.


## What it looks like
![replace2](http://i.imgur.com/qmJjS.png)

