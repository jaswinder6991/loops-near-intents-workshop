# Teachers Guide: Module 2 - Understanding Cross-Chain Assets

**Module Duration:** 20 minutes  
**Instructor Prep Time:** 10 minutes to review concepts  
**Key Focus:** Building conceptual foundation, preventing confusion about token representations

## Pre-Module Instructor Checklist

### 5 Minutes Before Module
- [ ] **Review multi-token concept** - Ensure you can explain ETH vs nETH vs wrapped ETH clearly
- [ ] **Prepare visual aids** - Draw token representation diagram on whiteboard if available
- [ ] **Have examples ready** - Real token IDs like `nep141:eth.bridge.near` vs `native-eth-arbitrum`
- [ ] **Test 1Click API endpoint** - Verify `yarn run tokens` works in workshop environment

## Step-by-Step Instructor Actions

### Step 1: Introduce Multi-Token Concept (8 minutes)

1. **Start with Web2 parallel**:
   ```
   "Think about money in your bank account vs. money in PayPal vs. money in Venmo.
   It's all 'your money' but each system represents it differently.
   Each has different capabilities - you can't use PayPal balance at an ATM."
   ```

2. **Draw the concept** (if whiteboard available):
   ```
   ETH Native (Ethereum) ← Bridge → nETH (NEAR) ← Bridge → ETH (Arbitrum)
        ↑                           ↑                       ↑
     Real ETH                 Representation           Real ETH
   ```

3. **Live demo token listings**:
   ```bash
   # Show students this command output
   yarn run tokens
   ```
   Point out how the same "ETH" appears with different token IDs.

### Step 2: Explain Token IDs (7 minutes)

1. **Break down a token ID**:
   ```
   nep141:eth.bridge.near
   ↑      ↑
   NEP-141 Contract Address
   Standard
   ```

2. **Compare representations**:
   - `nep141:eth.bridge.near` = ETH on NEAR
   - `native-eth-arbitrum` = Native ETH on Arbitrum
   - `nep141:wrap.near` = Wrapped NEAR

3. **Key teaching point**:
   "The token ID tells you WHERE the token exists and HOW to interact with it."

### Step 3: Connect to Workshop Operations (5 minutes)

1. **Map operations to token transformations**:
   - Deposit: `wrap.near` → Enable cross-chain swaps
   - Swap: `wrap.near` → `nep141:eth.bridge.near` (both on NEAR)
   - Withdraw: `nep141:eth.bridge.near` → `native-eth-arbitrum` (cross-chain)

2. **Preview the journey**:
   "You'll start with NEAR tokens, transform them through different representations, and end with ETH on Arbitrum that works with any Ethereum app."

## Common Questions to Prepare For

### About Token Representations
**Q: "Why can't I just send ETH directly from Ethereum to Arbitrum?"**
**A:** "You could! But it requires understanding bridges, gas fees on multiple chains, and complex routing. Intents let you just say 'I want ETH on Arbitrum' and handle the complexity for you."

**Q: "Is nETH 'real' ETH or just an IOU?"**
**A:** "It's backed 1:1 by real ETH locked in bridge contracts. Think of it like a bank certificate - it represents real ETH you can always redeem."

**Q: "What if the bridge gets hacked?"**
**A:** "Bridge risk exists, which is why we use small amounts for learning. In production, you'd research bridge security. The workshop uses established, audited bridges."

### About the 1Click API
**Q: "Why not just use a bridge directly?"**
**A:** "Bridges are like individual airline websites. 1Click API is like Expedia - it finds the best routes across all available bridges and handles the complexity."

**Q: "Does 1Click API charge extra fees?"**
**A:** "Yes, but it often saves money by finding optimal routes. Like how a travel agent might cost extra but saves you time and often gets better deals."

**Q: "What if 1Click API goes down?"**
**A:** "You could still use bridges directly, just like you could book flights directly with airlines. 1Click provides convenience, not lock-in."

## Common Student Mistakes to Watch For

### Conceptual Mistakes
❌ **Mistake:** "So nETH is just fake ETH?"
✅ **Correction:** "No! It's real ETH value, just represented on a different blockchain. Like how your bank balance shows real money even though it's just numbers in a computer."

❌ **Mistake:** "Why are there so many steps? Can't we just swap NEAR for ETH directly?"
✅ **Correction:** "We could, but then your ETH would only exist on NEAR. By bridging to Arbitrum, you get ETH that works with all Ethereum apps, DeFi protocols, etc."

❌ **Mistake:** Students assuming all operations happen instantly
✅ **Prevention:** Reinforce timing: "Cross-chain = slower but more powerful. On-chain = faster but limited to one ecosystem."

### Technical Confusion
❌ **Mistake:** Students confusing token IDs and thinking they need to remember them
✅ **Prevention:** "Don't memorize these! The 1Click API handles this. We're showing you so you understand what's happening behind the scenes."

❌ **Mistake:** Students asking about specific bridge protocols
✅ **Redirect:** "Great question! The beauty of intents is you don't need to know. But if you're curious, we can discuss bridge protocols after the workshop."

## Interactive Elements to Keep Students Engaged

### Quick Check-In (Mid-Module)
"Raise your hand if this makes sense: We're going to turn your NEAR tokens into ETH tokens that work on Arbitrum, and the 1Click API figures out all the steps in between."

### Analogy Building
Ask students: "Can anyone think of another example where the same value is represented differently in different systems?" (Examples: Game tokens across platforms, loyalty points, frequent flyer miles)

### Preview Exercise
"Look at the token list output. Find ETH representations. How many different places can ETH exist according to this API?" (Answer: Ethereum mainnet, Arbitrum, Base, NEAR, etc.)

## Timing Checkpoints

### 8 Minutes In
- Students should understand multi-token concept
- Key insight: Same value, different representations

### 15 Minutes In
- Students should understand token IDs are addresses/identifiers
- Comfortable with idea that 1Click API handles complexity

### 20 Minutes (End)
- Students should see the connection between concepts and upcoming workshop steps
- Ready for practical environment setup

## Advanced Questions (If Time Permits)

**Q: "How does the API know which bridge to use?"**
**A:** "It queries multiple bridges for quotes, compares fees and timing, then chooses the best route. Like how Google Maps compares different routes."

**Q: "Can I use this for my own app?"**
**A:** "Yes! The 1Click API has documentation for developers. This workshop shows you both how to use it and understand what it's doing."

**Q: "What about failed transactions?"**
**A:** "Great question! Cross-chain operations can fail at different steps. The API provides status tracking so you know where things are. We'll see this in action during the workshop."

## Red Flags to Address Immediately

🚨 **Student says: "This seems too complicated, I just want to swap tokens"**
**Response:** "I understand! That's exactly why intents were created. The complexity we're explaining now is handled automatically. We're showing you the 'why' so you understand the 'how' when we start building."

🚨 **Multiple students look confused about basic blockchain concepts**
**Response:** Pause and do a quick blockchain basics recap: "Let's quickly review what we mean by 'different blockchains' before continuing."

🚨 **Student asks detailed technical questions about bridge security**
**Response:** "Excellent question! Let's bookmark that for after we complete the practical sections. I want to make sure everyone follows the core concepts first."

## Success Criteria for Module 2

By the end of this module, students should:
- [ ] Understand that tokens can exist on multiple blockchains
- [ ] Know that token IDs specify WHERE and HOW to interact with tokens
- [ ] Grasp that intents abstract away cross-chain complexity
- [ ] See the connection between concepts and workshop operations
- [ ] Be motivated to see these concepts in action

## Transition to Module 3

**Good transition statement:**
"Now that you understand what's happening behind the scenes, let's set up your development environment so you can see these concepts in action. The next module will get your hands dirty with the actual tools."

**Check before moving on:**
- Students comfortable with multi-token concept
- No major confusion about token representations
- Students eager to start practical work 