# FileHandle

Abstraction on a Perl file descriptor, to interact with the contents of a disk file.

The filename to which a FileHandle refers, if any, can be obtained with `FileHandle().parent`, which may be `nil` or a File.
