# FAQ: growing a Windows C: drive from free space on the same disk

Short answers to the questions I get about extending C: when there is no new disk in the budget. Disclosure first: I work on ScsExpand (https://expand.scsoi.com/), so the product mentions are biased; the Windows behaviour described here is not.

## Does it reformat or merge the partitions?

No. Free space is taken from another partition **on the same physical disk** and given to C:. No reformat, no partition merge, and the files stay in place — the capacity moves from one partition to another. Nothing is copied and nothing is deleted.

## What exactly cannot be done?

The pre-check refuses these **before** starting, with the reason spelled out, instead of starting an operation that ends in a format prompt:

- free space that lives on a **second physical disk** (that is a different operation entirely),
- a **BitLocker**-locked volume,
- a **non-NTFS** source partition — FAT32, for example,
- **dynamic disks**.

## Is the restart a WinPE session?

No. One restart is needed, and the heavy work runs in a **guided restart environment**: a small boot agent is prepared, a one-time boot entry is registered, the machine restarts, the resize is applied, and Windows comes back on its own.

## What does it cost?

Ad-free, and the free download *is* the trial: one expansion of up to 5 GB, with the quota counted by expansion count and size rather than by trial days. A one-time buyout then allows unlimited expansions and size, limited only by the free space on the disk. There is no subscription to cancel.

## What should I check before I start?

- **Back up first.** Of the operations in this family, resizing the system partition is the one that can cost you data.
- Know which kind of "unallocated space" you actually have. Three different things get called that in a partition table, and they are not interchangeable.
- If you use BitLocker, suspend it yourself before the operation and turn it back on afterwards.

## Where to get it

Official site and downloads: https://expand.scsoi.com/

The longer measured write-up — the three kinds of unallocated space, the three expansion routes and their failure signs — is here: https://github.com/shuyingegit/scsexpand-volume-expand-guide
