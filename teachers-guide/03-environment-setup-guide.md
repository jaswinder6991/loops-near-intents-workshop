# Teachers Guide: Module 3 - Environment Setup

**Module Duration:** 25 minutes  
**Instructor Prep Time:** 45 minutes (CRITICAL!)  
**Key Focus:** Preventing setup failures, managing student funding, technical troubleshooting

## Critical Pre-Workshop Preparation

### 30 Minutes Before Workshop
- [ ] **Test complete setup flow** - Run through every command on fresh machine
- [ ] **Prepare NEAR funding method** - Account with (students × 0.25 NEAR) + buffer
- [ ] **Set up communication channel** - For account IDs and troubleshooting
- [ ] **Test venue internet** - Verify GitHub clone speed and npm performance

## Step-by-Step Instructor Actions

### Step 1: Staggered Installation (8 minutes)
```bash
# Group installations to prevent WiFi overload
# Group 1 (rows 1-2): npm install -g near-cli-rs
# Wait 2 minutes, then Group 2 (rows 3-4)
# Share commands immediately in chat
```

### Step 2: Account Creation Management (10 minutes)
```bash
# Coordinate timing - API rate limiting exists
near account create-account fund-later use-auto-generation

# Collect IDs systematically in shared doc:
# Student | Account ID | Funding Status
# Fund immediately as IDs come in
```

### Step 3: Environment Setup (5 minutes)
```bash
# Walk through together
cp .env.example .env
# Guide .env editing step-by-step
# Test immediately: node -e "require('dotenv').config(); console.log(process.env.NEAR_ACCOUNT_ID)"
```

### Step 4: Mass Verification (2 minutes)
```bash
# Everyone together:
near account view-account-summary ACCOUNT_ID network-config mainnet now
yarn run tokens
```

## Common Questions to Prepare For

**Q: "Permission denied installing NEAR CLI"**
**A:** "Try `sudo npm install -g near-cli-rs`. On Mac, might need npm permissions fix."

**Q: "How long until I get NEAR tokens?"**
**A:** "30-60 seconds. Check with balance command."

**Q: "I only see 0.2 NEAR, is that enough?"**
**A:** "Perfect! That's $0.20 worth - covers all workshop operations."

## Common Student Mistakes

❌ **Installing different NEAR CLI versions**
✅ **Prevention:** "Everyone use exact command: `npm install -g near-cli-rs`"

❌ **Using testnet commands**
✅ **Prevention:** "Always include `network-config mainnet`"

❌ **Sharing private keys in public chat**
✅ **Prevention:** "NEVER share private keys publicly! DM me if help needed."

## Quick Troubleshooting Commands

```bash
# NEAR CLI not found
export PATH=$PATH:~/.npm-global/bin

# Account funding
near tokens FUNDING_ACCOUNT transfer-near STUDENT_ACCOUNT '0.25 NEAR' network-config mainnet sign-with-keychain send

# Test environment
node -r dotenv/config -e "console.log(process.env.NEAR_ACCOUNT_ID)"
```

## Success Criteria

All students must have:
- [ ] NEAR CLI installed and working
- [ ] Funded account (0.2+ NEAR)
- [ ] Environment variables configured
- [ ] Verified API connectivity

## Red Flags Requiring Immediate Action

🚨 **Multiple CLI installation failures** → Switch installation method
🚨 **WiFi can't handle installs** → Use mobile hotspots or pre-built packages
🚨 **API rate limiting accounts** → Create accounts manually, distribute keys securely

## Timing Management

### 8 Minutes In
- Most students should have NEAR CLI installed
- Start account creation for fastest students

### 15 Minutes In  
- Most students should have accounts created
- Begin funding process
- Slower students catching up on installation

### 22 Minutes In
- All students should have funded accounts
- Environment variables configured
- Ready for verification

### 25 Minutes (End)
- Everyone should see their balance and token list
- Ready to start actual workshop operations

## Transition to Module 4

**Good transition statement:**
"Perfect! Everyone has a working environment and funded account. Now comes the fun part - let's make your first cross-chain deposit and watch your NEAR tokens get ready for cross-chain operations."

**Final check before proceeding:**
- All students can see their NEAR balance
- `yarn run tokens` works for everyone
- No unresolved technical issues

## Emergency Backup Plans

### If WiFi Completely Fails
- Switch to mobile hotspot
- Use pre-configured Docker containers
- Pair students with working setups

### If NEAR Network Issues
- Check status.near.org
- Consider rescheduling if major outage
- Use cached/pre-recorded examples

### If Too Many Students Have Issues
- Pair programming: 2 students per working setup
- Focus on demonstration with follow-up individual help
- Share screen with working environment for group follow-along 