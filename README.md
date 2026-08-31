Element Dot Product — SystemVerilog RTL
Question Description

Design a SystemVerilog module to calculate the dot product of two 3-element vectors. Inputs arrive through din in the order a1, a2, a3, b1, b2, b3. After the sixth input, run is asserted and dout produces a1*b1 + a2*b2 + a3*b3.

Logic Used

The design uses a 3-bit counter to track the six incoming values.

0 → a1
1 → a2
2 → a3
3 → b1
4 → b2
5 → b3

Six 8-bit registers store the inputs. if conditions select the register based on the counter.

On the sixth input:

run  <= 1;
dout <= a1*b1 + a2*b2 + a3*din;

din is used directly for b3 since b3 is registered on the same clock edge.

The counter then returns to 0 for the next set of inputs.

Synthesis Comparison
Metric	My RTL	Reference
Area	9013.6 µm²	9013.64 µm²
Max Frequency	177 MHz	135 MHz
Critical Path	5.64 ns	7.410 ns
Wires	94	993
Cells	~2100	2349

The area is practically identical, while my implementation achieves approximately 31% higher maximum frequency and a shorter critical path.

Alternative Approach

A shorter RTL implementation can use an array:

logic [7:0] mem [0:5];

with the counter directly selecting mem[count]. The three products can also be stored separately before adding them.

This reduces RTL code length, but shorter code does not necessarily mean lower synthesized area or better timing.
