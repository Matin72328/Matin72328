- 👋 Hi, I’m @Matin72328
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Matin72328/Matin72328 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract TrumpSup {
    string public name = "TrumpSup";
    string public symbol = "TRUMPSUP";
    uint8 public decimals = 18;
    uint256 public totalSupply = 1000000000 * 10 ** uint256(decimals);
    address public owner = 0x33736051D1A675683e06add8Ce5eE02f99418cCd;

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    constructor() {
        balanceOf[owner] = totalSupply;
    }

    function transfer(address to, uint256 value) public returns (bool) {
        require(balanceOf[msg.sender] >= value, "Insufficient Balance");
        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;
        return true;
    }

    function approve(address spender, uint256 value) public returns (bool) {
        allowance[msg.sender][spender] = value;
        return true;
    }

    function transferFrom(address from, address to, uint256 value) public returns (bool) {
        require(balanceOf[from] >= value, "Insufficient Balance");
        require(allowance[from][msg.sender] >= value, "Allowance Exceeded");
        balanceOf[from] -= value;
        balanceOf[to] += value;
        allowance[from][msg.sender] -= value;
        return true;
    }
}Act as an Expert Web3 Full-Stack Architect and Smart Contract Engineer. I want to build a SocialFi & Attention-Economy Token Launchpad web and mobile-first PWA application called **"Person.fun"** (inspired by Pump.fun, tailored for launching tokens around People, Celebrities, CEOs, Billionaires, Creators, and Self-Tokens).

### 1. CORE CONCEPT & VISION
"Person.fun" allows anyone to instantly create and trade tokens based on real-world individuals, creators, CEOs, billionaires, or themselves using an automated fair-launch bonding curve (no pre-sales, no team allocations, 100% rug-proof).

### 2. UNIQUE KILLER FEATURES TO IMPLEMENT
1. **Two Token Categories (Legal & Trust System):**
   - `🎭 Fan / Parody Tribute Token`: Created by fans for famous personalities (clearly labeled "Unofficial Fan Parody - Not affiliated").
   - `✅ Verified Self-Token`: Created or claimed by the actual person via Social OAuth verification (X/Twitter or Farcaster).
2. **"Claim Your Persona" Fee Escrow Vault:**
   - Every trade has a 1% fee: 0.5% goes to the Person.fun platform treasury, and 0.5% goes into an on-chain **Creator Escrow Vault** mapped to the person's social handle (e.g., `@elonmusk`).
   - If the real person verifies their X/Twitter account via OAuth, they can claim all accumulated escrow fees and turn the token badge into "✅ Verified".
3. **"King of the Persona" (Graduation & Canonical Ticker):**
   - Bonding curve progress bar from 0% to 100% (Target Market Cap: $69,000).
   - Once the bonding curve hits 100%, liquidity automatically migrates to Uniswap V3 / Raydium, LP tokens are burned forever, and that token becomes the official "Canonical Ticker" for that persona.
4. **Live Clout & Hype Meter:**
   - Each token page displays a "Hype Score" (0-100) and a "Trending Heating Up 🔥" ticker ribbon at the top of the homepage showing recent buys/sells in real time (shake animation on big buys).
5. **Token-Gated VIP Chat (Holder Lounge):**
   - Every token page has two chat tabs: "Public Hype Chat" and "VIP Holder Lounge" (only accessible to users holding at least 1,000 tokens of that person).

### 3. TECH STACK
- **Frontend:** Next.js 14+ (App Router), TypeScript, TailwindCSS, Shadcn/UI, Framer Motion (for live ticker animations), Lucide Icons.
- **Charts:** `lightweight-charts` (TradingView) for real-time 1m/5m/15m bonding curve price candles.
- **Web3 / Auth:** Wagmi + Viem + RainbowKit (or Privy.io style social login flow) configured for **Base Chain (EVM)** [or Solana if specified].
- **Smart Contracts:** Solidity (0.8.20+) using OpenZeppelin ERC-20, ReentrancyGuard, and a custom Constant Product Bonding Curve (`x * y = k` virtual reserves).

### 4. PAGES & UI/UX DESIGN (Dark Mode, Cyberpunk/Neon Web3 Aesthetic)
Build a complete, responsive, mobile-first PWA layout with the following screens:
1. **Top Live Ribbon:** Flashing live feed of latest token creations and trades (e.g., *"0x71...3a bought 0.5 ETH of $MUSK"*).
2. **Homepage (Discovery & Leaderboard):**
   - Hero section: **"King of the Clout"** (The token closest to 100% bonding curve graduation).
   - Filters: `🔥 Trending`, `🆕 Newly Launched`, `👑 Billionaires & CEOs`, `🎬 Celebrities`, `✅ Verified Creators`, `🎓 Graduated`.
   - Token Cards showing: Avatar, Name, `$TICKER`, Verification Badge (`🎭 Parody` vs `✅ Verified`), Market Cap, Bonding Curve % Progress Bar, and Unclaimed Creator Escrow Pool amount in USD.
3. **Create Persona Token Modal / Page (`/create`):**
   - Form fields: Person's Name, Ticker Symbol (`$`), Category (CEO, Celebrity, Creator, Self), Image Upload, X/Twitter Handle of the Person (for the Fee Escrow Vault), Description, and optional "Verify it's Me" toggle.
   - Instant Initial Buy prompt (allow creator to buy a small bag in the same transaction).
4. **Token Trading Terminal (`/person/[ticker]`):**
   - **Left/Center Column:** Persona Profile Header (with Escrow Vault banner: *"💰 $4,250 waiting in vault for @handle to claim!"*), TradingView Candlestick Chart, Bonding Curve Progress Bar, and Tabbed Chat (Public Comments vs. Token-Gated VIP Holder Chat) + Live Trades History Table.
   - **Right Column (Sticky Swap Widget):** Fast Buy/Sell box with quick slippage settings, preset amount buttons (`0.01 ETH`, `0.1 ETH`, `0.5 ETH`, `MAX`), real-time price impact calculation, and Top Holders list showing % supply owned.
5. **Claim Vault Page (`/claim`):**
   - A dedicated high-converting page where influencers/CEOs/creators can search their name, see how much unclaimed trading fee money is waiting for them, connect their X/Twitter to verify identity, and withdraw their crypto.

### 5. DELIVERABLES REQUESTED NOW
1. Write the complete **Solidity Smart Contracts** (`PersonToken.sol` and `PersonFunLaunchpad.sol`) including the virtual bonding curve math, 1% fee split (0.5% platform, 0.5% creator escrow vault), and graduation logic.
2. Build the full **Next.js Frontend prototype** with mock real-time data, interactive bonding curve buy/sell simulation, TradingView chart integration, and all 5 views mentioned above so I can test the full user flow immediately.
3. 
