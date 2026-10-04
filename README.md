# BrewMetrics BI

## What this project does
A version-controlled Power BI solution built for BrewMetrics Coffee Co. to analyze sales trends, city performance gaps, and store format effectiveness across retail locations[cite: 1]. The implementation demonstrates end-to-end business intelligence practices, including data cleaning in Power Query, star schema modeling, Copilot-assisted DAX development, and interactive dashboard creation[cite: 1].

## Data Model
The solution transforms raw transaction records into a star schema data model[cite: 1]:
* **Fact_Sales**: Contains core transactional records at the sale grain (`sale_id`, `date`, `city`, `store_format`, `item`, `quantity`, `unit_price`, `sales_amount`)[cite: 1, 3].
* **Dim_Date**: Date dimension query derived from transaction dates containing `Date`, `Year`, `Month`, `MonthName`, `Day`, `Week`, and `Quarter`[cite: 1, 3].
* **Dim_City**: Cleaned city dimension query containing 4 distinct cities (`Bengaluru`, `Chennai`, `Hyderabad`, `Coimbatore`)[cite: 1, 3].
* **Dim_Product**: Product catalog dimension query containing `category` and `item` details[cite: 1, 3].
* **Relationships**: Clean 1-to-many ($1:*$), single-direction filter relationships from each dimension table to `Fact_Sales`[cite: 1, 3].

### Data Cleaning Highlights
* Fixed a spelling typo in the raw data where `"Chenn"` was mapped to `"Chennai"`[cite: 1, 2].
* Removed incomplete record rows containing null values across city, format, and category fields[cite: 1, 2].

## Key Insights
1. **Cold Brew Seasonal Demand**: Cold Brew demonstrates clear demand spikes across April, peaking near $13K–$13.6K in revenue periodically[cite: 1, 15].
2. **City Revenue Dominance**: Bengaluru leads overall revenue across all store formats ($71.5K), outperforming Chennai ($64.9K), Hyderabad ($59.9K), and Coimbatore ($48.4K)[cite: 1, 15].
3. **Store Format & Basket Size Dynamics**: Flagship stores drive the highest total volume ($113.0K across all cities), while Kiosks maintain competitive average basket sizes (~$415.77), indicating high transaction efficiency per customer footprint[cite: 8, 15].

## Tools Used
* Power BI Desktop (`.pbip` format)
* GitHub & Git Command Line[cite: 1, 6]
* GitHub Copilot Extension in VS Code[cite: 1, 6]