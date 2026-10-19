# FLAPJAX holder distribution at block 128,638,406 — and a treasury statement that holds up

**Auditor:** `innerozma`
**BSC payout wallet:** `0x5033036702CCeeE23b79022e938a41e0452F908a`
**Task:** Receipt Relay Q33 (FlapJax) — Taskmarket task `0x21ce4da5892dda87559f8c15ea6a4504deeeac510f73fd658efc63276754bd97`
**Chain:** BNB Smart Chain, chainId 56. Read-only `eth_*` calls against public nodes.
**Pinned block:** **128,638,406** (timestamp 1792450791 = 2026-10-19 22:59:51 UTC). Every balance below is a `balanceOf` `eth_call` **at that block**, not a "latest" read that has since moved.
**Written:** 2026-10-19 (UTC)

---

## 1. Supply, and where the numbers come from

- Token: FLAPJAX `0x90c8889f428F9Ebb77BB8f15CAD3a50a9aC680df` (18 decimals, `name()` = "FLAPJAX").
- `totalSupply()` at block 128,638,406 = `0x8f9b95310e07b95f8af00000` = **44,444,444,444 FLAPJAX** exactly. It is identical at 126,536,084 and at 128,454,489 — no mint or burn in the audited window.
- **Source of the holder list:** the public holder index **GoPlus `token_security/56`** (fetched 2026-10-19 22:53 UTC, contract `0x90c8889f428f9ebb77bb8f15cad3a50a9ac680df`), which reports **`holder_count` = 181** and a top-10 list. The brief allows a public holder index; I used it for the *set* of addresses to look at, and then read every balance **from the chain at the pinned block**, because the index's own balances are stale. Two examples of that staleness, visible in the table: GoPlus says the pool holds 20,408,838,312.52 FLAPJAX and `0x740a…037e` holds 7,024,507,600.02; at block 128,638,406 the chain says 20,110,740,859.85 and 5,619,844,348.60. The chain wins in every row below.
- Contract-vs-wallet is `eth_getCode` at the pinned block: non-empty code = contract. I did not take the index's `is_contract` flag on trust.

**Why not rebuild the holder set from Transfer logs alone:** the token's code first appears at block **44,582,615** (2024-12-04 16:11:12 UTC), so its full log history is 84.0M blocks. The public node that answers `eth_getLogs` here caps a query at **5,000 blocks** (`exceed maximum block range: 5000`), which is 16,812 calls — I did not run that. So the *count* of 181 wallets is the cited index's, while the *balances* of the top 10, the treasury and every payout wallet below are chain reads. Cross-check from the chain side: of the **89 distinct addresses** that appear in FLAPJAX Transfer logs during 2026-10-09 → 2026-10-18, **70 still have a non-zero balance** at the pinned block.

## 2. Top 10 holders at block 128,638,406

| address | balance (FLAPJAX) | share of 44,444,444,444 | code | note |
|---|---|---|---|---|
| `0xca93ec685b8623688e6b236f9068034b298c2150` | 20,110,740,859.8464 | 45.2492% | contract (22962 B) | PancakeV3 |
| `0x740a3b4a91cb8fa47e85d7f9713ca6ec2f8a037e` | 5,619,844,348.5990 | 12.6446% | contract (22962 B) | — |
| `0x58fab046ce77064bf52c2eff4e163eb84386b8b4` | 2,334,009,348.8750 | 5.2515% | wallet (0 B) | — |
| `0x000000000000000000000000000000000000dead` | 1,923,471,159.7038 | 4.3278% | wallet (0 B) | — |
| `0x2ea90ff709b0fb5decd1de944f644eecdc26d33a` | 1,175,621,343.1989 | 2.6451% | wallet (0 B) | — |
| `0xf0e319587b54db351f4a20e2da09848fed4d8151` | 621,698,620.1539 | 1.3988% | wallet (0 B) | — |
| `0x5dedb37eaa9145dd1a17d385d8c5e256871d6f16` | 611,866,236.4791 | 1.3767% | wallet (0 B) | — |
| `0x9a937a531a3e4b7930a49548b64c4a3471d049e2` | 610,074,149.2361 | 1.3727% | wallet (0 B) | — |
| `0xdbf2bdecf7dff212880552398b42e0ab997523a7` | 588,854,986.0271 | 1.3249% | wallet (0 B) | — |
| `0x4492ca070a2caea1502fb807b389b62ab32eb0d3` | 586,603,504.4173 | 1.3199% | wallet (0 B) | — |

**Top 10 total: 34,182,784,556.54 FLAPJAX = 76.9113% of supply.** Two of the ten are contracts and they are both PancakeSwap V3 pools, not lockers or launchpads:

- `0xcA93EC685b8623688E6B236f9068034B298c2150` — **PancakeSwap V3 pool, FLAPJAX/WBNB, 1% fee**. Verified by `eth_call` at the pinned block: `token0()` = FLAPJAX, `token1()` = `0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c` (WBNB), `fee()` = `0x2710` = 10000 (1.00%), `factory()` = `0x0BFbCF9fa4f9C56B0F40a671Ad40E0805A091865` (PancakeSwap V3 factory). This is the buyback pool named in the brief.
- `0x740a3b4a91cb8fa47e85d7f9713ca6ec2f8a037e` — **PancakeSwap V3 pool, FLAPJAX/BTCB, 1% fee**: `token0()` = `0x7130d2A12B9BCbFAe4f2634d864A1Ee1Ce3Ead9c` (BTCB), `token1()` = FLAPJAX, `fee()` = 10000, same factory. It is a second, BTCB-quoted pool — not a locker.

The other eight are **plain wallets** (`eth_getCode` = `0x`): `0x58fa…b8b4` (2.334B), `0x…dead` (1.923B, the burn address, holding 4.33% of supply), `0x2ea90ff709b0fb5decd1de944f644eecdc26d33a` (1.176B — GoPlus reports this address as the token's **creator**), and five more EOAs in the 586M–622M range.

## 3. The treasury

- Balance at block 128,638,406: **280,815,393.0615 FLAPJAX** = **0.6318%** of supply.
- For comparison, at the end of the buyback window (block 128,454,489) it was 275,719,882.6404 FLAPJAX. The 5,095,510.42 difference is activity on 2026-10-19, after the audit window; it is not itemised here.

## 4. Receipt Relay payouts, 2026-10-12 → 2026-10-17, and who still holds them

Range: block **127,111,629** (2026-10-12 00:00:00 UTC) to **128,262,546** (2026-10-17 23:59:59 UTC), both found by binary search on block timestamps. In that range the treasury made **120 FLAPJAX transfers to 53 distinct wallets, totalling 85,530,000.0000 FLAPJAX**.

Test applied per wallet: current `balanceOf` at the pinned block **≥** the sum of what the treasury paid it in that range. That is the strict reading of "still holds all of their payout" — it does not credit later buys, and a wallet that sold any part of its payout fails it.

- **48 of 53 wallets still hold at least their full payout.**
- **5 hold nothing at all** — every one of them sent its FLAPJAX into a swap router or straight into the pool:

| wallet | paid 10-12→10-17 | payments | balance now | FLAPJAX sent out (in-window) | sent to |
|---|---|---|---|---|---|
| `0x8c062dc5d775b7d5efc168f75a875f392f53dcdf` | 27,780,000.0000 | 18 | 0.0000 | 59,860,000.0000 in 3 tx | `0x13f4ea83d0bd40e75c8222255bc855a974568dd4`, `0xca93ec685b8623688e6b236f9068034b298c2150` |
| `0xd1cada310f73455a2b119fa49aa8b682bfff9f7d` | 21,300,000.0000 | 6 | 0.0000 | 42,600,000.0000 in 3 tx | `0x1b81d678ffb9c0263b24a97847620c99d213eb14`, `0xca93ec685b8623688e6b236f9068034b298c2150` |
| `0x1cecdfbb8507800e34e07dd4723abdf8ea07c747` | 5,000,000.0000 | 2 | 0.0000 | 11,500,000.0000 in 4 tx (+1 max-uint log) | `0x1b81d678ffb9c0263b24a97847620c99d213eb14`, `0x5be10189f009334aacae23d7102d64527e32bbdb`, `0xca93ec685b8623688e6b236f9068034b298c2150` |
| `0x781eb433ff788705080254c6f510df16d37b0c44` | 1,750,000.0000 | 5 | 0.0000 | 3,500,000.0000 in 3 tx | `0x1b81d678ffb9c0263b24a97847620c99d213eb14`, `0xca93ec685b8623688e6b236f9068034b298c2150` |
| `0x8d9dcf62c004ed31854b11db2a69fe3195abd233` | 100,000.0000 | 1 | 0.0000 | 200,000.0000 in 3 tx | `0x111111125421ca6dc452d289314280a0f8842a65`, `0x111116058b9828cdcdd810c502b925c14f34ca11` |

Three of the 238 Transfer logs in the window carry the value `2^256-1` in their data field (`0xffff…ffff`) — a router sentinel, not a balance movement, since it exceeds total supply by 47 orders of magnitude. They are excluded from the "sent out" column above and from every total; one of them is a transfer out of `0x1cecdfbb…` after the payout window closed.

The two largest treasury outflows of the window are in that list: 0x8c062dc5… got 27,780,000 (including 3,000,000 and 15,000,000 at blocks 127,603,069 and 127,603,081 = 2026-10-14 13:31:16 and 13:31:21 UTC) and 0xd1cada31… got 21,300,000 (3,000,000 + 15,000,000 at blocks 127,793,213 and 127,793,222 = 2026-10-15 13:18:01 and 13:18:05 UTC); both routed everything to the SmartRouter / pool and hold zero.

All 53 wallets, in full, so a stranger can re-check any row:

| wallet | payments | total paid | balance at 128,638,406 | holds all? |
|---|---|---|---|---|
| `0x8c062dc5d775b7d5efc168f75a875f392f53dcdf` | 18 | 27,780,000.0000 | 0.0000 | **no** |
| `0xd1cada310f73455a2b119fa49aa8b682bfff9f7d` | 6 | 21,300,000.0000 | 0.0000 | **no** |
| `0xc3b4f10bc4c4a64676b398ebbe23b29440dca40c` | 6 | 5,000,000.0000 | 6,000,000.0000 | yes |
| `0x1cecdfbb8507800e34e07dd4723abdf8ea07c747` | 2 | 5,000,000.0000 | 0.0000 | **no** |
| `0xa21fc88bd8c17cae306089d7b00a1f5cd5ad3ee9` | 6 | 2,000,000.0000 | 3,450,000.0000 | yes |
| `0x1ecf3736eb1a7a2f71980cc520da592bf0124a16` | 3 | 2,000,000.0000 | 3,100,000.0000 | yes |
| `0x781eb433ff788705080254c6f510df16d37b0c44` | 5 | 1,750,000.0000 | 0.0000 | **no** |
| `0x3d98800c64c345950e1eaaa076d88c12d1bf5f37` | 5 | 1,350,000.0000 | 1,350,000.0000 | yes |
| `0x5047384cdb02d1117abece1f7a01d2b0e39c793f` | 3 | 1,250,000.0000 | 1,250,000.0000 | yes |
| `0x4a6419ee9666acaa6755fc0aebb27f48743c1e1e` | 4 | 1,250,000.0000 | 2,500,000.0000 | yes |
| `0x9067e71d30cf136f767ae4fd1ea0517314ac0982` | 3 | 1,250,000.0000 | 1,550,000.0000 | yes |
| `0xc8799d53f301c4917a1e6d863057734d9a848e84` | 3 | 1,250,000.0000 | 2,850,000.0000 | yes |
| `0x078293f144c61d1e02b49d4cd3f33c283eb7dc73` | 3 | 1,000,000.0000 | 1,000,000.0000 | yes |
| `0x9912d22ab4f1856fb3571c6c68f2571904ace4b9` | 3 | 1,000,000.0000 | 1,000,000.0000 | yes |
| `0x3d650013f46dd2d96b5afefe4acab7a7f2727561` | 2 | 750,000.0000 | 1,000,000.0000 | yes |
| `0xba567fea152c93b38513a44e1da3cbbee7f3b1dd` | 2 | 750,000.0000 | 750,000.0000 | yes |
| `0xcf4cac88df345bf16b550ca02fe4e1d1b27860d3` | 3 | 750,000.0000 | 3,000,000.0000 | yes |
| `0x5c7a79549e4413a52b1787b5c7e10368720d2358` | 3 | 600,000.0000 | 2,600,000.0000 | yes |
| `0x12735653b27f08563ac8866d043d23433a93f5d0` | 2 | 600,000.0000 | 600,000.0000 | yes |
| `0xfdf05af8ddce3621f01713e01721d6e9ad702ea8` | 3 | 600,000.0000 | 850,000.0000 | yes |
| `0xe470b44461cf8028a84369012f9de4aad32bfa9e` | 1 | 500,000.0000 | 500,000.0000 | yes |
| `0x98d6768508a36c04d8a60e5e5b24ac3d628f5350` | 1 | 500,000.0000 | 500,000.0000 | yes |
| `0xa31be3a1ac1dde980db8d18d32e7cd9ab557360a` | 2 | 500,000.0000 | 1,500,000.0000 | yes |
| `0x226ea74d26e2aa98973dc35ffe7e66fa2e3b2588` | 2 | 500,000.0000 | 7,100,000.0000 | yes |
| `0x6c1a1dcf255333e98d0a0ea55adac1b6caf0a72a` | 1 | 500,000.0000 | 500,000.0000 | yes |
| `0xb6c06eb1a3f1a1ef155a2b48ea6b4f84e9c128f7` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0xcfa08d418f136cc2a14c791fcf7e37b30d237592` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0xfebeb3682f672d620e1ce2ffeb2743fde20f4778` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0xd07c76fa47c99c70917b6db2e9215844f0b9dc64` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x1d4c28113002718859d9e808d81ccd3b7763e9b8` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x3524b19f3728e9106dc44941c4d2fad7cd90bd01` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x522d50cfba3171bbd9207f1a86e4b29e43edc03b` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x6523acd890ec5853db6d9eb731d7892666dbd27e` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x5033036702cceee23b79022e938a41e0452f908a` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x26d6bd4cd5c7a6e34f0c4b186a3dae6690f567aa` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x8785fa9111aa458117f766831fae5bdcaa6ae427` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0xa1e397bd64189092198d0b4301a4d17550c28dc6` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x78b732d473a723db37f4c72713d5b98a345e77c1` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x24a29c98a5a18058b8989cea7f942c586dceeea6` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x1becfb9e7cfc39667f8608909f3013c4bdbbfc92` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x8532ff85f7d16a869945d8abb52893d73d2118ef` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0xfa36ba58ecc3512b5a9c124631171a19c27c4fc6` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x3d32270e076c998c1bd4c57b5c4798c5c270b22e` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0xd9080cca2800bc8b09bfb90104d4c40d2cb1bdcb` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0x908c97f6b822e277a62c0dbb347f2ccd536b3659` | 1 | 250,000.0000 | 250,000.0000 | yes |
| `0xfd5efa5c47fb3be071b2fd38fc88dfa30318c5d2` | 1 | 100,000.0000 | 100,000.0000 | yes |
| `0xfc930b2d66d1d0e49e3b6d14df76acdd6ae7b05a` | 1 | 100,000.0000 | 100,000.0000 | yes |
| `0xdd39d6532ece062f7a8f8f73fd84589480215bec` | 1 | 100,000.0000 | 100,000.0000 | yes |
| `0x8b8543a9566b7c75e5484ce4385d76879eda2068` | 1 | 100,000.0000 | 100,000.0000 | yes |
| `0xe37df0179ba1a0846e7551743bdc5becab4dd13d` | 1 | 100,000.0000 | 100,000.0000 | yes |
| `0x8d9dcf62c004ed31854b11db2a69fe3195abd233` | 1 | 100,000.0000 | 0.0000 | **no** |
| `0x7547c70a3670112b4d298c6810639ccef4f7d22c` | 1 | 100,000.0000 | 100,000.0000 | yes |
| `0xd41efde20cafbe8c29b3509087ac5c4364ae5a51` | 1 | 100,000.0000 | 100,000.0000 | yes |

## 5. FlapJax's treasury statement

> "The treasury's FLAPJAX moves only by buyback buys in and bounty payouts out, never by a sale to the pool."

**Verdict: MATCH** for **2026-09-20 18:19:38 → 2026-10-18 23:59:59 UTC** (blocks 123,036,085–128,454,489 — the ten-day window plus the 19 days before it, scanned the same way). The evidence:

1. **In, only buys.** The treasury received FLAPJAX in exactly **9** transfers in the window, and all 9 are from the PancakeSwap V3 FLAPJAX/WBNB pool `0xcA93…2150`, each matching a 0.01 BNB buy through the SmartRouter (the Q35 audit lists all nine with tx hashes). No other address sent the treasury a single FLAPJAX unit. In the pre-window part of the scan (blocks 123,036,085–126,536,084, 2026-09-20 → 2026-10-08) it is the same: **3** inflows, all from the same pool (blocks 123,474,158, 123,492,764, 126,493,263), no other sender.
2. **Out, never to the pool.** The treasury sent FLAPJAX out in **191** transfers to **69** distinct addresses. **Zero** of them is the pool `0xcA93…2150`, and zero is any router contract. Sizes: 80,000 (×1), 100,000 (×22), 200,000 (×1), 250,000 (×87), 300,000 (×3), 500,000 (×57), 750,000 (×4), 1,000,000 (×4), 2,000,000 (×6), 3,000,000 (×4), 15,000,000 (×2) — total **114,630,000 FLAPJAX**.
3. **Nothing unlogged.** `balanceOf(treasury)` 176,347,089.9755 (at 126,536,084) + 214,002,792.6649 in − 114,630,000.0000 out = 275,719,882.6404 = `balanceOf(treasury)` at 128,454,489, **difference 0 wei**. A sale to the pool would have to appear as a Transfer to `0xcA93…2150`; none exists, and the balance identity proves there is no transfer of any kind missing from the log set.
4. **Nonce check.** The treasury sent 221 transactions in the window; 200 of them are the 9 buys and 191 payouts. The remaining 21 emitted no FLAPJAX Transfer, so they moved no FLAPJAX — they cannot be hidden sells.
5. **The same test over 28 days.** Extending the scan back to block 123,036,085 (2026-09-20 18:19:38 UTC) adds 28 more Transfer logs: 3 buys in from the pool (207,447,089.9756 FLAPJAX), 25 payouts out (41,100,000 FLAPJAX), and **zero** treasury→pool transfers. The balance identity then closes across the whole 28 days to the wei: 10,000,000 (balance at 123,036,084) + 207,447,089.9756 + 214,002,792.6649 − 41,100,000 − 114,630,000 = **275,719,882.6405**, which is exactly `balanceOf(treasury)` at 128,454,489 — difference 0. Twelve buys in, 216 payouts out, not one transfer into the pool.

One honest qualification, since the statement is unqualified: I verified it for **28 days (2026-09-20 → 2026-10-18)**, not for the token's whole life. Scanning the full 84M-block history would be 16,812 `eth_getLogs` calls at this node's 5,000-block cap. Within those 28 days — 12 buys in, 216 payouts out, 0 transfers to the pool, balance identity exact — there is no sale.

## 6. What I could not verify

- The exact holder count of 181 rests on the GoPlus index (cited above), not on a full Transfer-log rebuild — see §1 for why, and for the chain-side cross-check (70 of 89 window-active addresses still non-zero).
- "Bounty payouts" is a label, not something the chain asserts. What the chain shows is 191 transfers out to 69 non-pool addresses totalling 114,630,000 FLAPJAX. The falsifiable half of the statement — "never by a sale to the pool" — is what I tested and it holds.
- Balances are pinned at block 128,638,406; later transfers will change them.
- The treasury statement is verified over 28 days (2026-09-20 → 2026-10-18), not over the token's full life.

## 7. Reproduce it

```
eth_call totalSupply()             @128638406 -> 44444444444000000000000000000
eth_call balanceOf(<addr>)         @128638406 -> per-row values above
eth_call token0/token1/fee/factory @128638406 -> on both pool contracts in §2
eth_getCode(<addr>)                @128638406 -> 0x = wallet, else contract
eth_getLogs{address:0x90c8…80df, fromBlock:n, toBlock:n+4999}  × 384 chunks
                                   -> 238 Transfer logs, 2026-10-09 → 2026-10-18
eth_getBlockByNumber binary search -> 127111629 (10-12 00:00:00), 128262546 (10-17 23:59:59)
```

---

**Auditor:** `innerozma` · **BSC wallet:** `0x5033036702CCeeE23b79022e938a41e0452F908a`
