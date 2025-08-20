# Token-2022 AMM SDK Tutorials

This README covers the usage of the Token-2022 AMM SDK.  
You’ll learn how to:
- Connect a wallet
- Perform token swaps
- Add/remove liquidity
- Query pool state
- Get price quotes
- Handle slippage & confirmations

---

## Prerequisites

- Node.js >= 18
- pnpm or npm
- Solana wallet (e.g. Backpack, Phantom)
- Some SOL for gas fees

Install dependencies:

```bash
pnpm install
```

---

## Quickstart

```ts
import { Connection, Keypair } from "@solana/web3.js";
import { Amm } from "token-2022-amm";

const connection = new Connection("https://api.devnet.solana.com");
const wallet = Keypair.generate();

const amm = new Amm(connection, wallet);

console.log("AMM initialized:", amm.programId.toBase58());
```

---

## Swap Tokens

```ts
import { swap } from "token-2022-amm";

async function doSwap() {
  const result = await swap(amm, {
    pool: "POOL_PUBKEY",
    inputMint: "TOKEN_A",
    outputMint: "TOKEN_B",
    amountIn: 1000,
    minAmountOut: 900,
  });

  console.log("Swap signature:", result.signature);
}

doSwap();
```

---

## Add Liquidity

```ts
import { addLiquidity } from "token-2022-amm";

async function provideLiquidity() {
  const result = await addLiquidity(amm, {
    pool: "POOL_PUBKEY",
    amountA: 5000,
    amountB: 5000,
  });

  console.log("Liquidity provided:", result.signature);
}

provideLiquidity();
```

---

## Remove Liquidity

```ts
import { removeLiquidity } from "token-2022-amm";

async function withdrawLiquidity() {
  const result = await removeLiquidity(amm, {
    pool: "POOL_PUBKEY",
    lpAmount: 1000,
  });

  console.log("Liquidity withdrawn:", result.signature);
}

withdrawLiquidity();
```

---

# 🔹 Extra Sections

## Query Pool State

```ts
import { getPoolState } from "token-2022-amm";

async function fetchPool() {
  const pool = await getPoolState(amm, "POOL_PUBKEY");
  console.log("Pool reserves:", pool.reserves);
}
```

---

## Get Price Quote

```ts
import { getQuote } from "token-2022-amm";

async function quoteExample() {
  const quote = await getQuote(amm, {
    pool: "POOL_PUBKEY",
    inputMint: "TOKEN_A",
    outputMint: "TOKEN_B",
    amountIn: 1000,
  });

  console.log("Expected output:", quote.amountOut);
}
```

---

## Handle Slippage & Confirmations

```ts
import { swap } from "token-2022-amm";

async function safeSwap() {
  const result = await swap(amm, {
    pool: "POOL_PUBKEY",
    inputMint: "TOKEN_A",
    outputMint: "TOKEN_B",
    amountIn: 1000,
    minAmountOut: 950, // 5% slippage tolerance
    confirmOptions: { commitment: "finalized" },
  });

  console.log("Swap confirmed:", result.signature);
}
```

---

# ✅ Summary

- Use `swap` for token exchanges  
- Use `addLiquidity` / `removeLiquidity` to manage pools  
- Use `getPoolState` and `getQuote` for analytics  
- Always handle slippage & confirmations for safety  

Now you can build dApps that integrate Token-2022 AMM directly with TypeScript!
