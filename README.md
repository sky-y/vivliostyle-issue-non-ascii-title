# Vivliostyle Issue: press-ready Error when Title is non-ASCII 

When `title` on vivliostyle.config.js is non-ASCII characters, press-ready shows error and make empty PDF output.

Note: This could be an Error on [press-ready](https://github.com/vibranthq/press-ready) or [Create Book](https://github.com/vivliostyle/create-book) side.

- CASE 1: `npx vivliostyle build --press-ready`
  - will produce error: 
    - `GPL Ghostscript 9.23: **** Could not open the file `
    - `I/O Error: Couldn't open file`
- CASE 2: `npx press-ready build -i 科学の不思議.pdf -o press-ready.pdf`
  - input file: `科学の不思議.pdf` (non-ASCII characters)
  - output file: `press-ready.pdf`
    - will be empty PDF
  - will produce error: `Error: /undefinedfilename`

## Spec

- macOS Catalina 10.15.7

```
$ npx vivliostyle --version
cli: 3.0.0-pre.4
core: 2.1.4
$ npx press-ready --version
4.0.3
$ gs -h
GPL Ghostscript 9.23 (2018-03-21)
```

## Related Issue

[Error with --press-ready option on Windows · Issue #72 · vivliostyle/vivliostyle-cli](https://github.com/vivliostyle/vivliostyle-cli/issues/72)

## About this project

This project is originally generated by [Create Book](https://github.com/vivliostyle/create-book).

```
$ npm create book sample-book-kagakunofushigi
? description description
? author name アンリイ・ファブル（大杉栄、伊藤野枝訳）
? author email
? license CC0-1.0
? choose theme @vivliostyle/theme-techbook - Techbook (技術同人誌) theme
```

I renamed the generated directory to `vivlistyle-issue-toc-error`.

## Files

01.md:

```01.md
# 一　六人

或る夕方、まだ外がやう／＼暗くなりかけた時分から、六人の人達は、みんな一とかたまりになつて集まりました。

...
```

vivliostyle.config.js:

```vivliostyle.config.js
module.exports = {
  title: '科学の不思議', 
  author: 'アンリイ・ファブル（大杉栄、伊藤野枝訳）', 
  size: 'JIS-B5', // paper size.
  theme: '@vivliostyle/theme-techbook', // .css or local dir or npm package. default to undefined.
  entry: [
    '01.md',
  ], 
}
```

## How to Reproduce

- Clone this project

```
$ npm install

# CASE 1
$ npx vivliostyle build --press-ready

# CASE 2
$ npx vivliostyle build
$ npx press-ready build -i 科学の不思議.pdf -o press-ready.pdf
```

## Log

### CASE 1

```
$ npx vivliostyle build --press-ready
✔ 01.md 一　六人
✔ 01.md 一　六人
🚀 Running press-ready
==> Listing fonts in '/var/folders/hw/pnp2g_hx2zj3_4m40lyyqq8w0000gn/T/vivliostyle-cli-851a0f70-45ef-11eb-a64b-8dde9018055c.pdf'
name          type          embedded  subset 
[none]        Type 3        yes       no     
Verdana-Bold  CID TrueType  yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
Verdana       CID TrueType  yes       no     
[none]        Type 3        yes       no     
Verdana       CID TrueType  yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
==> Some fonts need to be outlined
==> Generating PDF
Input            /var/folders/hw/pnp2g_hx2zj3_4m40lyyqq8w0000gn/T/vivliostyle-cli-851a0f70-45ef-11eb-a64b-8dde9018055c.pdf 
Output           /Users/yuki/src/sample-vivliostyle-md/vivliostyle-issue-non-ascii-title/科学の不思議.pdf                  
Color Mode       CMYK                                                                                                      
Enforce outline  yes                                                                                                       
Boundary boxes   no                                                                                                        
==> GPL Ghostscript 9.23: **** Could not open the file /Users/yuki/src/sample-vivliostyle-md/vivliostyle-issue-non-ascii-title/�����������������.pdf .
**** Unable to open the initial device, quitting.
GPL Ghostscript 9.23 (2018-03-21)
Copyright (C) 2018 Artifex Software, Inc.  All rights reserved.
This software comes with NO WARRANTY: see the file PUBLIC for details.
==> Listing fonts in '/Users/yuki/src/sample-vivliostyle-md/vivliostyle-issue-non-ascii-title/科学の不思議.pdf'
Error: Command failed with exit code 1: pdffonts /Users/yuki/src/sample-vivliostyle-md/vivliostyle-issue-non-ascii-title/科学の不思議.pdf
I/O Error: Couldn't open file '/Users/yuki/src/sample-vivliostyle-md/vivliostyle-issue-non-ascii-title/<e7><a7><91><e5><ad><a6><e3><81><ae><e4><b8><8d><e6><80><9d><e8><ad><b0>.pdf': No such file or directory.

If you think this is a bug, please report at https://github.com/vivliostyle/vivliostyle-cli/issues
```

### CASE 2

```
$ npx vivliostyle build
✔ 01.md 一　六人
✔ 01.md 一　六人
🎉 Built successfully.

科学の不思議.pdf has been created.
```

```
$ npx press-ready build -i 科学の不思議.pdf -o press-ready.pdf
==> Listing fonts in '科学の不思議.pdf'
name          type          embedded  subset 
[none]        Type 3        yes       no     
Verdana-Bold  CID TrueType  yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
Verdana       CID TrueType  yes       no     
[none]        Type 3        yes       no     
Verdana       CID TrueType  yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
[none]        Type 3        yes       no     
==> Some fonts need to be outlined
==> Generating PDF
Input            科学の不思議.pdf 
Output           press-ready.pdf  
Color Mode       CMYK             
Enforce outline  yes              
Boundary boxes   no               
==> GPL Ghostscript 9.23: Unrecoverable error, exit code 1
GPL Ghostscript 9.23 (2018-03-21)
Copyright (C) 2018 Artifex Software, Inc.  All rights reserved.
This software comes with NO WARRANTY: see the file PUBLIC for details.
Error: /undefinedfilename in (/Users/yuki/src/sample-vivliostyle-md/vivliostyle-issue-non-ascii-title/\347\347\221\345\355\246\343\301\256\344\370\215\346\300\235\350\355\260.pdf)
Operand stack:

Execution stack:
   %interp_exit   .runexec2   --nostringval--   --nostringval--   --nostringval--   2   %stopped_push   --nostringval--   --nostringval--   --nostringval--   false   1   %stopped_push
Dictionary stack:
   --dict:996/1684(ro)(G)--   --dict:0/20(G)--   --dict:79/200(L)--
Current allocation mode is local
Last OS error: No such file or directory
==> Listing fonts in 'press-ready.pdf'
==> No fonts found
==> Every font is properly embedded
```

## About sample

青空文庫から転載・改変しました。

- ファーブル ジャン・アンリ『科学の不思議』（大杉 栄、伊藤 野枝 訳）
    - [図書カード：科学の不思議](https://www.aozora.gr.jp/cards/001049/card4920.html)

