[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=5aabe01b2a639311&file=Design%20of%20Machine%20Elements) > [Welding and Permanent Joints](obsidian://open?vault=Saarthak's_Headspace&file=Welding%20and%20Permanent%20Joints) > [[Fillet Joints]] > Eccentric Loading Perpendicular to Weld

---
![[Torsional Moment on Weld.png#align-right|400]]
- Welded to the plate by means of a circumferential fillet weld
- The shaft is subjected to torsional moment $M_t$ that induced torsional shear stresses weld
![[Torsional Moment on Weld-1.png#align-right|400]]
Considering an elemental section of area $\delta A$ at an angle $\theta$, subtending an angle $\delta\theta$ , then
$$\delta(I_{xx}) = \delta A\times y^2=(rd\theta t)(r\sin\theta)^2 =tr^3\sin^2\theta d\theta$$
Moment of inertia of 4 welds about X-axis is,
$$
I_{xx}=2\int_0^{\pi}tr^3\sin^2\theta d\theta=2tr^3(\frac{\pi}{2})= \pi tr^3
$$
- By symmetry, $I_{xx} = I_{yy}$
The polar moment of inertia is given as, 
$$J=I_{xx}+I_{yy}=2\pi tr^3$$
The torsional shear stress in weld is given as,
$$\tau = \frac{M_tr}{J} = \frac{M_tr}{2\pi tr^3}$$
