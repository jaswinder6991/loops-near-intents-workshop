# Teachers Guide: Module 1 - Introduction

**Module Duration:** 10 minutes  
**Instructor Prep Time:** 15 minutes before workshop  
**Key Focus:** Setting expectations, managing workshop logistics

## Pre-Workshop Instructor Checklist

### 30 Minutes Before Workshop
- [ ] **Test your own environment setup** - Run through Module 3 yourself to catch issues
- [ ] **Prepare student funding** - Ensure you have a method to send 0.2 NEAR to each student
- [ ] **Set up communication channel** - Slack/Discord for sharing account IDs quickly
- [ ] **Prepare backup WiFi** - Cross-chain operations require stable internet
- [ ] **Have explorer links ready** - nearblocks.io and arbiscan.io bookmarked

### 5 Minutes Before Workshop  
- [ ] **Open required tools**: Terminal, explorer sites, communication channel
- [ ] **Test internet speed** - Ensure 5+ Mbps for smooth API calls
- [ ] **Announce WiFi/setup time** - Let students know they can start environment setup

## Step-by-Step Instructor Actions

### Step 1: Workshop Introduction (3 minutes)
1. **Set realistic expectations**:
   - "Cross-chain operations take 5-15 minutes, not seconds"
   - "Your scripts will timeout at 60 seconds - this is normal, operations continue in background"
   - "We're using mainnet NEAR - real money, small amounts"

2. **Address security upfront**:
   - "Use test wallets only - never mainnet wallets with significant funds"
   - "You'll receive 0.2 NEAR (~$0.20) for the workshop"

### Step 2: Logistics Setup (5 minutes)
1. **Collect student information**:
   ```bash
   # Ask students to share in chat:
   # 1. Their name
   # 2. Their experience level (beginner/intermediate/advanced)
   # 3. Their NEAR account ID (after Module 3)
   ```

2. **Distribute materials**:
   - Share GitHub repository link
   - Share communication channel link
   - Share helpful explorer bookmarks

### Step 3: Set Technical Context (2 minutes)
1. **Emphasize key differences from traditional blockchain workshops**:
   - "We're using mainnet, not testnet"
   - "Cross-chain operations have different timing than single-chain"
   - "The 1Click API handles complexity - you don't need to understand bridge protocols"

## Common Questions to Prepare For

### About the Workshop Structure
**Q: "Why are we using mainnet instead of testnet?"**
**A:** "NEAR Intents and 1Click API only exist on mainnet. The intent infrastructure requires real liquidity and solvers that only operate on mainnet."

**Q: "What if something goes wrong with real money?"**
**A:** "You'll only use ~$0.20 worth of NEAR. Each operation costs fractions of a penny. It's safer than buying coffee."

**Q: "How long will each operation take?"**
**A:** "Show this timing chart:"
- NEAR deposits: 30 seconds
- Asset swaps: 2-5 minutes  
- Cross-chain withdrawals: 5-15 minutes
- Total workshop: 2.5-3 hours

### About Prerequisites
**Q: "I don't have much blockchain experience. Can I still follow along?"**
**A:** "Yes! This workshop teaches intent-based interactions, which are simpler than traditional blockchain development. We'll explain concepts as we go."

**Q: "Do I need to understand cross-chain bridges?"**
**A:** "No! That's the power of intents - they abstract away the complexity. You'll learn how to use them without needing to understand the underlying protocols."

## Common Student Mistakes to Watch For

### During Introduction
❌ **Mistake:** Students trying to set up development environment during introduction
✅ **Prevention:** "Hold off on setup until Module 3. Let's understand concepts first."

❌ **Mistake:** Students confused about mainnet vs testnet
✅ **Prevention:** Repeat multiple times: "We use mainnet because intents only work there. Amounts are tiny (~$0.20 total)."

❌ **Mistake:** Students worried about gas fees eating their funds
✅ **Prevention:** Show fee breakdown:
```
Total provided: 0.2 NEAR ($0.20)
Workshop operations: ~0.1 NEAR ($0.10)
Gas fees: ~0.005 NEAR ($0.005)
Safety buffer: 0.095 NEAR ($0.095)
```

### Timing Management Issues
❌ **Mistake:** Students rushing ahead to setup before understanding concepts
✅ **Prevention:** "The introduction builds foundation for everything else. Setup issues are easier to debug when you understand what you're building."

❌ **Mistake:** Students getting frustrated with "slow" cross-chain timing
✅ **Prevention:** Use Web2 parallels: "Cross-chain is like international wire transfers - they take time but they're reliable. On-chain swaps are like domestic transfers - much faster."

## Helpful Web2 Parallels to Use

1. **Cross-Chain Swaps = International Money Transfer**
   - "Like sending money from a US bank to a European bank"
   - "Multiple systems involved, takes time, but moves real value"

2. **Intents = Universal Payment Processor**
   - "Like PayPal handling different currencies behind the scenes"
   - "You say 'I want to pay €50' - PayPal figures out the conversion"

3. **1Click API = Travel Agency**
   - "You say 'I want to go to Paris' - they handle flights, hotels, connections"
   - "You say 'I want ETH on Arbitrum' - 1Click handles swaps, bridges, routing"

## Timing Checkpoints

### 3 Minutes In
- Students should understand this is cross-chain focus, not smart contract development
- Key concept: Intents abstract complexity

### 7 Minutes In  
- Students should be comfortable with mainnet usage
- Ready to move to concepts

### 10 Minutes (End)
- Clear transition: "Now let's understand what makes cross-chain operations possible"
- Students prepared for concept-heavy Module 2

## Red Flags to Address Immediately

🚨 **Student says: "I'll just use my main MetaMask wallet"**
**Response:** "Stop! Create a test wallet. We'll walk through this in Module 3."

🚨 **Student asks: "Can I use testnet instead?"**
**Response:** "No, intent infrastructure only exists on mainnet. But amounts are tiny - safer than a cup of coffee."

🚨 **Multiple students having WiFi issues**
**Response:** Consider switching to mobile hotspot or rescheduling if venue internet is unstable.

## Success Criteria for Module 1

By the end of this module, students should:
- [ ] Understand this is about using intents, not building them
- [ ] Be comfortable with mainnet usage for small amounts
- [ ] Know they'll receive 0.2 NEAR for the workshop
- [ ] Understand cross-chain operations take longer than single-chain
- [ ] Be ready to learn concepts in Module 2

## Transition to Module 2

**Good transition statement:**
"Now that you understand what we're building and the workshop logistics, let's dive into the concepts that make cross-chain swaps possible. In the next module, we'll explore what makes intents so powerful for cross-chain operations."

**Check before moving on:**
- All students have GitHub repo link
- Communication channel is working
- Students understand timing expectations 