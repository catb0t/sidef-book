# File

A File object represents the name of a local file. The literal syntax `%f` can be used:

```ruby
File("/path/to/file.ext")
%f(/path/to/file.ext)
```

A File object supports all kinds of directory tree operations defined on file*names*, such as creation and deletion, which do not rely on a file descriptor or the file's *contents*.

In order to get a handle (file descriptor) on a File object, it must be opened, such as with the `open*` methods.

```ruby
var file = File("file.txt")    # File object
var fh = file.open_r           # FileHandle object
say fh.lines                   # read the lines into an Array
```

A File abstracts an entity on the filesystem by name; a FileHandle abstracts a file descriptor in memory.

See the [FileHandle](syntax_and_semantics/builtin_types/filehandle.md) documentation for more information.
