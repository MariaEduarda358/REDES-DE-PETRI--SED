# 🚚 AGV Production System using Colored Petri Nets (CPN Tools)

## 📖 Overview

This project models an automated manufacturing system using **Colored Petri Nets (CPN)** in **CPN Tools 4.0.1**.

The modeled system consists of two production machines, two Automated Guided Vehicles (AGVs), an intermediate buffer, and a shared critical region. The model was developed to study synchronization, mutual exclusion, resource sharing, and discrete-event behavior in manufacturing systems.

The implementation follows the concepts of Colored Petri Nets, where system behavior is represented through places, transitions, tokens, and hierarchical pages.

---

## 🎯 Objectives

The main objectives of this project are:

- Model an automated production line using Colored Petri Nets.
- Synchronize production and transportation processes.
- Prevent resource conflicts through mutual exclusion.
- Represent buffer capacity constraints.
- Simulate the interaction between machines and AGVs.
- Explore hierarchical modeling in CPN Tools.

---

# 🏭 System Description

The production line is composed of:

- **Machine 1 (M1)** – Produces a workpiece.
- **AGV1** – Collects the finished workpiece from M1 and transports it to the buffer.
- **Buffer** – Temporary storage with limited capacity.
- **AGV2** – Collects the workpiece from the buffer and delivers it to Machine 2.
- **Machine 2 (M2)** – Performs the second manufacturing process.
- **Critical Region (RC)** – Shared transportation area that guarantees mutual exclusion between AGVs.

---

# 🏗️ Project Architecture

```
           +--------+
           |   M1   |
           +--------+
                |
         Piece Ready
                |
                ▼
           +--------+
           | AGV 1  |
           +--------+
                |
                ▼
      Critical Region
                |
                ▼
           +--------+
           | Buffer |
           +--------+
                |
                ▼
           +--------+
           | AGV 2  |
           +--------+
                |
                ▼
      Critical Region
                |
                ▼
           +--------+
           |   M2   |
           +--------+
```

---


# ⚙️ Petri Net Components

## Machine 1

Responsible for manufacturing a new workpiece.

Workflow:

```
Idle
 ↓
Start
 ↓
Processing
 ↓
Finish
 ↓
Piece_Ready
```

The machine remains idle until the AGV removes the produced workpiece.

---

## AGV1

Responsible for transporting parts from Machine 1 to the Buffer.

Workflow:

```
Free
 ↓
Move_to_M1
 ↓
At_M1
 ↓
Pick
 ↓
Loaded
 ↓
Enter_RC
 ↓
In_RC
 ↓
Move_to_Buffer
 ↓
At_Buffer
 ↓
Drop
 ↓
Free
```

---

## Buffer

Stores one workpiece before the second production stage.

Workflow:

```
Buffer_Empty
      ↓
   Receive
      ↓
 Buffer_Full
```

The stored workpiece remains in the buffer until AGV2 collects it.

---

## Critical Region

Controls access to the shared transportation corridor.

Workflow:

```
RC_Free
   ↓
Enter_RC
   ↓
RC_Busy
   ↓
Leave_RC
   ↓
RC_Free
```

Only one AGV may occupy the critical region at any given time.

---

## AGV2

Responsible for transporting workpieces from the Buffer to Machine 2.

Workflow:

```
Free
 ↓
Move_to_Buffer
 ↓
At_Buffer
 ↓
Pick
 ↓
Loaded
 ↓
Enter_RC
 ↓
In_RC
 ↓
Move_to_M2
 ↓
At_M2
 ↓
Drop
 ↓
Free
```

---

## Machine 2

Processes the workpiece delivered by AGV2.

Workflow:

```
Piece_Arrived
      ↓
Start
      ↓
Processing
      ↓
Finish
      ↓
Idle
```

---

# 🔄 Synchronization

The system uses shared places to synchronize different modules.

| Shared Resource | Purpose |
|-----------------|---------|
| Piece_Ready | Synchronizes M1 and AGV1 |
| Buffer_Full | Synchronizes Buffer and AGV2 |
| RC_Free | Grants permission to enter the Critical Region |
| RC_Busy | Indicates that the Critical Region is occupied |

---

# 🔒 Mutual Exclusion

The Critical Region ensures that only one AGV can access the shared corridor simultaneously.

This behavior is modeled using tokens:

- One token in **RC_Free** indicates that the region is available.
- Entering the region consumes the token.
- Leaving the region restores the token.

Therefore, concurrent access is naturally prevented by the Petri Net semantics.

---

# 📊 Features

- Hierarchical Colored Petri Net model
- Two-machine manufacturing line
- Two AGVs
- Shared buffer
- Mutual exclusion
- Token-based synchronization
- Modular architecture
- Event-driven simulation

---

# ▶️ Running the Simulation

Requirements:

- CPN Tools 4.0.1 (February 2015)

Steps:

1. Open the project in CPN Tools.
2. Initialize the marking.
3. Start the simulation.
4. Fire enabled transitions.
5. Observe the synchronization between modules.
6. Verify that:
   - M1 waits until the part is collected.
   - Buffer never exceeds its capacity.
   - Only one AGV occupies the critical region.
   - M2 processes received parts correctly.

---

# 🧪 Validation Scenarios

The following scenarios were used to validate the model:

- Normal production cycle
- Buffer occupation
- Critical region mutual exclusion
- AGV synchronization
- Continuous production
- Token conservation

---

# 🛠️ Technologies

- Colored Petri Nets
- CPN Tools 4.0.1
- Hierarchical Petri Nets
- Discrete Event Systems

---

# 📚 Concepts Applied

- Colored Petri Nets
- Hierarchical Modeling
- Resource Allocation
- Mutual Exclusion
- Manufacturing Systems
- AGV Scheduling
- Buffer Management
- Discrete Event Simulation

---

# 👨‍🎓 Academic Context

This project was developed as part of an academic study on **Discrete Event Systems** and **Colored Petri Nets**, with emphasis on modeling industrial production systems using hierarchical Petri Nets.

---

# 📄 License

This repository is intended for educational and academic purposes.
