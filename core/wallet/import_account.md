## How to import a GUI-wallet account into CLI-wallet

#### Table of Contents:
  1. [Find your private keys in your GUI-wallet](../wallet/import_account.md#1-find-your-private-keys-in-your-gui-wallet)
  2. [Connect to a CLI-wallet pointing it to a live node](../wallet/import_account.md#2-connect-to-a-cli-wallet-pointing-it-to-a-live-node)
  3. [Set a password and unlock](../wallet/import_account.md#3-set-a-password-and-unlock)
  4. [import key(s)](../wallet/import_account.md#4-import-keys)
  5. [Check your account](../wallet/import_account.md#5-check-your-account)
  6. [Often used Commands ](../wallet/import_account.md#often-used-commands)

***

CLI and GUI wallet are two separated applications. They use separated ways to represent backups. You can manually import keys from the GUI into the CLI to have a CLI-wallet.

Your wallet private keys have extremely important roles. By importing your private keys to a new CLI-wallet, you can control your account funds from the CLI-wallet. 

### 1. Find your private keys in your GUI-wallet

  1. Login to your GUI-wallet
  1. Go to [Settings] – [Permissions]. There are Active, Owner, and Memo tabs. 
  3. In the each tab, click your public key (or the key image). It will open a private key viewer.
  4. On the form, click [Show], (it might ask you to login) save your each private key and public key information to use later.
  
  > Important: Keep the private keys information to a safe place. 

### 2. Connect to a CLI-wallet pointing it to a live node

Example:

    ./programs/cli_wallet/cli_wallet --server-rpc-endpoint ws://localhost:8090
    Or 
    ./programs/cli_wallet//cli-wallet -s wss://bitshares.openledger.info/ws

You should get a prompt

    new>>>
    
### 3. Set a password and unlock    

Set a password for your CLI-wallet and unlock.

**Note:** This password does not need to be the same with your GUI-wallet password. You will create a *new wallet* and it will be secured by the new password.

    new >>> set_password mypass123
    set_password mypass
    null
    
    locked >>> unlock mypass123
    unlock mypass123
    null
    unlocked >>>

### 4. import key(s)

Import your each private key you saved from your GUI-wallet into your new CLI-wallet.

    import_key your-account-name ThisIsThePrivateKeyYouSaved

And you are done. No need to claim balance. Your account balances are in there. 

> Note: If you use the wallet to transfer funds, you just need to import the active private key. However, if you have different Active and Memo keys and use a Memo when you transfer, import the memo private key also. 

### 5. Check your account

Use `list_my_account`s to see your imported account.

And to check balance:

    unlocked >>> list_account_balances your-account-name
    list_account_balances your-account-name
    31016.69330 BTS
    0 CNY
    0 USD

    unlocked >>>

### Often Used Commands 


| | | |
|---|---|---|
| `set_password` |  | set a password to a cli wallet  |
| `unlock` | a wallet by the password  |  |
| `gethelp` | to see a command description. (e.g., gethelp "list_accounts")  |  |
| `info` | to view the current synchronization |  |
| `about` | |  |
| `import_key` | `import_key <name> "<wifkey>"` | use an existing account and the private key |
| `list_my_account` | to view the current synchronization |  |
| `get_account` |   |  |
| `import_balance` | import_balance <name> ["*"] true |  |
| `suggest_brain_key` |   |  |   
| `suggest_brain_key` |   |  |       
| `upgrade_account` | upgrade_account faucet true  | to get a LTM (Lifetime Member status |
| `register_account` | `register_account <name> <owner-public_key> <active-public_key> <registrar_account>  <referrer_account> <referrer_percent> <broadcast>` |  |
| `transfer` | `transfer <from> <to> <amount> <asset> <memo> <broadcast>` |  |
| `transfer2` | `transfer2 <from> <to> <amount> <asset> <memo> <broadcast>`  | return a transaction ID |
| `get_account_history` | e.g., get_account_history "name" "5" |  |     
| `get_privatre_key` |  get_privatre_key <public key>  | |
  
***



