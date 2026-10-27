# Representation of a Real-World Problem as a Markov Decision Process

## Aim

To identify a real-world sequential decision-making problem and represent it formally as a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, reward function, and Python implementation.

---

## Problem Statement

### Problem Description

An automatic vending machine allows customers to purchase products by inserting money and selecting their desired items. The machine must process customer requests and dispense the selected product after receiving the required payment.

The vending machine can be represented as a Markov Decision Process (MDP), where the operating conditions of the machine represent states, customer transaction operations represent actions, transition probabilities describe the possible changes between states, and rewards represent the success or failure of a transaction.

The objective is to complete transactions successfully by ensuring that payment is received before the product is dispensed.

---

## MDP Components

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of states |
| $A$ | Set of actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

For this problem, the discount factor is:

$$
\gamma = 0.9
$$

---

## State Space

The state space represents the possible operating conditions of the vending machine.

```text
S = {
    S0: Waiting for Customer,
    S1: Payment Received,
    S2: Product Dispensed
}
```

**State Descriptions:**

- **S0 – Waiting for Customer:** The vending machine is ready to accept a new transaction.
- **S1 – Payment Received:** The customer has inserted the required payment.
- **S2 – Product Dispensed:** The selected product has been successfully dispensed.

For this simplified model, the product-dispensed state is treated as a terminal state for the current transaction.

---

## Sample State

```text
Current State: S1
Description: Payment Received
```

For example, a customer inserts the required amount into the vending machine. The machine enters the payment-received state and waits for the customer to select a product.

---

## Action Space

The action space represents the operations available during a vending machine transaction.

```text
A = {
    A0: Insert Payment,
    A1: Select Product,
    A2: Dispense Product
}
```

**Action Descriptions:**

- **A0 – Insert Payment:** The customer inserts money into the vending machine.
- **A1 – Select Product:** The customer selects the desired product.
- **A2 – Dispense Product:** The machine releases the selected product after verifying the payment and selection.

These actions represent the simplified transaction operations available in the model.

---

## Sample Action

```text
Current State: S1
Selected Action: A1
Description: Select Product
```

When the vending machine has received the required payment, the customer selects a product. If the selection is valid and the product is available, the machine proceeds toward dispensing the product.

---

## Transition Probability

Transition probability describes the probability of moving from one state to another after an action is performed.

The general form is:

$$
P(s' \mid s,a)
$$

Where:

- $s$ represents the current state.
- $a$ represents the selected action.
- $s'$ represents the next state.

The following hypothetical transition probabilities are used in this example.

| Current State | Action | Next State | Probability |
|---|---|---|---:|
| S0 | A0 | S1 | 0.9 |
| S0 | A0 | S0 | 0.1 |
| S1 | A1 | S2 | 0.9 |
| S1 | A1 | S1 | 0.1 |
| S2 | A2 | S2 | 1.0 |

**Explanation:**

Suppose the vending machine is waiting for a customer (S0), and the customer inserts payment (A0).

$$
P(S1 \mid S0,A0) = 0.9
$$

This means there is a 90% probability that the machine successfully registers the payment and moves to the payment-received state.

There is a 10% probability that the payment is not registered and the machine remains in the waiting state.

Similarly, after the customer selects a product in state S1, there is a 90% probability of successfully dispensing the product and a 10% probability of remaining in the payment-received state.

**Note:** These probabilities are hypothetical values used for educational purposes.

---

## Reward Function

The reward function defines the feedback received by the agent after performing an action.

The general form is:

$$
R(s,a,s')
$$

The following reward values are used:

| Current State | Action | Next State | Reward |
|---|---|---|---:|
| S0 | A0 | S1 | +5 |
| S0 | A0 | S0 | -1 |
| S1 | A1 | S2 | +10 |
| S1 | A1 | S1 | -2 |
| S2 | A2 | S2 | +5 |

**Explanation:**

- A reward of **+5** is assigned when the payment is successfully received.
- A reward of **-1** is assigned when the payment is not registered.
- A reward of **+10** is assigned when the selected product is successfully dispensed.
- A reward of **-2** is assigned when the product is not dispensed after selection.
- A reward of **+5** is assigned for the terminal dispensing action in this simplified model.

The objective is to maximize the cumulative reward by completing vending machine transactions successfully.

---

## Graphical Representation

The following diagram represents the state transitions of the automatic vending machine.

```text
+---------------------------+
|                           |
| S0: Waiting for Customer  |
|                           |
+---------------------------+
              |
              | A0: Insert Payment
              | Probability: 0.9
              | Reward: +5
              v
+---------------------------+
|                           |
| S1: Payment Received      |
|                           |
+---------------------------+
              |
              | A1: Select Product
              | Probability: 0.9
              | Reward: +10
              v
+---------------------------+
|                           |
| S2: Product Dispensed     |
|                           |
+---------------------------+
```

**Graph Explanation:**

1. The nodes represent the three states of the vending machine.
2. The arrows represent actions that cause state transitions.
3. The probabilities indicate the likelihood of successful transitions.
4. The rewards indicate the feedback received after each transition.
5. The product-dispensed state represents the completion of the transaction.

The diagram shows the main successful path. The Python implementation also includes transitions where the machine remains in its current state.

---

## Python Representation

The following Python program represents the vending machine MDP using Python dictionaries.

```python
# MDP Representation using Python
# Automatic Vending Machine

print("Name: Mario Viofer J")
print("Register Number: 212223100032")

# Define states
states = {
    "S0": "Waiting for Customer",
    "S1": "Payment Received",
    "S2": "Product Dispensed"
}

# Define actions
actions = {
    "A0": "Insert Payment",
    "A1": "Select Product",
    "A2": "Dispense Product"
}

# Define transition probabilities
transitions = {
    "S0": {
        "A0": {
            "S1": 0.9,
            "S0": 0.1
        }
    },
    "S1": {
        "A1": {
            "S2": 0.9,
            "S1": 0.1
        }
    },
    "S2": {
        "A2": {
            "S2": 1.0
        }
    }
}

# Define reward function
rewards = {
    "S0": {
        "A0": {
            "S1": 5,
            "S0": -1
        }
    },
    "S1": {
        "A1": {
            "S2": 10,
            "S1": -2
        }
    },
    "S2": {
        "A2": {
            "S2": 5
        }
    }
}

# Define discount factor
gamma = 0.9

# Display state space
print("\nSTATE SPACE:")
for state, description in states.items():
    print(state, ":", description)

# Display action space
print("\nACTION SPACE:")
for action, description in actions.items():
    print(action, ":", description)

# Display transition probabilities
print("\nTRANSITION PROBABILITIES:")
for state, action_data in transitions.items():
    for action, next_states in action_data.items():
        print(state, "->", action, ":", next_states)

# Display reward function
print("\nREWARD FUNCTION:")
for state, action_data in rewards.items():
    for action, next_states in action_data.items():
        print(state, "->", action, ":", next_states)

# Display discount factor
print("\nDiscount Factor:", gamma)

# Sample decision
current_state = "S0"
selected_action = "A0"

print("\nSAMPLE DECISION:")
print("Current State:", states[current_state])
print("Selected Action:", actions[selected_action])

print("\nPossible Outcomes:")

for next_state, probability in transitions[
    current_state
][selected_action].items():

    reward = rewards[
        current_state
    ][selected_action][next_state]

    print(
        "Next State:", states[next_state],
        "| Probability:", probability,
        "| Reward:", reward
    )
```

---

## Output

The Python program produces output similar to the following:

```text
Name: Mario Viofer J
Register Number: 212223100032

STATE SPACE:
S0 : Waiting for Customer
S1 : Payment Received
S2 : Product Dispensed

ACTION SPACE:
A0 : Insert Payment
A1 : Select Product
A2 : Dispense Product

TRANSITION PROBABILITIES:
S0 -> A0 : {'S1': 0.9, 'S0': 0.1}
S1 -> A1 : {'S2': 0.9, 'S1': 0.1}
S2 -> A2 : {'S2': 1.0}

REWARD FUNCTION:
S0 -> A0 : {'S1': 5, 'S0': -1}
S1 -> A1 : {'S2': 10, 'S1': -2}
S2 -> A2 : {'S2': 5}

Discount Factor: 0.9

SAMPLE DECISION:
Current State: Waiting for Customer
Selected Action: Insert Payment

Possible Outcomes:
Next State: Payment Received | Probability: 0.9 | Reward: 5
Next State: Waiting for Customer | Probability: 0.1 | Reward: -1
```

---

## Result

The automatic vending machine problem was successfully represented as a Markov Decision Process. The state space, action space, transition probabilities, reward function, and discount factor were defined using Python dictionaries.

The Python implementation demonstrates how the vending machine can model transaction progress and possible outcomes based on customer actions. This MDP provides a basic representation of sequential decision-making in automated vending systems.

---
