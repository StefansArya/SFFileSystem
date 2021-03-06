<a href="https://www.patreon.com/stefansarya"><img src="http://anisics.stream/assets/img/support-badge.png" height="20"></a>

[![Written by](https://img.shields.io/badge/Written%20by-ScarletsFiction-%231e87ff.svg)](LICENSE)
[![Software License](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)
[![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=SFFileSystem%20is%20a%20library%20for%20accessing%20local%20file%20system%20for%20the%20current%20website%20on%20the%20browser.&url=https://github.com/ScarletsFiction/SFFileSystem&via=github&hashtags=SFFileSystem,file,html5,storage,cordova)

# SFFileSystem
A library for accessing local file system for the current website on the browser

## How to use
### Initialization
```js
var myFile = new SFFileSystem({ options });
```

### Options
| Property  | Details |
| --- | --- |
| home | Set the root folder |
| temporary | Store file to temporary storage that will vanish when the browser was refreshed |
| callback | Callback if the initialization was success |
| initError | Callback if the initialization was failed |

### Available Methods
#### home
This is the current root folder
```js
if(myFile.home.isDirectory === true)
    console.log("I'm a folder");

// For other usage please check the 'Directory Entry' and 'Both Entry'
```

#### path
Get directory entry from directory path
```js
myFile.path('/myFolder/subFolder', function(dirEntry){
    dirEntry.isDirectory === true
}, console.error);
```

#### exist
Check if file/folder was exist and return the type of the target
```js
myFile.exist('/myFolder/subFolder', function(exist){
    if(exist === 'file' || exist === 'folder')
        console.log(true);
    else
        console.log(false);
}, console.error);
```

#### list
Get contents from a path and return an array of string
```js
myFile.list('/myFolder', function(list){
    list instanceof Array;
    // ['myFile.txt', 'myFolder']
});
```

#### contents
Get contents from a path and return their Entry
```js
myFile.contents('/myFolder', function(list){
    list instanceof Array;
    // [FileEntry, DirectoryEntry, ...]
});
```


### Directory Entry
#### newFolder
Create new folder and get it's Entry
```js
dirEntry.newFolder('myFolder', function(subFolder){
    subFolder.isDirectory === true;
});
```

#### newFile
Create new file and get it's Entry
```js
dirEntry.newFile('myFile', function(fileEntry){
    // fileEntry.write('stuff');
});
```

#### getFolder
Go to deeper folder and return the Directory Entry
```js
dirEntry.getFolder('myFolder', function(subFolder){
    subFolder.isDirectory === true;
});
```

#### getFile
Get the file entry inside current folder
```js
dirEntry.getFile('myFile', function(fileEntry){
    fileEntry.isFile === true;
});
```

#### exist
Check if file/folder was exist and return the type of the target
```js
dirEntry.exist('myFolder', function(list){
    if(exist === 'file' || exist === 'folder')
        console.log(true);
    else
        console.log(false);
});
```

#### contents
Get contents from current folder and return their Entry
```js
dirEntry.contents(function(list){
    list instanceof Array;
    // [FileEntry, DirectoryEntry, ...]
});
```

#### list
Get contents from current folder and return their Entry
```js
dirEntry.list(function(list){
    list instanceof Array;
    // ['myFile.txt', 'myFolder']
});
```

### File Entry
#### write
Write blob or string to current file
```
fileEntry.write('string' || new Blob(['any'], {type:"text/plain"}));
```

#### append
Append blob or string to current file
```
fileEntry.append('string' || new Blob(['any'], {type:"text/plain"}));
```

#### read
Read current file as a string
```
fileEntry.read(function(value){
    console.warn(value);
});

// The alternative method is accessing the file from it's url
var url = fileEntry.toURL();
```

### Both Entry
#### remove
Rename current file/folder
```
anyEntry.remove();
dirEntry.removeRecursively();
```

#### rename
Rename current file/folder
```
anyEntry.rename('targetName');
```

#### copyTo
Copy current file/folder to other directory
```
anyEntry.copyTo('path' || DirectoryEntry);
```

#### moveTo
Move current file/folder to other directory
```
anyEntry.moveTo('path' || DirectoryEntry);
```

#### getParent
Get parent directory for current file/folder
```
anyEntry.getParent(function(dirEntry){
    dirEntry.isDirectory == true;
});
```

#### isFile
Return true is current entry is a file
```
if(anyEntry.isFile)
    console.log("I'm a file");
```

#### isDirectory
Return true is current entry is a folder
```
if(anyEntry.isDirectory)
    console.log("I'm a folder");
```

#### toURL
Return absolute URL of current file/folder
```
var url = anyEntry.toURL();
// url = filesystem:http://localhost/...
```

