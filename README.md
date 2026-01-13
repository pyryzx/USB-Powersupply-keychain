# Multi-Rail Power Supply Keychain (USB-C PD)

A compact, keychain-sized **USB-C powered** power supply that has four power rails:

- **+1.8 V** (up to 1.5 A)
- **+3.3 V** (up to 1.5 A)
- **+5 V** (up to 1.5 A)
- **+12 V (VBUS passthrough)** from the USB-C PD source

Clip this onto your keys, plug it into a USB-C PD charger, and you’ve got the most common lab voltages available from a single tiny board.

---

## Features

- USB-C input with **USB Power Delivery negotiation** (requests 12 V from a capable source)
- Multi-rail DC/DC conversion to generate **1.8 V, 3.3 V, and 5 V**
- **12 V VBUS rail is also available** as an output (source-dependent)
- Compact PCB with **keychain hole**


---

## Electrical Specs (Target)

> Real limits depend heavily on the USB-C PD source, total load, copper/thermal conditions, and airflow.

### Outputs

| Rail | Nominal Voltage | Max Current (design target) | Notes |
|---|---:|---:|---|
| +1.8V | 1.8 V | 1.5 A | Buck regulated |
| +3.3V | 3.3 V | 1.5 A | Buck regulated |
| +5V | 5.0 V | 1.5 A | Buck regulated |
| +12V | 12 V | Source-dependent | Direct from negotiated VBUS |

### Power Budget 

beware that even if each rail is “rated” for 1.5 A it is source dependent. 

Example (typical PD): **12 V × 3 A = 36 W available**  
Loads:
- 5 V @ 1.5 A ≈ 7.5 W  
- 3.3 V @ 1.5 A ≈ 5.0 W  
- 1.8 V @ 1.5 A ≈ 2.7 W  
Total ≈ 15.2 W (plus conversion losses)

Beware that current design is not yet optimized to be run at full capacity all the time. Heat generated is still a problem when run at max load.


## Output Connector / Pinout

### J3

Pin order (as labeled on schematic / silkscreen intent):

1. **+1.8V**
2. **+3.3V**
3. **+5V**
4. **+12V**
5. **GND**

---

## How It Works 

1. **USB-C input** comes in on the Type-C receptacle.
2. A **USB-C PD sink controller (CYPD3177-24LQ)** negotiates with the charger to request **12 V** output.
3. Once VBUS is valid, a small input switching/protection stage connects the negotiated rail to the board.
4. A **multi-output buck regulator (TPS65581PWP)** generates:
   - **1.8 V** (via L1)
   - **3.3 V** (via L2)
   - **5 V** (via L3)
5. The negotiated **+12 V VBUS** rail is also routed to the output header.

See: `schematic_keychain V2.pdf`. :contentReference[oaicite:1]{index=1}

---

## What This Is For

- Powering sensors, dev boards, and small embedded prototypes
- Quick “bench supply” substitute for field work
- Testing boards that need 1.8 V / 3.3 V / 5 V without dragging a lab PSU around

---

## What This Is NOT For

- Not a charger / power bank
- Not safety-certified equipment
- Not intended for life-critical, medical, automotive, or mains-related applications
- Not meant for inductive loads / motors directly 

---
