# 🦄 Token-2022 AMM Tutorials

Welcome to the **Token-2022 AMM (Automated Market Maker) Tutorials**.  
This document will guide you step-by-step through all the major features of the AMM:

1. Token Swapping  
2. Adding & Removing Liquidity  
3. Staking  
4. Farming  
5. Advanced Notes (Rust SDK, Extra Tips)  

---

## 1. 🔄 Token Swapping

### Concept
Token swapping allows users to exchange one token for another using the AMM’s liquidity pools.

### Steps
1. Connect your wallet (e.g. Backpack).  
2. Select the token you want to swap **from** and **to**.  
3. Enter the swap amount.  
4. Set slippage tolerance.  
5. Approve the transaction in your wallet.  

### Example (TypeScript)
```ts
import { swap } from './amm-sdk';

async function performSwap(wallet, tokenA, tokenB, amount) {
  const tx = await swap(wallet, tokenA, tokenB, amount);
  console.log("Swap transaction:", tx);
}
```

### Troubleshooting
- Ensure both tokens exist in the AMM.  
- If a swap fails, increase slippage tolerance slightly.  

---

## 2. 💧 Adding & Removing Liquidity

### Concept
Liquidity providers (LPs) deposit token pairs into pools and earn a share of trading fees.  
In return, LPs receive LP tokens representing their pool share.

### Steps to Add Liquidity
1. Connect your wallet.  
2. Choose a pool (e.g. SOL/USDC).  
3. Enter the amount of both tokens.  
4. Approve the transaction.  

### Steps to Remove Liquidity
1. Go to your “My Pools” dashboard.  
2. Select the LP tokens you want to redeem.  
3. Approve the transaction to get your tokens back.  

### Example (TypeScript)
```ts
import { addLiquidity, removeLiquidity } from './amm-sdk';

async function provideLiquidity(wallet, tokenA, tokenB, amountA, amountB) {
  const tx = await addLiquidity(wallet, tokenA, tokenB, amountA, amountB);
  console.log("Liquidity added:", tx);
}

async function withdrawLiquidity(wallet, lpToken, amount) {
  const tx = await removeLiquidity(wallet, lpToken, amount);
  console.log("Liquidity removed:", tx);
}
```

### Best Practices
- Be mindful of **impermanent loss**.  
- Larger pools reduce swap slippage.  

---

## 3. 🔐 Staking

### Concept
Staking allows users to lock LP tokens into a staking pool to earn rewards.  
Rewards may come from protocol fees or reward tokens.

### Steps
1. Connect wallet.  
2. Choose the LP token staking pool.  
3. Enter the number of LP tokens.  
4. Confirm staking.  
5. Claim rewards when ready.  

### Example (TypeScript)
```ts
import { stake, unstake, claimRewards } from './staking-sdk';

async function doStake(wallet, lpToken, amount) {
  const tx = await stake(wallet, lpToken, amount);
  console.log("Staked:", tx);
}

async function doUnstake(wallet, lpToken, amount) {
  const tx = await unstake(wallet, lpToken, amount);
  console.log("Unstaked:", tx);
}

async function claim(wallet, stakingPool) {
  const rewards = await claimRewards(wallet, stakingPool);
  console.log("Rewards claimed:", rewards);
}
```

### Notes
- Some pools have **lock-up periods**.  
- APY depends on pool size and rewards.  

---

## 4. 🌾 Farming

### Concept
Yield farming is a way to maximize returns by depositing LP tokens into farming contracts that distribute extra reward tokens.

### Steps
1. Connect wallet.  
2. Select a farming pool.  
3. Deposit LP tokens.  
4. Harvest rewards anytime.  

### Example (TypeScript)
```ts
import { farm, harvest } from './farming-sdk';

async function startFarming(wallet, lpToken, amount) {
  const tx = await farm(wallet, lpToken, amount);
  console.log("Farming started:", tx);
}

async function collectRewards(wallet, farmingPool) {
  const rewards = await harvest(wallet, farmingPool);
  console.log("Harvested rewards:", rewards);
}
```

### Risks vs Rewards
- High returns but higher risk.  
- Monitor rewards vs impermanent loss.  

---

## 5. ⚙️ Advanced Notes

### Rust SDK (Optional)
```rust
use amm_sdk::swap;

fn perform_swap(wallet: &Wallet, token_a: Pubkey, token_b: Pubkey, amount: u64) {
    let result = swap(wallet, token_a, token_b, amount);
    println!("Swap result: {:?}", result);
}
```

### Extra Tips
- **Slippage:** Keep between 0.1% - 1%.  
- **Transaction fees:** Always keep SOL for gas.  
- **Debugging:** If transaction fails, check explorer logs.  

---

## ✅ Conclusion

You’ve now learned how to:  
- Swap tokens  
- Provide and withdraw liquidity  
- Stake LP tokens  
- Yield farm for rewards  

For more examples, check the repo and SDK documentation.  
Happy building! 🚀
