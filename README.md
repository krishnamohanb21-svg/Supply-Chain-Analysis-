# Supply Chain Analysis — End-to-End Data Analytics & Power BI Dashboard
An end-to-end analytics project that cleans, explores, and visualizes supply chain operations data — spanning procurement, manufacturing, inventory, logistics, and quality — to surface cost drivers and actionable business recommendations.
# Table of Contents
Project Overview
Problem Statement
Dataset Description
Tools Used
Data Cleaning Process
Exploratory Data Analysis & Visualizations
Power BI Dashboard
Key Insights
Business Recommendations
Conclusion
# Project Overview
This project builds an end-to-end supply chain analytics platform that ingests raw procurement, manufacturing, inventory, and last-mile delivery data and turns it into actionable insight. Using Python for data cleaning and exploratory analysis and Power BI for interactive visualization, the project identifies cost drivers, quality risks, and logistics inefficiencies across the supply chain — and translates them into concrete business recommendations.
The workflow covers the full analytics lifecycle: data cleaning → exploratory data analysis → visualization → interactive dashboarding → business insight generation.
# Problem Statement of Supply Chain Analysis
Organizations possess an enormous amount of operational data on their modern supply chains, including all of their procurement, manufacturing, inventory, and shipping information, but their data is dispersed and fragmented. Because their data is separate, it results in inventory stockouts and surpluses, unreliably estimated demand, unnecessary shipping and manufacturing expenses, postponed lead times, and unmanaged supply chain risk. To alleviate and avoid these obstacles, organizations must apply an all-in-one analytical perspective, as it eliminates supply chain bottlenecks, decreases company costs, and scales for high-quality products.
# Dataset Description 
The dataset encompasses key metrics covering four critical dimensions of the supply chain lifecycle:
Product & Commercial Metrics: Product type, SKU, Price, Availability, Number of products sold, Revenue generated, Customer demographics.
Inventory & Order Logistics: Stock levels, Lead times, Order quantities, Shipping times, Shipping carriers, Shipping costs.
Supplier & Manufacturing Data: Supplier name, Location, Lead time (supplier), Production volumes, Manufacturing lead time, Manufacturing costs.
Quality & Logistics Management: Inspection results, Defect rates, Transportation modes, Routes, Costs.

Raw file: Supply_Chain.csv
Cleaned file:Supply_Chain_Cleaned.csv
# Tools Used
Category	Tools
Programming Language	Python 3
Development Environment	Jupyter Notebook
Data Analysis	Pandas, NumPy
Data Visualization	Matplotlib, Seaborn
Dashboarding / BI	Microsoft Power BI (Power Query, DAX, Data Model)
Data Format	CSV / XLSX

# Data Cleaning Process
The raw dataset was loaded and inspected in notebooks Supply_Chain Analysis.ipynb, following these steps:
Initial inspection — checked shape, column names, and data types (df.shape, df.info(), df.dtypes).
Missing value identification — ran df.isnull().sum() across all 24 columns.
Missing value handling — applied context-appropriate imputation:
Numeric fields (e.g. Price) → filled with mean
Skewed numeric fields (e.g. Defect rates) → filled with median
Categorical fields (e.g. Inspection results) → filled with mode
Duplicate detection & removal — checked df.duplicated().sum() and df.duplicated().mean() * 100 to quantify and remove exact duplicate records.
Validation — re-ran null and duplicate checks post-cleaning to confirm 0 missing values and 0 duplicate rows.
Export — saved the cleaned dataset to Supply_Chain_Cleaned.csv for downstream EDA and Power BI use.

# Exploratory Data Analysis & Visualizations
EDA covered descriptive statistics, correlation analysis, group-wise aggregation, pattern identification, and outlier detection (IQR method) — see the full notebook for code and outputs.
Product type vs. units sold <img width="1919" height="1267" alt="Chart 1" src="https://github.com/user-attachments/assets/3ff04a11-2e44-464c-88ae-e23402f992dc" />
Product type vs. revenue generated <img width="2023" height="1227" alt="Chart 2" src="https://github.com/user-attachments/assets/d9fb08c1-e4b5-494c-b8d2-27bb0b4fb52c" />
Skincare leads with ₹241,629 in total revenue, ahead of haircare (₹174,454) and cosmetics (₹161,519).
Shipping carrier vs. shipping cost <img width="1991" height="1267" alt="Chart 4" src="https://github.com/user-attachments/assets/5c5316e7-16bf-4fdf-a2fa-2ef049f46c9c" />
Carrier A runs the highest average shipping cost (₹5.64), Carrier B the lowest (₹5.44).
Transportation mode vs. total logistics cost <img width="1878" height="1169" alt="Chart 5" src="https://github.com/user-attachments/assets/d7f4e733-7f4b-45c0-bb64-ea761e725bc1" />
Road freight accounts for the largest share of total logistics cost (₹16,047), while Sea is the cheapest overall (₹7,102).
Location vs. revenue generated<img width="1943" height="1242" alt="Chart 3" src="https://github.com/user-attachments/assets/17cfd1fd-7824-4997-bbc5-29d999cbc0c4" />
Mumbai and Kolkata are the top two revenue-generating hubs.
Supplier vs. average lead time<img width="1973" height="1214" alt="Chart 6" src="https://github.com/user-attachments/assets/a51d47eb-7502-405e-b386-8eceb7d5889a" />
Supplier 3 has the longest average lead time (20 days); Supplier 1 the shortest (15 days).
Correlation heatmap<img width="2001" height="2184" alt="Chart 7" src="https://github.com/user-attachments/assets/2162c840-b99a-483f-9463-0b9e617c396f" />
Most numeric supply chain metrics are only weakly correlated — revenue, pricing, manufacturing, and shipping largely vary independently, so no single lever drives performance.
# Findings summary 
100 SKUs across 3 categories, zero missing values/duplicates after cleaning.
Revenue varies widely across products, indicating uneven portfolio performance.
Numeric supply-chain metrics are weakly correlated — revenue is driven by a mix of factors, not one variable.
Outliers exist in Defect rates, Costs, and Revenue — a handful of SKUs/orders show unusually high values.
Costs and shipping performance vary meaningfully by transport mode and carrier — a logistics optimization opportunity.
# Power BI Dashboard
An interactive Power BI report (Supply_Chain_Analysis.pbix) was built on top of the cleaned dataset, with a data model connecting Supply_Chain, Product type vs Revenue, and Product Type vs No. of products sold tables.
Power BI Dashboard <img width="2082" height="1108" alt="Power BI Dashboard" src="https://github.com/user-attachments/assets/880d6d6a-2080-4ebe-a6db-05cf2e6f2d53" />
Data model view <img width="1478" height="791" alt="image" src="https://github.com/user-attachments/assets/cd8ae406-e54e-490d-9f53-5c6b463609af" />
# Key DAX measures created:
Total Revenue         = SUM(Supply_Chain[Revenue generated])
Total Units Sold       = SUM(Supply_Chain[Number of products sold])
Average Defect Rate    = AVERAGE(Supply_Chain[Defect rates])
Average Ship Cost      = SUM(Supply_Chain[Shipping costs])
The dashboard lets a user filter and drill down by Product type, Location, Supplier, Carrier, and Transportation mode, giving supply chain, procurement, logistics, and quality stakeholders self-service visibility into revenue, cost, lead time, and defect metrics.
Open Supply_Chain_Analysis.pbix in Power BI Desktop to explore the full interactive report.
# Key Insights
1)Top-performing category: Skincare generates the highest total revenue (₹241,629); cosmetics lags behind (₹161,519).
2)Regional concentration: Mumbai contributes the highest total revenue among all locations — demand/supply is geographically concentrated.
3)Shipping carrier cost gap: Carrier A is the most expensive carrier on average; Carrier B is the most cost-efficient.
4)Transportation mode cost impact: Road freight contributes the largest share of total logistics cost, suggesting a route/mode mix review could unlock savings.
5)Quality/defect risk: Average defect rate across all SKUs is ~2.3%, with failed-inspection batches running notably higher — certain suppliers/SKUs merit quality audits.
6) Revenue vs. volume: Revenue doesn't scale purely linearly with units sold across product types — pricing strategy materially affects outcomes.
# Business Recommendations
R1	Reallocate marketing and inventory investment toward skincare (the strongest revenue generator), while investigating cosmetics' underperformance.
R2	Consolidate shipments with lower-cost, high-performing carriers (e.g., Carrier B) and renegotiate contracts with higher-cost carriers such as Carrier A.
R3	Implement stricter supplier quality audits for SKUs/suppliers with above-average defect rates to reduce failed inspections and rework costs.
R4	Optimize the transportation mode mix — shift a portion of Road volume to lower-cost alternatives where delivery-time requirements allow.
# Future scope:
1) IoT Real Time Integration : Integrate with a shipping carriers' GPS data, as well as with their telemetry data for real-time route optimization and delivery visibility.
2) Automatic Demand Forecasting : Utilize sophisticated time-series modeling techniques (ARIMA, Prophet, LSTM etc.), and customer demographic data to predict sales velocity.
3) Prescriptive Replenishment Planning : Proactively determine reorder points and auto generate purchase orders based on real-time stock levels, and vendor lead-times.
4) Sustainability and carbon footprint tracking : Measure and track emissions per mile for each transit mode and route, as a contribution to the green supply chain.
# Conclusion 
By uniting product economics, inventory logistics, manufacturing parameters, and quality metrics into a single analytical model, this project addresses the fundamental inefficiencies of fragmented supply chain management. The unified framework empowers data-driven decision-making, significantly reduces lead times and defect rates, minimizes logistics and manufacturing costs, and builds a resilient, customer-centric supply ecosystem.






