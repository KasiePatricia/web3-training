# Week 1: Getting Started with the Starknet Ecosystem

**Duration:** [Start Date] - [End Date]  
**Status:** In Progress  
**Completion:** 0%

---

## 📋 Week Overview

This week lays the foundation for your Starknet journey. You'll understand blockchain scalability, learn why Starknet uses STARKs, get familiar with Cairo syntax, and set up your complete development environment.

### Learning Objectives

By the end of Week 1, you will be able to:
- ✅ Explain how Starknet works as a Layer 2 solution
- ✅ Understand the difference between STARKs and SNARKs
- ✅ Describe Starknet's architecture and transaction lifecycle
- ✅ Write basic Cairo programs
- ✅ Set up and use development tools (Scarb, Foundry)
- ✅ Interact with Starknet testnet using wallets

---

## 📚 Topics Breakdown

### Session 1: Introduction to Starknet (Monday)

#### 1.1 What is Starknet?

**Key Concepts:**
- Starknet is a permissionless Layer 2 validity rollup on Ethereum
- Uses cryptographic proofs (STARKs) to verify computation
- Enables high throughput and low costs while inheriting Ethereum's security

**Why Starknet Matters:**
- Solves Ethereum's scalability trilemma (security, decentralization, scalability)
- 1000x improvement in transaction throughput
- Maintains Ethereum-level security
- Native Account Abstraction

**My Notes:**
```
[Write your understanding of what Starknet is and why it exists]




```

**Questions:**
1. 
2. 

---

#### 1.2 STARK vs SNARK

**STARKs (Scalable Transparent ARgument of Knowledge):**

| Feature | Description | Advantage |
|---------|-------------|-----------|
| Transparent | No trusted setup required | More secure, no ceremony needed |
| Quantum-resistant | Safe against quantum computers | Future-proof |
| Scalable | Faster proving for large computations | Better for complex apps |
| Proof Size | Larger proofs (few hundred KB) | Trade-off for security |

**SNARKs (Succinct Non-interactive ARgument of Knowledge):**

| Feature | Description | Disadvantage |
|---------|-------------|--------------|
| Trusted Setup | Requires ceremony to generate parameters | Security risk if compromised |
| Quantum-vulnerable | Can be broken by quantum computers | Not future-proof |
| Succinct | Very small proofs (~200 bytes) | Good for L1 verification |
| Slower Proving | Slower for large computations | - |

**Visual Comparison:**
```
STARKs:
Setup: None ✅
Quantum Safe: Yes ✅
Proof Size: Large (~100KB) ⚠️
Proving Speed: Fast ✅
Use Case: Complex computations

SNARKs:
Setup: Required ⚠️
Quantum Safe: No ⚠️
Proof Size: Small (~200 bytes) ✅
Proving Speed: Moderate
Use Case: Simple proofs
```

**My Understanding:**
```
Why does Starknet use STARKs instead of SNARKs?

[Write your explanation here]




```

**Practice Question:**
If you were building a Layer 2 solution today, which proof system would you choose and why?

**My Answer:**
```




```

---

#### 1.3 Starknet Architecture

**Core Components:**

1. **Sequencer**
   - Orders incoming transactions
   - Executes transactions and updates state
   - Currently centralized (decentralization in progress)
   - Run by Starknet Foundation

2. **Prover**
   - Generates STARK proofs of executed transactions
   - Proves computation was done correctly
   - Runs off-chain to save costs

3. **L1 Core Contract (Ethereum)**
   - Verifies STARK proofs on Ethereum
   - Stores state commitments
   - Final source of truth

**Transaction Flow:**
```
1. User submits transaction
   ↓
2. Sequencer receives and orders it
   ↓
3. Sequencer executes transaction
   ↓
4. State updated on L2
   ↓
5. Prover generates STARK proof
   ↓
6. Proof submitted to L1 Core Contract
   ↓
7. L1 verifies proof
   ↓
8. Final settlement on Ethereum
```

**Diagram Notes:**
[Draw or paste a diagram of the architecture]

**My Notes:**
```
Key takeaways about architecture:




```

---

#### 1.4 Transaction Types

**Three Main Transaction Types:**

**1. DECLARE Transaction**
- Registers a contract class on Starknet
- Makes the code available for deployment
- Returns a class hash
```cairo
// Example: You write an ERC20 contract
// First, you DECLARE it to register the code
```

**2. DEPLOY Transaction**
- Creates an instance of a declared contract class
- Assigns a unique address
- Initializes constructor parameters
```cairo
// After DECLARE, you DEPLOY to create actual contract
// Can deploy same class multiple times with different addresses
```

**3. INVOKE Transaction**
- Calls functions on deployed contracts
- Reads or writes data
- Most common transaction type
```cairo
// Example: transfer(recipient, amount) on ERC20
```

**Transaction Lifecycle:**

| State | Description | Time |
|-------|-------------|------|
| Received | Transaction received by sequencer | Instant |
| Pending | Waiting to be executed | Seconds |
| Accepted on L2 | Executed and included in L2 block | ~Minutes |
| Accepted on L1 | Proof verified on Ethereum | ~Hours |

**My Example:**
```
Walk through a real transaction (like sending tokens):
1. DECLARE: Register ERC20 contract code
2. DEPLOY: Create your token at address 0x123...
3. INVOKE: Call transfer() to send tokens

[Write your own example here]


```

---

#### 1.5 Finality and Consensus

**Understanding Finality:**

**Soft Finality (L2):**
- Transaction accepted by sequencer
- Included in L2 block
- State updated on Starknet
- Time: ~10-60 seconds
- Can theoretically be reverted

**Hard Finality (L1):**
- STARK proof verified on Ethereum
- Becomes part of Ethereum's history
- Irreversible (as secure as Ethereum)
- Time: ~4-6 hours

**Current Consensus Model:**
```
Starknet Today:
- Centralized sequencer (Starknet Foundation)
- Plans for decentralization
- Multiple provers can verify (anyone can prove)

Future Plans:
- Decentralized sequencer network
- Fast finality improvements
- Multiple sequencer options
```

**My Notes:**
```
Questions about finality:
- 
- 

Understanding:



```

---

### Session 2: Cairo Language Basics (Wednesday)

#### 2.1 Why Cairo?

**Cairo's Unique Features:**

1. **Provable Computation**
   - Every Cairo program can be proven with STARKs
   - Enables verifiable computing at scale

2. **Safety & Security**
   - Type-safe like Rust
   - Memory-safe
   - Prevents common vulnerabilities

3. **Efficiency**
   - Optimized for STARK proving
   - Compiled to Sierra (Safe Intermediate Representation)
   - Then to CASM (Cairo Assembly)

**Comparison with Solidity:**

| Feature | Cairo | Solidity |
|---------|-------|----------|
| Purpose | Provable computation | Smart contracts |
| Safety | Very high | Moderate |
| Learning Curve | Steeper | Easier |
| Proving | Native STARK support | No built-in proving |
| Syntax | Rust-inspired | JavaScript-inspired |

**My Thoughts:**
```
Why I'm learning Cairo:




Challenges I anticipate:



```

---

#### 2.2 Cairo Syntax Overview

**Basic Program Structure:**

```cairo
// 1. Module declaration (optional)
mod my_module;

// 2. Imports
use core::traits::Into;
use core::option::OptionTrait;

// 3. Main function
fn main() {
    // Your code here
    let message = "Hello, Starknet!";
    println!("{}", message);
}
```

**Comments:**
```cairo
// Single-line comment

/*
   Multi-line comment
   Can span multiple lines
*/

/// Documentation comment
/// Used for generating docs
fn documented_function() {
    // Implementation
}
```

**Variables:**
```cairo
// Immutable by default (like Rust)
let x = 5;
// x = 6;  // ❌ Error: cannot reassign

// Mutable variables
let mut y = 10;
y = 15;  // ✅ Works

// Type annotations
let z: u32 = 100;
let name: felt252 = 'Alice';
```

**Data Types:**
```cairo
// Integers
let small: u8 = 255;           // 0 to 255
let medium: u32 = 4294967295;  // 0 to 2^32-1
let large: u64 = 18446744073709551615;  // 0 to 2^64-1
let huge: u128 = 340282366920938463463374607431768211455;
let massive: u256 = 1_000_000_000_000_000_000;

// Field element (Cairo's special type)
let felt_num: felt252 = 123456789;

// Boolean
let is_active: bool = true;
let is_complete: bool = false;

// Strings (short strings only)
let short_str: felt252 = 'Hello';  // Max 31 characters
```

**Practice Exercise 1:**
```cairo
// Create a program that declares variables of each type
// Try to compile it with `scarb build`

[Write your code here or in a file]
```

---

#### 2.3 Functions

**Function Declaration:**
```cairo
// Basic function
fn greet() {
    println!("Hello!");
}

// Function with parameters
fn add(a: u32, b: u32) -> u32 {
    a + b  // Last expression is returned (no semicolon)
}

// Or use explicit return
fn subtract(a: u32, b: u32) -> u32 {
    return a - b;
}

// Multiple return values (using tuples)
fn divide_and_remainder(dividend: u32, divisor: u32) -> (u32, u32) {
    let quotient = dividend / divisor;
    let remainder = dividend % divisor;
    (quotient, remainder)
}

// Function visibility
pub fn public_function() {
    // Can be called from outside module
}

fn private_function() {
    // Only within module
}
```

**Practice Exercise 2:**
```cairo
// Write a function that:
// 1. Takes two numbers
// 2. Returns their sum, difference, and product
// Hint: Use tuples for multiple returns

[Your solution here]
```

---

#### 2.4 Control Flow

**If Expressions:**
```cairo
fn check_number(x: u32) {
    if x > 10 {
        println!("Greater than 10");
    } else if x > 5 {
        println!("Greater than 5");
    } else {
        println!("5 or less");
    }
}

// If as expression (returns value)
fn max(a: u32, b: u32) -> u32 {
    if a > b {
        a
    } else {
        b
    }
}
```

**Loops:**
```cairo
// Loop (infinite, must break)
fn count_to_five() {
    let mut counter = 0;
    loop {
        counter += 1;
        if counter == 5 {
            break;
        }
    }
}

// While loop
fn countdown(mut n: u32) {
    while n > 0 {
        println!("{}", n);
        n -= 1;
    }
}

// For loop (not in basic Cairo, use loop or while)
```

**Match (Pattern Matching):**
```cairo
fn describe_number(x: u32) -> felt252 {
    match x {
        0 => 'zero',
        1 => 'one',
        2 => 'two',
        _ => 'many',  // Default case
    }
}
```

**Practice Exercise 3:**
```cairo
// Write a function that:
// 1. Takes a number
// 2. Prints "Even" if even, "Odd" if odd
// 3. Uses if expression

[Your solution here]
```

---

### Session 3: Setting Up and First Program (Friday)

#### 3.1 Verifying Your Installation

**Checklist:**
```bash
# Run these commands and record output
asdf --version
# My output: 

scarb --version
# My output: 

snforge --version
# My output: 

sncast --version
# My output: 
```

**Status:**
- [ ] All tools working
- [ ] Need to fix: _______

---

#### 3.2 Creating Your First Cairo Project

**Step-by-Step:**

```bash
# 1. Create project directory
mkdir ~/cairo-projects
cd ~/cairo-projects

# 2. Create new project
scarb new hello_starknet
cd hello_starknet

# 3. View project structure
tree .
```

**Project Structure:**
```
hello_starknet/
├── Scarb.toml          # Project configuration
└── src/
    └── lib.cairo       # Main source file
```

**Understanding Scarb.toml:**
```toml
[package]
name = "hello_starknet"              # Your project name
version = "0.1.0"                    # Version number
edition = "2024_07"                  # Cairo edition

[dependencies]
starknet = ">=2.8.2"                 # Starknet library version

[[target.starknet-contract]]         # Compile as Starknet contract
```

**My First Program (src/lib.cairo):**
```cairo
// Delete default content and write:

fn main() {
    let message: felt252 = 'Hello, Starknet!';
    println!("{}", message);
}
```

**Compile and Run:**
```bash
# Build the project
scarb build

# Output:
# My build output:


```

**Troubleshooting:**
```
If you get errors:
1. Check syntax carefully
2. Ensure Scarb.toml is correct
3. Try `scarb clean` then `scarb build`

My errors and solutions:



```

---

#### 3.3 Practice Programs

**Program 1: Calculator**
```cairo
// Create src/calculator.cairo
// Implement add, subtract, multiply, divide functions

[Your code here]
```

**Program 2: Data Types Explorer**
```cairo
// Create a program that uses all data types
// u8, u32, u64, u128, u256, felt252, bool

[Your code here]
```

**Program 3: Control Flow**
```cairo
// Write a function that categorizes a number
// Range 0-10: "small"
// Range 11-100: "medium"
// Range 101+: "large"

[Your code here]
```

---

#### 3.4 Working with Wallets

**Argent X Setup:**

1. **Installation Completed:**
   - [ ] Installed browser extension
   - [ ] Created wallet
   - [ ] Backed up seed phrase securely
   - [ ] Switched to Sepolia testnet

2. **My Wallet Info:**
   ```
   Wallet Address: 0x...
   Network: Sepolia Testnet
   Initial Balance: 0 ETH
   ```

3. **Getting Testnet Tokens:**
   ```bash
   # Visit: https://starknet-faucet.vercel.app/
   # Connect wallet
   # Request tokens
   
   Transaction Hash: 
   Amount Received: 
   Date: 
   ```

**Braavos Setup:**

1. **Installation Completed:**
   - [ ] Installed browser extension
   - [ ] Created wallet
   - [ ] Backed up seed phrase
   - [ ] Switched to Sepolia testnet

2. **My Wallet Info:**
   ```
   Wallet Address: 0x...
   Network: Sepolia Testnet
   Initial Balance: 0 ETH
   ```

**Wallet Comparison Notes:**
```
Argent X:
Pros: 
Cons: 

Braavos:
Pros: 
Cons: 

Which I prefer and why:


```

---

## 📝 Week 1 Assignment

**Due Date:** [Date]  
**Status:** ⬜ Not Started | ⬜ In Progress | ⬜ Completed

### Part 1: Environment Verification (25 points)

- [ ] Take screenshots of successful installation
- [ ] Document any issues faced and solutions
- [ ] Create a test project that compiles successfully

**My submission:**
```
Screenshot links:
- 
- 

Issues faced:


```

---

### Part 2: Cairo Programming (50 points)

**Task:** Create a Cairo program that demonstrates understanding of:
1. Variables (mutable and immutable)
2. All data types
3. Functions with parameters and return values
4. Control flow (if/else, loops)
5. Proper code organization and comments

**Requirements:**
```cairo
// Your program should:
// 1. Have at least 3 functions
// 2. Use at least 5 different data types
// 3. Include control flow logic
// 4. Be well-commented
// 5. Compile without errors

[Write your program here or link to GitHub]
```

**My Program:**
- Repository: [GitHub link]
- Description: 
- Challenges faced: 

---

### Part 3: Written Explanation (25 points)

Write 200-300 words explaining:

1. **Why does Starknet use STARKs instead of SNARKs?**
```
[Your answer here]






```

2. **What is one advantage and one challenge of Cairo compared to Solidity?**
```
Advantage:



Challenge:



```

---

## 🎯 Learning Outcomes Check

Rate your understanding (1-5, where 5 is complete mastery):

| Topic | Rating | Notes |
|-------|--------|-------|
| Starknet Architecture | _/5 | |
| STARK vs SNARK | _/5 | |
| Transaction Lifecycle | _/5 | |
| Cairo Syntax | _/5 | |
| Data Types | _/5 | |
| Functions | _/5 | |
| Control Flow | _/5 | |
| Development Setup | _/5 | |
| Wallet Usage | _/5 | |

**Overall Week 1 Confidence:** ___/10

---

## 📚 Additional Resources

### Must-Read
- [ ] [Cairo Book - Chapter 1-3](https://book.cairo-lang.org/)
- [ ] [Starknet Documentation - Getting Started](https://docs.starknet.io/)
- [ ] [Understanding STARKs](https://starkware.co/stark/)

### Recommended Videos
- [ ] [Starknet Overview](https://www.youtube.com/results?search_query=starknet+overview)
- [ ] [Cairo Programming Basics](https://www.youtube.com/results?search_query=cairo+programming)

### Practice Resources
- [ ] [Cairo by Example](https://cairo-by-example.com/)
- [ ] [Starklings Exercises](https://github.com/shramee/starklings-cairo1)

---

## 💭 Reflection

### What I Learned This Week
```
Key concepts I now understand:
1. 
2. 
3. 

Skills I developed:
1. 
2. 
```

### Challenges Faced
```
Biggest challenge:


How I overcame it:


What I'd do differently:


```

### Questions for Next Week
1. 
2. 
3. 

### Goals for Week 2
- [ ] 
- [ ] 
- [ ] 

---

## 📊 Time Tracking

| Activity | Time Spent |
|----------|------------|
| Monday Class | 2h |
| Monday Review | ___h |
| Wednesday Class | 2h |
| Wednesday Practice | ___h |
| Friday Class | 2h |
| Friday Practice | ___h |
| Assignment Work | ___h |
| Additional Learning | ___h |
| **Total** | **___h** |

---

## ✅ Week 1 Completion Checklist

### Knowledge
- [ ] Can explain Starknet architecture
- [ ] Understand STARK vs SNARK differences
- [ ] Know transaction types and lifecycle
- [ ] Comfortable with Cairo syntax
- [ ] Can write basic Cairo programs

### Practical Skills
- [ ] Development environment fully set up
- [ ] Created and compiled first Cairo project
- [ ] Wallets installed and funded
- [ ] Can navigate Scarb commands
- [ ] Understand project structure

### Assignment
- [ ] Part 1 completed
- [ ] Part 2 completed
- [ ] Part 3 completed
- [ ] Submitted on time
- [ ] Code pushed to GitHub

### Community
- [ ] Joined Starknet Discord
- [ ] Introduced myself to cohort
- [ ] Asked at least one question in class
- [ ] Helped a peer (if possible)

---

**Week 1 Status:** ⬜ In Progress | ⬜ Completed  
**Date Completed:** [Date]  
**Ready for Week 2:** ⬜ Yes | ⬜ Need to review

---

**Notes to Self:**
```
What went well:


What needs improvement:


Motivation check:


```