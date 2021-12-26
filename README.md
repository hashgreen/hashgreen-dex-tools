# Hashgreen DEX Tools

In this repository, we generate "offer files" for Hashgreen DEX testing on `testnet10`. 

## Prerequisite

### Prepare a Chia wallet key

If you already have a 24-word mnemonic key, you can ignore this part.

    Do `chia keys generate && chia keys show --show-mnemonic-seed | tail -n1 > ./key` after `chia init` has been done.
    You will generate a key at `./key`.

### Libraries
- MacOS (Intel): `brew install boost cmake gmp node`.
- MacOS (M1): 

    ```bash
    arch -arm64 brew install boost cmake gmp node
    brew reinstall python
    ```

- Windows (WSL):

    ```bash
    # https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
    nvm install --lts
    sudo apt install libatk1.0-0 libatk-bridge2.0-0 libgdk_pixbuf-2.0 libgtk2.0-0 libgtk-3-0 libgbm1
    ```

## Chia Wallet Offer

1. Clone the Chia Blockchain repository.

    ```bash
    git clone https://github.com/Chia-Network/chia-blockchain.git
    cd chia-blockchain
    git checkout 7b277e991efdfc20dfb50ac10b0fdefc0903d45d
    ```

2. Install the Chia library.
    
    ```bash
    sh install.sh
    source activate
    ```

3. Configure the Chia library.

    If you have an existing key, copy it to `./key`. 
    If not, you will need a key file following [Prerequisite: Prepare a Chia wallet key](#prepare-a-chia-wallet-key).
    
    ```bash    
    chia init
    chia configure --testnet true
    chia configure --log-level INFO
    chia configure --upnp false
    chia keys add -f ./key
    # or if you have your 24-word mnemonics, do `chia keys add` for the prompt
    ```

4. Build the Chia GUI library.

    ```bash
    sh install-gui.sh
    cd chia-blockchain-gui
    npm run electron &
    ```

5. Wait until the wallet is synced and then add the `TMJV` token with its asset id `cfa74593a6ad28436815ba1ebc486bf4344e880461c1b2fa550319a9e8479a14`.

6. Follow the instructions on GUI to generate offers.
