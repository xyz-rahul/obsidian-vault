every browser is based on some engine used to run js
node uses v8 engine (used by chrome)


## Synchronous
Synchronous is a blocking architecture and is best for programming reactive systems.
As a single-thread model, it follows a strict set of sequences, which means that operations are performed one at a time, in perfect order.
While one operation is being performed, other operations’ instructions are blocked. The completion of the first task triggers the next, and so on.

## Asynchronous
Asynchronous is a non-blocking architecture, which means it doesn’t block further execution while one or more operations are in progress. With async programming, multiple related operations can run concurrently without waiting for other tasks to complete.


os
fs
event 
http


important global obj

setTimeout()
clearTimeout()

setInterval()
clearInterval()


## structure of modules 
```javascript
{
  id: '.',
  path: '/Users/rahulkumar/dev',
  exports: {},
  filename: '/Users/rahulkumar/dev/main.js',
  loaded: false,
  children: [],
  paths: [
    '/Users/rahulkumar/dev/node_modules',
    '/Users/rahulkumar/node_modules',
    '/Users/node_modules',
    '/node_modules'
  ],
  [Symbol(kIsMainSymbol)]: true,
  [Symbol(kIsCachedByESMLoader)]: false,
  [Symbol(kIsExecuting)]: true
}

```

# Import and Export 


Exporting from JavaScript allows you to make functions, objects, or variables available for use in other JavaScript modules or scripts. There are several ways to export in JavaScript, depending on the environment and the JavaScript module system you are using:

1. **CommonJS (Node.js) Syntax:**
   
   ```javascript
   // Export a single function, object, or variable
   module.exports = functionName; // Exporting a function
   module.exports = { key: value }; // Exporting an object
   module.exports = variableName; // Exporting a variable

   // Export multiple functions, objects, or variables
   module.exports.functionName = functionName;
   module.exports.variableName = variableName;
   ```

`import`
```js
const fn_name = require('./module_name')
```
2. **ES6 Module Syntax:**
   
   ```javascript
   // Export a single function, object, or variable
   export default functionName; // Default export
   export { functionName }; // Named export

   // Export multiple functions, objects, or variables
   export { functionName, variableName };
   ```

   When using ES6 modules, you import exports using `import` statements:
   
   ```javascript
   // Importing a default export
   import functionName from './modulePath';

   // Importing named exports
   import { functionName, variableName } from './modulePath';
   ```

3. **Browser Global (Legacy):**

   If you are working with scripts that are loaded directly into the browser without any module system, you can attach functions, objects, or variables directly to the `window` object:
   
   ```javascript
   // Exporting to the global scope (window object)
   window.functionName = functionName;
   window.variableName = variableName;
   ```

Each method has its use case depending on your project setup and requirements. For modern JavaScript development, ES6 modules are increasingly the preferred method due to their support in modern browsers and Node.js with the `--experimental-modules` flag or newer versions.




## path

```javascript
const path = require('path');

// Example paths for demonstration
const path1 = '/foo/bar/baz/asdf/quux.txt';
const path2 = '/foo/bar/baz';

// path.join([...paths])
const joinedPath = path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// Joins all given path segments together using the platform-specific separator as a delimiter, then normalizes the resulting path.

// path.resolve([...paths])
const resolvedPath = path.resolve('foo/bar', '/baz');
// Resolves the specified paths into an absolute path.

// path.basename(path[, ext])
const basename = path.basename(path1);
// Returns the last portion of a path, similar to the Unix `basename` command.

// path.dirname(path)
const dirname = path.dirname(path1);
// Returns the directory name of a path, similar to the Unix `dirname` command.

// path.extname(path)
const extname = path.extname(path1);
// Returns the extension of the path, from the last occurrence of the `.` (dot) character to the end of the string in the last portion of the path.

// path.parse(pathString)
const pathObj = path.parse(path1);
// Returns an object from a path string, providing useful properties such as `dir`, `root`, `base`, `name`, and `ext`.

// path.normalize(path)
const normalizedPath = path.normalize('/foo/bar//baz/asdf/quux/..');
// Normalizes a given path, resolving `..` and `.` segments.

// path.relative(from, to)
const relativePath = path.relative(path1, path2);
// Returns the relative path from `from` to `to`.

// path.isAbsolute(path)
const isAbsolute1 = path.isAbsolute(path1);
const isAbsolute2 = path.isAbsolute('foo/bar');
// Determines if the given path is an absolute path.

// path.sep
const pathSeparator = path.sep;
// Platform-specific path segment separator (`\` on Windows, `/` on POSIX).

// path.delimiter
const pathDelimiter = path.delimiter;
// Platform-specific path delimiter (`:` on POSIX, `;` on Windows).
```

## os
```javascript
const os = require('os');

// os.arch()
const architecture = os.arch();
// Returns the operating system CPU architecture.

// os.cpus()
const cpus = os.cpus();
// Returns an array of objects containing information about each CPU/core installed.

// os.totalmem()
const totalMemory = os.totalmem();
// Returns the total amount of system memory in bytes.

// os.freemem()
const freeMemory = os.freemem();
// Returns the amount of free system memory in bytes.

// os.homedir()
const homeDirectory = os.homedir();
// Returns the path to the current user's home directory.

// os.hostname()
const hostname = os.hostname();
// Returns the hostname of the operating system.

// os.platform()
const platform = os.platform();
// Returns the operating system platform (e.g., 'darwin', 'win32', 'linux').

// os.release()
const release = os.release();
// Returns the operating system release.

// os.tmpdir()
const tempDirectory = os.tmpdir();
// Returns the operating system's default directory for temporary files.

// os.type()
const osType = os.type();
// Returns the operating system name.

// os.uptime()
const uptime = os.uptime();
// Returns the system uptime in seconds.

// os.userInfo([options])
const userInfo = os.userInfo({ encoding: 'utf8' });
// Returns information about the current user.

// os.endianness()
const endianness = os.endianness();
// Returns the endianness of the CPU ('BE' for big endian, 'LE' for little endian).

// os.constants
const constants = os.constants;
// An object containing various OS-specific constants.

```


## fs

```javascript
const fs = require('fs');

// Asynchronous functions
fs.readFile('/path/to/file.txt', 'utf8', (err, data) => {});
fs.writeFile('/path/to/newfile.txt', 'content', 'utf8', (err) => {});
fs.appendFile('/path/to/file.txt', 'data to append', 'utf8', (err) => {});
fs.rename('/path/to/oldfile.txt', '/path/to/newfile.txt', (err) => {});
fs.unlink('/path/to/file.txt', (err) => {});
fs.mkdir('/path/to/newdir', { recursive: true }, (err) => {});
fs.readdir('/path/to/dir', { withFileTypes: true }, (err, files) => {});
fs.stat('/path/to/file.txt', (err, stats) => {});

// Synchronous functions (not recommended for heavy I/O operations)
fs.readFileSync('/path/to/file.txt', 'utf8');
fs.writeFileSync('/path/to/newfile.txt', 'content', 'utf8');
fs.appendFileSync('/path/to/file.txt', 'data to append', 'utf8');
fs.renameSync('/path/to/oldfile.txt', '/path/to/newfile.txt');
fs.unlinkSync('/path/to/file.txt');
fs.mkdirSync('/path/to/newdir', { recursive: true });
fs.readdirSync('/path/to/dir', { withFileTypes: true });
fs.statSync('/path/to/file.txt');
```

## event

```javascript
const EventEmitter = require('events');

// Create an EventEmitter instance
const emitter = new EventEmitter();

// Event listener registration
emitter.on('event', (arg1, arg2) => {
    console.log('Event occurred with arguments:', arg1, arg2);
});

// Emitting an event
emitter.emit('event', 'arg1value', 'arg2value');

// Removing an event listener
function listenerFunction(arg1, arg2) {
    console.log('Listener function called with arguments:', arg1, arg2);
}
emitter.on('anotherEvent', listenerFunction);
emitter.emit('anotherEvent', 'foo', 'bar');
emitter.removeListener('anotherEvent', listenerFunction);


```


