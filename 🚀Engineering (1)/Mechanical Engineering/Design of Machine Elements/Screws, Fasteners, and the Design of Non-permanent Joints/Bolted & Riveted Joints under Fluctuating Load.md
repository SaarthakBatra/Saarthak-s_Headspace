[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=Saarthak's_Headspace&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=Saarthak's_Headspace&file=Design%20of%20Machine%20Elements) > [Screws, Fasteners, and the Design of Non-permanent Joints](obsidian://open?vault=Saarthak's_Headspace&file=Screws,%20Fasteners,%20and%20the%20Design%20of%20Non-permanent%20Joints) > Bolted & Riveted Joints under Fluctuating Load

---
If external load on a bolt varies from $0$ to $P$ then,
- $P_{max} = P$ and  $P_{min} = 0$,		then
- $P_{b_{max}} = P_i + CP$ and $P_{b_{min}} = P_i$,	where $C = \frac{k_b'}{k_b' + k_c'} = \frac{1}{1 + (\frac{k_c'}{k_b'})}$
- Mean components $P_{b_m} = \frac{1}{2}[\ P_{b_{max}} + P_{b_{min}}\ ]$
- Alternating components $P_{b_a} = \frac{1}{2}[\ P_{b_{max}} - P_{b_{min}}\ ]$
- It is desirable to design the bolts on the basis of static strength rather than on the basis of endurance limit. 
- Therefore, in automotive applications, the connecting rod bolts are tightened with very high pre-load with the stress approaching the yield point.

## Example
### Q1.
The assembly of two circular plates clamped together by means of a bolt, which is shown in Fig. , is subjected to a variable force $P$ varying from $0$ to $10 kN$. The bolt is made of plain carbon steel $45C8$ ($S_{ut} = 630\ N/mm^2$; $S_{yt} = 380\ N/mm^2$ and $E = 207000\ N/mm^2$). The two circular plates are made of aluminium ($E = 71000\ N/mm^2$). The fatigue stress concentration factor is $2.2$ and the expected reliability is $90\%$. The initial pre-load in the bolt is $5 kN$. Determine the size of the bolt if the factor of safety is $2$.
#### ans.
we have, 
- $P_i = 5kN$,	$P = 0 - 10kN$,		$fs = 2$
- For bolts,
	$S_{ut} = 630\ N/mm^2$, 	$S_{yt} = 380\ N/mm^2$,	$E = 207000\ N/mm^2$, $K_f = 2.2$,	$R = 90\%$
- For Plates,	$E = 71000\ N/mm^2$
##### Endurance limit stress for bolt
$S_e' = 0.5 S_{ut} = 0.5(630) = 315\ N/mm^2$
For axial loading, size factor = 1
For $90\%$ reliability, 
	$K_c = 0.897$
	$K_d = \frac{1}{K_f} = \frac{1}{2.2} = 0.4545$
	$S_e = K_bK_cK_dS_e'$ $= 1\times0,891\times0.4545\times315$ $= 128.42\ N/mm^2$
##### Construction of Goodman diagram
![[Bolted & Riveted Joints under Fluctuating Load-Goodman Diagram.png#align-right|Goodman Diagram|400]]
$k_b' = \frac{\pi\times d^2\times 207000}{4\times50} = 3251.55d^2$
Area of two plates $A_c = \frac{\pi (2d)^2}{4} = 2.356d^2\ mm^2$
$k_c' = \frac{A_cE_c}{l} = \frac{2.356d^2\times 71000}{50} = 3345.52d^2$
$C = \frac{k_b'}{k_b' + k_c'} = \frac{3251.55d^2}{3251.55d^2 + 3345.52d^2} = 0.4929$
then, 
	$P_{max} = 5000 + (0.4929)(10000) = 9929\ N$
	$P_{min} = 5000 + (0.4929)(0) = 5000\ N$
	$P_{m} = \frac{9929 + 5000}{2} = 7464.5\ N$
	$P_{a} = \frac{9929 - 5000}{2} = 2474.5\ N$

##### Permissible stress amplitude
from, $\frac{S_m}{630}+\frac{S_a}{128.42} = 1$ and $S_m = \frac{P_i}{A}+S_a = \frac{5000}{A}+S_a$
and $\sigma_a = \frac{P_a}{A} = \frac{S_a}{fs} \implies \frac{2464.5}{A} = \frac{630 - \frac{5000}{A}}{5.9\times2}$
we have, $A =54.1\ mm^2$ 
Hence $M10 \times 1.25$ bolt


### Q2
![[Bolted & Riveted Joints under Fluctuating Load-Q2.png#align-right|400]]
Fig. shows the arrangement of supporting a machine weighing $200 kg$ at a distance of $1 m$ from the nearest point of support. The operation of the machine creates a rotating unbalanced force of $2000 N$ in the plane of the figure and at the position of the machine. The speed of rotation is $14 rpm$. The weight of the channel is $20\ kg/m$. Two bolts, denoted by $1$ and $2$, hold the channel to the main frame. The bolts are located at $35$ and $270 mm$ from the nearest point of support. The following data is given for the bolts: 
	Ultimate tensile strength = $960 MPa$, 
	Yield point strength = $850 MPa$, 
	Endurance limit in bending = $500 MPa$, 
	Fatigue stress concentration factor = $3.0$, 
	Factor of safety = $2$ 
The initial preload in each bolt is $55 kN$. The ratio of stiffness of the parts held together by the bolts to the stiffness of the bolts is $3$. Assume Goodman line as the criterion of failure. Determine the size of the bolts. 
#### ans
we have,
	$S_{ut} = 960\ N/mm^2$,	$S_{yt}=850\ N/mm^2$,	$S_e' = 500\ M/mm^2$,		$fs = 2$, 	$K_f = 3$, $\frac{k_c'}{k_b'} = 3$, 	$P_i = 55kN$
##### Endurance Limit Stress for Bolt
$$K_d=\frac{1}{K_f}=\frac{1}{3}\implies S_e=K_dS_e' = \frac{500}{3}=166.67\ N/mm^2$$
##### Force Analysis
![[Bolted & Riveted Joints under Fluctuating Load-ans2_1.png#align-left|200]]
###### At bracket
- The load tends to tilt the bracket about our pivot point C
- $\delta_i = \frac{P_iL}{AE}$
$$\frac{P_1}{P_2} = \frac{\delta_1}{\delta_2} = \frac{l_1}{l_2} = \frac{270}{35} = 0.1296$$

###### At channel
![[Bolted & Riveted Joints under Fluctuating Load-ans2_2.png#align-right|300]]
- Weight of channel $W_{ch}$= $20\times9.81$ $= 196.2N$
- Weight of machine $W_m$ = $200\times9.81$ $= 1962N$
1.  Case1: Rotating force acting downwards
$$
\begin{align}
& W_{ch}(500) + (W_m+2000)(1000) = P_1(270)+(0.1296)P_1(35)& \\ 
&\implies P_1 = 14788.95N\ \ \ and\ \ \ P_2 = 1916.65N&
\end{align}
$$
	
2. Case2: Rotating force acting upwards
$$
\begin{align}
& W_{ch}(500) + (W_m-2000)(1000) = P_1(270)+(0.1296)P_1(35)& \\ 
&\implies P_1 = 218.91N\ \ \ and\ \ \ P_2 = 28.37N&
\end{align}
$$
Hence, force acting on $1$ is critical and fluctuates from $218.91N$ to $14788.95N$

##### Goodman Diagram
![[Bolted & Riveted Joints under Fluctuating Load-ans2_3.png#align-right|400]]
- $P_i = 55000N$
- $C = \frac{1}{1 + (\frac{k_c'}{k_b'})}  = 0.25$
- $\Delta P = 0.25P$
- $P_b = P_i + \Delta P$ $= P_i + 0.25P$

Hence, we have
$$
\begin{align}
P_{max} = 58697.24N,\ \ \ P_{min}=55054.73N &\implies P_m=56875.99N,\ \ \ P_a=1821.26N \\
\implies \tan\theta = \frac{P_a}{P_m} = \frac{1821.26}{56875.99} &= 0.032\ \ \ or\ \ \ \theta = 1.834\deg
\end{align}
$$
- External force ($P$) does not vary from zero to $P_{max}$ but from $218.91 N$ to $14 788.95 N$ in every cycle. 
- Therefore, the load line will not be inclined at 45° to the X-axis. The load line will be inclined at 1.834° with the Xaxis.
For $S_m\ \ and\ \ S_a$ (Coordinates of point C) we have, permissible stress amplitude -
$$
\begin{align}
\frac{S_m}{960}+\frac{S_a}{166.67}=1\ \ and\ \ S_m &= \frac{P_i}{A}+x = \frac{P_i}{A}+\frac{S_a}{\tan\theta} = \frac{55000}{A}+\frac{S_a}{0.032} \\
\implies S_a &= 25.939-\frac{1486.05}{A} 
\end{align}
$$
where,
	$A$ = Tensile stress area of bolt
	
##### Size of Bolt
$$\sigma_a = \frac{P_a}{A} = \frac{S_a}{fs}\implies A = 197.71mm^2$$
Hence, $M20 \times 2\ \ (A=258mm^2)$ is suitable for our application.
##### Static calculations
$$
\begin{align}
P_{max} = 58697.24N\implies &\sigma_t=\frac{P_{max}}{A} = 227.51\ N/mm^2 \\
\therefore\ \ \ \ fs = \frac{S_{yt}}{\sigma_t} &= \frac{850}{227.51}=3.74
\end{align}
$$


---