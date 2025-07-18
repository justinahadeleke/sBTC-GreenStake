
#  sBTC-GreenStake - Decentralized Asset Management & Governance Contract

A Clarity smart contract for **tokenized renewable energy asset management**, allowing users to register assets, purchase shares, earn revenue, and participate in decentralized governance. This contract is suitable for fractional ownership and transparent decision-making for assets like solar, wind, hydro, or biomass facilities.

---

## 🚀 Features

* **Asset Registration**: Register tokenized energy assets with location and financial data.
* **Fractional Ownership**: Users can purchase shares and claim proportional revenue.
* **Revenue Distribution**: Asset revenues are distributed based on shares owned.
* **Governance System**: Shareholders submit/vote on proposals for asset-related decisions.
* **Asset Metrics**: Track operational metrics such as energy produced, ROI, efficiency, etc.
* **On-chain Voting**: Supports vote thresholds, quorums, and execution delays.

---

## 🧠 Architecture Overview

### ✅ Core Concepts

* **Asset**: A real-world renewable project represented on-chain.
* **Shares**: Units of ownership; priced in STX and tied to revenue/voting power.
* **Revenue**: Distributed proportionally based on shares.
* **Proposals**: Created and voted on by shareholders to manage assets.
* **Governance Settings**: Configurable parameters for voting rules and quorum thresholds.

---

## 📦 Storage Structures

### Assets

```clojure
assets: {
  asset-id: uint,
  name: string,
  asset-type: "solar" | "wind" | "hydro" | "biomass",
  total-shares: uint,
  available-shares: uint,
  share-price: uint,
  total-revenue: uint,
  revenue-per-share: uint,
  status: "proposed" | "active",
  creation-height: uint,
  last-updated: uint,
  location: { latitude: int, longitude: int }
}
```

### Ownership

```clojure
ownership: {
  asset-id: uint,
  owner: principal,
  shares: uint,
  revenue-claimed: uint,
  last-claim-height: uint,
  voting-power: uint
}
```

### Asset Metrics

```clojure
asset-metrics: {
  energy-produced: uint,
  operational-hours: uint,
  maintenance-cost: uint,
  efficiency-rating: uint,
  carbon-offset: uint,
  peak-output: uint,
  lifetime-roi: uint
}
```

### Proposals

```clojure
proposals: {
  proposer: principal,
  proposal-type: string,
  description: string,
  amount: uint,
  votes-for: uint,
  votes-against: uint,
  status: "active" | "executed" | "rejected",
  start-height: uint,
  end-height: uint,
  execution-delay: uint,
  quorum-reached: bool
}
```

---

## 🛠️ Public Functions

### `register-asset`

Register a new renewable asset with required metadata and financials.

```clojure
(register-asset name type total-shares share-price latitude longitude)
```

### `purchase-shares`

Buy available shares in a registered asset.

```clojure
(purchase-shares asset-id share-count)
```

### `distribute-revenue`

Send revenue to be distributed to shareholders.

```clojure
(distribute-revenue asset-id amount)
```

### `submit-proposal`

Submit a governance proposal related to an asset.

```clojure
(submit-proposal asset-id type description amount)
```

---

## 🔍 Read-Only Functions

### `get-asset-info`

Retrieve asset metadata and status.

```clojure
(get-asset-info asset-id)
```

### `get-ownership-info`

Get share ownership and revenue claim status for a principal.

```clojure
(get-ownership-info asset-id owner)
```

### `get-asset-metrics`

View the asset’s operational performance and ROI.

```clojure
(get-asset-metrics asset-id)
```

### `get-governance-settings`

Retrieve governance rules for an asset.

```clojure
(get-governance-settings asset-id)
```

### `get-proposal-info`

Get detailed info about a proposal.

```clojure
(get-proposal-info asset-id proposal-id)
```

---

## 🔐 Permissions

* Only the **contract owner** (deployer) can:

  * Register the first assets
  * Distribute revenue

* **Any user** can:

  * Purchase shares in active assets
  * Submit proposals (with minimum voting power)
  * View all asset data

---

## ⚠️ Error Codes

| Code   | Meaning                       |
| ------ | ----------------------------- |
| `u401` | Not authorized                |
| `u403` | Invalid amount                |
| `u405` | Insufficient shares available |
| `u406` | STX transfer failed           |
| `u412` | Attempt to buy 0 shares       |
| `u417` | Proposal quorum not met       |
| ...    | (See full list in contract)   |

---

## 📈 Tokenomics

* **Minimum Investment**: 1 STX
* **Voting Power**: Proportional to shares
* **Revenue Share**: Based on `revenue-per-share`

---
