# Background : STA and its role in design flow

Static Timing Analysis (STA) is a technique used to verify the timing of a digital design, ensuring that it meets the timing constraint at any possible situation. STA is static in nature, allowing for the timing of many paths within a reasonable duration. This advantage over dynamic timing analysis, which applies a stimulus to input signals and observes and verifies the behaviour that results.

STA is a fundamental step in any design flow as it can be performed across multiple instances in the design flow. It is generally not performed at the RTL design level, as the priority at that stage is to ensure logical functionality rather than timing constraints. The lack of timing information makes STA even more undesirable. The illustration (Fig. 1) below showcases the versatility of STA in a design flow.

Synthesis is the process of converting the RTL design written using a hardware-descriptive language (HDL) into gate-level netlist using design constraints defined in a Synopsys Design Constraint (SDC) file and environment variables. The gate-level netlist defines the logical connectivity of the design that can be further optimized over various corners. STA can be performed prior to the post-synthesis optimization stage to identify the presence of critical and failing paths in the design.

STA is more prominent in the Physical design stage instead of the Logic stage mentioned so far. As the stages progress, real clocks and routes are implemented on the gate-level netlist, and STA can be performed.

Partitioning involves segmenting the logical netlist into partitions and treating each one as a black box, reducing the complexity of the design and making the verification and analysis process easier. Floor planning involves creating a blueprint on which logical cells would be placed, with the netlist converted into logical cells using technology files and standard cell libraries provided by the foundry.

Clock tree synthesis (CTS) is performed on the post-placement layout to distribute the clock across the layout. After the CTS stage, routing of the design involves connecting the placed logical cells for signal propagation via nets. The metal layer information is extracted by the process design kit (PDK), which contains parameters such as pitch, number of tracks, thickness, minimum width, and vias.

In the physical design stage, metal traces or interconnects are used for routing, resulting in finite delay during propagation. The Standard Parasitic Extraction File (SPEF) is obtained during the extraction stage, which includes information about the approximate length of interconnects. For nanometer designs, RC-parasitics dominate power dissipation and define interconnect delays. The scaling of transistor technologies leads to the prevalence of coupling among interconnects, contributing to cross-talk and noise. Therefore, static timing analysis (STA) should include the effects of noise and cross-talk at later stages of the physical design.

![](/images/theory/sta_vlsi.png)

- Fig.1 Demonstrates the role of STA in a design flow

Various techniques, such as wire-load models (WLMs), are used to estimate the length of interconnects. The extraction tool can be used for final verification or iterative optimization. It is crucial to consider the effect of cross-talk and noise due to coupling, as it is impractical to consider it during the global routing phase due to the absence of finalized routes.

The execution of static timing analysis depends on several key factors within a gate-level netlist, including the chosen interconnect modelling approach, the modeling of clocks, and the inclusion or exclusion of coupling effects between signals. These considerations shape the static timing analysis process, tailoring it to specific design requirements and objectives.



