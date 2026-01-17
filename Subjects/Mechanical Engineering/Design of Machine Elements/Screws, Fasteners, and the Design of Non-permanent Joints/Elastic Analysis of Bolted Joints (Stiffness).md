[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=Saarthak's_Headspace&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=Saarthak's_Headspace&file=Design%20of%20Machine%20Elements) > [Screws, Fasteners, and the Design of Non-permanent Joints](obsidian://open?vault=Saarthak's_Headspace&file=Screws,%20Fasteners,%20and%20the%20Design%20of%20Non-permanent%20Joints) > Elastic Analysis of Bolted Joints (Stiffness)

---
![[Elastic Analysis of Bolted Joints (Stiffness) - bolted joint in tension.png#align-right|Bolted Joint in Tension|400]]
- Tightening of nut results in tensile stress in the bolt which is assumed to be within elastic limit and obey's Hooke's law
- Stiffness of component is given as, 
	$k' = \frac{P}{\delta} = \frac{AE}{l}$
- Stiffness of bolt is given as, 
	$k'_b = \frac{\pi}{4}\frac{E}{l}d^2$ $N/mm$ 
	where
	$d$ = nominal diameter of bolt
	l = thickness of parts held together by bolt
- Stiffness of components held together with bolt, where outer dia is $3d$ and inner dia is $d$ for grip of bolt
	$k'_1 = k'_2 = \frac{AE}{l} = \frac{2\pi d^2E}{l}$
- Combines stiffness of components is given as,
	$\frac{1}{k'_c} = \frac{1}{k'_1}+\frac{1}{k'_2}$
- When nut is tightened, 
	1. we get an initial tension called pre-load $P_i$, 
	2. $P_i$ elongates the bolt by $\delta_b$ and compresses the two parts by $\delta_c$
- When parts are used we get an external force $P$ which,
	1. Elongates the bolt by $\Delta\delta$, increasing the bolt load by $\Delta P$
	2. Decompresses the parts by $\Delta\delta$ and reduces the total load by $\Delta P$
	Hence we have,
	- $k_b' = \frac{\Delta P}{\Delta\delta}$ ,
	- $k_c' = \frac{P-\Delta P}{\Delta\delta}$
	$\implies \Delta P = CP$      where $C = \frac{k_b'}{k_b'+k_c'}$ and,
	Resultant Bolt Load $P_b = P_i + \Delta P$
- Ghaskets
	1. Soft Gasket
		$k_c' << k_b' \implies \frac{k_c'}{k_b'} = 0 \implies C = 1$
		Hence, $P_b = P_i + P$
	2. Hard Gasket
		$k_c' >> k_b' \implies \frac{k_c'}{k_b'} \to \infty \implies C = 0$
		Hence, $P_b = P_i$	

---