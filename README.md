# webgen-yui-compressor
A webgen extension to call YUICompressor

## Introduction

This package extends [webgen](http://webgen.gettalong.org/), a static website
generator, by a content processor that
calls [YUICompressor](http://yui.github.io/yuicompressor/) to compress your
JavaScript and/or CSS files.

## Requirements

You need the [YUICompressor](http://yui.github.io/yuicompressor/) binary, which
must be executable by the webgen process.

## How to Use

Copy the contained `yui_compressor/` folder to the `ext/` folder within your webgen
project.

To compress your source files, add this content processor as the **last**
processor in the pipeline for JavaScript and/or CSS nodes.  This can either be
done by adding `yui_compressor` to the source path name
(e.g. `js/myfile.yui_compressor.js`) or by explicitly specifying the pipeline
using a meta information node, for example (in a `metainfo` file):

```YAML
/**/*.scss:
  pipeline: [scss,yui_compressor]
  dest_path: <parent><basename>.css
```

Note that when working with Sass/SCSS files, you have to either use a meta
information node (as shown above), or rename your files to something like
`myfile.scss.yui_compressor.css` to ensure that the Sass/SCSS processor will run
first.

### Global configuration options

The following configuration options can be set:

+ `content_processor.yui_compressor.bin`

  Path to the YUICompressor binary, defaults to `yui-compressor`

+ `content_processor.yui_compressor.options`

  [Command-line options](http://yui.github.io/yuicompressor/#using) for the
  YUICompressor binary, as a hash.  Keys should correspond to command-line
  options (with hyphens replaced by underscores); values are only considered for
  options that accept values, and ignored otherwise.

  The following options are accepted: charset, line_break, nomunge,
  preserve_semi, disable_optimizations

+ `content_processor.yui_compressor.typemap`

  A hash mapping file extensions to content types.  If you use a file extension
  *other than* `.css`, `.sass`, `.scss`, or `.js`, you need to specify how
  YUICompressor should treat the content.  Valid content types are `css` and
  `js`.

## Contact

For any questions, contact Marcel Bollmann (<bollmann@linguistics.rub.de>).

## License

This extension is licensed under GPLv3, just like webgen itself.
