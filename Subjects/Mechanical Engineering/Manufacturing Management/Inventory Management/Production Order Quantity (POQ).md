[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Manufacturing Management](obsidian://open?vault=5aabe01b2a639311&file=Manufacturing%20Management) > [[Inventory Management]] > Production Order Quantity (POQ)

---
Used when units are produced and sold simultaneously i.e order is received gradually as inventory is simultaneously depleted

## Assumptions
1. Only one product is involved (one SKU(stock keeping unit))
2. Demand is known and independent of decisions for other items
3. Usage rate is constant
4. Usage is a continuous process while production is a periodical process
5. Production rate is constant
6. Lead time (time between placement and receipt of an order) is know and constant
7. Quantity discounts are not possible
## Model
![[Production Order Quantity (POQ) - Inventory Level.png#align-right|Inventory Level|400x200]]
![[Production Order Quantity (POQ) - Lnventory Level 2.png#align-right|400x200]]
- Order Quantity = $Q$
- Average Inventory = $\frac{Q}{2}$
- Production Rate = $p$
- Inventory Demand per period = $d$
- Cost of placing order = $C_0$
- Annual per-unit carrying cost = $C_c$
- Annual Demand = $D$

### Production Run Quantity
$$Q_p = \sqrt{(\frac{2DC_0}{C_c})(\frac{p}{p-d})}$$

### Total Annual Cost
$$\text{Total cost} = \frac{C_0 D}{Q}+\frac{C_CI_{max}}{2}$$
- where,
	- Maximum Inventory Level, $I_{max} = Q(1-\frac{d}{p})$
	- Number of production runs, $N=\frac{D}{Q}$
	- Expected time b/w orders = $\frac{\text{Total Time Period}}{N}$
	- 