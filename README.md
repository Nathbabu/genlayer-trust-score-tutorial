# 🚀 From Zero to GenLayer: Building a Trust Score dApp

> 🚀 A beginner-friendly guide to building your first GenLayer Intelligent Contract

---

## 🌐 What is GenLayer?

GenLayer is a new type of blockchain that allows smart contracts to use AI and real-world data to make decisions.

Unlike traditional blockchains where contracts follow fixed rules, GenLayer introduces **Intelligent Contracts** that can:

- Understand natural language  
- Use APIs and external data  
- Make reasoning-based decisions  

This makes GenLayer more flexible and powerful for real-world applications.

---

## 🧠 How GenLayer Works (Simple Explanation)

GenLayer uses a unique system where multiple validators (including AI models) evaluate the same request.

Instead of relying only on strict code execution, GenLayer allows:

- AI-based reasoning  
- External data fetching  
- Consensus between multiple results  

This is what enables more advanced applications compared to traditional blockchains.

---

## ⚙️ Key Concepts

### 🔹 Optimistic Democracy Consensus
GenLayer allows multiple validators (including AI models) to evaluate and agree on results instead of relying on a single execution.

### 🔹 Equivalence Principle
Different validators may use different approaches (AI models or APIs), but they should still produce consistent results to ensure fairness.

---

### In this tutorial, we will build a simple **Trust Score dApp** step-by-step.

---

## 🧑‍💻 Step 1: Create a Contract in GenLayer Studio

Open GenLayer Studio: [https://studio.genlayer.com](https://studio.genlayer.com) 
create a new contract file.

Paste the following code:

```python
# v0.2.16
# { "Depends": "py-genlayer:latest" }

from genlayer import *

class TrustScore(gl.Contract):

    # Storage (GenLayer does not support dict directly)
    scores: str

    def __init__(self):
        self.scores = "{}"

    @gl.public.write
    def set_score(self, token: str, score: u256) -> None:
        import json
        data = json.loads(self.scores)
        data[token.upper()] = int(score)
        self.scores = json.dumps(data)

    @gl.public.view
    def get_score(self, token: str) -> u256:
        import json
        data = json.loads(self.scores)
        return data.get(token.upper(), 0)
```

### Contract Code
<img width="905" height="560" alt="contract" src="https://github.com/user-attachments/assets/4e66a30f-9249-4aee-adcf-5e8e1dbe844d" />


### Deployment

---

## 🚀 Step 2: Deploy the Contract

1. Select execution mode: **Leader Only (Fast / No Validation)**
2. Click **Run ▶️**
3. Click **Deploy Contract**

After deployment, your contract will be live.

---

<img width="1035" height="469" alt="run   debug" src="https://github.com/user-attachments/assets/92072c63-f74e-4073-a1f8-d8570ae7a4b8" />
<img width="1116" height="473" alt="deploy" src="https://github.com/user-attachments/assets/6413715c-dc22-4ab6-950a-9ef2d6f60a69" />



## ⚠️ Important Note

GenLayer currently does not support native dictionary (`dict`) storage.  
We use a **JSON string workaround** to store key-value data.

---

## 🧪 Step 3: Test the Contract

### 🔹 Write Data

Call `set_score` with:

- token: `btc`
- score: `85`

Click **Send Transaction** and wait until it shows **FINALIZED**

---

### Setting Score
<img width="1345" height="585" alt="set score" src="https://github.com/user-attachments/assets/75d9404d-e170-4802-9786-df3597d3d4c7" />

---

### 🔹 Read Data

Call `get_score` with:

- token: `BTC`

Click **Call Contract**

---

## 🎯 Expected Output

```
85
```

### Output Result
<img width="1348" height="586" alt="result" src="https://github.com/user-attachments/assets/a7d377d4-90f7-4ef2-98ec-62bd3da86f15" />

This confirms that your contract is working correctly.

---

## 🌐 Frontend Interaction (genlayer-js)

In a real-world application, users do not interact directly with the contract through the Studio.

Instead, a frontend (website or app) communicates with the contract using **genlayer-js**.

Basic flow:

1. User enters a token (e.g., BTC)
2. Frontend sends request to contract
3. Contract returns trust score
4. UI displays the result

Example (conceptual):

```javascript
const score = await contract.get_score("BTC");
console.log(score);
```
---

## 🏁 Conclusion

In this tutorial, we built a simple Trust Score dApp using GenLayer.

This demonstrates how Intelligent Contracts can:
- Store data  
- Process user input  
- Return results on-chain  

---

## 🔮 Next Steps

- Add AI to automatically generate trust scores  
- Connect real-time crypto data APIs  
- Build a frontend dashboard  
---
