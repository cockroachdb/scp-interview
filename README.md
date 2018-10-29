# SCP interview

## Setup

To enable SSH to yourself on macOS:

```shell
$ sudo systemsetup -setremotelogin on
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

On Linux, you'll need to consult your distribution's documentation.

You can verify that SSH is setup properly by running:

```shell
$ ssh localhost echo "All set!"
All set!
```

If you see any output besides "All set", something is not configured correctly.

You should additionally "build" a "binary" by running:

```shell
$ bin/build
```

The resulting "binary" will be named build/customdb.

## Interface

You must implement a bin/dist command that satisfies the following synopsis:

```shell
$ bin/dist BINARY HOSTS
```

BINARY is the file to be distributed to each host. HOSTS is a file that lists
the targets to which BINARY should be distributed. Each line in HOSTS has the
following form:

```
MACHINE:TARGET-PATH
```

bin/dist must copy the binary to the desired TARGET-PATH on each MACHINE. Note
that TARGET-PATH is not necessarily the same on each machine.

## Benchmarking

The time it takes bin/dist to distribute a binary to a cluster of eight
"remote" machines is measured by bin/bench. Note that bin/bench simulates
network latencies between the local machine and the hosts listed in HOSTS.

## Cleanup

On macOS, you may want to disable remote login like so:

```
sudo systemsetup -setremotelogin off
```

You'll also want to delete any files starting with "scp-interview" in your home
directory:

```
rm ~/scp-interview*
```
