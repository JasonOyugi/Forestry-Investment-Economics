# Forestry Investment Economics

## Forest Production 

### Silviculture Costs
Annual silviculture costs for a 1 ha plantation under the following configurable scenario settings:
- Rotation $R \in \\{4,5,\dots,15\\}$ years  
- Thinning $\in \\{\text{"yes"},\text{"no"}\\}$
  - If `thinning = "no"`:
    - Silviculture runs at full (baseline) intensity in all years.
  - If `thinning = "yes"`:
    - Thinning is implemented as intensity discounts on maintenance-related costs (no thinning cost is incurred).
    - Discount timing is rotation-dependent:
      - First discount: if $R \ge 6$, a discount factor is applied starting in year 4
      - Second discount: if $R \ge 9$, a stronger discount factor is applied starting in year 7
- Quantity weighting $\lambda_q \in (min_q, max_q)$ (i.e man-days, input quantities)
- Wage / price weighting $\lambda_p \in (min_p, max_p)$ (i.e wages and unit prices)
- Labour mix $\in \\{\text{unskilled}, \text{skilled}\\}$
    - If `skilled`, unskilled man-days are converted to skilled man-days using a fixed efficiency factor

Annual costs are computed for each year $t = 1,\dots,R$. 
- Labour cost and allowance, computed as $\text{Labour cost} = \lceil \text{man-days} \rceil \cdot \text{wage} + \lceil \text{man-days} \rceil \cdot \text{allowance}$
- Consumable and operational inputs computed as $\text{quantity} \cdot \text{unit price}$
- Fixed or variable silviculture items (tools, PPE, transport, overheads) as defined in the operation library

### Forest Retail Cashflow
Cashflow for a 1 ha plantation, conditional on the silviculture costs model and the following scenario settings:
- Initial stocking $N_0$ (trees per hectare)
- Thinning schedule and prices: Each thinning year $t \in \mathcal{T}$ has an associated price per tree $p_t^{\text{thin}}$ and removes a fixed fraction $\theta_t \in (0,1)$ of the standing trees
- Final harvest: Occurs in year $R$. All remaining trees are harvested at a roundwood price per tree $p^{\text{final}}$
- Thinning revenue: $\text{Revenue}_t^{\text{thin}}=\theta_t \cdot N_t \cdot p_t^{\text{thin}}$ for $t \in \mathcal{T}$. 
- Final harvest revenue: $\text{Revenue}_R^{\text{final}} = N_R \cdot p^{\text{final}}$ at $t = R$
For each year $t = 1,\dots,R$:
- $CF_t = \text{Revenue}_t - \text{Silviculture cost}_t$
- Net Present Value (NPV): $\text{NPV} = \sum_{t=1}^{R}\frac{CF_t}{(1+r)^t}$
- Internal Rate of Return (IRR): $\sum_{t=1}^{R}\frac{CF_t}{(1+\text{IRR})^t}=0$
- Payback period: The first year $t$ for which cumulative cashflow becomes non-negative

### Roundwood Retail Cashflow
Harvest and haulage costs for a single harvest event over a plantation area of size A (ha), under the following configurable scenario settings.

Expenditure:
- Felling method $\in \\{\text{"chainsaw"},\text{"harvester"}\\}$
- Extraction method $\in \\{\text{"manual"},\text{"tractor"},\text{"belllogger"}\\}$
- Loading method $\in \\{\text{"manual"},\text{"machine"}\\}$
- Equipment regime $\in \\{\text{"rented"},\text{"owned"}\\}$
  - If `rented`: daily rental rates apply ($\lceil d \rceil \cdot \text{rental rate}$)
  - If `owned`: daily maintenance rates apply ($\lceil d \rceil \cdot \text{maintenance rate}$)

Operations (intensity parameters):
- Mensuration: $v_M \in [0,1]$
- Felling: $v_F \in [0,1]$
- Extraction: $v_E \in [0,1]$
- Loading: $v_L \in [0,1]$
- Haulage: $v_H \in [0,1]$
- Regulatory: $v_R \in [0,1]$
- Allowance: $p_{\text{allow}} \in [0,1]$
- Permit strictness: $p_{\text{permit}} \in [0,1]$ 

For each quantity specified as $(q_{\min}, q_{\max})$:
- Effort/consumption quantities increase with intensity: $\text{eff}(v) = (1-v),q_{\min} + v,q_{\max}$
- Productivity quantities (e.g. stems per day) decrease with intensity: $\text{prod}(v) = (1-v),q_{\max} + v,q_{\min}$

Price and wage weighting
- Wage weighting: $\lambda_w \in \(w_{\text{min}}, w_{\text{max}}\)$
- Price weighting: $\lambda_p \in \(p_{\text{min}}, p_{\text{max}}\)$

Site and scale parameters:
- Harvest area: $A$ (ha)
- Stems per hectare: $N_{\text{ha}}$
- Mean tree volume: $\bar v$ (m³)
- Haul distance: $D$ (km)
- Truck payload capacity: $C$ (m³ per trip)
- Labour (including allowance) and equipment cost
  - For any labour category requiring $d$ man-days: $\text{Labour cost}\lceil d \rceil \cdot \text{wage} + \left\lceil 2d \right\rceil / 2 \cdot \text{allowance}$






