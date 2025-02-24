# **Huffman-Inspired Wormhole Naming System for EVE Online**

## **Overview**

- **4-character max callable name** for ease of use in comms.  
- **Encodes full jump path** from origin (Terra).  
- **Indicates entry hole at each step** to navigate without leaving EVE's window.  
- **Scales to deep chains (7+ jumps)** while maintaining readability.  
- **Frequent paths get shorter codes**, making navigation faster.  

---

## **Naming Format**
**`[Jump Path]-[Destination] [Sig] [EoL]`**

### **1. Jump Path Encoding (≤3 Characters)**  
- **A, B, C, etc.** → Order of wormhole entry from each system.  
- **1st hole = A, 2nd hole = B, 3rd hole = C, etc.**
- **At 5+ jumps, compressed shorthand starts (D, E, F... instead of repeating letters).**

### **2. Destination Class (1 Character)**  
- **5 = C5**
- **3 = C3**
- **2 = C2**
- **H = Highsec**
- **L = Lowsec**
- **N = Nullsec**
- **T = Thera**

### **3. Optional Sig & EoL (Not in Callable Part)**  
- **Sig ID** → E.g., ABC-123
- **(EoL)** → Marks End of Life holes

---

## **Example Chains**

### **Shallow Chain (≤4 Jumps)**
```
T (Terra)
├── A5-5  ABC-123  (First C5 from T, enter via A)
│   ├── AA-5  DEF-456  (First C5 from A5, enter via A)
│   │   ├── AAB-2  GHI-789  (First C2 from AA, enter via B)
│   ├── AB-5  JKL-987  (Second C5 from A5, enter via B)
│   │   ├── ABB-3  MNO-654  (First C3 from AB, enter via B)
│   │   ├── ABC-3  PQR-321  (Second C3 from AB, enter via C)
│   │   │   ├── ABCC-L  STU-246  (First Lowsec from ABC, enter via C, EoL)
```

### **Deep Chain (7+ Jumps)**
```
T (Terra)
├── A5-5  (First C5 from T, enter via A)
│   ├── AA-5  (First C5 from A5, enter via A)
│   │   ├── AAB-2  (First C2 from AA, enter via B)
│   │   │   ├── AABC-3  (First C3 from AAB, enter via C)
│   │   │   │   ├── AABCD-5  (First C5 from AABC, enter via D)
│   │   │   │   │   ├── AABCDE-2  (First C2 from AABCD, enter via E)
│   │   │   │   │   │   ├── AABCDF-L  (First Lowsec from AABCDE, enter via F)
```

---

## **How to Read and Navigate**
| Name | Path from Terra | Next Jump | Destination |
|------|---------------|-----------|-------------|
| A5-5  | A | Take A | C5 |
| AA-5  | A → A | Take A | C5 |
| AAB-2 | A → A → B | Take B | C2 |
| AABC-3 | A → A → B → C | Take C | C3 |
| AABCD-5 | A → A → B → C → D | Take D | C5 |
| AABCDE-2 | A → A → B → C → D → E | Take E | C2 |
| AABCDF-L | A → A → B → C → D → E → F | Take F | Lowsec |

At **10+ jumps**, the shorthand continues:
- **7th jump → G**, **8th jump → H**, **9th jump → I**, etc.
- Example: `"AABCGT-3"` (10th jump = `T`), ensuring readability.

---
