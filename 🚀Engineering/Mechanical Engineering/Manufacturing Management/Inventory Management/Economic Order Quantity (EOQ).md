[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=Saarthak's_Headspace&file=Mechanical%20Engineering) > [Manufacturing Management](obsidian://open?vault=Saarthak's_Headspace&file=Manufacturing%20Management) > [Inventory Management](obsidian://open?vault=Saarthak's_Headspace&file=Inventory%20Management) > Economic Order Quantity (EOQ)

---
A classic model developed to minimize total annual inventory cost

## Assumptions
1. Only one product is involved (one SKU(stock keeping unit))
2. Demand is known, constant and independent of decisions for other items
3. The entire order quantity (Q) is received in a single delivery
4. No shortages
5. Lead time (time between placement and receipt of an order) is know and constant
6. Quantity discounts are not possible
7. Only two types of costs are relevant
	1. setup/order costs
	2. holding/carrying costs
8. Stockouts (shortages) can be completely avoided if orders are placed at the right time

## Model
![[Basic Economic Order Quantity (EOQ) - Inventory Cycle.png#align-right|Inventory Cycle|400x200]]
Classic economic model that **minimizes** Total Cost
- Order Quantity = $Q$
- Average Inventory = $\frac{Q}{2}$
- Reorder Point (ROP) = $R$
- Cost of placing order = $C_0$
- Annual per-unit carrying cost = $C_c$
- Annual Demand = $D$

### Average Inventory Levels and Number of Orders
![[Economic Order Quantity (EOQ) - Average Inventory Level and Number of Orders.png#align-right|400x300]]
Keeping Total Annual Orders constant, we can order in two ways
1. Small order quantity per order but more number of orders
	- Average Inventory Levels are low
	- Low holding costs
	- High ordering costs
2. Big order quantity per order but small number of orders
	- Average Inventory Levels are high
	- High holding costs
	- Low ordering costs

### Total Annual Cost
Annual set-up cost + Annual holding cost
![[Economic Order Quantity (EOQ) - Q vs Annual Cost.png#align-right|Order quantity vs Annual Cost|400x200]] 
$$\text{Total cost} = \frac{C_0 D}{Q}+\frac{C_CQ}{2}$$
- where,
	- $\frac{C_0D}{Q}$ = Annual ordering cost
	- $\frac{C_cQ}{2}$ = Annual carrying cost

### Optimal Order Quantity ($Q_{opt}$)
Differentiating Total Cost and finding the point of minima
$$Q_{opt} = \sqrt{\frac{2C_0D}{C_c}}$$
- where,
	- At $Q_{opt}$ we have, $$\frac{C_0D}{Q} = \frac{C_cQ}{2}$$
	- Orders per year, $$N = \frac{D}{Q}$$


### Re-Order Point (ROP)
![[Economic Order Quantity (EOQ) - Safety Stock.png#align-right|400x250]]
Inventory level at which a new order is placed
$$R = dL$$
- where,
	- $d$ = demand rate per period = $\frac{D}{\text{Time Period}}$
	- $L$ = lead time
	- Safety Stock = Stack held in excess of expected demand due to variable demand rate and lead time

---
#incomplete