[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=Saarthak's_Headspace&file=Mechanical%20Engineering) > [Engines, Motors & Mobility](obsidian://open?vault=Saarthak's_Headspace&file=Engines,%20Motors%20%26%20Mobility) > Engine

---
An engine is a device which transforms one form on energy into another form of energy.
## Heat Engine
![[Engine-Classification of heat engine.png#align-right|CLassification of Heat Engines|400]]
Heat engine is a device which transforms the chemical energy of a fuel into thermal energy and utilizes this thermal energy to perform useful work. 
Thus, thermal energy is converted to mechanical energy in a heat engine. 
### Types of Heat Engines 
#### Based on Fuel Combustion
1. [[Internal Combustion Engine]] (IC Engines) 
2. [[External Combustion Engine]] (EC Engines)

#### Based on Mechanism of Motion
1. [[Reciprocating Engine]]

#### Based on Fuel Used
1. [[Spark Ignition Engine]] (SI Engine)
2. [[Compression Ignition Engine]] (CI Engine)

### Engine Parameters
1. **Torque :** A measure of an engine’s abilityto do work
	$$T_b = Fb\ Nm$$
	---
2. **Break Power :**
	The useful mechanical energy. The rate at which work is done
	$$P_b = \omega T_b=2\pi NT_b$$
	where,
		$\omega$ = Angular velocity of crank shaft $(rad/s)$
		$N$ = Speed of crank shaft $(rev/s)$
	---
3. **Indicated Power :**
	The total power created from heat energy$$P_i = \frac{W_iN}{n_R}$$ where,
		$W_i = \int p\ dV$ = Indicated work
		$N$ = Speed of crank shaft $(rev/s)$
		$n_R$ = Number of crack revolutions per cycle
			1. $n_R = 2$ for 4 stroke engine
			2. $n_R = 1$ for 2 stroke engine
	---
4. **Friction Power :**
	$$P_f = P_i-P_b$$
	---
5. **Mechanical Efficiency :**
	$$\eta_m=\frac{P_b}{P_i} = 1-\frac{P_f}{P_i}$$
	---
6. **Thermal Efficiency :**
	$$\eta_t=\frac{W}{Q_{in}} = \frac{P}{\eta_cm_fQ_{HV}}$$
	---
7. **Indicated Thermal Efficiency :** ![[power chart.png#align-right|300x200]]$$\eta_{ith} = \frac{P_i}{energy\ in\ fuel\ per\ sec}=\frac{P_i}{\dot{m}\times calorific\ value\ of\ fuel}$$ where,
	$\dot{m}$ = Mass of fuel per sec

	- Indicated thermal efficiencies are typically 50% to 60% and brake thermal efficiencies are usually about 30%
	---
8. **Break Thermal Efficiency :**
	$$\eta_{bth} = \frac{P_b}{\dot{m}\times calorific\ value\ of\ fuel}$$
	---
9. **Volumetric Efficiency :**
- Due to the short cycle time and flow restrictions less than ideal amount of air enters the cylinder
- The effectiveness of an engine to induct air into the cylinders id measured by the volumetric efficiency which is the ratio of actual air inducted divided by the theoretical air inducted
	$$\eta_{v} = \frac{\dot{m_a}}{\rho_a V_d(\frac{N}{n_R})}$$
	where, 
		$\dot{m_a}$ = Volume flow rate of air into the intake system for both SI and CI
		$\rho_a$ = Inlet air density
		$V_d$ = Volume displaced by system
	---
10. **Relative Efficiency/Efficiency ratio :**
	$$\eta_{rel} = \frac{Actual\ thermal\ efficiency}{Air- standard\ efficiency}$$
	---
11. **Indicated Mean effective pressure (IMEP) :** ![[IMEP.png#align-right|250x400]]
	Average pressure inside cylinders
	$$p_{im} = \frac{W_i}{V_d}=\frac{60000\times P_i(kW)}{LAnK}\ \ (N/m^2)$$
	where,
		$V_d = V_{BDC} - V_{TDC}$
		$L$ = Length of the stroke $(m)$
		$A$ = Area of piston $(m^2)$
		$N$ = Crankshaft speed $(rpm)$
		$n$ = Number of power strokes
			1. $\frac{N}{2}$ for 4 stroke engine
			2. $N$ for 2 stroke engine
		$K$ = Number of cylinders
		$L$ = Length of the stroke

	---
12. **Break Mean effective pressure :**
	$$p_{bm} = \frac{60000\times P_b(kW)}{LAnK}\ \ (N/m^2)$$

	---
13. **Mean piston speed :**
	$$\overline{s}_{p} = 2LN$$
	---
14. **Specific Power Output :**
	Power output per unit piston area
	$$P_{s} = \frac{P_b}{A}=p_{bm}\times \overline{s}_p$$

	---
15. **Specific Fuel Consumption :** ![[bsfc.png#align-right|300x200]]![[performance map.png#align-right|300x200]]
	Measure of how efficiently the fuel supplied is used to make power $$bsfc = \frac{m_f\times3600}{P_b}\ \ (\frac{kg}{kW\ hr})$$
	- Point of minima exists
	- At high speeds the bsfc increases due to increased friction
	- At lower speeds the bsfc increases due to increased time for heat losses from the gas to the cylinder and piston walls
	- bsfc decreases with compression ratio due to higher thermal efficiency ($r\uparrow \implies bsfc\downarrow$)
	- Performance maps are used to display the bfsc over the engines full load and speed range.
	---
16. **Air fuel ratio :**
	$$A/F = \frac{\dot{m_a}}{\dot{m_f}}$$
- For combustion to take place the proper ratio of air and fuel must be present in the cylinder
- SI: AF$\to$ [2,18]
- CI: AF$\to$ [18,80]

---
16. **Equivalence ratio :**
	$$\text{Equivalance ratio} = \frac{\text{actual Fuel Air ratio}}{\text{stochiometric Fuel Air ratio}}$$

## Types of engines
1. [[External Combustion Engine]]  (EC Engine)
2. [[Internal Combustion Engine]] (IC Engine)
3. Hydraulic Turbines
4. Electric Motors
5. Petrol Engines
6. Heat Engine

---