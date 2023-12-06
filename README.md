# lua-lar
Allows loading lua modules from a compressed file (zip, tgz)

## lua version supported
Luajit 2

## usage
Create your own zipped or tar/gzipped archive from any lua (and data) files. The compressed archive can contain subdirectories as well.

- for zip compressed files use the **.zip** or **.lar** extensions

- for gzipped tar files you can use the **.tgz** or **.tar.gz** or the **.largz** extensions.


### examples

compressed library content e.g.
```
mylib.lar
├── dir
│   ├── subdir1
│   │   └── module1.lua
|   └── subdir2
│       └── module2.lua
├── test.lua
├── test.json  
└── init.lua
```
requiring lua module:
```
require "lar"

-- accessing test.lua from outside
test = require "mylib.test"
-- include module1 from inside of 'test.lua'
mod1 = require "dir.subdir.module2"
-- accessing module2.lua from outside
mod2 = require "mylib.dir.subdir.module2"
```
using **package.path**:

```
package.path = package.path .. ";mylib/?.lua"
require "lar"
test = require "test"

...

package.path = package.path .. ";[PATH_TO_LIB]/?/init.lua"
-- requires init.lua inside the lua archive
my_lib = require "mylib"
```

## additional feaures
### decompressing a file from the archive
```
local lar = require "lar"
local str1 = lar.unzip("mylib.lar","test.json")
local str2 = lar.ungztar("my.tgz","file2.txt")
local str3 = lar.gunzip("my.gz")
```
### listing files from an archive
```
local lar = require "lar"
table_of_names_tar = lar.tgz_list("my.tar.gz")
table_of_names_zip = lar.zip_list("my.zip")
```
### extracting all files from the archive
```
local lar = require "lar"
success = lar.unzip_all("my.zip",
  function (name,data)
    print(string.format("file: %d / size: %d", name, data:len()))
  end
)
```

