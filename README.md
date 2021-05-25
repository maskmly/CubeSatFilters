# UHF+VHF Filter Design for CubeSat Communication System

The following are the steps taken to design and simulate the analogue filters for a CubeSat communication system. The design is in accordance with the standards approved by the government of Canada and Canadian Satellite Design Competition (CSDC) guidlines. The purpose of this filter is to remove unwanted components from down-link and up-link signals.

The simulation of this design was solely done on eysight Advanced Design System software. The objective is to design two band-pass ﬁlters with center frequencies at 144 and 442 MHz. The ﬁlter with center frequency in the VHF region is implemented for up-link signals, and the one in the UHF region is implemented for down-link signals. Since the communication protocol in use is 2FSK, the minimum bandwidth for the VHF ﬁlter is 4.8 KHz, and for the UHF ﬁlter is 38.4 KHz. The following is the formula to obtain a minimum bandwidth for 2FSK signals:

BW = 2R<sub>b</sub> + 2&Delta;f

Where R<sub>b</sub> is bit rate and &Delta;f is frequency shift. For us to have no overlap between the transmitted binary signals, the frequency shift must be greater than or equal to the bit rate. Up-link communications are to occur at a rate of 1200 bps and down-link communications occur at a rate of 9600 bps. Hence, during design we must make sure the bandwidth of the S<sub>21</sub> response is not less than the bandwidth determined by the above equation.

In the following design a 3rd order circuit is used to achieve the required performance using only passive components:

![higher band 3](images/higherBand3.png)

This is a 3rd order Butterworth filter. This design was simply put together by superposing a low-pass filter onto a high-pass filter. The following figure better represents the design rational:

![lpf hpf superposition](images/lpfHpfSuperposition.png)

The component values are calculated using 3rd order circuit formulas which can be derived from scratch. However, for the sake of saving time I will skip the derivation part. To calculate the component values first we define the problem as follows:

Design a band-pass filter having a maximally flat response, with N=3. The centre frequency is 442 MHz, the bandwidth is 5% of the centre frequency, and the impedance is 50 Ohms to match the load.

*f<sub>c</sub>* = 442 MHz <br>
*&omega;<sub>0</sub>* = 884&pi;10<sup>6</sup> <br>
*&Delta; = 0.05* <br>
*N* = 3 <br>
*Z<sub>0</sub>* = 50&ohm;

The factor *g<sub>k</sub>* is called the element value of the circuit and the formula for it is as follows:

![gk equation](images/eqGk.png)

Note that for series components we use the following formulas to calculate L and C (Repeat the same process accounting for different element values and/or centre frequencies):

![series L equation](images/eqLseries.png)

![series C equation](images/eqCseries.png)

And for parallel components we use the following formulas:

![parallel L equation](images/eqLparallel.png)

![parallel C equation](images/eqCparallel.png)

The S<sub>21</sub> responses for the UHF radio band based on the calculated values are as follows:

![-3db UHF S21](images/calculatedNeg3dbUHF1.png)
UHF S<sub>21</sub> response (-3 dB limited y-axis)

![-40db UHF S21](images/calculatedNeg40dbUHF1.png)
UHF S<sub>21</sub> response (-40 dB limited y-axis)

And the VHF radio band on calculated values is as follows:

![-3db VHF S21](images/calculatedNeg3dbVHF1.png)
VHF S<sub>21</sub> response (-3 dB limited y-axis)

![-40db VHF S21](images/calculatedNeg40dbVHF1.png)
VHF S<sub>21</sub> response (-40 dB limited y-axis)

I hope this article has shed some light on how to design band-pass filters using only passive components.