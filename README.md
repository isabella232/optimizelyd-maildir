# optimizelyd-maildir 

This is another approach to implementing optimizelyd as a maildir queue implementation.  Right now, it is a very generic maildir queue consumer that takes files from new moves them to cur, sends them via json if a request body was provided.  If there is no request body it is sent as a GET.  The response is read but not consumed at this point. The queued items are json human readable files that contain a url and a request body.

* since it uses the filesystem, it is very transparent and also easy to understand from an ops perspective.  
* it is very easy to scale via nfs mount (there can be several queue writers but only one queue consumer at this time). 
* it uses os calls.
For these reasons, the [Rust](https://www.rust-lang.org/en-US/) programming language was chosen for implementation.

## Background
The queue is based on the lockes maildir queue.  The maildir queue file structure is shown below:
![Maildir structure](https://en.wikipedia.org/wiki/Maildir#/media/File:Maildir.png)

https://en.wikipedia.org/wiki/Maildir


## Project status

* `src/` contains implementation of the maildirqueue, the jsonsender, and the main module to drive the consuming.
* `examples/` contains a sample maildirqueue directory.  You can test by running ../optimizelyd-maildir client for client test and leave off the client if you want the server side.  

## Building

cargo build

### Prerequisites

```sh
# Install [rustup](https://github.com/rust-lang-nursery/rustup.rs), the Rust toolchain manager,
# with the instructions found at https://rustup.rs/. Current instructions as of May 2017:
curl https://sh.rustup.rs -sSf | sh

# Bash users, you can persist the just-installed CLI tools to your $PATH with
echo 'export PATH=$HOME/.cargo/bin:$PATH' >> ~/.bash_profile`
```

### Compiling, running tests, etc.

```sh
# From the repo root,
cargo build

