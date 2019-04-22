go-difflib
==========

[![Build Status](https://travis-ci.org/martinohmann/go-difflib.svg?branch=master)](https://travis-ci.org/martinohmann/go-difflib)
[![GoDoc](https://godoc.org/github.com/martinohmann/go-difflib?status.svg)](https://godoc.org/github.com/martinohmann/go-difflib)

This is a fork of [go-difflib](https://github.com/pmezard/go-difflib) by
Patrick Mezard with added support for colored diffs and go modules. It can be
used as a drop-in replacement for the original implementation which is not
maintained anymore.

Go-difflib is a partial port of python 3 difflib package. Its main goal
was to make unified and context diff available in pure Go, mostly for
testing purposes.

The following class and functions (and related tests) have be ported:

* `SequenceMatcher`
* `unified_diff()`
* `context_diff()`

## Installation

```bash
$ go get github.com/martinohmann/go-difflib/difflib
```

### Quick Start

Diffs are configured with Unified (or ContextDiff) structures, and can
be output to an io.Writer or returned as a string.

```Go
diff := difflib.UnifiedDiff{
    A:        difflib.SplitLines("foo\nbar\n"),
    B:        difflib.SplitLines("foo\nbaz\n"),
    FromFile: "Original",
    ToFile:   "Current",
    Context:  3,
}
text, _ := difflib.GetUnifiedDiffString(diff)
fmt.Printf(text)
```

would output:

```
--- Original
+++ Current
@@ -1,3 +1,3 @@
 foo
-bar
+baz
```

### Color support

Colored diffs can be enabled by setting the `Color` struct field of the
`UnifiedDiff` (or `ContextDiff`) structs to `true`.

```Go
diff := difflib.UnifiedDiff{
    A:        difflib.SplitLines("foo\nbar\n"),
    B:        difflib.SplitLines("foo\nbaz\n"),
    FromFile: "Original",
    ToFile:   "Current",
    Context:  3,
    Color:    true,
}

// writes a colored diff
text, _ := difflib.GetUnifiedDiffString(diff)
fmt.Printf(text)
```
