---
id: 95f7193b-9940-42ba-841f-3e2a4d937ba3
title: 10 Blocks
desc: ''
updated: 1619808544810
created: 1619804977969
---
## Goals

Implement Roam like block references in Dendron

## Context

Block references let you embed blocks of text into different parts of your code

## [Lookup](https://handbook.dendron.so/notes/b89ba854-72fb-4ebc-a8a0-55960b89e9dc.html#lookup)

This section describes existing work that has been done on this topic. 

- [roam block references](https://www.roamtips.com/home/what-is-block-roam-research)
- [obsidian links to blocks](https://help.obsidian.md/How+to/Link+to+blocks)

## Proposal

Extend Dendron syntax to support block references. Obsidian has a great implementation of this already - unless there are critical deficiencies, we should adhere to their implementation and strive for interoperability. 

## Details

- to create a block, add `#^{id}` to the end of a [[wiki link|dendron.topic.links#wiki-links]]
  ```
  [[filename#^1234]]
  ```
- typing `^` will trigger a search of all blocks that currently exist within the file
- inputting `enter` will generate a block anchor, a random id, in the target file 
- typing `^^` will trigger a search of all existing block anchors

## Tasks

- [ ] [[Parsing block syntax|dendron.rfc.10-blocks.parsing-block-syntax]]
- [ ] [[Markdown integration|dendron.rfc.10-blocks.markdown-integration]]
- [ ] [[Html integration|dendron.rfc.10-blocks.html-integration]]
- [ ] [[Integration with Vscode|dendron.rfc.10-blocks.vscode-integration]]

## Example

### Block link inside same file

- link to block 

```md
Some notes ^dcf64c

[[filename#^dcf64c]]

More notes
```

- html

```html
<!-- source -->
<div id="dcf64c">
<a aria-hidden="true" href="#dcf64c"><span class="icon icon-link"></span></a>
<p> Some notes </p>
</div>

<a  href="...#^dcf64c">filename</a>

<div>
<p> More Notes </p>
</div>
```

### Block link to other file

- link to block 

  - file a

  ```md
  Some notes ^dcf64c
  ```

  - file b

  ```md
  [[filename#^dcf64c]]

  More notes
  ```

- html

  - a.html

  ```html
  <!-- source -->
  <div id="dcf64c">
  <a aria-hidden="true" href="#dcf64c"><span class="icon icon-link"></span></a>
  <p> Some notes </p>
  </div>
  ```

  - b.html

  ```html
  <a  href="...#^dcf64c">filename</a>

  <p> More Notes </p>
  ```

### Block reference to other file

- link to block 

  - file a

  ```md
  Some notes ^dcf64c
  ```

  - file b

  ```md
  ![[filename#^dcf64c]]

  More notes
  ```

- html

  - a.html

  ```html
  <!-- source -->
  <div id="dcf64c">
  <a aria-hidden="true" href="#dcf64c"><span class="icon icon-link"></span></a>
  <p> Some notes </p>
  </div>
  ```

  - b.html

  ```html
  <p>Some notes</p>

  <p> More Notes </p>
  ```

## Tradeoffs

- we are using a purely plaintext based approach of doing block references which means that we are leaving artifacts in the source doc when we generate a block reference
  - alternatives are using a separate mapping file or using a db, the former adds a layer of indirection that doesn't fit with our current note modal, the latter is currently out of scope

## Discussion

