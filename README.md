# lua-lar
Allows  loading lua modules from a compressed file (zip, tgz)

## lua version supported
Luajit 2

### usage example

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
requiring lua modules:
```
-- accessing test.lua from outside
test = require "mylib.test"
-- include module1 from inside of 'test.lua'
mod1 = require "dir.subdir.module2"
-- accessing module2.lua from outside
mod2 = require "mylib.dir.subdir.module2"
```
using **package.path**:



