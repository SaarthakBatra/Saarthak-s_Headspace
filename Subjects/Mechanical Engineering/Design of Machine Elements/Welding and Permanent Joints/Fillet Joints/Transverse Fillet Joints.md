[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=5aabe01b2a639311&file=Design%20of%20Machine%20Elements) > [Welding and Permanent Joints](obsidian://open?vault=5aabe01b2a639311&file=Welding%20and%20Permanent%20Joints) > [Fillet Joints](obsidian://open?vault=5aabe01b2a639311&file=Fillet%20Joints) > Transverse Fillet Joints

---
![[Transverse Fillet Joints - under tension.png#align-right|400]]
A single transverse fillet weld subjected to a tensile force, follows relation
$$P = 0.707\ h\ l\ \sigma_t$$
and Double transverse fillet weld follows,
$$P = 1.414\ h\ l\ \sigma_t$$
where,
	$\sigma_t$ = permissible tensile stress ($N/mm^2$)

![[Transverse Fillet Joints- maximum shaer.png#align-right|400]]
## Maximum Shear Stress
We cut a plane of with $t'$ at angle $\theta$ on the weld to get the maximum shear angle where $t' = \frac{h}{\sin\theta + \cos\theta}$ and $P_s = P\ \sin\theta$ , then
$$\tau = \frac{P\sin\theta(\sin\theta + \cos\theta)}{hl}$$
Differentiating wrt $\theta$ and setting derivative $0$, we get
$$\theta = 67.5\deg\ \ \ for\ \ \ \tau = \tau_{max}$$
Hence, maximum allowable load for single weld
$$P_{max} = 0.828
9\ h\ \tau_{max}$$

## Examples
### Q1.
![[Transverse Fillet Joints-Q1.png#align-right|400]]
Two steel plates, $120 mm$ wide and $12.5 mm$ thick, are joined together by means of double transverse fillet welds as shown in Fig. The maximum tensile stress for the plates and the welding material should not exceed $110 N/mm^2$. Find the required length of the weld, if the strength of weld is equal to the strength of the plates.

#### ans.
For plates we have, $w = 120mm$, $t = 12.5mm$
For welds we have, , $h = 12.5mm$, $\sigma_t = 110\ N/mm^2$
now, the maximum tensile force on plates is
	$P = w\ t\ \sigma_t$ $= 120\times12.5\times110$ $= 165000N$
then,
	$P = 1.414\ h\ l\ \sigma_t$ $\implies 165000 = (1.414)(12.5)(l)(110)$
	or, $l = 84.87mm$
Adding 15mm of length for starting and stopping of the weld run, we have,
	length of weld $(l) = 99.87\approx100mm$

---