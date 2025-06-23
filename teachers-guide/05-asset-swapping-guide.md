# Teachers Guide: Module 5 - Asset Swapping

**Module Duration:** 20 minutes  
**Instructor Prep Time:** 15 minutes  
**Key Focus:** First cross-chain swap, managing timing expectations, understanding on-chain vs cross-chain

## Pre-Module Instructor Checklist

### 10 Minutes Before Module
- [ ] **Verify all students have wNEAR** - Check balances from Module 4
- [ ] **Test swap script** - Ensure `yarn run swap` works in environment
- [ ] **Prepare timing explanation** - Swaps take 2-5 minutes, longer than deposits
- [ ] **Have explorer ready** - For monitoring swap transactions

## Step-by-Step Instructor Actions

### Step 1: Pre-Swap Setup (3 minutes)
```bash
# Verify everyone has wNEAR
near view intents.near mt_batch_balance_of '{
  "account_id": "YOUR_ACCOUNT_ID", 
  "token_ids": ["nep141:wrap.near"]
}' --networkId mainnet

# Should see: ["100000000000000000000000"] (0.1 NEAR)
```

### Step 2: Execute Swaps (12 minutes)
```bash
# CRITICAL: Don't let everyone run simultaneously
# Group execution prevents API overload
# Group 1: yarn run swap
# Wait for "Transaction hash" output
# Group 2: yarn run swap
# Continue until all complete
```

### Step 3: Monitor and Verify (5 minutes)
```bash
# Check ETH balance after completion
near view intents.near mt_batch_balance_of '{
  "account_id": "YOUR_ACCOUNT_ID", 
  "token_ids": ["nep141:eth.bridge.near"]
}' --networkId mainnet

# Should see ETH amount (varies by market rates)
```

## Critical Timing Expectations

**Set these expectations clearly:**
- Swap operations: 2-5 minutes (not instant!)
- Script will show status updates: PENDING → PROCESSING → COMPLETE
- This is ON-CHAIN swapping (all on NEAR blockchain)
- Much faster than true cross-chain operations

## Common Questions to Prepare For

**Q: "Why is this taking so long? It's just a token swap!"**
**A:** "Even though both tokens are on NEAR, the Intent system needs to find solvers, execute the swap, and confirm. 2-5 minutes is actually fast for intent-based operations!"

**Q: "How much ETH will I get for my 0.1 NEAR?"**
**A:** "It depends on current market rates. You might get 0.00004-0.00008 ETH (~$0.08-0.16). The important thing is learning the process!"

**Q: "Is this 'real' ETH or just tokens representing ETH?"**
**A:** "These are ETH tokens on NEAR - they represent real ETH value. In the next module, we'll withdraw them as native ETH on Arbitrum."

**Q: "What if the swap fails?"**
**A:** "The system will show error status. Usually caused by market volatility or insufficient liquidity. We can retry or adjust amounts."

## Common Student Mistakes

❌ **Running swap multiple times while first is processing**
✅ **Prevention:** "Wait for COMPLETE status before running again!"

❌ **Panicking when swap takes 3-4 minutes**
✅ **Prevention:** "This is normal! Watch the status updates - PROCESSING means it's working."

❌ **Expecting exact ETH amounts**
✅ **Prevention:** "Amount varies with market rates. Focus on successful completion, not exact numbers."

❌ **Confusing this with cross-chain bridging**
✅ **Prevention:** "This swap happens entirely on NEAR. True cross-chain comes in Module 6."

## Status Monitoring

**Typical progression students will see:**
```bash
Quote status: PENDING_DEPOSIT
Quote status: PENDING_DEPOSIT  
Quote status: PROCESSING
Quote status: PROCESSING
Swap completed successfully!
```

**If stuck on PENDING_DEPOSIT >3 minutes:**
- Check transaction hash on explorer
- Verify sufficient wNEAR balance
- Check for network congestion

## Interactive Tracking

Create real-time progress board:
```
Student | Swap TX | Status | ETH Received
Alice   | AbC123  | ✅ COMPLETE | 0.000045 ETH  
Bob     | DeF456  | ⏳ PROCESSING | ...
Carol   | GhI789  | ✅ COMPLETE | 0.000042 ETH
```

## Troubleshooting Quick Fixes

```bash
# Swap fails with "insufficient balance"
# Check wNEAR balance:
near view intents.near mt_batch_balance_of '{"account_id": "ACCOUNT", "token_ids": ["nep141:wrap.near"]}' --networkId mainnet

# Market volatility error
# Wait 2 minutes, retry swap

# Script timeout but transaction succeeded
# Check ETH balance manually - swap may have completed
```

## Success Criteria

By end of module, students should have:
- [ ] Successfully swapped wNEAR for ETH tokens
- [ ] ETH balance visible in Intent contract
- [ ] Understanding that this was on-chain (NEAR only)
- [ ] Ready for true cross-chain withdrawal

## Transition to Module 6

**Good transition statement:**
"Perfect! You now have ETH tokens on NEAR. But what if you want to use these ETH tokens on Arbitrum with DeFi protocols? That's where true cross-chain operations come in. Next, we'll withdraw your ETH from NEAR to Arbitrum - this is where timing gets longer but the power of cross-chain really shows!"

## Red Flags

🚨 **Multiple swaps failing** → Check 1Click API status, market volatility
🚨 **Students running multiple swaps** → Stop immediately, explain status monitoring
🚨 **Network congestion causing long delays** → Consider batching or rescheduling 