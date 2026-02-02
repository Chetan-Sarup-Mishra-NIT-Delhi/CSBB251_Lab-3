# 8x1 Multiplexer and 8x3 Encoder Circuit Design Using Logisim

## Aim
To design, simulate, and verify the working of 8x1 Multiplexer and 8x3 Priority Encoder circuits using Logisim software and validate their operation through truth tables.

## Materials/Resources Needed

### Software
- **Logisim** (digital logic circuit simulator)
- Compatible with Windows, macOS, and Linux operating systems

### Circuit Components (in Logisim)
- AND gates
- OR gates
- NOT gates
- Input pins
- Output pins
- Wires/connectors
- Text labels (for documentation)
- LEDs (for output visualization)

## Theory

### 8x1 Multiplexer (MUX)
A multiplexer is a combinational circuit that selects one of several input signals and routes it to a single output line. An 8x1 multiplexer has:

- **8 Data Inputs**: D0, D1, D2, D3, D4, D5, D6, D7
- **3 Select Lines**: S0, S1, S2 (since 2³ = 8)
- **1 Output**: Y

**Working Principle:**
The three select lines generate a 3-bit binary code (000 to 111) that determines which of the 8 input lines is routed to the output. The select lines act as an address to choose the specific input.

**Key Equation:**
```
Y = D0·S2'·S1'·S0' + D1·S2'·S1'·S0 + D2·S2'·S1·S0' + D3·S2'·S1·S0 
    + D4·S2·S1'·S0' + D5·S2·S1'·S0 + D6·S2·S1·S0' + D7·S2·S1·S0
```

**Circuit Implementation:**
- 3 NOT gates (for select line complements)
- 8 AND gates (4-input each: 3 select inputs + 1 data input)
- 1 OR gate (8-input)

**Truth Table:**

| S2 | S1 | S0 | Output Y |
|----|----|----|----------|
| 0  | 0  | 0  | D0       |
| 0  | 0  | 1  | D1       |
| 0  | 1  | 0  | D2       |
| 0  | 1  | 1  | D3       |
| 1  | 0  | 0  | D4       |
| 1  | 0  | 1  | D5       |
| 1  | 1  | 0  | D6       |
| 1  | 1  | 1  | D7       |

### 8x3 Priority Encoder
An encoder is a combinational circuit that performs the inverse operation of a decoder. An 8x3 priority encoder (also called Octal-to-Binary encoder) has:

- **8 Input Lines**: D0, D1, D2, D3, D4, D5, D6, D7 (or I0 to I7)
- **3 Output Lines**: Q0, Q1, Q2 (binary code)
- **Priority Feature**: When multiple inputs are high simultaneously, the input with highest priority is encoded

**Working Principle:**
The encoder converts an 8-bit input (octal) to a 3-bit binary output. In a priority encoder, if multiple inputs are active, the highest priority input (typically the highest numbered input) is encoded, ignoring all others.

**Priority Order:** D7 > D6 > D5 > D4 > D3 > D2 > D1 > D0

**Key Equations:**
```
Q0 = D1 + D3 + D5 + D7
Q1 = D2 + D3 + D6 + D7
Q2 = D4 + D5 + D6 + D7
```

**Truth Table (Priority Encoder):**

| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 | Q2 | Q1 | Q0 |
|----|----|----|----|----|----|----|----|----|----|----|
| 0  | 0  | 0  | 0  | 0  | 0  | 0  | 1  | 0  | 0  | 0  |
| 0  | 0  | 0  | 0  | 0  | 0  | 1  | X  | 0  | 0  | 1  |
| 0  | 0  | 0  | 0  | 0  | 1  | X  | X  | 0  | 1  | 0  |
| 0  | 0  | 0  | 0  | 1  | X  | X  | X  | 0  | 1  | 1  |
| 0  | 0  | 0  | 1  | X  | X  | X  | X  | 1  | 0  | 0  |
| 0  | 0  | 1  | X  | X  | X  | X  | X  | 1  | 0  | 1  |
| 0  | 1  | X  | X  | X  | X  | X  | X  | 1  | 1  | 0  |
| 1  | X  | X  | X  | X  | X  | X  | X  | 1  | 1  | 1  |

*Note: X = Don't care (can be 0 or 1)*

## Procedure

### Part A: 8x1 Multiplexer Circuit

1. **Launch Logisim** and create a new project

2. **Add Input Pins:**
   - Place 8 input pins and label them as D0 through D7 (data inputs)
   - Place 3 input pins and label them as S0, S1, S2 (select lines)

3. **Add NOT Gates:**
   - Place 3 NOT gates
   - Connect S0, S1, and S2 to NOT gates to generate S0', S1', and S2'

4. **Add AND Gates:**
   - Place 8 AND gates (configure each to have 4 inputs)
   - Connect each AND gate with appropriate combination of select lines and one data input:
     - AND1: D0, S2', S1', S0'
     - AND2: D1, S2', S1', S0
     - AND3: D2, S2', S1, S0'
     - AND4: D3, S2', S1, S0
     - AND5: D4, S2, S1', S0'
     - AND6: D5, S2, S1', S0
     - AND7: D6, S2, S1, S0'
     - AND8: D7, S2, S1, S0

5. **Add OR Gate:**
   - Place one OR gate with 8 inputs
   - Connect all AND gate outputs to the OR gate

6. **Add Output:**
   - Place one output pin or LED labeled Y
   - Connect the OR gate output to this pin

7. **Add Labels:** Use text tool to label all components clearly

8. **Test the Circuit:**
   - Use the "Poke" tool to set different combinations of select lines
   - For each select combination (000 to 111), verify that the corresponding data input appears at output Y
   - Test with various data input patterns to ensure correct selection

### Part B: 8x3 Priority Encoder Circuit

1. **Create New Circuit** in the same Logisim project

2. **Add Input Pins:**
   - Place 8 input pins and label them as D0 through D7
   - These represent the octal input lines

3. **Add OR Gates:**
   - Place 3 OR gates (each with 4 inputs)
   - Configure according to the Boolean equations

4. **Connect Q0 Output:**
   - Connect D1, D3, D5, and D7 to the first OR gate
   - This produces Q0 (LSB of binary output)

5. **Connect Q1 Output:**
   - Connect D2, D3, D6, and D7 to the second OR gate
   - This produces Q1 (middle bit of binary output)

6. **Connect Q2 Output:**
   - Connect D4, D5, D6, and D7 to the third OR gate
   - This produces Q2 (MSB of binary output)

7. **Add Output Pins:**
   - Place 3 output pins or LEDs labeled Q0, Q1, Q2
   - Connect OR gate outputs to respective pins

8. **Add Labels:** Label all components for clarity

9. **Test the Circuit:**
   - Test with single input active at a time (D0=1, others=0, then D1=1, others=0, etc.)
   - Verify binary output matches expected encoding
   - Test priority by activating multiple inputs simultaneously
   - Verify highest priority input determines the output
   - Check all 8 input combinations systematically

## Results

### 8x1 Multiplexer Verification
The 8x1 Multiplexer circuit successfully routed the selected input to the output based on the select line combination. Testing confirmed:
- For select lines 000 (binary 0), data input D0 appeared at output Y
- For select lines 001 (binary 1), data input D1 appeared at output Y
- Pattern continued correctly through all 8 combinations (000 to 111)
- Each select combination correctly enabled only one data path
- Output changed immediately when select lines were modified

The multiplexer demonstrated proper data selection functionality with all 8 inputs accessible through the 3 select lines.

### 8x3 Priority Encoder Verification
The 8x3 Priority Encoder circuit successfully converted octal inputs to binary outputs with proper priority handling. Testing validated:
- Single active input produced correct 3-bit binary encoding
  - D0=1 produced output 000
  - D1=1 produced output 001
  - D7=1 produced output 111
- Multiple simultaneous inputs correctly prioritized highest numbered input
  - D7=1, D3=1, D1=1 produced output 111 (D7 has highest priority)
  - D5=1, D2=1 produced output 101 (D5 has highest priority)
- All three output bits (Q0, Q1, Q2) functioned correctly according to Boolean equations
- Priority logic successfully ignored lower priority inputs when higher ones were active

The encoder outputs matched the theoretical truth table for all test cases, confirming correct implementation.

## Key Differences

| Feature | 8x1 Multiplexer | 8x3 Priority Encoder |
|---------|----------------|----------------------|
| Function | Data selection | Data encoding |
| Inputs | 8 data + 3 select | 8 data inputs |
| Outputs | 1 output | 3 outputs |
| Operation | Routes selected input to output | Converts octal to binary |
| Multiple Active Inputs | Controlled by select lines | Highest priority encoded |
| Gates Required | 3 NOT + 8 AND + 1 OR | 3 OR (4-input each) |
| Application | Data routing, signal selection | Data compression, interrupt handling |

## Applications

### Multiplexer Applications:
- Data routing in communication systems
- Digital signal switching
- Arithmetic logic unit (ALU) input selection
- Memory address selection
- Data bus implementation in microprocessors

### Encoder Applications:
- Priority interrupt systems in microprocessors
- Data compression circuits
- Keyboard encoding
- Position encoding in control systems
- Octal to binary conversion in digital systems

## Conclusion
Both 8x1 Multiplexer and 8x3 Priority Encoder circuits were successfully designed and verified using Logisim. The multiplexer demonstrated accurate data selection based on control signals, while the priority encoder correctly converted octal inputs to binary outputs with proper priority handling. These circuits are fundamental building blocks in digital systems for data routing and encoding operations.
