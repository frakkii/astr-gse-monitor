# Methodology
- Check for electrical requirements (voltage, current, signal type)
- Ensure there's some margin beyond worst-case electrical demand
- Ensure mounting type is board compatible (SMD or through-hole, since I'm hand soldering)
- Ensure proper safety certifications are met for critical components (e.g. anything
AC power adjacent)
- Ensure component is in stock and the lead time is reasonable, otherwise check
different distributors

---

# Components Needed

## MCU
- **Why is it needed?**:
 
- **Criteria**:


## CAN Transceiver
- **Why is it needed?**:
 
- **Criteria**:


## Ethernet PHY
- **Why is it needed?**:
 
- **Criteria**:


## Ethernet connector
- **Why is it needed?**:
 
- **Criteria**:


## CAN connector
- **Why is it needed?**:
 
- **Criteria**:


## AC-DC Conversion Module
- **Why is it needed?**:
 
- **Criteria**:


## AC-DC Terminal Block
- **Why is it needed?**:
    Must allow the board to connect to generator 120VAC power
    (line and neutral only, since AC-DC conversion module does not need GND)
  
- **Criteria**:
   - Must have line + neutral ports only (2 positions)
   - Must exceed 120VAC voltage rating
   - Wire gauge compatibility: 18 AWG according to AC-DC module it's paired with
   - Mounting type SMD or through hole
   - Has safety certification: UL/CE recognized
   - Screw terminal type

- **Decision Matrix**:

| Criteria | TB0010-500-02GR | 2440 Pololu |
|---|---|---|
| Meets core spec (elec. requirement)? | yes | yes |
| Margin (more than 120VAC) | yes, comfortably | yes, comfortably |
| Fits mechanically (mount/size)? | through hole | through hole |
| Safety/certification adequate? | yes, UL 1059 certified, IEC 60947-7-4 compliant, RoHS compliant |  UL and IEC rating, but not formally certified for those except RoHS|
| In stock / lead time | 4,927 in stock | 813 in stock |
| Cost (CAD) | $0.55/unit | $1.89/ 4 units|
| **Verdict** | **Selected** because it's formally certified, better stock, comparable/lower cost | Rejected because it lacks formal safety certification |

 
