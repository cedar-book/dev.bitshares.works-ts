## Getting Started

> See [System Requirements](../nodes_full_witness/full_nodes.md#system-requirements) if you are interested to run a node (updated: 2018-07-02).

BitShares Core is the BitShares blockchain implementation and command-line interface. The web wallet is [BitShares UI](https://github.com/bitshares/bitshares-ui).

Visit [BitShares.org](https://bitshares.org/) to learn about BitShares and join the community at [BitSharesTalk.org](https://bitsharestalk.org/).


> NOTE: The official BitShares git repository location, default branch, and submodule remotes were recently changed. Existing repositories can be updated with the following steps:

    git remote set-url origin https://github.com/bitshares/bitshares-core.git
    git checkout master
    git remote set-head origin --auto
    git pull
    git submodule sync --recursive
    git submodule update --init --recursive


***

### Installation and Build
Select an operation system and install and build.

- [Ubuntu Linux](../installation/build_ubuntu.md#building-on-ubuntu)
- [OS X](../installation/build_osx.md#building-on-os-x)
- [Windows](../installation/build_windows.md#building-on-windows)
- [Windows - CLI Tools](../installation/windows_cli_tool.md#cli-wallet-on-windows-x64)

### Build and Run BitShares-Core in WSL (Installation Option)
- Use **Windows Subsystem for Linux**
  - [Instruction how to prepare Ubuntu to Windows 10 OS](../installation/wsl.md#windows-subsystem-for-linux-wsl) 

***

### Known issues

- [Boost versions](../installation/boost_versions.md#boost-version)

***

