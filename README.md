# fixme3: Running a Rust (Cargo) Project in GitHub Codespaces

This guide explains how to run this Rust project in a GitHub Codespace without installing Rust or Cargo on your own device.

## Prerequisites

- A GitHub account
- This repository on GitHub

## 1. Open the Codespace

1. Open the repository on GitHub.
2. Click **Code** → **Codespaces** tab → **Create codespace on main**.
3. Wait for the VS Code editor to load in your browser.

## 2. Install Rust (one time per Codespace)

If you see `bash: cargo: command not found`, Rust is not installed yet. Install it with rustup:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
```

Load Rust into the current terminal session (otherwise open a new terminal):

```bash
source "$HOME/.cargo/env"
```

Verify the installation:

```bash
cargo --version
```

## 3. Run the project

Run this from the folder that contains `Cargo.toml` (here: `/workspaces/fixme1`):

```bash
cargo run
```

The first run takes a little longer because Cargo downloads and compiles the dependencies.

## Notes

- The code uses the `xor_cryptor` crate. If it is missing from `Cargo.toml`, add it with:

  ```bash
  cargo add xor_cryptor
  ```

- Dependencies are downloaded from [crates.io](https://crates.io) and are free to use.
- The Rust install lasts only for the current Codespace. If you rebuild or create a new Codespace, repeat step 2.

## Optional: Preinstall Rust automatically

Create the file `.devcontainer/devcontainer.json` with this content, then rebuild the Codespace. Rust will then be available every time without manual installation.

```json
{
  "image": "mcr.microsoft.com/devcontainers/rust:latest"
}
```

## Save your work, then stop and delete the Codespace

1. Save your work to GitHub:

   ```bash
   git status
   git add .
   git commit -m "save work"
   git push
   ```

2. Stop the Codespace: press `Ctrl+Shift+P`, type **Codespaces: Stop Current Codespace**, and press Enter.
3. Delete it: go to [github.com/codespaces](https://github.com/codespaces), click the **...** menu next to your Codespace, choose **Delete**, and confirm.

Deleting a Codespace does not delete the repository. Anything not committed and pushed is lost.

## Troubleshooting

| Problem | Fix |
|---|---|
| `cargo: command not found` | Run the install command in step 2, then `source "$HOME/.cargo/env"` |
| Crate not found on build | Run `cargo add <crate-name>` or check `[dependencies]` in `Cargo.toml` |
| `could not find Cargo.toml` | `cd` into the project folder (`/workspaces/fixme1`) and run again |
