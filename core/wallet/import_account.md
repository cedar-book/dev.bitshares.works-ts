## How to import a GUI-wallet account into CLI-wallet

CLI and GUI wallet are two separated applications. They use separated ways to represent backups. You can manually import keys from the GUI into the CLI to have a CLI-wallet.

Your wallet private keys have extremely important roles. By importing your private keys to a new CLI-wallet, you can control your account funds from the CLI-wallet. 

### 1.Find your private keys in your GUI-wallet

- Login to your GUI-wallet
- Go to [Settings] – [Permissions]. There are Active, Owner, and Memo tabs. 
- In the each tab, click your public key (or the key image). It will open a private key viewer.
- On the form, click [Show], (it might ask you to login) save your each private key and public key information to use later.

### 2.Connect to a CLI-wallet pointing it to a live node

Example:

    ./programs/cli_wallet/cli_wallet --server-rpc-endpoint ws://localhost:8090
    Or 
    ./programs/cli_wallet//cli-wallet -s wss://bitshares.openledger.info/ws

You should get a prompt

    new>>>
    
### 3.Set a password and unlock    

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


### 5.Check your account

Use `list_my_account`s to see your imported account.

And to check balance:

    unlocked >>> list_account_balances your-account-name
    list_account_balances your-account-name
    31016.69330 BTS
    0 CNY
    0 USD

    unlocked >>>

### Often use Commands 




