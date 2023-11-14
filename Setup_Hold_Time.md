# Understanding Setup and Hold Time in Digital Design :

Timing constraints are crucial in determining the timing intent of a design, with two of the most prominent ones being Setup and Hold time. These constraints are essential for the proper operation of digital circuits, achieving design closure, improving performance, and guaranteeing reliable circuit operation. It is critical for designers to recognize how setup and hold times interact with signal transitions to build digital systems that adhere to their intended specifications and reliability standards. This region can be visualised in the illustration, Fig. 5, the data must remain stable in the region and any changes outside this region is permissible. When there is a timing violation, the sequential elements enter a condition known as metastability.

![](/images/theory/setup_hold.png)

- Fig. 5 General idea of Setup and Hold time

Timing violations function similarly to warning signals that need to be resolved for proper functioning and ensuring reliability of the design. The setup and hold time create a specific region for a clock signal where any changes in the data signal could result in a timing violation. When there is a timing violation, the sequential elements enter a condition known as metastability, which could lead to erroneous outputs. The unpredictable nature of the metastable state makes it necessary to eliminate any possibility of metastability in the design.

The active edge of the clock is assumed to be the positive edge for the illustration (Fig. 5) above and the same concept applies to a negative edge of the clock. The example covered provides a brief insight on the concept of setup and hold time, for an in-depth analysis a simplified two-flop system shall be analysed (Fig. 6) for setup and hold analysis separately.

![](/images/theory/setup_hold_r2r.png)

- Fig. 6 Simplified Two-Flop system

The setup and hold time define the relationship between the data-pin (D-pin) and the clock pin, with the active edge of the clock assumed to be the positive edge and the same concept applies to a negative edge of the clock. For an in-depth analysis, a simplified two-flop system shall be analysed for setup and hold analysis separately.

Key terminologies during setup and hold analysis include slack, clock skew, and clock-to-Q delay. Slack measures the amount by which a signal path goes over or under its time constraints, while clock skew refers to the difference in the clock signal's arrival times at various components or flip-flops within a digital circuit. Excessive clock skew can cause setup and hold time violations, which can result in erratic behaviour or inaccurate data acquisition. An optimal clock skew is vital for efficient and reliable distribution of clock signal, achieved by creating effective clock trees during the clock tree synthesis stage.

Slack, clock skew, and clock-to-Q delay are the fundamental ideas of timing analysis in digital circuit design. Engineers rigorously monitor these parameters to ensure that digital systems operate reliably and efficiently, ensuring that signals are processed precisely and synchronously in intricate designs. Consider the simplified segment of a larger system consisting of two flip-flops is considered, with non-zero clock skew (tskew), combinational delay (tcomb), and clock-to-q delay (tc2q) in the fig. 6.


## Setup Analysis :

For setup analysis, let the setup time for both registers be tsu and the clock period be tClk . The setup check is passed when the arrival time is less than the required time due to the fact that the data must remain stale before the active clock edge for the setup check. The active edge for the analysis is the positive edge of the clock.    
The arrival time is computed by simply following the sequence of events mentioned below : 
1. The launch clock signal reaches the launch flop after a time $Δ1$
2. The launch flop takes tc2q to produces a valid output
3. Finally, the output of launch flop takes tcomb to reach the capture flop

Now, this arrival time (<i>t_arrival</i>) must be setup time ($tsu$) before the second rising edge actually reaches the clock. This means required time can be computed using the events below, similar to arrival time :

1.	The second rising edge arrives after time <i>t_Clk<i> from time zero.
2.	The capture signal reaches the capture flop after $Δ2$
3.	The data should arrive at a time before the event 2 occurs, i.e $tsu$

Hence, arrival time and required time are given by the summation of the events mentioned above , i.e <i>t_arrival</i> is equal to $Δ1 +  tc2q + tcomb$  and <i>t_required</i> is  equal to $tClk + Δ2 + (-tsu)$. Thus the condition for setup analysis can be given by the equations (2): 

$Δ1 +  tc2q + tcomb  ≤  tClk + Δ2 -tsu(2)$

The equation (2) can be rearranged as equation (3) where clock skew is considered positive (capture clock as reference) and $Δskew$ is given as $Δ2 - Δ1$.

$tc2q + tcomb +tsu ≤   tClk + Δskew(3)$

Now, the maximum operating frequency of the design with the timing constraints provided by the designer can be computed by equation (4), Hence setup analysis is crucial to evaluate the permissible frequency of the system under given constraints. The parameters in the equation can be optimised further to improve the frequency performance of the design.

$fClk(max)= 1/(tc2q + tcomb +tsu -Δskew)(4)$

The setup slack is computed as the difference of required and arrival time, as illustrated in equation (5). Setup slack or slack in general acts as an indication of integrity for a timing path. Positive setup slack implies that data arrives before the required time hence the setup check is cleared, whereas a negative setup slack implies that the data arrives after required time which causes a setup timing violation.

$T(setup Slack)= (tClk + Δskew- tsu) -(tc2q +tcomb)(5)$

Setup analysis is also referred to as Late analysis.  

## Hold Analysis :

Hold analysis can be conducted in a manner like setup analysis with slight adjustments. The hold requirement states that the data launched at the current clock edge must not travel to the capture flop before the hold time has passed after the clock edge. This essentially means that the hold analysis is conducted after the active clock edge has passed, which means hold analysis is independent of clock period and hence hold equations do not contain  $tClk$ term. The hold check is passed when the arrival time is more than the required time  since the data must remain stable after the active clock edge for the hold check. The active edge for the analysis is the positive edge of the clock. The arrival time and required time equations remain the same as setup analysis except the exclusion of clock period. The hold analysis equation can be formulated as under : 

$Δ1 +  tc2q + tcomb  >  Δ2 + thold(6)$

This equation (6) can be further simplified by assuming positive skew, i.e  $Δ2$ is greater than Δ1 and skew is computed with respect to capture clock path. The modified equation is given as follows : 

$tc2q + tcomb >  Δskew +  thold(7)$

The hold slack is computed as the difference of arrival and required time, as illustrated in equation (8).  

$T(hold Slack)= (tc2q +tcomb)-( Δskew+  thold)(8)$

For no hold violations, the hold slack (T_hold-slack) should be positive. Hence the arrival data should be as late as possible. Hold analysis is also referred to as early analysis. It is crucial to note that all the preceding equations apply to an oversimplified situation, thus they may vary depending on the complexity and design of the circuit, but the basic notion is the same. As a result, the equations themselves are not particularly significant; rather, the process used to generate the equations is what matters most. 

## Setup-Hold Time Analogy :

A common question that may arise while learning about setup-hold times is <b>*Why do we require both setup and hold, why not just one of them?*</b> This is a fundamental question that can be answered in many ways. According to my understanding, any system whether be it a flip-flop or a simple AND gate, requires certain time frame to figure out that an event has occured (event in this context means a data-transition), much like us humans or any sort of life-form. This time-frame is refeered as reaction time, it determines how long does it take for an entity to detect a change has occured ; in simple words it is the difference between the time taken by the entity to detect the change and the time instance of occurance of an event. So, this *reaction time* is analogous to the setup time. Hence, to ensure the data is captured by the system it should *not* change within the reaction time (setup time) frame, else it won't be captured properly causing metastability and setup violation. 

This analogy can be extended to hold time as well. As discussed above that reaction time is the time required for a system to recognize to a stimulus, now the time required by the system to act onto that stimulus after recognizing it is called the response time. A system (considiring digital systems), in addition to a reaction time(setup time), also requires this response time to determine whether the transition that has occured is a 0 or a 1. This response time is analogous to hold time. Hence, to ensure that the data is properly "understood" by the system, the data must not change within this 'deciding phase' or the response time (hold time) frame.

For a system to be reliable and efficient, it requires to have both these distinct time frames (setup and hold) as taking away one of them can cause issues and 



