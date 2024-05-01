# Example of Using the **child_process**

spawn()

### **Spawn**

Spawn in computing refers to a function that loads and executes a new child process. The current process may wait for the child to terminate or may continue to execute concurrent computing. Creating a new subprocess requires enough memory in which both the child process and the current program can execute.

[Wikipedia](<https://en.wikipedia.org/wiki/Spawn_(computing)>)

Spawn (computing)

function in

Node.js

### **Node.js**

Node.js is a cross-platform, open-source JavaScript runtime environment that can run on Windows, Linux, Unix, macOS, and more. Node.js runs on the V8 JavaScript engine, and executes JavaScript code outside a web browser. Node.js lets developers use JavaScript to write command line tools and for server-side scripting.

[Wikipedia](https://en.wikipedia.org/wiki/Node.js)

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ82uBPqnWciRtiFtYrB3OCdcaZLC789VVaMpSBQzC3S1we1p12)

[Wikipedia](https://en.wikipedia.org/wiki/File:Node.js_logo.svg)

More about Node.js

Run this and all code blocks above⇧↵

Run this code block⌥⇧↵

```typescript
const { spawn } = require('child_process');

const child = spawn('ls', ['-lh', '/usr']);

child.stdout.on('data', (data) => {
	console.log(`stdout: ${data}`);
});

child.stderr.on('data', (data) => {
	console.error(`stderr: ${data}`);
});

child.on('close', (code) => {
	console.log(`child process exited with code ${code}`);
});
```

This code will spawn a new process that will execute the `ls` command with the arguments `-lh` and `/usr`. The `stdout` and `stderr` events are used to listen for data from the child process, and the `close` event is used to listen for the child process to exit.

**Here is an example of the output of this code**:

Execution output

```bash
stdout: total 20
drwxr-xr-x 2 user user 4096 Apr 29 16:30 .
drwxr-xr-x 3 user user 4096 Apr 29 16:30 ..
-rw-r--r-- 1 user user   35 Apr 29 16:30 .bash_history
-rw-r--r-- 1 user user   69 Apr 29 16:30 .bash_profile
-rw-r--r-- 1 user user 1024 Apr 29 16:30 .bashrc
drwx------ 2 user user 4096 Apr 29 16:30 .cache
drwx------ 3 user user 4096 Apr 29 16:30 .config
...
```

The `child_process.spawn()` function is a powerful tool that can be used to spawn

child processes

### **Child process**

A child process in computing is a process created by another process. This technique pertains to multitasking operating systems, and is sometimes called a subprocess or traditionally a subtask. There are two major procedures for creating a child process: the fork system call and the spawn.

[Wikipedia](https://en.wikipedia.org/wiki/Child_process)

![](https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcS5ExisfxqSZAOMjGtxSs5i_3pt5T32nYKzhv7jKGuKZHJgqgkK)

[GraphQL (The Guild)](https://the-guild.dev/blog/nodes-child-process)

More about child processes in Node.js. It can be used to execute commands, open files, and even start other Node.js applications.
