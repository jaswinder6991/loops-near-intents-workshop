# Teachers Guide: Module 4 - Cross-Chain Deposits

**Module Duration:** 15 minutes  
**Instructor Prep Time:** 20 minutes  
**Key Focus:** First real transaction, balance management, setting expectations for cross-chain timing

## Pre-Module Instructor Checklist

### 15 Minutes Before Module
- [ ] **Verify all students have funded accounts** - Check the status from Module 3
- [ ] **Test deposit script yourself** - Ensure `yarn run deposit` works in venue environment
- [ ] **Prepare balance tracking** - Set up monitoring for student progress
- [ ] **Have explorer links ready** - nearblocks.io bookmarked for transaction verification
- [ ] **Review wrap.near registration** - Ensure all students completed registration

### 5 Minutes Before Module
- [ ] **Check API status** - Verify 1Click API is responsive
- [ ] **Prepare timing expectations** - Deposits typically take 30-60 seconds
- [ ] **Set up group communication** - For sharing transaction hashes and troubleshooting

## Step-by-Step Instructor Actions

### Step 1: Pre-Deposit Verification (3 minutes)

1. **Mass balance check**:
   ```bash
   # Have everyone run this together:
   near account view-account-summary YOUR_ACCOUNT_ID network-config mainnet now
   ```
   Students should see ~0.2 NEAR balance.

2. **Verify wrap.near registration**:
   ```bash
   # Check if students completed registration:
   near view wrap.near storage_balance_of '{"account_id": "STUDENT_ACCOUNT"}' --networkId mainnet
   ```
   Should return a balance object, not null.

3. **Address any missing registrations immediately**:
   ```bash
   # For students who missed registration:
   near contract call-function as-transaction wrap.near storage_deposit json-args '{"account_id": "STUDENT_ACCOUNT"}' prepaid-gas '100.0 Tgas' attached-deposit '0.00125 NEAR' sign-as STUDENT_ACCOUNT network-config mainnet sign-with-access-key-file ~/.near-credentials/implicit/STUDENT_ACCOUNT.json
   ```

### Step 2: Coordinate First Deposit (8 minutes)

1. **Explain what will happen before executing**:
   ```
   "This deposit will:
   - Take 0.1 NEAR from your account
   - Wrap it into wNEAR (NEP-141 token)
   - Enable it for cross-chain swaps
   - Complete in 30-60 seconds"
   ```

2. **Execute deposits in small groups**:
   ```bash
   # Don't have everyone run simultaneously
   # Group 1: Run deposit command
   yarn run deposit
   
   # Wait for Group 1 to see "Transaction hash", then
   # Group 2: Run deposit command
   # Continue until all groups complete
   ```

3. **Monitor transaction hashes**:
   - Have students share transaction hashes in chat
   - Spot-check a few transactions on nearblocks.io
   - Look for successful "wrap" function calls

### Step 3: Balance Verification and Troubleshooting (4 minutes)

1. **Check wrapped NEAR balance**:
   ```bash
   # Have everyone verify together:
   near view intents.near mt_batch_balance_of '{
     "account_id": "YOUR_ACCOUNT_ID", 
     "token_ids": ["nep141:wrap.near"]
   }' --networkId mainnet
   ```

2. **Interpret results**:
   ```json
   // Success looks like:
   ["100000000000000000000000"]  // 0.1 NEAR in yoctoNEAR
   
   // Failure looks like:
   ["0"]  // No wrapped NEAR
   ```

3. **Address any failures immediately** - See troubleshooting section below.

## Common Questions to Prepare For

### About the Deposit Process
**Q: "Why do I need to wrap NEAR? Can't I just use regular NEAR for swaps?"**
**A:** "Think of it like converting cash to a prepaid card. Wrapped NEAR (wNEAR) is the 'token format' that the Intent contracts understand. Regular NEAR is the 'native currency' format."

**Q: "Where does my NEAR go when I wrap it?"**
**A:** "It goes to the wrap.near contract, which gives you back wNEAR tokens representing the same value. It's like depositing $100 and getting a $100 gift card - same value, different format."

**Q: "What if I want my original NEAR back?"**
**A:** "You can unwrap wNEAR back to NEAR anytime. But for this workshop, we'll trade the wNEAR for ETH, then withdraw ETH to Arbitrum."

### About Timing and Fees
**Q: "Why did this take 30 seconds? I thought blockchain was instant."**
**A:** "Blockchains need time for confirmations. 30 seconds is actually fast! Cross-chain operations we'll do later take 5-15 minutes."

**Q: "How much did this deposit cost in fees?"**
**A:** "About 0.001 NEAR (~$0.001) in gas fees. Much cheaper than Ethereum mainnet!"

**Q: "My balance went from 0.2 to 0.09 NEAR - where did the rest go?"**
**A:** "0.1 NEAR was wrapped (now it's wNEAR), ~0.001 for gas fees, and you have ~0.09 NEAR left for future operations."

### About Next Steps
**Q: "Now I have wNEAR - what can I do with it?"**
**A:** "Now you can swap it for other tokens! In the next module, we'll swap your wNEAR for ETH. The wNEAR enables cross-chain operations."

**Q: "Can I wrap more NEAR if I want?"**
**A:** "Yes! But for the workshop, 0.1 NEAR worth of wNEAR is perfect. It leaves you with enough NEAR for gas fees."

## Common Student Mistakes to Watch For

### Before Deposit Execution
❌ **Mistake:** Students trying to deposit all their NEAR (0.2 NEAR)
✅ **Prevention:** "Keep 0.1 NEAR unwrapped for gas fees! Only wrap 0.1 NEAR."

❌ **Mistake:** Students skipping wrap.near registration
✅ **Prevention:** Check registration status before allowing deposits. Fix missing registrations immediately.

❌ **Mistake:** Students using testnet commands
✅ **Prevention:** "Remember: add `--networkId mainnet` to all commands!"

### During Deposit Execution
❌ **Mistake:** Students panicking when script takes time
✅ **Prevention:** "30-60 seconds is normal! Don't close the terminal or run the command again."

❌ **Mistake:** Students running multiple deposits simultaneously
✅ **Prevention:** "Wait for the first deposit to complete before trying again. Multiple deposits will consume your balance."

❌ **Mistake:** Students not saving transaction hashes
✅ **Prevention:** "Copy the transaction hash! We'll use it to verify the operation on the blockchain explorer."

### After Deposit Completion
❌ **Mistake:** Students confused by balance checking commands
✅ **Prevention:** Demonstrate the difference:
   ```bash
   # NEAR balance (should decrease):
   near account view-account-summary YOUR_ACCOUNT_ID network-config mainnet now
   
   # wNEAR balance (should show new tokens):
   near view intents.near mt_batch_balance_of '{"account_id": "YOUR_ACCOUNT_ID", "token_ids": ["nep141:wrap.near"]}' --networkId mainnet
   ```

## Troubleshooting Common Issues

### Deposit Script Fails
```bash
# Common error: "Account doesn't have enough balance"
# Check actual balance:
near account view-account-summary ACCOUNT_ID network-config mainnet now

# If balance < 0.15 NEAR, send more funds:
near tokens YOUR_FUNDING_ACCOUNT transfer-near STUDENT_ACCOUNT '0.1 NEAR' network-config mainnet sign-with-keychain send
```

### Registration Issues
```bash
# Error: "Account not registered with wrap.near"
# Fix registration:
near contract call-function as-transaction wrap.near storage_deposit \
  json-args '{"account_id": "STUDENT_ACCOUNT"}' \
  prepaid-gas '30.0 Tgas' \
  attached-deposit '0.00125 NEAR' \
  sign-as STUDENT_ACCOUNT \
  network-config mainnet \
  sign-with-keychain send
```

### Balance Verification Issues
```bash
# Student sees "0" wNEAR balance after successful deposit
# Check transaction status:
near transaction view-status TRANSACTION_HASH --networkId mainnet

# If transaction succeeded but balance is 0, wait 30 seconds and check again
# Sometimes indexing takes time
```

### Network Connectivity Issues
```bash
# Student can't connect to NEAR network
# Test connection:
curl -s https://rpc.mainnet.near.org/status

# If network issues, switch to backup RPC:
export NEAR_NETWORK_ID=mainnet
export NEAR_RPC_URL=https://near-mainnet.infura.io/v3/YOUR_KEY
```

## Interactive Elements to Keep Students Engaged

### Real-Time Monitoring
Create a shared tracking board:
```
Student | Deposit TX | Status | wNEAR Balance
Alice   | AbC123...  | ✅     | 0.1 NEAR
Bob     | DeF456...  | ⏳     | Checking...
Carol   | GhI789...  | ✅     | 0.1 NEAR
```

### Blockchain Explorer Demo
1. **Show a student's transaction on nearblocks.io**:
   - Find the transaction hash
   - Show the function call to wrap.near
   - Point out the fee structure
   - Show the resulting token transfer

2. **Key teaching moment**:
   "Notice how the blockchain records everything permanently. Your deposit is now part of the global ledger."

### Group Verification
"Everyone who sees '100000000000000000000000' in their wNEAR balance, raise your hand!"

## Timing Checkpoints

### 3 Minutes In
- All students verified their NEAR balance
- Any missing registrations completed
- Ready to start deposits

### 8 Minutes In
- First group completed deposits successfully
- Transaction hashes shared and verified
- Second group starting deposits

### 12 Minutes In
- All students completed deposits
- wNEAR balances verified
- Any issues resolved

### 15 Minutes (End)
- Everyone has 0.1 wNEAR tokens
- Understanding of wrap/unwrap concept
- Ready for swapping operations

## Advanced Teaching Opportunities

### If Students Want to Explore Further
Show the wrap.near contract on explorer:
```
Visit: nearblocks.io/address/wrap.near
Show: Recent transactions, total value locked, contract methods
Explain: "This contract holds real NEAR and issues wNEAR tokens 1:1"
```

### Connect to DeFi Concepts
"This wrapping process is fundamental to DeFi. You've just used the same mechanism that powers lending protocols, DEXs, and yield farming."

### Preview Next Module
"Now you have wNEAR tokens that the Intent system recognizes. In the next module, we'll swap these wNEAR tokens for ETH tokens - still all happening on NEAR blockchain!"

## Red Flags Requiring Immediate Action

🚨 **Multiple students get "Account not registered" errors**
**Action:** Pause workshop, batch-register accounts, then continue

🚨 **Student accidentally wrapped all their NEAR (no gas money left)**
**Action:** Send additional NEAR for gas fees: `near tokens YOUR_ACCOUNT transfer-near STUDENT_ACCOUNT '0.05 NEAR'`

🚨 **Deposits taking longer than 2 minutes**
**Action:** Check NEAR network status, consider switching RPC endpoints

🚨 **Students see successful transaction but 0 wNEAR balance**
**Action:** Wait for indexing, check transaction details, verify correct token ID in balance query

## Success Criteria for Module 4

By the end of this module, all students should have:
- [ ] Successfully wrapped 0.1 NEAR into wNEAR tokens
- [ ] Verified their wNEAR balance shows ~0.1 NEAR worth
- [ ] Still have ~0.09 NEAR for gas fees
- [ ] Understand the wrapping concept and its purpose
- [ ] Transaction hash saved for reference

## Transition to Module 5

**Good transition statement:**
"Excellent! You've just completed your first cross-chain preparation step. Your NEAR is now in a format that can be swapped for other tokens. In the next module, we'll swap your wNEAR for ETH - and this swap happens entirely on NEAR, which is much faster and cheaper than doing it on Ethereum!"

**Check before moving on:**
- All students have positive wNEAR balance
- No unresolved transaction failures
- Students understand the wrapped token concept
- Everyone still has NEAR for gas fees

## Notes for Future Workshop Iterations

### What Works Well
- Staggered execution prevents network congestion
- Real-time transaction monitoring builds confidence
- Blockchain explorer demos reinforce concepts

### Areas to Improve
- Consider pre-registering all accounts with wrap.near
- Provide balance calculation helpers
- Create automated status checking scripts

### Student Feedback Common Themes
- "Seeing the transaction on the explorer was cool"
- "I thought wrapping was more complicated"
- "The timing was reasonable, not too slow" 
