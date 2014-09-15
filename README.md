JException Genie
==
JException Genie is a Java Agent. JException Genie attempts to provide useful information to Users and Newcomers alike.

Version
==
0.0.1

Dependencies
==

JException Genie is written in both Java and JavaScript (Node.JS)

* [Java Development Kit 8] - A development environment for building applications and components using the Java programming language.
* [Node.js] - a curated set of user interface interactions, effects, widgets, and themes built on top of the jQuery

Getting Started
==
[IntelliJ IDEA] was used in developing JException Genie. In order to start developing, use IDEA to open the project file. If you do not have IntelliJ IDEA, you may use any other IDE/Compiler toolchain of your choice.

_Notes_
--
I _fucking hate_ Node's require system! I have written an import utility which can be found in the _BuildTools/imports.js_ file. Here are two examples, one with and one without.

__Without__
```javascript
// Random JavaScript code without the imports tool.

var fs = require("fs"),
    path = require("path"),
    url = require("url"),
    _ = require("underscore"),
    prompt = require("prompt"),
    dns = require('dns'),
    EventEmitter = require('events').EventEmitter;

var evtEmit = new EventEmitter();

evtEmit.on("log", function (msg) {
    console.log("[LOG]: " + msg);
});

function localFile(file) {
    var path = __dirname + file;
    evtEmit.emit("log", path);
    return path;
}

evtEmit.on("read", function (what) {
    console.log("Reading from: ", what);
    evtEmit.emit("log", "reading");
});

evtEmit.on("write", function (what) {
    console.log("Writing to: ", what);
    evtEmit.emit("log", "writing");
});

evtEmit.on("readJson", function (path) {
    evtEmit.emit("read", path);
    fs.readFile(path, function (err, data) {
        var jsonObj = JSON.parse(data);
        evtEmit.emit("log", "Changing Data");
        _.keys(jsonObj).forEach(function (key) {
            jsonObj[_.uniqueId(key)] = jsonObj[key];
        });
        evtEmit.emit("changedJson", path, jsonObj);
    });
});

evtEmit.on("changedJson", function (path, newJson) {
    evtEmit.emit("log", "Writing File");
    fs.writeFile(path, JSON.stringify(newJson), function (err) {
        evtEmit.emit("write", path);
    });
});

evtEmit.emit("log", "emit readJson");

evtEmit.emit("readJson", localFile("/data.json"));

```

__With__
```javascript
// The same random JavaScript code with the imports tool.
// The imports tool contains pre-existing imports; chalk, fs, url, underscore,exec and prompt
with(require("./imports")([
        ["path"],
        ["url"],
        ["dns"],
        ["EventEmitter", "events", "EventEmitter"]
     ])) {
    var evtEmit = new EventEmitter();

    evtEmit.on("log", function (msg) {
        console.log("[LOG]: " + msg);
    });

    function localFile(file) {
        var path = __dirname + file;
        evtEmit.emit("log", path);
        return path;
    }

    evtEmit.on("read", function (what) {
        console.log("Reading from: ", what);
        evtEmit.emit("log", "reading");
    });

    evtEmit.on("write", function (what) {
        console.log("Writing to: ", what);
        evtEmit.emit("log", "writing");
    });

    evtEmit.on("readJson", function (path) {
        evtEmit.emit("read", path);
        fs.readFile(path, function (err, data) {
            var jsonObj = JSON.parse(data);
            evtEmit.emit("log", "Changing Data");
            _.keys(jsonObj).forEach(function (key) {
                jsonObj[_.uniqueId(key)] = jsonObj[key];
            });
            evtEmit.emit("changedJson", path, jsonObj);
        });
    });

    evtEmit.on("changedJson", function (path, newJson) {
        evtEmit.emit("log", "Writing File");
        fs.writeFile(path, JSON.stringify(newJson), function (err) {
            evtEmit.emit("write", path);
        });
    });

    evtEmit.emit("log", "emit readJson");

    evtEmit.emit("readJson", localFile("/data.json"));
}

```

__The Import Tool__

```javascript
module.exports = (function (defaultPackages, additional) {
    var requireModules = function (modules) {
        var imports = {};
        if (Array.isArray(modules) && modules.length >= 0) {
            defaultPackages = defaultPackages.concat(modules);
        }
        defaultPackages.forEach(function (module) {
            switch (module.length) {
            case 1:
                imports[module[0]] = require(module[0]);
                break;

            case 2:
                imports[module[0]] = require(module[1]);
                break;

            case 3:
                imports[module[0]] = require(module[1])[module[2]];
                break;
            }
        });
        return imports;
    };
    return additional ? requireModules(additional) : requireModules();
})
([
    // var chalk = require("chalk");
    ['chalk'],

    // var fs = require("fs");
    ['fs'],

    // var url = require("url");
    ['url'],

    // var _ = require("underscore");
    ['_', 'underscore'],

    // var exec = require("child_process").exec;
    ['exec', 'child_process', 'exec'],

    // var prompt = require("prompt");  
    ['prompt']
]);

```

License
--
The license JException Genie uses grants free access to source code for any purpose you wish. To avoid license compatibility issues, we ask you to put your contributions to this project under the same license as we do with ours.

If you contribute to InfernoMod, you license your code to the public under the ISC license (and CC-by license for other media).
You must therefore be able to grant this license.

This means that you either;
 1. Hold the copyright to the contribution, which is the case if you produced it yourself.
 2. You have acquired the work from a source that is ISC / CC-by compatible, for example code in the public domain or code that itself underlies the ISC license. 
 
In the first case, you retain your copyright. You never need to transfer your copyright to the InfernoMod project. You can relicense your work to other parties any way you like. However, you cannot withdraw your license under the terms of the ISC license.

####The ISC license

Permission to use, copy, modify, and/or distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

####Frequently Asked Questions

Can I contribute work to InfernoMod which falls under the GPL?

No. The GPL license requires everything to be distributed on its terms, and we have contributors who do not want that. However, if you are the copyright holder of the work and are willing to re-license the work under ISC license terms, you can do that.


####What about other licenses?

Other permissive licenses like the MIT license or BSD licenses as well as public domain (of course). LGPL code is okay for libraries, too.


####May I use ISC licensed work in a GPL project?

Under the terms of the ISC license, you may do that - of course you still need to abide to the ISC license and print the copyright notice and the license in all copies.
[Java Development Kit 8]:http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[IntelliJ IDEA]:http://www.jetbrains.com/idea/
[Node.js]:http://nodejs.org/
