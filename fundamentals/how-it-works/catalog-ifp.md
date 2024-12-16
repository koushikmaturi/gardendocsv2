---
hidden: true
---

# Catalog IFP

Catalog's Instant Finality Protocol (IFP) is one of the critical components that contribute to Garden's ability to execute trustless cross-chain swaps involving Bitcoin (and likewise PoW chains) in as little as **30 seconds**. By leveraging Bitcoin's scripting capabilities and advanced transaction mechanics, the IFP enhances transaction speed while maintaining decentralization.

## How do IFP addresses work?

An IFP address is a specialized Bitcoin address type, constructed using a specific pay-to-script-hash (P2SH) script. Its key features include:

* **2-of-2 multisig configuration:** The address requires two private keys, one held by the user and the other secured in a trusted execution environment (TEE).
* **30-day escape hatch:** This ensures that funds can be recovered under specific conditions if necessary.
* **TEE rules for replace-by-fee (RBF):**
  * **New outpoints:** Can be added to a transaction while performing an RBF.
  * **Existing outpoints:** Can only be updated if there is a valid spending transaction that uses the specific outpoint to create new outpoints. The original outpoint is replaced with outputs from the signed spending transaction.

This setup provides controlled flexibility for transaction updates while maintaining Bitcoin’s trustless integrity.

## Why does Garden use IFP addresses?

Garden leverages IFP addresses to facilitate instant atomic swaps, reducing settlement times significantly. Here's how:

* **Solver settlements:** Solvers use IFP addresses for settling intents, ensuring funds are securely locked and transferred quickly.
* **Immediate usability:** Funds received from an IFP address appear immediately in the user’s wallet without requiring the standard 1 confirmation on the Bitcoin chain. Users can use these funds right away and transfer them to another bitcoin address according to the TEE-enforced rules described earlier.
* **Cascading transactions:** In theory, this process can continue indefinitely. The recipient of the user’s transferred funds can further transfer them to another address, creating a new outpoint. When the transaction is confirmed in mempool, the IFP ensures the funds are securely transferred to the final outpoint, maintaining atomicity throughout the process.



