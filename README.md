# full.js

**TL;DR**: Node.js clone in pure JavaScript.

`full.js` is Node.js without C++ parts. The goal is to implement **100%**
of Node.js API without any dependencies on any C++ libraries.

Requirements: it runs on Ubuntu 14.04 x86_64, not tested on other systems.

## API Status

### [`events`](https://nodejs.org/api/events.html)

*Depends on:* Has no dependencies.

Verbatim copy from Node.js

 - [X] `EventEmitter`


### [`process`](https://nodejs.org/api/process.html)

*Depends on:* `process.syscall`, `events`

Extra:

 - [X] `process.syscall(number, ...args): number`
 - [X] `process.syscall64(number, ...args): number`
 - [ ] `process.asyscall(number, ...args, callback)`
 - [ ] `process.asyscall64(number, ...args, callback)`
 - [ ] `process.malloc(address, size): Buffer`

Standard:

 - [ ] `Event: 'beforeExit'`
 - [ ] `Event: 'disconnect'`
 - [ ] `Event: 'exit'`
 - [ ] `Event: 'message'`
 - [ ] `Event: 'rejectionHandled'`
 - [ ] `Event: 'uncaughtException'`
 - [ ] `Event: 'unhandledRejection'`
 - [ ] `Event: 'warning'`
 - [ ] `Signal Events`
 - [ ] `process.abort()`
 - [ ] `process.arch`
 - [X] `process.argv`
 - [ ] `process.chdir(directory)`
 - [X] `process.config`
 - [ ] `process.connected`
 - [ ] `process.cpuUsage([previousValue])`
 - [X] `process.cwd()` -- check it is 100% compatible with Node.js
 - [ ] `process.disconnect()`
 - [X] `process.env`
 - [ ] `process.emitWarning(warning[, name][, ctor])`
 - [X] `process.execArgv`
 - [X] `process.execPath`
 - [ ] `process.exit([code])`
 - [ ] `process.exitCode`
 - [ ] `process.getegid()`
 - [ ] `process.geteuid()`
 - [X] `process.getgid()`
 - [ ] `process.getgroups()`
 - [ ] `process.getuid()`
 - [ ] `process.hrtime([time])`
 - [ ] `process.initgroups(user, extra_group)`
 - [ ] `process.kill(pid[, signal])`
 - [ ] `process.mainModule`
 - [ ] `process.memoryUsage()`
 - [X] `process.nextTick(callback[, arg][, ...])`
 - [X] `process.pid`
 - [ ] `process.platform`
 - [X] `process.release`
 - [ ] `process.send(message[, sendHandle[, options]][, callback])`
 - [ ] `process.setegid(id)`
 - [ ] `process.seteuid(id)`
 - [ ] `process.setgid(id)`
 - [ ] `process.setgroups(groups)`
 - [ ] `process.setuid(id)`
 - [ ] `process.stderr`
 - [ ] `process.stdin`
 - [ ] `process.stdout`
 - [X] `process.title`
 - [ ] `process.umask([mask])`
 - [ ] `process.uptime()`
 - [X] `process.version`
 - [X] `process.versions`
 - [X] `process.features`
 - [ ] `Exit Codes`


### [`Buffer`](https://nodejs.org/api/buffer.html)

*Depends on:* `ArrayBuffer`

Use `buffer` *npm* package, which was originally written for Browserify. Internally
it uses `ArrayBuffer`, which is what we need. `buffer` has also a fallback
for older browsers to emulate `ArrayBuffer` with plain JavaScript objects, we may
want to remove that option, as it is no-no for us.

TODO: check all methods work correctly, including the `.slice()` method.

 - [X] `Buffer`


### `StaticBuffer`

*Depends on:* `Buffer`, `process.syscall`, `process.malloc`

 - [ ] `StaticBuffer`
 

### [`util`](https://nodejs.org/api/util.html)

*Depends on:* `Buffer`

 - [X] `util.debuglog(section)`
 - [X] `util.deprecate(function, string)`
 - [X] `util.format(format[, ...])`
 - [X] `util.inherits(constructor, superConstructor)`
 - [X] `util.inspect(object[, options])` -- slightly broken
 - [X] `util.inspect.colors`
 
Deprecated APIs:

 - [X] `util.debug(string)`
 - [X] `util.error([...])`
 - [X] `util.isArray(object)`
 - [X] `util.isBoolean(object)`
 - [X] `util.isBuffer(object)`
 - [X] `util.isDate(object)`
 - [X] `util.isError(object)`
 - [X] `util.isFunction(object)`
 - [X] `util.isNull(object)`
 - [X] `util.isNullOrUndefined(object)`
 - [X] `util.isNumber(object)`
 - [X] `util.isObject(object)`
 - [X] `util.isPrimitive(object)`
 - [X] `util.isRegExp(object)`
 - [X] `util.isString(object)`
 - [X] `util.isSymbol(object)`
 - [X] `util.isUndefined(object)`
 - [X] `util.log(string)`
 - [X] `util.print([...])`
 - [X] `util.puts([...])`
 - [X] `util._extend(obj)`
 
Extra:

 - [X] `util.extend(...objects)` 


### [`assert`](https://nodejs.org/api/assert.html)

*Depends on:* `util`, `Buffer`

 - [X] `assert(value[, message])`
 - [X] `assert.deepEqual(actual, expected[, message])`
 - [X] `assert.deepStrictEqual(actual, expected[, message])`
 - [X] `assert.doesNotThrow(block[, error][, message])`
 - [X] `assert.equal(actual, expected[, message])`
 - [X] `assert.fail(actual, expected, message, operator)`
 - [X] `assert.ifError(value)`
 - [X] `assert.notDeepEqual(actual, expected[, message])`
 - [X] `assert.notDeepStrictEqual(actual, expected[, message])`
 - [X] `assert.notEqual(actual, expected[, message])`
 - [X] `assert.notStrictEqual(actual, expected[, message])`
 - [X] `assert.ok(value[, message])`
 - [X] `assert.strictEqual(actual, expected[, message])`
 - [X] `assert.throws(block[, error][, message])`


### [`path`](https://nodejs.org/api/path.html)

*Depends on:* `util`

Verbatim copy from Node.js

 - [X] `path`


### [`stream`](https://nodejs.org/api/stream.html)

*Depends on:* `events`, `util`, `Buffer`

Almost verbatim copy from Node.js

 - [X] `stream`
 
 
### [`libjs`](http://www.npmjs.com/package/libjs)

*Depends on:* `process.syscall`, `process.syscall64`, `process.asyscall`, `process.asyscall64`

Wrapper around system calls.


### [`fs`](https://nodejs.org/api/fs.html)

*Depends on:* `events`, `path`, `Buffer`, `stream`, `libjs`

Implements `fs.js` API as in the docs, with few minor differences, here are the known ones:

 1. Some error messages may be different.
 2. `utimes()` sets file time in seconds, instead of milliseconds.
 3. `futimes()` is not implemented.
 4. `watch()` function is implemented using the same `inotify(7)` system calls that Node.js is using, 
    however, I don't know why Node.js emits only change and rename events, when `inotify(7)` provides 
    a much more diverse event set, so the mapping to change and rename might be a bit off. It internally 
    uses Inotify class from `libaio` package, for more control and better performance use the 
    `libaio.Inotify` class directly instead.
 5. `readdir()` results may differ as libfs implements it itself instead of using `libc`'s C implementation.
 6. `realpath()` results may differ as libfs implements it itself instead of using `libc`'s C implementation.
 7. `fs.ReadStream` and `fs.WriteStream` are not implemented yet.
 
- [ ] `persistent` option in watchFile() and watch() methods is always true, even if you set it to false.

Below synchronous methods are implements using `process.syscall`:

 - [ ] `fs.accessSync(path[, mode])`
 - [ ] `fs.appendFileSync(file, data[, options])`
 - [ ] `fs.chmodSync(path, mode)`
 - [ ] `fs.chownSync(path, uid, gid)`
 - [X] `fs.closeSync(fd)`
 - [ ] `fs.existsSync(path)`
 - [ ] `fs.fchmodSync(fd, mode)`
 - [ ] `fs.fchownSync(fd, uid, gid)`
 - [ ] `fs.fdatasyncSync(fd)`
 - [ ] `fs.fstatSync(fd)`
 - [ ] `fs.fsyncSync(fd)`
 - [ ] `fs.ftruncateSync(fd, len)`
 - [ ] `fs.futimesSync(fd, atime, mtime)`
 - [ ] `fs.lchmodSync(path, mode)`
 - [ ] `fs.lchownSync(path, uid, gid)`
 - [ ] `fs.linkSync(srcpath, dstpath)`
 - [ ] `fs.lstatSync(path)`
 - [ ] `fs.mkdtempSync(prefix)`
 - [ ] `fs.mkdirSync(path[, mode])`
 - [X] `fs.openSync(path, flags[, mode])`
 - [ ] `fs.realpathSync(path[, options])`
 - [X] `fs.readFileSync(file[, options])`
 - [ ] `fs.readlinkSync(path[, options])`
 - [ ] `fs.symlinkSync(target, path[, type])`
 - [X] `fs.statSync(path)`
 - [ ] `fs.truncateSync(path, len)`
 - [ ] `fs.renameSync(oldPath, newPath)`
 - [ ] `fs.readSync(fd, buffer, offset, length, position)`
 - [ ] `fs.writeSync(fd, buffer, offset, length[, position])`
 - [ ] `fs.writeSync(fd, data[, position[, encoding]])`
 - [ ] `fs.writeFileSync(file, data[, options])`
 - [ ] `fs.unlinkSync(path)`
 - [ ] `fs.rmdirSync(path)`
 
Below asynchronous methods are implemented using `process.asyscall`:
 
 - [ ] `fs.access(path[, mode], callback)`
 - [ ] `fs.appendFile(file, data[, options], callback)`
 - [ ] `fs.chmod(path, mode, callback)`
 - [ ] `fs.chown(path, uid, gid, callback)`
 - [ ] `fs.close(fd, callback)`
 - [ ] `fs.exists(path, callback)`
 - [ ] `fs.fchmod(fd, mode, callback)`
 - [ ] `fs.fchown(fd, uid, gid, callback)`
 - [ ] `fs.fdatasync(fd, callback)`
 - [ ] `fs.fstat(fd, callback)`
 - [ ] `fs.fsync(fd, callback)`
 - [ ] `fs.ftruncate(fd, len, callback)`
 - [ ] `fs.futimes(fd, atime, mtime, callback)`
 - [ ] `fs.lchmod(path, mode, callback)`
 - [ ] `fs.lchown(path, uid, gid, callback)`
 - [ ] `fs.link(srcpath, dstpath, callback)`
 - [ ] `fs.lstat(path, callback)`
 - [ ] `fs.mkdir(path[, mode], callback)`
 - [ ] `fs.mkdtemp(prefix, callback)`
 - [ ] `fs.open(path, flags[, mode], callback)`
 - [ ] `fs.read(fd, buffer, offset, length, position, callback)`
 - [ ] `fs.readFile(file[, options], callback)`
 - [ ] `fs.readlink(path[, options], callback)`
 - [ ] `fs.realpath(path[, options], callback)`
 - [ ] `fs.rename(oldPath, newPath, callback)`
 - [ ] `fs.rmdir(path, callback)`
 - [ ] `fs.stat(path, callback)`
 - [ ] `fs.symlink(target, path[, type], callback)`
 - [ ] `fs.truncate(path, len, callback)`
 - [ ] `fs.unlink(path, callback)`
 - [ ] `fs.write(fd, buffer, offset, length[, position], callback)`
 - [ ] `fs.write(fd, data[, position[, encoding]], callback)`
 - [ ] `fs.writeFile(file, data[, options], callback)`
 
There is no such `readdir` Linux system call, instead `libc` implements it
itself, here we too implement the `readdir` function in JavaScript, so it
might not be 100% compatible with Node.js:
 
 - [ ] `fs.readdirSync(path[, options])`
 - [ ] `fs.readdir(path[, options], callback)`
 
Times are currently resolved to millisecond accuracy, you can still use
`utimes` but if you specify time with microsecond accuracy it will be rounded
to milliseconds:
  
 - [ ] `fs.utimes(path, atime, mtime, callback)`
 - [ ] `fs.utimesSync(path, atime, mtime)`
 
We use `inotify` syscall interface (just like `libuv` in Node.js) from 
[`libaio`](http://www.npmjs.com/package/libaio) package:   

 - [ ] `fs.watch(filename[, options][, listener])`
 
Below file watching just polls file system (as does Node.js) using `setTimeout()`. There
are some incompatibilities with Node.js, see [`fslib`](http://www.npmjs.com/package/fslib):
 
 - [ ] `fs.unwatchFile(filename[, listener])`
 - [ ] `fs.watchFile(filename[, options], listener)` 
 - [ ] `Class: fs.FSWatcher`
     - [ ] `Event: 'change'`
     - [ ] `Event: 'error'`
     - [ ] `watcher.close()`

Other:
    
 - [ ] `Class: fs.ReadStream`
     - [ ] `Event: 'open'`
     - [ ] `Event: 'close'`
     - [ ] `readStream.path`
     - [ ] `fs.createReadStream(path[, options])`
 - [ ] `Class: fs.Stats`
 - [ ] `Class: fs.WriteStream`
     - [ ] `Event: 'open'`
     - [ ] `Event: 'close'`
     - [ ] `writeStream.bytesWritten`
     - [ ] `writeStream.path`
     - [ ] `fs.createWriteStream(path[, options])`
 - [ ] `fs.constants`
     - [ ] FS Constants
     - [ ] File Access Constants
     - [ ] File Open Constants
     - [ ] File Type Constants
     - [ ] File Mode Constants


### [`Console`](https://nodejs.org/api/console.html)

*Depends on:* `util`, `stream`, `fs`, `assert`

 - [ ] `new Console(stdout[, stderr])`
 - [ ] `console.assert(value[, message][, ...])`
 - [ ] `console.dir(obj[, options])`
 - [ ] `console.error([data][, ...])`
 - [ ] `console.info([data][, ...])`
 - [ ] `console.log([data][, ...])`
 - [ ] `console.time(label)`
 - [ ] `console.timeEnd(label)`
 - [ ] `console.trace(message[, ...])`
 - [ ] `console.warn([data][, ...])`


### [`dgram`](https://nodejs.org/api/dgram.html)

*Depends on:* 

 - [ ] `Class: dgram.Socket
     - [ ] `Event: 'close'`
     - [ ] `Event: 'error'`
     - [ ] `Event: 'listening'`
     - [ ] `Event: 'message'`
     - [ ] `socket.addMembership(multicastAddress[, multicastInterface])`
     - [ ] `socket.address()`
     - [ ] `socket.bind([port][, address][, callback])`
     - [ ] `socket.bind(options[, callback])`
     - [ ] `socket.close([callback])`
     - [ ] `socket.dropMembership(multicastAddress[, multicastInterface])`
     - [ ] `socket.send(msg, [offset, length,] port, address[, callback])`
     - [ ] `socket.setBroadcast(flag)`
     - [ ] `socket.setMulticastLoopback(flag)`
     - [ ] `socket.setMulticastTTL(ttl)`
     - [ ] `socket.setTTL(ttl)`
     - [ ] `socket.ref()`
     - [ ] `socket.unref()`
 - [ ] `dgram.createSocket(options[, callback])`
 - [ ] `dgram.createSocket(type[, callback])`

Below is list of already implemented API and roadmap on how the rest of the API will be implemented.

 - [`dgram.js`](https://nodejs.org/api/dgram.html), [`net.js`](https://nodejs.org/api/net.html) and [`http.js`](https://nodejs.org/api/http.html) networking stack will be implemented using `epoll` system calls.
 - [`fs.js`](https://nodejs.org/api/fs.html) -- *synchronous* functions are implemented in [`libfs`](http://www.npmjs.com/package/libfs)
 using system calls, also `libfs` will implement *asynchronous* `fs` calls in four ways:
    1. fake *async* wrappers around *synchronous/blocking* `fs` calls;
    2. thread pool where *blocking* function will be executed in parallel using `treads-a-go-go`, analogous to what `libuv` does;
    3. `Worker` pool, similar to *2.*, but less efficient;
    4. using *asynchronous* Linux system calls: `io_submit`.
 - [`dns.js`](https://nodejs.org/api/dns.html) will be replaced by [`node-dns`](https://github.com/tjfontaine/node-dns).
 - [`tls.js`](https://nodejs.org/api/tls.html) will be replaced by [`forge`](https://github.com/digitalbazaar/forge). 
 - [`https.js`](https://nodejs.org/api/https.html) will have to be put together using `http.js` and `tls.js`. 
 - [`zlib.js`](https://nodejs.org/api/tls.html) will be replaced by [`pako`](https://github.com/nodeca/pako).
 - For [`crypto.js`](https://nodejs.org/api/crypto.html) there is `browserify-crypto` and some other libraries we can use.
 - Pure JavaScript modules will be adopted *as-is*:
    - `assert.js`
    - `console.js`
    - `events.js`
    - `path.js`
    - `process.js`
    - `punycode.js`
    - `querystring.js`
    - `readline.js`
    - `repl.js`
    - `module.js`
    - `url.js`
    - `util.js`
    - `stream.js`
    - `string_decoder.js`
 - *Misc* V8 and Node.js specific modules:
    - `vm.js`
    - `v8.js`
    - `os.js`
    - `tty.js`
    - `timers.js`
 - These we need to think about:
    - `child_process.js`
    - `cluster.js`
