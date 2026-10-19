# Retail Inventory and Replenishment Optimization

An Excel project that uses historical retail sales and inventory data to analyse demand, identify stock risks, and calculate replenishment recommendations.

## Project files

| File | Contents |
|---|---|
| `Original_Data.xlsx` | Original sales, products, stores, and inventory data. |
| `Retail_Inventory_Optimization.xlsx` | Dashboard, analysis, forecasts, planning assumptions, and validation checks. |

The project workbook contains its source data.

## Dataset

The project uses the Maven Toys retail dataset.

| Item | Coverage |
|---|---|
| Sales period | 1 January 2017 to 30 September 2018 |
| Inventory date | 1 October 2018 |
| Sales records | 829,262 |
| Products | 35 |
| Stores | 50 |
| Recorded store-product inventory pairs | 1,593 |

Revenue is calculated as units sold multiplied by the catalogue selling price. Historical discounts and price changes are not available.

## Workbook sections

| Worksheet | Purpose |
|---|---|
| Executive Dashboard | Summarises sales, inventory, stock risks, and key comparisons using charts and slicers. |
| Sales Data | Holds sales transactions and supporting demand summaries. |
| Product Data | Shows product prices, costs, margins, and demand information. |
| Store Data | Contains store names, cities, locations, and opening dates. |
| Inventory Data | Analyses stock on hand, inventory value, demand, and coverage. |
| ABC Analysis | Classifies products by annual consumption value. |
| Demand Forecasting | Calculates a 30-day moving-average forecast and evaluates a historical holdout period. |
| Inventory Optimization | Contains editable planning assumptions and replenishment calculations. |
| Stockout Analysis | Prioritises store-product pairs requiring attention. |
| Validation Checks | Compares calculated totals with source controls. |

## How I did it

1. Organised the sales, product, store, and inventory data into separate tables.
2. Used Power Query to clean and prepare the data, check keys, join related tables, and create daily and monthly summaries.
3. Calculated sales revenue, margins, inventory value, and demand measures using Excel formulas.
4. Applied ABC analysis to classify products by annual consumption value.
5. Built a 30-day moving-average forecast and compared a historical holdout forecast with actual sales.
6. Calculated EOQ, safety stock, reorder points, and recommended orders using editable planning assumptions.
7. Created PivotTables, charts, and slicers to present the results in the dashboard.
8. Checked totals against the original data and tested how changing planning assumptions affected the recommendations.


### Editable planning inputs

The amber cells on **Inventory Optimization** contain the main planning inputs. Record the starting values before trying a scenario so you can restore the original case.

| Input | What it controls |
|---|---|
| Supplier lead time | Expected time between placing and receiving an order. It affects lead-time demand, safety stock, and reorder points. |
| Ordering cost | Assumed cost of placing one order. It affects EOQ. |
| Annual holding cost rate | Annual inventory carrying cost as a proportion of unit cost. It affects EOQ and estimated holding costs. |
| Cycle service level | Target used to calculate the safety-stock allowance. It is not the same as order fill rate. |
| Demand multiplier | Scales demand statistics for an inventory-planning scenario. It does not rewrite the historical sales data. |

For a simple demonstration, increase supplier lead time, inspect the resulting reorder points and recommended orders, then restore the starting value. Keep units consistent: lead time is in days, service level and holding rate are percentages, and ordering cost is per order.

### Reading the results

| Result | Meaning |
|---|---|
| EOQ | Economic order quantity under the model's cost assumptions. |
| Safety stock | Extra stock allowance for demand variability during lead time. |
| Reorder point | Stock threshold used to trigger replenishment. |
| Coverage days | Approximate number of days that current stock can support at the estimated demand rate. |
| Stockout Risk | Stock is below expected demand during the assumed lead time. |
| Reorder Soon | Stock covers expected lead-time demand but is at or below the reorder point. |
| Sufficient Stock | Stock is above the reorder point. |
| MAE | Mean absolute error: average absolute difference between forecast and actual quantities in the holdout period. Lower values indicate smaller errors for that evaluation. |

Risk and replenishment counts usually refer to **store-product pairs**. A distinct-product count measures something different because the same product can need replenishment at several stores.


## Analysis methods

| Method | Approach |
|---|---|
| ABC classification | Ranks annual demand multiplied by unit cost. Class A includes the product crossing 80% of cumulative consumption value; class B includes the product crossing 95%; remaining products are class C. |
| Annual demand | Uses the last 365 days of recorded sales. |
| Daily demand statistics | Uses 90 calendar days, including days with zero sales. |
| Demand forecast | Uses average daily sales over the latest 30 days, multiplied by 30. |
| EOQ | Estimates order quantity from annual demand, ordering cost, and annual holding cost per unit. |
| Safety stock | Uses demand variability, assumed lead time, and the selected service level. |
| Reorder point | Combines expected demand during lead time with safety stock. |
| Recommended order | When stock is at or below the reorder point, orders toward reorder point plus EOQ, rounded up to whole units. |

### Forecast period and evaluation

The next forecast covers **1–30 October 2018**, based on the historical data supplied. It is not a forecast for the current year.

For evaluation, the September 2018 forecast is calculated using sales from 2–31 August 2018 and compared with actual September sales. September actuals are not used to fit that holdout forecast.

This is a simple statistical baseline, not an AI prediction model. The charts also show actual demand against a prior 30-day moving average.

## Assumptions and limitations

- Lead time, ordering cost, holding cost rate, and service level are planning assumptions, not observed supplier terms.
- There are 157 store-product combinations without inventory records. These are unknown quantities and are excluded from inventory risk counts.
- Sales may understate demand when products were out of stock. Historical stockout rates cannot be measured from this dataset.
- The moving average does not explicitly model seasonality, promotions, or changing market conditions. One holdout period does not establish year-round forecast accuracy.
- Inventory position is approximated using stock on hand. Supplier schedules, open purchase orders, backorders, minimum order quantities, capacity, and expiry constraints are unavailable.
- Existing analysis ranges cover the supplied dataset. Adding periods, products, or stores requires reviewing query outputs, formulas, and chart ranges.
- Written dashboard findings describe the original full-data planning case; they do not automatically rewrite themselves when assumptions or filters change.

The recommendations are model outputs for analysis and planning. They do not demonstrate realised cost savings or guarantee future results.
