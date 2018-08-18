## Introduction & Architectures 

#### Table of Contents:
- [BitShares Architecture  ](#bitshares-architecture--github-repositories-and-entities)
- [Development Environments and Requirements](#development-environments-and-requirements)
- [BitShares Core Projects Guide](#bitshares-core-projects-guide)
- [BitShares Core Code Management - GitFlow](#bitshares-core-code-management---gitflow)
- [Your purpose and a download branch](#your-purpose-and-a-download-branch)

***

Welcome to BitShares! In this section, you will find the overview of BitShares Architecture (repositories and entities), and how the Core team processes the development work.  If you are interested in contributing to the Core team, you might want to check the Contribution Guide and the GitFlow to understand how BitShares-Core team handles the repository files and branches.  If you would like to know the Core team current project, issues, and the releases plans, check under the Issues and the Projects tabs.

### BitShares Architecture – GitHub Repositories and Entities
- [GitHub Repositories and Entities with a guide (pdf)](../knowledge_base/shared_files/BitShares_Architecture-V3.pdf) 

![BitShares Architecture](../imgs/structure/bitshares-architecture-v3notop.png)


### Development Environments and Requirements

BitShares offers you to install BitShares-Core into different platforms; **Linux:Ubuntu (x64), OSx, and Windows**.  There are  dependencies to check when you download OpenSSL and  Boost. Please make sure which versions you downloaded. 

Also, if you are a Windows user, you have other two choices to install BitShares Core to your Windows (x64) Operation System.  One is **CLI-Wallet tools for Windows (x64)**, another is **Windows SubSystem for Linux (WSL)**.  

The CLI-wallet tools for Windows (x64) allows you to try several methods to get the data from BitShares blockchain without the BitShares Core installation. After you download the cli-wallet tools, you will find a cli_wallet executable to try Wallet API. 

Another option, Windows SubSystem for Linux (WSL).  This is for a developer who uses a Windows 10 (x64) Operation System and wants to build BitShares Core on Ubuntu. 

> See [System Requirements](../nodes_full_witness/full_nodes.md#system-requirements) to run a node (updated: 2018-07-02).

### BitShares code and files 

- Open Source program
- Language uses (mainly): BitShares-Core(C++), python
- BitShares GitHub 
  - **BitShares-Core (C++)** - BitShares Blockchain implementation and command-line interface.
  - **Bitshares-FC** - Fast-compiling C++ library 
  - **BitShares python** - Fully featured client-side library for the BitShares Blockchain - written entirely in python.
  - **BitShares-UI** - Fully featured Graphical User Interface / Reference Wallet for the BitShares Blockchain.
  - **BSIPs** - BitShares Improvement Proposals and Protocols. These technical documents describe the process of updating and improving the BitShares blockchain and technical ecosystem.
  - **BitSharesjs** - JavaScript tools for BitShares Encryption and Serialization.
  - **BitSharesjs-ws** - Javascript websocket interface for Bitshares 
  - more
  
  
### BitShares Core Projects Guide
- [Contribution Guide](../intro/contribution_guide.md#contribution-guide) [DRAFT]
- [Contribution Guide Project](https://github.com/bitshares/bitshares-core/projects/6)

**BitShares-Core (Team) :**
This is a team of developers who manage BitShares-Core code updates and handle the issues that are submitted by developers. The team creates a project plan of next release and delivers to the Bitshares community about the Project information. 
  - **Roles** 
    - improving
    - maintaining
    - upgrading protocol if needed
    - making Project plans for the future release
    - creating/ announcing  Release 
    
### BitShares Core Code Management - GitFlow
This section describes and defines how changes flow into our code and through the various stages of development until it finally goes into production.

- [Purpose](../intro/bitshares_core_gitflow.md)
- [Non-Consensus: Development / Release / Bugfix Workflows](../intro/bitshares_core_gitflow.md#non-consensus-development--release--bugfix-workflows)
- [Consensus: Development / Release / Bugfix Workflows](../intro/bitshares_core_gitflow.md#consensus-development--release--bugfix-workflows)
- [Goals To Achieve](../intro/bitshares_core_gitflow.md#goals-to-achieve)
- [Basic Rules](../intro/bitshares_core_gitflow.md#basic-rules)
- [How To Create a Release](../intro/bitshares_core_gitflow.md#how-to-create-a-release)
- [How To Create an Emergency Fix](../intro/bitshares_core_gitflow.md#how-to-create-an-emergency-fix)
- [Emergency Fix Workflows](../intro/bitshares_core_gitflow.md#emergency-fix-workflows)

***

### Your purpose and a download branch
The below table list is just a guide. If you are interested to learn BitShares Node or CLI wallet, using TestNet might be adequate to start. If you are a developer who is interested to contribute to the BitShares Core team, downloading a developer branch might be a good start. Select an appropriate branch when you install BitShares-Core.  

After you know which branch to download, your next step is the installation of BitShares-Core. Check the [BitShares Installation Guide](../installation/README.md#install-a-development-environment) and select your Operation System to follow the installation steps. 

Your purpose might be trying some API calls to query the BitShares Blockchain data, using a CLI Wallet to manage your assets, or running a node. In any events, you will create an account and interact with the blockchain. If you install BitShares-Core, it would be a better understanding of the BitShares Node and System Requirements. So, we recommend you to read [the BitShares Nodes](../nodes_full_witness/README.md#bitshares-nodes-and-p2p-network) section and [BitShares Accounts](../accounts/README.md#bitshares-accounts) section before the installation. 


|   purpose      | Extract only |Tx+not modify code| Tx+modify code | Develop branch | Release branch |Testnet: may use|
| ------------------- |:----------:|:---:|:---:|:---:|:---:|:---:|
| Only Extract Data from the Blockcahin |[X] |  |  |  | install | public|
| Want to use BitShares Blockchain for business | | [x] |  |  | install |(public) |
| Want to help the Core Team          | |  | [x] |install  |  |public |
| Fork: experiment with changes, etc  | |  | [x] | Entire Core repo | Entire Core repo |private |
| Want to develop own application     | |  | [x] |  | install |private |
| Want to build tools for trading     | |[x] | |  | install |private |
| Want to create a custom blockchain  | |  | [x] |  | install |private |


***


