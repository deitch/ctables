# ctables
Control iptables inside a container from the underlying host

## Install
Just copy the ctables file to your underlying host and place in your executable path, e.g. `/usr/local/bin/ctables`. Make sure it is executable, `chmod a+x /usr/local/bin/ctables`.

## Usage

    ctables <command> <container>

Where:

* `command`: one of `up` or `down`
* `container`: container ID or name

You can run `up` multiple times, it is idempotent. If the container's network already is `up`, it will leave it as is. Similarly, you can run `down` multiple times. If the container's network already is down, it will leave it as is. 

You only need one invocation of `up` to reverse 1, 2 or 1,000 `down`; you only need one invocation of `down` to reverse 1, 2 or 1,000 `up`.

## How it works
When you invoke `down`, ctables does the following:

1. Find the container by name or ID
2. Enter the container and add an iptables rule to drop all inbound traffic
3. Enter the container and add an iptables rule to drop all outbound traffic

When you invoke `up`, ctables does the following:

1. Find the container by name or ID
2. Enter the contaienr and remove any rules that block all inbound traffic
3. Enter the contaienr and remove any rules that block all outbound traffic

## License
See the LICENSE file.

