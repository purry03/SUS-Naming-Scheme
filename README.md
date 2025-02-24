# **Huffman-Inspired Wormhole Naming System for EVE Online**

## **Overview**

- **Prevents clash with farm chains** using prefix
- **Encodes full jump path** from origin (Terra).  
- **Indicates entry hole at each step** to navigate without leaving EVE's window.  

---

## **Naming Format**
**`[Chain Prefix][Jump Path]-[Destination] [Sig] [EoL]`**

### **1. Chain Prefix (1 character)**  
(can be dropped for main chains like the one from terra but mandatory for farm and op-hole chains)  
- **A, B, C, etc.** → A unique prefix to the origin system from which the chain is being scanned
- **Can accomodate upto 26 separate chains**
- **Whenever two separate chains clash we know which bookmark belongs to which chain**

### **2. Jump Path Encoding (≤3 Characters)**  
- **A, B, C, etc.** → Order of wormhole entry from each system.  
- **1st hole = A, 2nd hole = B, 3rd hole = C, etc.**
- **At 5+ jumps, compressed shorthand starts (D, E, F... instead of repeating letters).**

### **3. Destination Class (1 Character)**  
- **5 = C5**
- **3 = C3**
- **2 = C2**
- **H = Highsec**
- **L = Lowsec**
- **N = Nullsec**
- **T = Thera**
- **P = Pochven**

### **4. Optional Sig & EoL (Not in Callable Part)**  
- **Sig ID** → E.g., ABC (omit the number)
- **(EoL) (REDUCED) (CRIT) (5JJ)** → Misc info about holes if needed

---

## **Example Chains**

```
T (Terra) [The prefix is optional for Terra]
├── TA5-5  ABC REDUCED  (First C5 from T, enter via A)
│   ├── TAA-5  DEF  (First C5 from A5, enter via A)
│   │   ├── TAAB-2  GHI EOL CRIT  (First C2 from AA, enter via B)
│   ├── TAB-5  JKL-987  (Second C5 from A5, enter via B)
│   │   ├── TABB-3  MNO  (First C3 from AB, enter via B)
│   │   ├── TABC-3  PQR  (Second C3 from AB, enter via C)
│   │   │   ├── TABCC-L  STU  (First Lowsec from ABC, enter via C, EoL)
```
```
X (OP Hole) [The prefix is now mandatory]
├── XA5-5  CHE  (First C5 from O, enter via A)
│   ├── XAA-5  YGC  (First C5 from A5, enter via A)
│   │   ├── XAAB-2  QHX  (First C2 from AA, enter via B)
│   │   │   ├── XAABC-3  QCH  (First C3 from AAB, enter via C)
│   │   │   │   ├── XAABCD-5  ODS  (First C5 from AABC, enter via D)
```

## **How to Read and Navigate**

Since there is no prefix, we know this is Terra's chain

| Name | Path from Terra | Next Jump | Destination |
|------|---------------|-----------|-------------|
| A5-5  | A | Take A | C5 |
| AA-5  | A → A | Take A | C5 |
| AAB-2 | A → A → B | Take B | C2 |
| AABC-3 | A → A → B → C | Take C | C3 |
| AABCD-5 | A → A → B → C → D | Take D | C5 |
| AABCDE-2 | A → A → B → C → D → E | Take E | C2 |
| AABCDF-L | A → A → B → C → D → E → F | Take F | Lowsec |

---
