# An Introduction to STA Essentials :

Static timing analysis (STA) is a technique used to calculate the upper bound on the delay of every path leading from primary inputs to primary outputs in digital circuits. STA is effective for characterizing the timing behaviour of digital circuits, pinpointing the critical path, and obtaining precise delay data. It helps in recognising and classifying certain groups of paths according to their start-points and end-points, which can be defined as a logical or physical path through a design that represents the flow of signal from a specific start-point and end-point. A straightforward circuit with two ideal flip-flops and two combinational blocks is depicted in Fig. 2. In this illustration, STA determines the earliest possible timing for clocking FF2 while ensuring that all flip-flops and registers are latching valid signals. Each combinational block delay is pre-characterized before STA, either in the form of an equation or a look-up table. It is used to explain the delay between each input and each output pin.

![](/images/theory/reg_to_reg.png)

- Fig. 2 Simple register-to-register path

In the illustration above (Fig. 2), to perform a simple STA to time the register-to-register path the following condition (eq. 1) needs to be met first : 

<i>[ Cell Delay of gates (G1,G2) + Interconnect Delays of wires (W1,W2,W3)] < Required_delay_on_the_path   (1)</i>

Timing Paths are an important aspect of STA that aids in recognising and classifying certain groups of paths according to their start-points and endpoints. A timing path can be defined as a logical or physical path through a design that represents the flow of signal from a specific start-point and end-point. In general, start-points are primary inputs and clock pins of a register (flip-flop, latch, memory) and end-points are primary outputs and data pins of a register. The above example mentioned (Fig. 2), had a register-to-register path. There are essentially four types of timing paths in a gate-level design, namely input-to-register, register-to-register, register-to-output, input-to-output paths. The visual representation of these paths can be observed in the illustration (Fig. 3).

![](/images/theory/timing_path.png)

- Fig. 3 Timing paths in a design

Timing constraints are essential for ensuring that all possible paths in a design are constrained for timing. These constraints originate from system specifications and design implementation and help with performance optimization, power efficiency improvement, design closure, and rigorous design verification processes. Some essential constraints include setup time, hold time, Clock-to-Q delay, pulse width and period.

Timing constraints are traditionally postulated in the form of a look-up table (LUT), which can vary in complexity depending on the abstraction of values and the procedure through which they are captured. In the given example of a LUT( fig. 4 ), the values present in the table indicate the cell delays for different combinations of index 1 and index 2 parameters. The various values of these indices are defined separately in the liberty or .lib file.

![](/images/theory/lut.png)

The STA tool searches for the value's position in the index 1 array and index 2 array, respectively, to determine the row and column, respectively. Finding the cell delay for a certain input transition time and output capacitance load is made easier by using the ordered pair of row and column provided by the indices. The units of all the values associated are predefined in the liberty file at the beginning. LUTs are a great way to calculate STA delay for systems with lower complexity and fewer occurrences because of how easily they can be used.


