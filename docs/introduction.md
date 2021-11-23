---
title: Introduction
subtitle:
tags: [speculos, emulate, emulator, Nano X emulator]
category: Speculos
author:
toc: true
layout: doc
sort: 6
---


The goal of the Speculos project is to emulate Ledger Nano S, Nano X and Blue apps on
standard desktop computers, without any hardware device. Click here to be redirect to [the Speculos GitHub repository](https://github.com/ledgerhq/speculos).

Usage example:

```shell
./speculos.py apps/btc.elf
# ... and open a browser on http://127.0.0.1:5000
```

## Bugs and contributions

Feel free to open issues and create pull requests on [the Speculos GitHub repository](https://github.com/ledgerhq/speculos).

The `master` branch is protected to disable force pushing. Contributions should
be made through pull requests, which are reviewed by @LedgerHQ members before
being merged to `master`:

- @LedgerHQ members can create branches directly on the repository (if member of
  a team with write access to the repository)
- External contributors should fork the repository


## Limitations

The emulator handles only a few syscalls made by common apps; for instance,
syscalls related to app install, firmware update or OS info can't be
implemented.

There is absolutely no guarantee that apps will have the same behavior on
hardware devices and Speculos:

- Invalid syscall parameters might throw an exception on a real device while
  being ignored on Speculos.
- Attempts to perform unaligned accesses when not allowed (eg. dereferencing a
  misaligned pointer) will cause an alignment fault on a hardware device.


## Security

Apps can make arbitrary Linux system calls (and use QEMU
[semihosting](../user/semihosting) features), thus don't run Speculos on
untrusted apps.

It's worth noting that the syscall implementation (`src/`) doesn't expect
malicious input. By the way, in Speculos, there is no privilege separation
between the app and the syscalls. This doesn't reflect the security of the
firmware on hardware devices where app and OS isolation is enforced.

Speculos is not part of Ledger bug bounty program.