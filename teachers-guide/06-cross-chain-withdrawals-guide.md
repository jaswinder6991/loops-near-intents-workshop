# Teachers Guide: Module 6 - Cross-Chain Withdrawals

**Module Duration:** 30 minutes  
**Instructor Prep Time:** 20 minutes  
**Key Focus:** Managing 60-second script timeout expectations, true cross-chain operations

## Critical Pre-Module Briefing

### MOST IMPORTANT MESSAGE TO DELIVER:
**"Your scripts WILL timeout at 60 seconds showing 'Quote hasn't been settled' - this is NORMAL and EXPECTED. Your cross-chain transfer continues processing for 5-15 minutes in the background. DO NOT retry the script!"**

## Pre-Module Instructor Checklist

### 15 Minutes Before Module
- [ ] **Verify all students have ETH tokens** - Check balances from Module 5
- [ ] **Test withdrawal script** - Confirm `yarn run withdraw` behavior in environment
- [ ] **Prepare EVM addresses** - Students need Arbitrum wallet addresses
- [ ] **Set up monitoring tools** - Arbiscan.io and nearblocks.io ready

## Step-by-Step Instructor Actions

### Step 1: Expectation Setting (5 minutes)

**Critical messaging:**
```
"Cross-chain withdrawals work differently:
- Script runs for 60 seconds, then times out (NORMAL!)
- Operation continues 5-15 minutes in background
- Final result: ETH appears in your Arbitrum wallet
- NEVER retry a withdrawal script!"
```

### Step 2: EVM Address Setup (5 minutes)
```bash
# Students need Arbitrum wallet addresses
# They can use MetaMask, or create test wallet
# Update .env file:
EVM_PRIVATE_KEY=arbitrum_wallet_private_key

# Or modify withdraw.ts with specific address
receiverAddress: '0x1234567890123456789012345678901234567890'
```

### Step 3: Execute Withdrawals (15 minutes)
```bash
# CRITICAL: Stagger execution even more than swaps
# Only 2-3 students execute simultaneously
# Group 1: yarn run withdraw
# Wait for script timeout (60 seconds)
# Group 2: yarn run withdraw
# Continue...
```

### Step 4: Post-Timeout Monitoring (5 minutes)
```bash
# After script timeout, check NEAR balance:
near view intents.near mt_batch_balance_of '{
  "account_id": "YOUR_ACCOUNT_ID", 
  "token_ids": ["nep141:eth.bridge.near"]
}' --networkId mainnet

# Should show 0 or reduced ETH (tokens sent to bridge)
```

## Managing Student Anxiety During Timeout

**When scripts timeout (EVERY script will), immediately announce:**

```
"EVERYONE LISTEN: Your scripts just showed 'Quote hasn't been settled' 
- This is 100% normal and expected
- Your withdrawal is still processing successfully
- DO NOT run the script again
- Check your Arbitrum wallet in 10-15 minutes
- We'll verify together"
```

## Timeline Management

**0-60 seconds:** Script execution (students see status updates)
**60 seconds:** Script timeout message appears (NORMAL!)
**2-5 minutes:** Cross-chain bridge processing begins
**5-15 minutes:** ETH appears in Arbitrum wallets
**Total workshop time needed:** 30 minutes (allows for full completion)

## Common Questions During Timeout Period

**Q: "My script failed! Should I run it again?"**
**A:** "NO! The timeout is expected. Your withdrawal is processing. Running again creates duplicate transactions."

**Q: "How do I know if it actually worked?"**
**A:** "Check two things: 1) Your NEAR ETH balance went to zero, 2) Wait 15 minutes, check Arbitrum wallet."

**Q: "What if nothing appears in my Arbitrum wallet?"**
**A:** "Wait the full 15 minutes. Cross-chain operations need multiple blockchain confirmations. If still nothing after 20 minutes, we'll investigate."

**Q: "Why is cross-chain so much slower?"**
**A:** "Cross-chain involves multiple blockchains, bridge protocols, and security confirmations. It's like international wire transfer vs. domestic - more steps, but enables global interoperability."

## Verification Process

### After Script Timeout (Check immediately):
```bash
# Verify ETH was sent from NEAR
near view intents.near mt_batch_balance_of '{
  "account_id": "STUDENT_ACCOUNT", 
  "token_ids": ["nep141:eth.bridge.near"]
}' --networkId mainnet

# Should show ["0"] (ETH sent to bridge)
```

### After 15 Minutes (Final verification):
- Check student Arbitrum wallets for incoming ETH
- Visit arbiscan.io with student wallet addresses
- Look for recent ETH transactions

## Troubleshooting

**Student panic during timeout:**
```
"Remember: timeout = normal. Your transaction hash was ABC123... 
Let's check it on nearblocks.io to confirm it went through."
```

**No ETH received after 20 minutes:**
```
1. Check transaction status on nearblocks.io
2. Verify correct Arbitrum address used
3. Check if bridge experienced delays
4. Contact 1Click API support if needed
```

**Student wants to retry:**
```
"STOP! Never retry cross-chain withdrawals. Check your NEAR balance first - 
if ETH is gone from NEAR, withdrawal is processing successfully."
```

## Success Criteria

By end of module, students should have:
- [ ] Successfully initiated cross-chain withdrawal
- [ ] Understood that 60-second timeout is normal
- [ ] ETH balance reduced/eliminated on NEAR
- [ ] ETH appearing in Arbitrum wallet (or confident it will)

## Advanced Teaching Moment

**After successful withdrawals, explain the power:**
"You've just moved value between two completely different blockchains without understanding bridge protocols, managing gas on multiple chains, or dealing with complex routing. This is the power of intent-based operations!"

## Red Flags

🚨 **Student runs withdrawal twice** → Check for duplicate transactions, might need support
🚨 **Multiple students report no Arbitrum ETH after 25 minutes** → Check bridge status, network issues
🚨 **Students using wrong network addresses** → Verify all addresses are Arbitrum-compatible

## Transition to Module 7

**After confirming some students received ETH on Arbitrum:**
"Congratulations! You've completed the full cross-chain journey - NEAR to ETH on Arbitrum. In our final module, we'll explore advanced workflows and reverse flows, plus discuss real-world applications of what you've learned." 