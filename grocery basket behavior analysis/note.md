# Grocery Basket Analysis — methodology and store management notes

## Rebuilding shopping visits

The original dataset is item-level: one row represents one recorded product purchase. For this analysis, I treated a shopping visit as a unique combination of `Member_number` and `Date`.

That produces **14,963 baskets** from **38,765 item rows**. The data covers **3,898 customers**, **167 products**, and dates from **1 January 2014 to 30 December 2015**.

I kept repeated member-date-product rows in basket size and product purchase counts because they can represent repeated units of the same product. For product co-occurrence, I used only unique products inside each basket so the same repeated item does not multiply a pair count.

Purchase frequency is the number of unique shopping dates per member.

The frequency requirement has an overlap between `6–10 visits` and `10+ visits`. To avoid assigning a customer with exactly 10 visits to two groups, I used these mutually exclusive segments:

- 1 visit
- 2–5 visits
- 6–10 visits
- 11+ visits

## Reading the basket pattern

The average basket contains **2.59 items**, the median is **2**, and the largest basket contains **11 items**.

The strongest pattern is the dominance of two-item baskets: **67.37% of all baskets contain exactly two items**. This makes the data look more like frequent small missions than large weekly stock-up trips.

For store layout, I would treat that as an opportunity to create one additional purchase around common staple missions. Small complementary displays near high-demand items, checkout-adjacent convenience products, and simple cross-merchandising can be more useful here than designing only for large baskets.

## Using staple demand for inventory and placement

The top products by purchase count are:

- **whole milk — 2,502**
- **other vegetables — 1,898**
- **rolls/buns — 1,716**

Whole milk is also involved in several of the strongest product pairs. The most common pair is **other vegetables + whole milk**, which appears in **222 baskets**. Other strong milk combinations include rolls/buns, soda and yogurt.

For inventory planning, these staples should have a higher replenishment priority because a stockout would affect many shopping missions. For layout, the pair results can be used for cross-merchandising or nearby secondary displays, especially where the goal is to turn a two-item basket into a three-item basket.

## Separating traffic from basket depth

Thursday has the highest number of shopping visits with **2,188 baskets**. Monday is the lowest with **2,067**, so the busiest and quietest weekdays differ by only about **5.9%**.

That means weekday traffic is fairly balanced rather than concentrated in one extreme peak day. I would still give Thursday slightly more attention for shelf replenishment and checkout coverage, but I would not redesign staffing around a single weekday spike.

Average basket size is highest on Wednesday at roughly **2.61 items**, while Thursday is lower at roughly **2.57**. The averages are close across the entire week, which suggests that weekday differences are mainly about the number of visits rather than major changes in how much each visitor buys.

## Looking at customer frequency without overvaluing a few shoppers

The customer frequency groups are strongly concentrated in the middle:

- **349 customers (8.95%)** made 1 visit
- **2,819 customers (72.32%)** made 2–5 visits
- **725 customers (18.60%)** made 6–10 visits
- **5 customers (0.13%)** made 11 visits

The ten most active customers generate only **0.70% of all baskets**. This is a low concentration, so store demand is not dependent on a tiny group of heavy shoppers.

For retention activity, I would focus more on moving customers from the 2–5 visit group into the 6–10 visit group than on building a strategy around a very small VIP segment. For inventory planning, the low concentration also means product demand should be managed around broad customer behavior rather than the preferences of a few individuals.

## Four store management takeaways

**Keeping staple availability extremely reliable.** Whole milk, vegetables and rolls/buns are the most frequently purchased products, and milk appears in several leading product combinations. These products should receive frequent stock checks and replenishment priority.

**Designing for one more item in small baskets.** Two-item baskets represent 67.37% of visits. Complementary placement and small impulse additions around staple zones can target basket expansion without depending on large shopping trips.

**Planning slightly more operational capacity for Thursday, not a full peak-day strategy.** Thursday leads transaction volume, but the weekday spread is narrow. A modest increase in replenishment or checkout attention is more justified than a large staffing shift.

**Growing medium-frequency customers instead of relying on VIPs.** Most customers sit in the 2–5 visit segment and the top ten shoppers account for only 0.70% of baskets. Retention efforts have more room to scale by increasing repeat visits across the broad middle of the customer base.
