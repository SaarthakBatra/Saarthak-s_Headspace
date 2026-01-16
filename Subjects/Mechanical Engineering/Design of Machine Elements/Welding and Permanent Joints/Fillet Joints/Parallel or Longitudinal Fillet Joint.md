[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=5aabe01b2a639311&file=Design%20of%20Machine%20Elements) > [Welding and Permanent Joints](obsidian://open?vault=Saarthak's_Headspace&file=Welding%20and%20Permanent%20Joints) > [[Fillet Joints]] > Parallel or Longitudinal Fillet Joint

---
![[Parallel or Longitudinal Fillet Joint.png]]
For a weld we have,
$$t = h\cos(45\deg) = 0.707\ h$$
A single parallel fillet weld subjected to a tensile force, follows relation
$$P = 0.707\ h\ l\ \tau$$
and Double parallel fillet weld follows,
$$P = 1.414\ h\ l\ \tau$$
where,
	$\sigma_t$ = permissible tensile stress ($N/mm^2$)

## Maximum Shear Stress
![[Parallel or Longitudinal Fillet Joint-maximum shear.png#align-right|400]]
We cut a plane of with $t'$ at angle $\theta$ on the weld to get the maximum shear angle where $t' = \frac{h}{\sin\theta + \cos\theta}$ and see that,
$$\theta = 45\deg\ \ \ for\ \ \ \tau = \tau_{max}$$
Hence, maximum allowable load for single weld
$$P_{max} = 0.707\ h\ \tau_{max}$$

## Examples
### Q1.
![[Parallel or Longitudinal Fillet Joints-Q1.png#align-right|400]]
A steel plate, $100 mm$ wide and $10 mm$ thick, is welded to another steel plate by means of double parallel fillet welds as shown in Fig. The plates are subjected to a static tensile force of $50 kN$. Determine the required length of the welds if the permissible shear stress in the weld is $94 N/mm^2$.
#### ans.
We have, $P = 50kN$, $\tau = 94\ N/mm^2$, $h = 10mm$
now, 
	$P = 1.414\ h\ l\ \tau$ $\implies 50\times10^3 = (1.414)(10)(l)(94)$
	or, $l = 37.62mm$
Adding 15mm of length for dtarting and stopping of the weld run, we have,
	length of weld $(l) = 52.62\approx55mm$