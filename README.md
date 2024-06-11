<img width="3300" alt="nexus_docs-header" src="https://github.com/0xmoei/Nexus-zkevm/assets/90371338/7264cc44-1e13-48af-bbeb-afddc21a1ab2"><h1 align="center"># The Nexus zkVM</h1>
![Screenshot_1](https://github.com/0xmoei/Nexus-zkevm/assets/90371338/d81728cd-31c7-4178-bec5-9ea43a88573c)


> The Nexus zkVM is a modular, extensible, open-source, and highly-parallelized zkVM, designed to run at a trillion CPU cycles proved per second given enough machine power.

## Submit ZK Proof
> Note that if you are using VPS, use `Mobaxterm` client to connect to SSH to be able to download files from your server to your local PC

### 1-Install Nexus zkVM CLI
1- Update packages:
```console
sudo apt update && sudo apt upgrade
```
2- Install cmake:
```console
sudo apt install build-essential cmake
```
3- Install Rust:
```console
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
. "$HOME/.cargo/env"

# Redirect rust to RISC-V:
rustup target add riscv32i-unknown-none-elf
```
4- Install Nexus zkVM CLI:
```console
cargo install --git https://github.com/nexus-xyz/nexus-zkvm nexus-tools --tag 'v1.0.0'
```
5- Verify Installation:
```console
cargo nexus --help
```
![Screenshot_1](https://github.com/0xmoei/Nexus-zkevm/assets/90371338/067241cf-8583-42de-806f-fb10b7a78edc)

### 2-Create a new Nexus project
1- Create directory:
```console
cargo nexus new nexus-project
```
2- Go to Directory
```
cd nexus-project
```
3- Edit `main.rs`
```
# Open edit menu
nano src/main.rs

# Delete everything and paste the following code
#![no_std]
#![no_main]

fn fib(n: u32) -> u32 {
    match n {
        0 => 0,
        1 => 1,
        _ => fib(n - 1) + fib(n - 2),
    }
}

#[nexus_rt::main]
fn main() {
    let n = 7;
    let result = fib(n);
    assert_eq!(result, 13);
}
```
To save: `Ctrl+X` `Y` `Enter`

### 3- Run Nexus
```console
cargo nexus run -v
```

### 4- Prove your program
Generate a proof for your Rust program using the Nexus zkVM.
```
cargo nexus prove
```

### 5-Verify your proof
Finally, load and verify the proof:
```
cargo nexus verify
```

#

Easily done! Now download and SAVE your `NEXUS-PROOF` file in a safe place!
![Screenshot_1](https://github.com/0xmoei/Nexus-zkevm/assets/90371338/595dc0eb-2301-45e8-b595-48d4d3fdc062)

#
