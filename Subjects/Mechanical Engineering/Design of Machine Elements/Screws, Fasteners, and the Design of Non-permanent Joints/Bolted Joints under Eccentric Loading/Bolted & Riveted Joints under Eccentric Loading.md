[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=5aabe01b2a639311&file=Design%20of%20Machine%20Elements) > [[Screws, Fasteners, and the Design of Non-permanent Joints]] > Bolted Joints under Eccentric Loading

---
## Cases of Applied Load
1. [[Parallel to axis of bolts]]
2. [[Perpendicular to axis of bolts]]
3. [[In the plane of bolts]]

## Examples
### Q1
![[Case2 + Case3 - Q1.png#align-right|300]]
Fiq. shows a solid forged bracket to carry a vertical load of 13.5kN applied through the center of hole. The square flang is secured to the flat side of vertical column through four bolts. Calculate the diameter of the bolts, if the permissible stress is 65MPa in shear.
Given: $W = 13.5 \times10^3\ N$, $\tau = 65\ N/mm^2$, $n=4$

ans. 
$F_{s_1} =\frac{W}{n}$ $= \frac{13.5 \times 10^3}{4}$ $= 3375N$

We have two eccentricities here
#### ans.
##### Part 1 : Case 2
- Tensile Load
- $e/l = 300 mm$
- $F_t = \frac{(Wl)l_{max}}{\sum_i^nl_i^2}$ $= \frac{13.5\times10^3\times300\times237.5}{37.5^2+37.5^2+237.5^2+237.5^2}$ $= 8318.9N$

##### Part 2 : Case 3
- Torsional Shear Load
- $e/l = 250 mm$
- $r = \sqrt{100^2 + 100^2}$ $= 141.4mm$
- $\theta = \tan^{-1}(\frac{100}{100})$ $= 45\deg$
- $F_{s_2} = \frac{We}{nr}$ $= \frac{13.5\times10^3\times250}{4\times141.4}$ $=5967.1N$
###### Equivalent Shear Load(case3)
$F_s = \sqrt{F_{s_1}^2 + F_{s_2}^2 + 2F_{s_1}F_{s_2}cos\theta}$ $= \sqrt{3375^2+5967.1^2+2\times3375\times5967.1\times\cos(45\deg)}$ $= 8687.8N$

###### Equivalent Shear Load(System)
$F_{s_{eq}} = \frac{1}{2}[\ \sqrt{F_t^2 + 4F_s^2}\ ]$ $= \frac{1}{2}[\ \sqrt{8318.9^2 + 4\times8687.8^2}\ ]$ $= 9632.2N$

##### Bold Diameter
We know, $F_s = \frac{\pi}{4}d_c^2\tau$
i.e $9632.2 = \frac{\pi}{4}d_c^2\times65$
$\implies d_c = 13.7mm$
$\therefore\ \ d = 1.2d_c = 16.44mm$
