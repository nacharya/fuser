# Outerbanks changes 

All the changes we mention here are for [fuser fork](http://github.com/nacharya/fuser.git)
The original for this fork is [fuser](https://github.com/cberner/fuser)
The early versions for Rust were called `rust-fs` or `fuse-rs`. Some of them 
still exist and the crates are found but are not that current. 
The most current version is `fuser`


### **MacOS related**

Installation 

```bash
% brew install macfuse 
```
Make sure the `cargo deny` works on the system

```bash
% cargo install cargo-deny
```

```bash
% cargo clippy --fix --example "simple" --allow-staged --allow-dirty
```
or simply
```bash
% make macfix
```
Now only build the stuff we need in Mac OS X
```bash
% make macbuild
```


### **Debian12 Related**

Installation 
```bash
% sudo apt install fuse3 libfuse3-dev -y
```

Build the entire set
```bash
% make
```
### Simple tests 

Run a simple hello world session 

Modify the file `/etc/fuse.conf` and enable the field `user_allow_other`
This is a handy field *only* during development as we rely on the `--auto_unmount`
feature for ease of use. 

Now let's look at the `hello` fuse 

Shell 1
```bash
% cd target/debug/examples
% mkdir foo
% ./hello --auto_unmount ./foo/
```

Now in another window, fo to the `foo` directory used above

Shell 2
```bash
% cd target/debug/examples/foo
% ls
hello.txt
% cat hello.txt
Hello World!
% cd ..
```

Here is a simple cleanup 

Shell 1
```bash
% % ./hello --auto_unmount ./foo/
% ^C
%
```

Shell 2
```bash
% cd target/debug/examples
% rm -rf foo
```
