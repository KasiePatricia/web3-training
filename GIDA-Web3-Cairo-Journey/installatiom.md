# Development Environment Setup Guide

## 🛠️ Installation Process

This guide documents the complete setup of your Starknet development environment.

---

## System Information

- **Operating System:** [Your OS - e.g., macOS Sonoma, Ubuntu 22.04, Windows 11 + WSL2]
- **Installation Date:** [Date you started setup]
- **Last Updated:** [Current date]

---

## Prerequisites

Before starting, ensure you have:
- [ ] Terminal/Command Line access
- [ ] Internet connection
- [ ] Administrative privileges on your machine

---

## 1. Installing asdf (Version Manager)

### Why asdf?
asdf is a universal version manager that allows you to manage multiple runtime versions with a single CLI tool.

### Installation Steps

**For macOS:**
```bash
# Install using Homebrew
brew install asdf

# Add to your shell configuration
echo -e "\n. $(brew --prefix asdf)/libexec/asdf.sh" >> ~/.zshrc
source ~/.zshrc
```

**For Linux:**
```bash
# Clone asdf repository
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0

# Add to bash profile
echo '. "$HOME/.asdf/asdf.sh"' >> ~/.bashrc
echo '. "$HOME/.asdf/completions/asdf.bash"' >> ~/.bashrc
source ~/.bashrc
```

**For Windows (WSL2):**
```bash
# Same as Linux installation
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0
echo '. "$HOME/.asdf/asdf.sh"' >> ~/.bashrc
source ~/.bashrc
```

### Verification
```bash
asdf --version
# Expected output: v0.14.0 or similar
```

**Status:** ✅ Installed

---

## 2. Installing Scarb (Cairo Package Manager)

### What is Scarb?
Scarb is the Cairo package manager and build tool, similar to Cargo for Rust or npm for JavaScript.

### Installation Steps

**Method 1: Using asdf (Recommended)**
```bash
# Add scarb plugin to asdf
asdf plugin add scarb

# Install latest version
asdf install scarb latest

# Set global version
asdf global scarb latest
```

**Method 2: Using Installation Script**
```bash
curl --proto '=https' --tlsv1.2 -sSf https://docs.swmansion.com/scarb/install.sh | sh
```

### Verification
```bash
scarb --version
# Expected output: scarb 2.8.4 or higher
```

### Common Issues & Solutions

**Issue 1:** Command not found
```bash
# Solution: Make sure asdf is properly configured in your shell
source ~/.bashrc  # or ~/.zshrc for macOS
```

**Issue 2:** Old version installed
```bash
# Solution: Update to latest
asdf install scarb latest
asdf global scarb latest
```

**Status:** ✅ Installed

---

## 3. Installing Starknet Foundry

### What is Starknet Foundry?
Starknet Foundry is a toolchain for developing, testing, and deploying Starknet smart contracts. It includes:
- **snforge:** Testing framework for Cairo contracts
- **sncast:** Command-line tool for Starknet interactions

### Installation Steps

**Using asdfrs (Recommended)**
```bash
# Add starknet-foundry plugin
asdf plugin add starknet-foundry

# Install latest version
asdf install starknet-foundry latest

# Set global version
asdf global starknet-foundry latest
```

**Using Installation Script**
```bash
curl -L https://raw.githubusercontent.com/foundry-rs/starknet-foundry/master/scripts/install.sh | sh
```

**Using snfoundryup (Alternative)**
```bash
# Install snfoundryup
curl -L https://raw.githubusercontent.com/foundry-rs/starknet-foundry/master/scripts/install.sh | sh

# Restart terminal, then run
snfoundryup
```

### Verification
```bash
# Check snforge
snforge --version
# Expected output: snforge 0.31.0 or higher

# Check sncast
sncast --version
# Expected output: sncast 0.31.0 or higher
```

### Configuration

Create a foundry configuration file (optional, for project-specific settings):
```bash
# In your project directory
touch snfoundry.toml
```

**Status:** ✅ Installed

---

## 4. Installing VS Code Extensions (Recommended)

### Required Extensions

1. **Cairo 1.0** by StarkWare
   - Syntax highlighting for Cairo
   - Code completion
   - Error detection

2. **Starknet Contracts** by Eric Lau
   - Additional Cairo support
   - Contract templates

### Installation
```bash
# Open VS Code
code .

# Search for extensions in the Extensions marketplace
# Or install via command line:
code --install-extension starkware.cairo1
```

---

## 5. Wallet Installation

### Argent X Wallet

**Installation:**
1. Visit: https://www.argent.xyz/argent-x/
2. Click "Download for Chrome/Firefox/Edge"
3. Add extension to browser
4. Click the extension icon
5. Choose "Create a new wallet"
6. **IMPORTANT:** Securely backup your seed phrase
7. Set a strong password

**Network Configuration:**
1. Open Argent X
2. Click Settings (gear icon)
3. Select "Developer settings"
4. Enable "Testnet mode"
5. Switch to "Sepolia Testnet"

**Status:** ✅ Installed

### Braavos Wallet

**Installation:**
1. Visit: https://braavos.app/
2. Click "Install Extension"
3. Add to browser
4. Create new wallet
5. **IMPORTANT:** Backup seed phrase securely
6. Set strong password

**Network Configuration:**
1. Open Braavos
2. Click network dropdown (top of wallet)
3. Select "Sepolia Testnet"

**Status:** ✅ Installed

---

## 6. Getting Testnet Tokens

### Starknet Sepolia Faucet

**Steps:**
1. Visit: https://starknet-faucet.vercel.app/
2. Connect your wallet (Argent X or Braavos)
3. Click "Request tokens"
4. Wait for confirmation (usually 1-2 minutes)
5. Check wallet balance

**Alternative Faucets:**
- https://faucet.goerli.starknet.io/ (if Sepolia is down)
- Starknet Discord #faucet channel

**Status:** ✅ Tokens Received

---

## Verification Checklist

Run these commands to verify your complete setup:

```bash
# 1. Check asdf
asdf --version
echo "✅ asdf installed"

# 2. Check Scarb
scarb --version
echo "✅ Scarb installed"

# 3. Check Starknet Foundry
snforge --version
sncast --version
echo "✅ Starknet Foundry installed"

# 4. Create test project
mkdir -p ~/cairo-test
cd ~/cairo-test
scarb new hello_cairo
cd hello_cairo
scarb build
echo "✅ Test project builds successfully"
```

**All checks passed?** 
- [ ] Yes, everything works!
- [ ] No, I have issues (document below)

---

## Troubleshooting

### Common Issues

**Issue:** `scarb: command not found`
**Solution:**
```bash
# Reload shell configuration
source ~/.bashrc  # or ~/.zshrc

# Or reinstall using asdf
asdf reshim scarb
```

**Issue:** `snforge: command not found`
**Solution:**
```bash
# Check if starknet-foundry is installed
asdf list starknet-foundry

# If not listed, install
asdf install starknet-foundry latest
asdf global starknet-foundry latest
```

**Issue:** Wallet not connecting to testnet
**Solution:**
1. Clear browser cache
2. Remove and re-add wallet extension
3. Try alternative faucet
4. Check network status at status.starknet.io

---

## Installation Log

Document any issues you encountered and how you resolved them:

### [Date] - Issue 1
**Problem:** [Describe the issue]
**Solution:** [How you fixed it]
**Time spent:** [Approximate time]

### [Date] - Issue 2
**Problem:** 
**Solution:** 
**Time spent:** 

---

## Next Steps

After completing installation:
1. ✅ All tools installed and verified
2. ⬜ Create first Cairo project
3. ⬜ Begin Week 1 learning materials
4. ⬜ Join Starknet community Discord

---

## Useful Commands Reference

```bash
# asdf commands
asdf list                    # List all installed versions
asdf current                 # Show current versions
asdf plugin list             # List installed plugins

# Scarb commands
scarb new <project_name>     # Create new project
scarb build                  # Build project
scarb test                   # Run tests
scarb fmt                    # Format code

# Starknet Foundry commands
snforge test                 # Run tests
snforge test --help          # Show test options
sncast account list          # List accounts
sncast declare               # Declare contract
sncast deploy                # Deploy contract
```

---

## Resources

- [asdf Documentation](https://asdf-vm.com/)
- [Scarb Documentation](https://docs.swmansion.com/scarb/)
- [Starknet Foundry Book](https://foundry-rs.github.io/starknet-foundry/)
- [Cairo Installation Guide](https://book.cairo-lang.org/ch01-01-installation.html)

---

**Installation completed on:** [Date]  
**Total time spent:** [Time]  
**Ready to start learning:** ✅