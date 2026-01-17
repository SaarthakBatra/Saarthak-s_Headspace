[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=Saarthak's_Headspace&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=Saarthak's_Headspace&file=Design%20of%20Machine%20Elements) > [Welding and Permanent Joints](obsidian://open?vault=Saarthak's_Headspace&file=Welding%20and%20Permanent%20Joints) > [Fillet Joints](obsidian://open?vault=Saarthak's_Headspace&file=Fillet%20Joints) > [Eccentric Loading](obsidian://open?vault=Saarthak's_Headspace&file=Eccentric%20Loading) > Bending Moment on Weld

---
![[Bending Moment on Weld-1.png#align-right|400]]
![[Bending Moment on Weld.png#align-right|400]]

## Primary Shear Stress
-  The force P through the plane of welds causes the primary shear stress $\tau_1$ ,
$$\tau_i = \frac{P}{A}$$
where,
	$A$ = Throat are of all welds
## Secondary Shear Stress
- The moment $M_b$ causes bending stresses in the welds $\sigma_b$,
$$\sigma_b = \frac{M_b\ y}{I}$$
where, 
	$y$ = distance of point in weld from Neutral-axis
	$I$ = moment of inertial of all welds based on throat area
The polar moment of inertia of a weld about $X-axis$ using $W_i$ and parallel axis theorem is,
$$
\begin{align}
I_{xx} = \frac{bt^3}{12}+bt(\frac{d}{2})^2&\approx bt(\frac{d}{2})^2\ \ \ [\because t<<b]\\
\implies I = 2I_{xx} &=t(\frac{bd^2}{2})
\end{align}
$$
where, 
	$r_1$ = distance between $G_1$ and $G$

## Resultant Shear Stress
$$\tau=\sqrt{(\frac{\sigma_b}{2})^2+\tau_1^2}$$
## Examples
### Q1.
A beam of rectangular crosssection is welded to a support by means of fillet welds as shown in Fig. Determine the size of the welds, if the permissible shear stress in the weld is limited to $75\ N/mm^2$.
![[Bending Moment on Weld-Q1.png#align-right|400]]
#### ans.
We have, $P=25kN$, $\tau=75\ N/mm^2$
##### Primary Shear Stress
![[Bending Moment on Weld-ans1.png#align-right|400]]
Area of welds is,
$$A=2[100t+150t]=500t\ mm^2$$
Hence, the primary shear stress in welds is,
$$\tau_1 = \frac{P}{A}=\frac{25000}{500t}=\frac{50}{t}\ N/mm^2$$
##### Bending Stress
Moment of inertia of 4 welds about X-axis is,
$$
I_{xx}=2[\frac{bt^3}{12}+bt(\frac{d}{2})^2]+2[\frac{td^3}{12}]=t[\frac{bd^2}{2}+\frac{d^3}{6}]= 1687500t\ mm^4\
$$
Hence, the bending stress is
$$\sigma_b=\frac{M_b\ y}{I}=\frac{25000\times500\times75}{1687500t}=\frac{555.55}{t}\ N/mm^2$$
##### Maximum Shear Stress
$$\tau = \sqrt{(\frac{\sigma_b}{2})^2+\tau_1^2}=\sqrt{(\frac{555.55}{2t})^2+(\frac{50}{t})^2}=\frac{28
2.24}{t}\ N/mm^2$$

##### Size of Weld
The permissible shear stress gives, $\tau = 75 = \frac{282.24}{t}$ $\implies t=3.76mm$
hence,
$$h=\frac{t}{0.707}=5.32mm\approx6mm$$





### Q2.
A circular beam, $50 mm$ in diameter, is welded to a support by means of a fillet weld as shown in Fig. Determine the size of the weld, if the permissible shear stress in the weld is limited to $100\ N/mm^2$.
![[Bending Moment on Weld-Q1-1.png#align-right|400]]

#### ans.
We have, $P=10kN$, $\tau=100\ N/mm^2$
##### Primary Shear Stress
Area of welds is,
$$A=\pi Dt=50\pi t\ mm^2$$
Hence, the primary shear stress in welds is,
$$\tau_1 = \frac{P}{A}=\frac{10000}{50\pi t}=\frac{63.66}{t}\ N/mm^2$$
##### Bending Stress
![[Bending Moment on Weld-ans1-1.png#align-right|400]]
Considering an elemental section of area $\delta A$ at an angle $\theta$, subtending an angle $\delta\theta$ , then
$$\delta(I_{xx}) = \delta A\times y^2=(rd\theta t)(r\sin\theta)^2 =tr^3\sin^2\theta d\theta$$
Moment of inertia of 4 welds about X-axis is,
$$
I_{xx}=2\int_0^{\pi}tr^3\sin^2\theta d\theta=2tr^3(\frac{\pi}{2})= \pi tr^3
$$
Hence, the bending stress is
$$\sigma_b=\frac{M_b\ y}{I}=\frac{10000\times200\times25}{\pi t 25^3}=\frac{1018.59}{t}\ N/mm^2$$
##### Maximum Shear Stress
$$\tau = \sqrt{(\frac{\sigma_b}{2})^2+\tau_1^2}=\sqrt{(\frac{1018.59}{2t})^2+(\frac{63.66}{t})^2}=\frac{513.26}{t}\ N/mm^2$$


##### Size of Weld
The permissible shear stress gives, $\tau = 100 = \frac{513.26}{t}$ $\implies t=5.13mm$
hence,
$$h=\frac{t}{0.707}=7.26mm\approx8mm$$



---
#incomplete