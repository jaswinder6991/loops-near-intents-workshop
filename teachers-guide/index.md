# Teachers Guide Index

## Quick Navigation

### Core Module Guides
1. **[Introduction Guide](01-introduction-guide.md)** - Setting expectations and workshop logistics
2. **[Cross-Chain Assets Guide](02-cross-chain-assets-guide.md)** - Teaching multi-token concepts  
3. **[Environment Setup Guide](03-environment-setup-guide.md)** - Managing technical setup and student funding
4. **[Cross-Chain Deposits Guide](04-cross-chain-deposits-guide.md)** - First real transactions and balance management
5. **[Asset Swapping Guide](05-asset-swapping-guide.md)** - On-chain swaps and timing expectations
6. **[Cross-Chain Withdrawals Guide](06-cross-chain-withdrawals-guide.md)** - Managing timeout expectations and anxiety
7. **[Advanced Workflows Guide](07-advanced-workflows-guide.md)** - Complex operations and real-world applications
8. **[Conclusion Guide](08-conclusion-guide.md)** - Wrap-up, feedback, and next steps

### Essential Resources
- **[README](README.md)** - Complete instructor preparation guide
- **[Quick Reference](#quick-reference)** - Emergency commands and common fixes

## Quick Reference

### Emergency Commands
```bash
# Fund student account
near tokens FUNDING_ACCOUNT transfer-near STUDENT_ACCOUNT '0.25 NEAR' network-config mainnet sign-with-keychain send

# Check student balance  
near account view-account-summary STUDENT_ACCOUNT network-config mainnet now

# Check wNEAR balance
near view intents.near mt_batch_balance_of '{"account_id": "STUDENT_ACCOUNT", "token_ids": ["nep141:wrap.near"]}' --networkId mainnet

# Check ETH balance
near view intents.near mt_batch_balance_of '{"account_id": "STUDENT_ACCOUNT", "token_ids": ["nep141:eth.bridge.near"]}' --networkId mainnet
```

### Critical Timing Reminders
- **Deposits:** 30-60 seconds
- **Swaps:** 2-5 minutes  
- **Withdrawals:** 5-15 minutes (script times out at 60 seconds - NORMAL!)
- **Total workshop:** 2.5-3 hours

### Red Flag Responses
🚨 **"Should I run the script again?"** → "NO! Wait for completion or timeout first"
🚨 **"My script failed"** → Check if it's normal timeout vs. actual error
🚨 **"Can I use testnet?"** → "No, intents only work on mainnet"

## Module Timing Overview

| Module | Duration | Critical Focus |
|--------|----------|----------------|
| 1 | 10 min | Set expectations |
| 2 | 20 min | Explain concepts |
| 3 | 25 min | Technical setup |
| 4 | 15 min | First transaction |
| 5 | 20 min | Swap operations |
| 6 | 30 min | Timeout management |
| 7 | 20 min | Advanced workflows |
| 8 | 15 min | Conclusion |
| **Total** | **2h 35m** | **Plus Q&A buffer** |

## Pre-Workshop Checklist Summary

### 48 Hours Before
- [ ] Complete workshop yourself
- [ ] Prepare funding strategy
- [ ] Test venue setup

### Day Of
- [ ] Fund students as accounts created
- [ ] Manage command execution timing  
- [ ] Monitor for red flags

### During Workshop
- [ ] Set realistic expectations
- [ ] Coordinate technical operations
- [ ] Manage student anxiety during timeouts 