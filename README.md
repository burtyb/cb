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

# What does it do?

cb is a simple block archive/extract tool. 

The program simply looks through the source files and generates a hash (MD5/SHA1/etc) of the source blocks (4096 bytes by default) and only saves each unique block once. When these blocks are used again (either in the same or different input file) a pointer to the output file and position of the block is saved reducing the space used. The blocks and pointers are then optionally compressed before being written to the output file.

# What is/isn't it for?

cb is designed to archive uncompressed disk images (such as USB/SD card images Raspberry Pi, etc.).

It can be used to archive multiple files deduplicating any repeated blocks (4096 bytes by default) no matter where they are in the source file and then optionally compressing these to disk using XZ/BZ2.

cb is not a generic archive tool, to have any chance of saving space repeated blocks must fall on the block boundary.

# How well does it work?

My use case for the tool is archiving previous versions of the https://clusterhat.com/ Raspbian based images, so these tests are based on that use.

## Quick test

These quick tests compare archiving the Raspbian 2018-11-13 images (desktop full, desktop and lite versions).

The original .zip files use 3.2GB of disk space (2018-11-13-raspbian-stretch-full.zip 1.9G / 2018-11-13-raspbian-stretch-lite.zip 352M / 
2018-11-13-raspbian-stretch.zip 1.1G). Expanded the files use 9.84GB (2018-11-13-raspbian-stretch-full.img 5.0G / 2018-11-13-raspbian-stretch.img 3.2G / 2018-11-13-raspbian-stretch-lite.img 1.8G).

Using the "cb" archive tool the file size with no compression is 4.3G, but using internal compression (xz -9) the file size is only 1.4G.

## Raspbian releases

When doing a longer test with all releases of Raspbian for the Raspberry Pi (57GB in 69 zip files - 186G extracted) archives with "cb" to 25G (compression disabled) and then to 5.7G using either builtin or external compression (xz -9).
