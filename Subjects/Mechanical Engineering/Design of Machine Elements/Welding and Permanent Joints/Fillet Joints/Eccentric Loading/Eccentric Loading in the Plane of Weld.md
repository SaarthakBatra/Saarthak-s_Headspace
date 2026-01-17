[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=5aabe01b2a639311&file=Design%20of%20Machine%20Elements) > [Welding and Permanent Joints](obsidian://open?vault=5aabe01b2a639311&file=Welding%20and%20Permanent%20Joints) > [Fillet Joints](obsidian://open?vault=5aabe01b2a639311&file=Fillet%20Joints) > [Eccentric Loading](obsidian://open?vault=5aabe01b2a639311&file=Eccentric%20Loading) > Eccentric Loading in the Plane of Weld

---
![[Eccentric Loading in the Plane of Weld.png#align-right|Eccentri Loading in Plane of Weld|400]]
## Primary Shear Stress
- The force P acting through the centre of gravity causes direct shear stress in the welds called primary shear stress $\tau_1$ ,
$$\tau_i = \frac{P}{A}$$
where,
	$A$ = Throat are of all welds
## Secondary Shear Stress
![[Eccentric Loading in the Plane of Weld- shear stress.png#align-right|Primary and Secondary Shear Stress|400]]
- The couple M causes torsional shear stresses in the throat area of welds called secondary shear stress $\tau_2$ ,
$$\tau_2 = \frac{Mr}{J}$$
where, 
	$r$ = distance of point in weld from G
	$J$ = polar moment of inertial of all welds about G
The polar moment of inertia of a weld about $G$ using $G_i$ and parallel axis theorem is,
$$J_{G1} = \frac{Al^2}{12} \implies J_G = A[\frac{l^2}{12}+r_1^2]$$
where, 
	$r_1$ = distance between $G_1$ and $G$

## Examples
### Q1.
A welded connection, as shown in Fig. is subjected to an eccentric force of $60 kN$ in the plane of the welds. Determine the size of the welds, if the permissible shear stress for the weld is $100\ N/mm^2$. Assume static conditions.
![[Eccentric Loading in the Plane of Weld-Q1.png#align-right|400]]
#### ans.
We have, $P=60kM$, $\tau=100\ N/mm^2$
##### Primary Shear Stress
![[Eccentric Loading in the Plane of Weld-ans1_1.png#align-right|400]]
By symmetry $G$ is midway between the two horizontal welds, i.e
$$\bar{y} = 50mm$$
Taking moment about the vertical weld and treating the weld as a line,
$$
\begin{align}
(50+100+50)\bar{x}= &50\times25+50\times25+100\times0 \\
\implies\ \ \ \ \bar{x}&=12.5mm
\end{align}$$
Area of welds is,
$$A=A_1+A_2+A_3=50t+50t+100t=200t\ mm^2$$
Hence, the primary shaer is,
$$\tau_1 = \frac{P}{A}=\frac{60000}{200t}=\frac{300}{t}\ N/mm^2$$
##### Secondary Shear Stress
Distance of farthest point $A$ from $G$,
$$
\begin{align}
&r=\sqrt{(50-12.5)^2+50^2}=62.5mm \\
and\ \ \ \ &\theta=\tan^{-1}(\frac{50}{50-12.5})=53.13\deg\\
\implies &\phi = 36.87\deg
\end{align}
$$
also,
$$
\begin{align}
&e=(50-\bar{x})+150=187.5mm\\
&M=P\times e=11250\times10^3\ Nmm\\
&\overline{G_1G}(r_1)=\overline{G_2G}(r_2)=\sqrt{(25-12.5)^2+50^2}=51.54mm\\
&\overline{G_3G}(r_3)=\bar{x}=12.5mm\\
&J_1=J_2=50t[\frac{50^2}{12}+(51.54)^2]=143235.25t\ mm^4\\
&J_3 = 100t[\frac{100^2}{12}+(12.5)^2] = 98958.33t\ mm^4\\
&\implies J=J_1+J_2+J_3=385428.83t
\end{align}
$$
Hence, the secondary shear is
$$\tau_2=\frac{Mr}{J}=\frac{11250\times10^3\times62.5}{385428.83t}=\frac{1824.27}{t}\ N/mm^2$$
##### Resultant Shear Stress
![[Eccentric Loading in the Plane of Weld-ans1_2.png#align-right|400]]
- The secondary shear stress is inclined at 36.87° with the horizontal and is resolved into vertical and horizontal components as shown
$$
\begin{align}
\tau_{vertical} &= \tau_1+\tau_2\ sin\phi = \frac{1094.56}{t}+\frac{300}{t}=\frac{1394.56}{t}\ N/mm^2\\
\tau_{horizontal}&=\tau_2\ \cos\phi= \frac{1459.41}{t}\ N/mm^2\\
\implies \tau &= \sqrt{(\frac{1394.56}{t})^2+(\frac{1459.41}{t})^2} = \frac{2018.58}{t}\ N/mm^2
\end{align}
$$
##### Size of Weld
The permissible shear stress gives, $\tau = 100 = \frac{2018.58}{t}$ $\implies t=20.19mm$
hence,
$$h=\frac{t}{0.707}=28.56mm$$





### Q2.
An eccentrically loaded bracket is welded to the support as shown in Fig.  The permissible shear stress for the weld material is $55\ N/mm^2$ and the load is static. Determine the throat and leg dimensions for the welds.
![[Eccentric Loading in the Plane of Weld-Q2.png#align-right|400]]

#### ans.
We have, $P=25kM$, $\tau=55\ N/mm^2$
##### Primary Shear Stress
By symmetry $G$ is midway between the two vertical welds, i.e
$$\bar{x} = 50mm$$
Taking moment about the horizontal weld and treating the weld as a line,
$$
\begin{align}
(150+150+100)\bar{y}= &150\times75+150\times75+100\times0 \\
\implies\ \ \ \ \bar{y}&=56.25mm
\end{align}$$
Area of welds is,
$$A=A_1+A_2+A_3=150t+150t+100t=400t\ mm^2$$
Hence, the primary shaer is,
$$\tau_1 = \frac{P}{A}=\frac{25000}{400t}=\frac{62.5}{t}\ N/mm^2$$
##### Secondary Shear Stress
Distance of farthest point $A$ from $G$,
$$
\begin{align}
&r=\sqrt{(150-56.25)^2+50^2}=106.25mm \\
and\ \ \ \ &\theta=\tan^{-1}(\frac{150-56.25}{50})=61.93\deg\\
\implies &\phi = 28.07\deg
\end{align}
$$
also,
$$
\begin{align}
&e=50+100=150mm\\
&M=P\times e=3750000\ Nmm\\
&\overline{G_1G}(r_1)=\overline{G_2G}(r_2)=\sqrt{(75-56.25)^2+50^2}=53.4mm\\
&\overline{G_3G}(r_3)=\bar{y}=56.25mm\\
&J_1=J_2=150t[\frac{150^2}{12}+(53.4)^2]=708984t\ mm^4\\
&J_3 = 100t[\frac{100^2}{12}+(56.25)^2] =399740t\ mm^4\\
&\implies J=J_1+J_2+J_3=1817708t\ mm^4
\end{align}
$$
Hence, the secondary shear is
$$\tau_2=\frac{Mr}{J}=\frac{3750000\times106.25}{1817708t}=\frac{219.2}{t}\ N/mm^2$$
##### Resultant Shear Stress
![[Eccentric Loading in the Plane of Weld-ans2.png#align-right|400]]
- The secondary shear stress is inclined at 28.07° with the horizontal and is resolved into vertical and horizontal components as shown
$$
\begin{align}
\tau_{vertical} &= \tau_1+\tau_2\ sin\phi = \frac{103.14}{t}+\frac{62.5}{t}=\frac{165.64}{t}\ N/mm^2\\
\tau_{horizontal}&=\tau_2\ \cos\phi= \frac{193.42}{t}\ N/mm^2\\
\implies \tau &= \sqrt{(\frac{165.64}{t})^2+(\frac{193.42}{t})^2} = \frac{254.65}{t}\ N/mm^2
\end{align}
$$
##### Size of Weld
The permissible shear stress gives, $\tau = 55 = \frac{254.65}{t}$ $\implies t=4.63mm$
hence,
$$h=\frac{t}{0.707}=6.55mm\approx7mm$$




---
