[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=Saarthak's_Headspace&file=Mechanical%20Engineering) > [Manufacturing Management](obsidian://open?vault=Saarthak's_Headspace&file=Manufacturing%20Management) > [Forecasting Methods](obsidian://open?vault=Saarthak's_Headspace&file=Forecasting%20Methods) > [Quantitative Methods](obsidian://open?vault=Saarthak's_Headspace&file=Quantitative%20Methods) > Exponential Smoothing

---
A weighted moving average forecasting techniques in which data points are weighted by an exponential function
- Smooths out irregular fluctuations
- As value of "$n$" increases, forecast become smoother but less sensitive to recent changes
$$F_t = F_{t-1}+\alpha(A_{t-1} - F_{t-1})$$
- where, 
	- $F_t$ = New forecast for period t
	- $F_{t-1}$ = Previous periods forecast
	- $A_{t-1}$ =Previous periods actual demand
	- $\alpha$ = Smoothing constant
	- $(A-F)$ = Error term

## Smoothing Constant


---
#incomplete