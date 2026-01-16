[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Engines, Motors & Mobility](obsidian://open?vault=5aabe01b2a639311&file=Engines,%20Motors%20%26%20Mobility) >  [[Engine]] > Compression Ignition Engine

---
- Works on the Diesel Cycle
- Diesel used as fuel, which has a high self-ignition temperature
- Air used instead of Air-fuel mixture
- Self ignition of fuel
- Compression ratio of 16 - 20

## Four Stroke SI Engine
![[Spark Ignition Engine-4stroke SI Engine Cycle.png#align-right|400]]
![[Spark Ignition Engine-Piston strokes.png#align-right|Actual Four-Stroke SI Engine|400]]
- Cycle of operation completes in 4 strokes of the piston or two revolutions of crankshaft
- Each stroke consists of $180\deg$ of crankshaft rotation
- One complete 4 stroke cycle takes $720\deg$ of cranks rotation
- 5 Events occur during one complete 4 stroke cycle
### Events of a four stroke engine
![[Spark Ignition Engine-PV Diagram.png#align-right|PV Diagram for Four-Stroke SI Engine|400]]
![[Compression Ignition Engine-ideal PV diagram.png#align-right|Ideal Diesel Cycle PV Diagram|400]]
1. Suction or Intake Stroke
	- $0\to1$
	- Piston at TDC and about to move downwards
	- Inlet valve opens instantaneously
	- Exhaust valve is closed
	- Due to suction created by downward movement, the air is drawn into cylinder
	- When piston reached BDC, stroke ends and inlet closes instantaneously
2. Compression Stroke
	- Compression: $1\to2$ and Combustion: $2\to3$
	- Air is compressed by the return stroke into $V_c$
	- Both inlet and exhaust valves are closed
	- At end of stroke, charge is ignited with help of a spark plug
	- Heat addition at constant volume at ignition, increasing pressure.
	- Temperature increases $\uparrow$ and Pressure increases $\uparrow$
	- $\Delta T\approx 2000^{\circ}C$
3. Expansion or Power Stroke
	- Expansion: $3\to4$ and Blow-down: $4\to5$
	- High pressure forced piston towards BDC producing Power
	- Both intake and exhaust valve in closed position
	- Temperature decreases $\downarrow$ and Pressure decreases $\downarrow$
4. Exhaust Stroke
	- $5\to0$
	- Exhaust valve opens instantaneously
	- Pressure falls to atmospheric value
	- Some residual gasses left in the system


## Diesel Cycle
The air standard cycle for CI engine
![[Compression Ignition Engine-Ideal Diesel Cycle PV.png#align-right|Ideal Diesel Cycle PV Diagram|400]]
![[Compression Ignition Engine-Ideal Deisel cycle Ts diagram.png#align-right|Ideal Diesel Cycle Ts Diagram|400]]
- $1\to2$ : Isentropic Compression
- $2\to3$ : Heat Addition at Constant Pressure
- $3\to4$ : Isentropic Expansion
- $4\to5$ : Heat Rejection at Constant Volume
- Isentropic Relations
	$$\frac{T_1}{T_2}=(\frac{V_2}{V_1})^{k-1}=(\frac{V_3}{V_4})^{k-1} = \frac{T_4}{T_3}$$
- Energy balance for any process:
	$$(q_{in}-q_{out})+(w_{in}-w_{out}) = \Delta u$$
- Heat transfer from the working fluid
	$$
	\begin{align}
	&q_{in} = u_3-u_2=c_p(T_3-T_2)\\
	-&q_{out} = u_4-u_1=c_v(T_4-T_1)\\
	\end{align}
	$$
- Thermal efficiency of ideal Diesel cycle
	$$\eta_{th} = \frac{w_{net}}{q_{in}} = 1-\frac{q{out}}{q{in}} = 1-\frac{T_4-T_1}{k(T_3-T_2)}=1-\frac{1}{r^{k-1}}[\frac{r_c^k-1}{k(r_c-1)}]$$
	where,
		$r$ = Compression ratio
		$r_c = \frac{V_3}{V_2}$ = Cutoff Ratio
		$k = \frac{c_p}{c_v}$ = Specific Heat Ratio

- $$(\eta_{th})_{otto} > (\eta_{th})_{diesel}$$

## Modern CI Engines
- Combustion process of **early CI engines** is best approximated by a constant heat addition process $\to$ **Diesel Cycle**
- Combustion process of **modern CI engines** is best approximated by a combination of constant volume and constant pressure process $\to$ **Dual Cycle**
![[Earlier vs Modern CI Engine.png]]