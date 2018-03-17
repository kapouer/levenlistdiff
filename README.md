list-diff-hash
==============

Fork of [list-diff.js](https://github.com/toplan/list-diff),
with support for a hash function.

## Introduction

Diff two lists/strings in time O(n*m).

The algorithm finding the minimal amount of moves(patches) is [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance).

## Install

```
npm install list-diff-hash --save
```

## Usage

```javascript
var Diff = require("list-diff-hash")
var oldList = [{id: "a"}, {id: "b"}, {id: "c"}, {id: "d"}, {id: "e"}]
var newList = [{id: "c"}, {id: "a"}, {id: "b"}, {id: "e"}, {id: "f"}]

var patches = Diff(oldList, newList, "id")

patches.forEach(function (patch) {
  if (patch.type === Diff.DELETION) {
    oldList.splice(patch.index, 1)
  } else if (patch.type === Diff.INSERTION) {
    oldList.splice(patch.index, 0, patch.item)
  } else if (patch.type === Diff.SUBSTITUTION) {
    oldList.splice(patch.index, 1, patch.item)
  }
})

// now `oldList` is equal to `newList`
// [{id: "c"}, {id: "a"}, {id: "b"}, {id: "e"}, {id: "f"}]
console.log(oldList)
```

With a hash function:

```
var patches = Diff(oldList, newList, function(item) {
	return item.id
})
```

If `list-diff-hash.js` is added to a web page, it is exposed as `window.ListDiff`.

## License 
MIT
