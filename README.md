# Compress Blocks

cb is a tool for compressing files with repeated blocks (such as Raspberry Pi SD images etc.)


```
usage: cb [-h] (-a | -x | -l) [-b BLOCK] [-D] [-p]
          [-H {md5,sha1,sha224,sha256,sha384,sha512}] [-c {none,xz,bz2}]
          [-C {1,2,3,4,5,6,7,8,9}] [-L] [-v] [-S]
          file [files [files ...]]

Compress Blocks

positional arguments:
  file                  In/output archive filename
  files                 Files to compress

optional arguments:
  -h, --help            show this help message and exit
  -a, --archive         Create archive
  -x, --extract         Extract archive
  -l, --list            List archive files
  -b BLOCK, --block BLOCK
                        Block size in bytes (default 4096)
  -D, --debug           Show LOTS of debug information
  -p, --progress        Show progress
  -H {md5,sha1,sha224,sha256,sha384,sha512}, --hash {md5,sha1,sha224,sha256,sha384,sha512}
                        Hash algorithm (default sha1)
  -c {none,xz,bz2}, --compression {none,xz,bz2}
                        Builtin compression algorithm
  -C {1,2,3,4,5,6,7,8,9}, --compressionlevel {1,2,3,4,5,6,7,8,9}
                        Compression level 1-9
  -L, --savelast        Save clone pointer to last block instead of first
  -v, --verbose         Show hash signatures
  -S                    TODO stuff :)
```
