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
     Handles CAN FD communication, RMII/Ethernet control, and all sensor/monitoring logic for the board.

- **Criteria**:
    - Must support CAN FD natively
    - Must support Ethernet (RMII) via internal MAC
    - Enough GPIO/ADC channels for RMII, CAN, and all monitoring functions (power supply health, temp, valve/E-stop sensing)

- **Chosen**: STM32H723VE, also mass used by avionics team for the development of all PCB boards within the rocket

## CAN Transceiver
- **Why is it needed?**:
    Converts the MCU's logic-level CAN signals into the differential CANH/CANL signals needed for the actual bus.
  
- **Criteria**:
    - Must support CAN FD
    - 3.3V compatible with MCU logic
  
- **Chosen**: ATA6563

## Ethernet PHY
- **Why is it needed?**:
    Handles the physical-layer Ethernet signaling (RMII interface to MCU, magnetics/RJ45 on the other side) so the board can bridge CAN to Ethernet.
  
- **Criteria**:
    - RMII interface (uses MCU's internal MAC instead of SPI, since STM32H723VE supports it internally)
    - 3.3V compatible
 
- **Chosen**: LAN8720A

## Ethernet connector
- **Why is it needed?**:
    Physical RJ45 jack + integrated magnetics needed to actually connect an Ethernet cable to the LAN8720A.
- **Criteria**:
    - Auto-MDIX support
    - Exposed TX/RX center taps (required by LAN8720A's application circuit)
    - 1:1 turns ratio (correct for 10/100 Ethernet)
    - Shielded
    - Through-hole, right-angle
- **Chosen**: RJMG1S8008101BR (Amphenol)


## CAN connector
- **Why is it needed?**:
    Physical connector needed to bring the CAN bus wiring from the rocket's internal CAN network onto the board.
- **Criteria**:
     tbd


## AC-DC Conversion Module
- **Why is it needed?**:
    The board is fed 120VAC directly from the generator (independent from the DC supplies it monitors), so it needs its own AC-to-3.3V conversion stage.
 
- **Criteria**:
    - Input range covering 120VAC with margin (generator power can fluctuate more than clean utility power)
    - 3.3V output with real margin above worst-case board current draw
    - Isolated, safety certified
    - In stock, reasonable lead time

- **Chosen**: MPM-05-3.3 (Mean Well) —> 1.25A rated output at 3.3V, giving comfortable, proportionate margin over the board's worst-case current draw once all monitoring functions are included. Universal 80-264VAC input covers the generator source with margin.

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

## Fuse for AC to DC conversion module
- **Why is it needed?**
    It protects board wiring/connector from  excessive current flow.

- **Note**:
    Scherz, Paul, and Simon Monk. Practical Electronics for Inventors. — fuse sizing rule: rated current should be ~50% larger than expected nominal current; for 120VAC applications, fuse placed in the hot line, positioned before the protected device.

- **Fuse size required:**
    Since the MPM-05-3.3 has a nominal current of 0.2A, I will aim to find a slow-blow fuse of about 0.4A. A slow-blow fuse type is chosen due to the component's cold start at 25A.

- **Other criteria**
    - Must exceed 120VAC with margin
    - Fuse holder and replaceable fuse cartridge will be chosen due to simplicity of replacement compared to soldering and resoldering it every time it blows --> THUS, both of those components must match sizes

- **Fuse holder chosen** --> 696108003002 from Wurth Elektronik, $0.64 per unit, 32,090 in stock, 20A current rating, 250VAC working voltage
- **Fuse cartridge chosen** --> 
  
  

 
