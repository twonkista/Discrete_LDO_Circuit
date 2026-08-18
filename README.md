Discrete LDO regulator (5V→3.3V) built from scratch on breadboard. Designed and debugged a TLV431-based shunt regulator with feedback control, 
achieving stable 3.1V output validated under real load (ESP32 module). Independent design and not based on an existing reference circuit.

I didn't have time to make it a PCB and this was gonna be part of a larger project but due 
to time and money constraints, the LDO is what I have done since it is the bulk of the project. The rest are just peripherals.

The idea of this LDO is to take a USB Type C input from a laptop and convert the laptop output port voltage (my laptop sends in 5V) and change that to around 3.3V.
Since it's a breadboard some of the resistor values are way off and to be honest I didn't have the best amount of resources for this

It right now sends in a 3.1V output which is close and is within the ESP32 tolerance level. 

<img width="400" height="400" alt="IMG_5649" src="https://github.com/user-attachments/assets/27158419-65f7-49c3-a6c2-fc8c47369806" />
<img width="400" height="400" alt="IMG_5650" src="https://github.com/user-attachments/assets/73095b4d-4667-47ee-b96a-515e2d2d8a5c" />
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/0def0950-a705-496b-a14b-ce725b1e1c40" />
<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/f55c82e4-f130-4533-b29d-01f3a7c6fc82" />



To be really honest the breadboard framework is kinda hard to really be worth the time to actually make it better. For the future projects I'll just use off the shelf parts
for better use of my time. I have looked at countless lectures and notes of this circuit and it took a while (maybe 1-2 weeks) just to understand how this thing works. 

Here is the parts list:

USB Type C breakout
MP6002 OP Amp
TLV431 1.24V shunt resistor (for the reference voltage, this one was a piece of work and I burnt through 2 of them)
BS250 PMOS transistor
5 10K resistors (I had to use 4 10K resistors in parallel just so I can make it a 2.5K resistor)
1 16K resistor (from the voltage divider calculation)
0.1uF ceramic cap (for input voltage)
10uF aluminum cap (for output voltage)

PS. the discrepancy from the LTSPICE diagram with the breadboard is the reference voltage. I wanted to make it simple for the diagram then I figured out how to use the TLV431. The LTSpice diagram was more
to prove my concept. I chose to make that from scratch rather than relying on an already existing one. 

Lessons Learned / Debugging Notes

Reference voltage tuning: Needed a specific resistance value for the TLV431's reference divider that wasn't achievable with a single resistor on hand
Validating under load: A bench measurement of 3.1V doesn't guarantee a stable rail under real current draw. Used a bare ESP32 module (no firmware) as a load test to confirm the regulator holds voltage through power-on current spikes, not just at idle.
