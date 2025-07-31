# dv.view not rendering for inline Dataview JS
To avoid copy-pasting the inline query for backlinks for each zettel (using the [Templater plugin](https://silentvoid13.github.io/Templater/)), I wanted to store the backlink generation code in a separate `.js` file.

The problem with this is that [inline Dataview JS](https://blacksmithgu.github.io/obsidian-dataview/queries/dql-js-inline/#inline-dataview-js) [doesn't work with asynchronous functions](https://github.com/blacksmithgu/obsidian-dataview/issues/1372) (functions called with `await`) that return a Promise: they need to return a single, renderable JS value.

The solution: DON'T USE INLINE DATAVIEW JS.

Any query large enough that it needs to be modularized should be handled with regular [Dataview JS](https://blacksmithgu.github.io/obsidian-dataview/queries/dql-js-inline/#dataview-js) blocks, not inline.

This can be achieved by including the desired static contents of the line in the `.js` file and then displaying with a `dv.span` element.
