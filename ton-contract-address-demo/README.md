# Cross-Referencing Contracts on TON with `initOf` and `contractAddress`

This project demonstrates how two smart contracts (`Todo1` and `Todo2`) on The Open Network (TON) can calculate and reference each other’s addresses **before deployment** using `initOf` and `contractAddress`.

It’s a foundational concept for modular and interconnected smart contract systems on TON.

---

## 📄 Summary

This example explores how two smart contracts — Todo1 and Todo2 — can compute each other's addresses before they are deployed.

Using:
- `initOf`: to generate a virtual initialization cell
- `contractAddress`: to calculate the resulting on-chain address

This is especially useful in situations where contracts need to reference each other without being deployed yet — avoiding circular dependencies.

---

## 📁 Contracts

### 🔹 `contracts/Todo1.fc`
```fift
import "@stdlib/deploy";

contract Todo1 with Deployable {
    seqno: Int as uint64 = 1;

    init() {}

    get fun myAddress(): Address {
        return myAddress();
    }

    get fun otherAddress(): Address {
        let init: StateInit = initOf Todo2();
        return contractAddress(init);
    }
}
```

### 🔹 `contracts/Todo2.fc`
```fift
import "@stdlib/deploy";

contract Todo2 with Deployable {
    seqno: Int as uint64 = 2;

    get fun otherAddress(): Address {
        let init: StateInit = initOf Todo1();
        return contractAddress(init);
    }
}
```

---

## 🧠 Real-Life Analogy

Imagine you’re setting up two physical offices:

- **Office A** (Todo1) knows its own address (via `myAddress()`).
- **Office A** can also predict where **Office B** (Todo2) would be built, just by using its blueprints (via `initOf Todo2()` and `contractAddress()`).
- Similarly, **Office B** can pre-calculate **Office A**'s address.

This enables early linking between contracts before actual deployment.

---

## 🔧 When Is This Useful?

- **Factory Contracts**: Predictable addresses for spawned contracts
- **Two-Way Interactions**: Mutual referencing
- **Upgrade Planning**: Contracts can know future versions' addresses
- **Cross-Contract Linking**: For paired NFTs, DAO-treasury setups, etc.

---

## 🌏 About TON Society India

TON Society India is the regional chapter of TON Society — a global community supporting developers, creators, and blockchain enthusiasts building on The Open Network (TON).

We connect, collaborate, and innovate within the TON ecosystem.

---

## 👤 Author

**Parthasarathireddy**  
Member, TON Society India  
🗓️ Written on May 12, 2025

---

## 🎉 Fun Note

> “Aw man, I didn’t win the funny giveaways at the Chennai event — guess my luck took a lunch break and never came back.  
But hey, fingers crossed I win the Tactical Launchpad! 😂”
