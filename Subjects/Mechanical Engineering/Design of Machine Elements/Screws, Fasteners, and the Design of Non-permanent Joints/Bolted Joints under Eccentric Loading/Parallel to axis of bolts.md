[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Design of Machine Elements](obsidian://open?vault=5aabe01b2a639311&file=Design%20of%20Machine%20Elements) > [Screws, Fasteners, and the Design of Non-permanent Joints](obsidian://open?vault=5aabe01b2a639311&file=Screws,%20Fasteners,%20and%20the%20Design%20of%20Non-permanent%20Joints) > [[Bolted & Riveted Joints under Eccentric Loading]] > Parallel to axis of bolts

---

![[Parallel to the axis of the bolt.png]]
- Applied load W is parallel to the axis passing through the center of the bolts and acting in a different plane than the bolts
![[Parallel to the axis of the bolt - Primary Load.png#align-right|300x300]]

## Primary Load
- Tensile Load
- Without considering eccentricity (e), assume load acts directly on the bolt
- The load acts directly on the bolts
- Point C acts as the **Pivot Point**
- Primary Load (Tensile): 
	$F_{t1} = \frac{W}{n}$
	where
	$W$ = Total applied load
	n = Total number of bolts


## Secondary Load
- Tensile Load
- Considering the eccentricity (distance of load from bolt)
- Tries to rotate assembly about A
- Point A is **Pivot Point**
- Load on point i $(W_i)$ = $wl_i$
	where 
	$w$ (Weight per unit length) = $\frac{W}{l}$
	$l_i$ =  distance of bolt $i$ from the pivot point
![[Parallel to the axis of the bolt - Secondary load.png#align-right|300x300]]
- Taking moment about A, we have
	$Wl = \sum_{i = 1}^{i = n} W_il_i$
	$Wl = w\sum_{i = 1}^{i = n} l_i^2$ 
	where
	$n$ = number of bolts
- Secondary Load(Tensile): 
	$F_{t2} = W_{max} = \frac{(Wl)l_{max}}{\sum_i^nl_i^2}$
	where
	$W_{max}$ = Maximum Load on a bolt
	$W$ = Total Load
	l = Distance of applied load from pivot point
	$l_{max}$ = Maximum length of a bolt from pivot point
	$l_i$ = Distance of bolt $i$ from pivot point
	n = number of bolts

## Total tensile load - $F_t = F_{t1} + F_{t2}$


 