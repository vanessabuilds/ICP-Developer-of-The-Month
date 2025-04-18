ICP Developer of the Month: My ICP Journey 🚀

Over the past thirty days I dove head‑first into the Internet Computer (ICP) ecosystem—learning Motoko from scratch, wiring up NFID email auth, learning how to move real bitcoin with ckBTC, and, for the **MoMo Mini‑Hackathon**, building a proof‑of‑concept **on‑chain sentiment‑analysis canister** using the MotokoLearn library. In this post I’ll recap what I learned and link the key resources.

---

### 📚 Week 1 – Bootcamp & Foundations  

| Goal | Take‑aways |
|------|------------|
| **Understand the Dev‑of‑the‑Month rules** |
| **Learn Motoko basics** |
| **Spin up local replica** | `dfx start --clean`, `dfx deploy`—all code runs identically on mainnet |

---

### 🔐 Week 2 – Identity: NFID + Email Login  

* NFID lets users sign‑in with **email or Google** while still producing a WebAuthn‑backed ICP principal.  
* In the front‑end I added:

```ts
import { NFID } from "@nfid/wallet";
const identity = await NFID.init({ providers:["email"] }).signin();
```

* Result: a familiar Web 2 UX and no separate wallet extension needed.

---

### 🪙 Week 3 – ckBTC Payments  

* **ckBTC** is a *chain‑key* twin of real bitcoin, held by ICP canisters—no bridges.  
* Demo code (Motoko):

```motoko
import ckBTC "canister:ckbtc";
await ckBTC.transfer("bc1q...", 100_000);  // 0.001 BTC
```

* Transfers finalize in ~2 seconds with reduced fees.

---

### 🤖 Week 4 – Special Project: On‑Chain Sentiment AI  

#### Why MotokoLearn?  
The GitHub repo provides CART trees and random forests that fit inside Wasm limits.

#### How it works  
1. **Training**: Used labelled sentences → `fitRegression` → depth‑5 tree stored in `stable var modelTree`.  
2. **Inference**: Message length → predict float → clamp to {2,0,‑1,‑2,‑3}.  
3. **Routing**  
   * neutral → chatbot script 
   * crisis → hotline script  
   * else → **LLM canister** with a CBT‑style system prompt.


```motoko
let msgs = [
  { role = #system_; content = systemPrompt },
  { role = #user;    content = input      }
];
let answer = await LLM.chat(#Llama3_1_8B, msgs);
```

---

### 🏆 Demo Highlights  

| Scenario | Flow |
|----------|------|
| “What day is it?” | neutral → friendly redirect |
| “I hate myself…” | crisis → immediate hotline list |
| “I got a promotion!” | positive → LLM |
| “I am sad” | negative → LLM |
---

### 💡 Lessons Learned  

* Motoko’s *actor model* feels like TypeScript + Rust safety.  
* On‑chain ML is feasible today for small trees.  
* NFID lowers onboarding friction.  
* ckBTC showcases ICP’s native multi‑chain vision.  

---

### 🛠️ Next Steps & Mini‑Hackathon Ideas  

| Idea | Stack |
|------|-------|
| Voice sentiment (WebSpeech → MotokoLearn) | JS + Motoko |

Thanks for following my journey—see you in the forum, and happy hacking!
