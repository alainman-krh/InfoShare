## `Controller`/`worker` chains (C/W-chains): a unifying framework
**NOTE**: Not sure if these definitions are correct. Slowly building them up.

# C/W-chain: introduction
<!----------------------------------------------------------------------------->
This section, will introduce the "`controller`/`worker` chain" (C/W-chain): a
new framework intended to unifying existing concepts such as the
`client`/`server`, and `master`/`slave` architectures.

It is hoped that the terminology resulting from the C/W-chain viewpoint will
help highlight both the strengths and weaknesses of different software
architectures, and therefore simplify the associated design/documentation
efforts.

For example the C/W-chain framework should assist in:
- Identifying which component is the "`client`", and which is the "`server`".
- Selecting more intuitive names for software components/modules/etc.

# C/W-chain: examples
<!----------------------------------------------------------------------------->
### Concrete examples of "links"
- `user`/`terminal` link: Historically a physical connection between human and
  a "terminal" (keyboard in, display out). In modern computers, this interface
  has been extended by multiple links, making the implementation significantly
  more complex. That said, the resulting user experience should be seamless.
- `terminal`/`REPL` link: Read-Evaluate-Print-Loops make it possible for the
  user to input data from the terminal, and see what they are typing.
- `shell`/`OS` link: The shell embeds a REPL module, and provides (hopefully)
  basic/uniform access to the underlying operating system.

### Generic examples of "links"
Eventually, software developers formed more practical design patterns,
and named them to facilitate communication of their solutions:
- `master`/`slave` link: A single `master` (`controller`) orchestrates
  communication with multiple `slaves` (`workers`).
- `client`/`server` link: This design pattern supports multiple `controllers`
  simultaneously requesting services from a single `server`. To accomplish
  this feat, `servers` employ a `listener` process to orchestrate the
  distribution of work. If resources are available, the `listener` spins
  up new `worker` threads, and connects them with their `clients`
  (`controllers`).

### "Complete" example of a chain
A "console application" is a good starter example of a simple
`controller`/`worker` software chain. The following list hilights individual
C/W-chain links using the "`<-C/W->`" token:
- end user <-C/W-> terminal <-C/W-> REPL <-C/W-> shell <-C/W-> OS: app launcher
- OS <-C/W-> console application <-C/W-> OS: SATA controller <-C/W-> HDD controller <-C/W-> hard drive.

**Note**: the chain described above was split into two segments for the sake of
readability. Multiple links were also omitted in an effort to keep the example
tractable.

# Expanding on terminology
<!----------------------------------------------------------------------------->
### Core definitions
- User/"end user": A human `controller` trying to accomplish a task.
- User (analogy): Entity external to a given software component (not
  necessarily human), acting as a `controller` to the service being provided.


### Server (disambiguation)
- Server (hardware): A physical computer providing a service for a user/`controller`.
- Server (virtualization): A sub-allocation of physical server hardware
  (Virtual Machine; VM) acting as an (mostly) independent virtual computer, also
  providing a service for a user/`controller`. For optimum performance,
  sub-allocations might dedicate entire hardware components to a VM, but often
  needs to provide time-shared (arbitrated) access to said physical resources.
- Server (client-server): Software providing a service. Services typically run
  continuously in the background on server hardware (or VM).
- Server (client-server)

### Networking definitions

# Request - Worker
<!----------------------------------------------------------------------------->


# Client-Server
<!----------------------------------------------------------------------------->
Definitions
- `Clent`: makes requests for a service (to be performed by the `Server`).
- `Server`:
- `Listener`: root process that listens for TCP/IP connection requests,
  and spins up `worker` threads

### More info about `listen`
Source: <https://stackoverflow.com/questions/34073871/socket-programming-whats-the-difference-between-listen-and-accept>:
> `listen` prepares socket for the next `accept` call. `Listen` also allows one to
> setup the backlog - the number of connections which will be accepted by the
> system, and than put to wait until your program can really `accept` them.
> Everything which comes after the backlog is full well be rejected by the
> system right away.
> `listen` never blocks, while `accept` will block (unless the socket is in
> non-blocking mode) until the next connection comes along. Obviously, this
> does not have to be two separate functions - it is conceivable that
