List cgroups info in a tree
====

Like `systemctl status`, but different info attached.

Requirement
----

* Python 3.8+
* cgroups v2 (unified hierarchy)
* less

Usage
----

```
$ ./cgtree --help
usage: cgtree [-h] [-p] (--swap | --zswap | --memory)

show cgroup metrics in a tree

options:
  -h, --help     show this help message and exit
  -p, --process  show processes in group
  --swap         show swap and zswap usage
  --zswap        show decompressed and compressed zswap usage
  --memory       show current and peak memory usage
```

Example output:

```
$ ./cgtree -p --memory
/ [cur: 104.6MiB, swap: 16.0KiB, peak: 104.6MiB]
├─init.scope [cur: 1.7MiB, swap: 0B, peak: 2.8MiB]
│ └─1 /usr/lib/systemd/systemd
├─dev-hugepages.mount [cur: 3.2MiB, swap: 0B, peak: 3.9MiB]
├─user.slice [cur: 34.2MiB, swap: 0B, peak: 34.2MiB]
│ └─user-1000.slice [cur: 34.2MiB, swap: 0B, peak: 34.2MiB]
│   ├─user@1000.service [cur: 5.0MiB, swap: 0B, peak: 7.2MiB]
│   │ └─init.scope [cur: 36.0KiB, swap: 0B, peak: 324.0KiB]
│   │   ├─68 /lib/systemd/systemd --user
│   │   └─69 (sd-pam)
│   └─session-16.scope [cur: 29.2MiB, swap: 0B, peak: 29.2MiB]
│     ├─65 sshd: lilydjwg [priv]
│     ├─86 sshd: lilydjwg@pts/1
│     ├─127 -zsh
│     └─147 /usr/bin/python3 ./cgtree -p --memory
└─system.slice [cur: 49.7MiB, swap: 16.0KiB, peak: 75.6MiB]
  ├─console-getty.service [cur: 308.0KiB, swap: 0B, peak: 656.0KiB]
  │ └─58 /sbin/agetty -o -p -- \u --noclear --keep-baud console 115200,38400,9600 tmux-256color
  ├─systemd-logind.service [cur: 1.5MiB, swap: 0B, peak: 2.0MiB]
  │ └─54 /lib/systemd/systemd-logind
  ├─dbus.service [cur: 2.6MiB, swap: 0B, peak: 3.0MiB]
  │ └─52 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
  ├─ssh.service [cur: 6.4MiB, swap: 0B, peak: 7.6MiB]
  │ └─60 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
  └─systemd-journald.service [cur: 27.9MiB, swap: 4.0KiB, peak: 29.6MiB]
    └─17 /lib/systemd/systemd-journald
```

If you use Vim, you can use [vim-foldtree](https://github.com/lilydjwg/vim-foldtree) to view a foldable tree inside Vim.
