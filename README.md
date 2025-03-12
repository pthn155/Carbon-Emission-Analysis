# Carbon-Emission-Analysis

![image](https://github.com/pthn155/Carbon-Emission-Analysis/blob/main/cover.jpg)

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development

### Data Source: Where our data comes from
Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).

### Data Structure: 
The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.
![image](https://github.com/pthn155/Carbon-Emission-Analysis/blob/main/Database%20diagram.png)

### Let's have a look at the data


`select *
from product_emissions pe 
limit 5`

|id|company_id|country_id|industry_group_id|year|product_name|weight_kg|carbon_footprint_pcf|upstream_percent_total_pcf|operations_percent_total_pcf|downstream_percent_total_pcf|
|--|----------|----------|-----------------|----|------------|---------|--------------------|--------------------------|----------------------------|----------------------------|
|10056-1-2014|82|28|2|2014|Frosted Flakes(R) Cereal|0.7485|2|57.50|30.00|12.50|
|10056-1-2015|82|28|15|2015|"Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)"|0.7485|2|57.50|30.00|12.50|
|10222-1-2013|83|28|8|2013|Office Chair|20.68|73|80.63|17.36|2.01|
|10261-1-2017|14|16|25|2017|Multifunction Printers|110.0|1488|30.65|5.51|63.84|
|10261-2-2017|14|16|25|2017|Multifunction Printers|110.0|1818|25.08|4.51|70.41|
###### 1. Which products contribute the most to carbon emissions?

###### 6. What is the trend of carbon footprints (PCFs) over the years?
`SELECT year, count(distinct product_name) as count_product,
sum(avg_pcf) AS sum_pcf
FROM (
  SELECT year, product_name,
  ROUND(AVG(carbon_footprint_pcf),2) AS avg_pcf
  FROM product_emissions AS prod_em
  GROUP BY year, product_name
  ) AS tb
  GROUP BY year`
| year | count_product | sum_pcf     | 
| ---: | ------------: | ----------: | 
| 2013 | 176           | 496005.50   | 
| 2014 | 186           | 548213.50   | 
| 2015 | 217           | 10810407.00 | 
| 2016 | 215           | 1608962.17  | 
| 2017 | 57            | 224799.67   | 
`SELECT prod_em.year, ind_gr.industry_group,
ROUND(AVG(carbon_footprint_pcf),2) AS avg_pcf
FROM product_emissions AS prod_em
JOIN industry_groups AS ind_gr ON ind_gr.id = prod_em.industry_group_id
GROUP BY 1, 2
ORDER BY industry_group, year, avg_pcf DESC`
| year | industry_group                                                         | avg_pcf   | 
| ---: | ---------------------------------------------------------------------: | --------: | 
| 2015 | "Consumer Durables, Household and Personal Products"                   | 116.38    | 
| 2013 | "Food, Beverage & Tobacco"                                             | 94.25     | 
| 2014 | "Food, Beverage & Tobacco"                                             | 99.44     | 
| 2015 | "Food, Beverage & Tobacco"                                             | 0.00      | 
| 2016 | "Food, Beverage & Tobacco"                                             | 4011.56   | 
| 2017 | "Food, Beverage & Tobacco"                                             | 143.73    | 
| 2015 | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 685.31    | 
| 2015 | "Mining - Iron, Aluminum, Other Metals"                                | 2727.00   | 
| 2013 | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 16135.50  | 
| 2014 | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 40215.00  | 
| 2015 | "Textiles, Apparel, Footwear and Luxury Goods"                         | 14.33     | 
| 2013 | Automobiles & Components                                               | 26037.80  | 
| 2014 | Automobiles & Components                                               | 20910.45  | 
| 2015 | Automobiles & Components                                               | 37146.68  | 
| 2016 | Automobiles & Components                                               | 40138.09  | 
| 2013 | Capital Goods                                                          | 5015.83   | 
| 2014 | Capital Goods                                                          | 10411.00  | 
| 2015 | Capital Goods                                                          | 3505.00   | 
| 2016 | Capital Goods                                                          | 796.13    | 
| 2017 | Capital Goods                                                          | 18989.80  | 
| 2015 | Chemicals                                                              | 1949.03   | 
| 2013 | Commercial & Professional Services                                     | 144.63    | 
| 2014 | Commercial & Professional Services                                     | 119.25    | 
| 2016 | Commercial & Professional Services                                     | 96.33     | 
| 2017 | Commercial & Professional Services                                     | 370.50    | 
| 2013 | Consumer Durables & Apparel                                            | 286.70    | 
| 2014 | Consumer Durables & Apparel                                            | 113.10    | 
| 2016 | Consumer Durables & Apparel                                            | 40.07     | 
| 2015 | Containers & Packaging                                                 | 373.50    | 
| 2015 | Electrical Equipment and Machinery                                     | 891050.73 | 
| 2013 | Energy                                                                 | 750.00    | 
| 2016 | Energy                                                                 | 2506.00   | 
| 2015 | Food & Beverage Processing                                             | 7.05      | 
| 2014 | Food & Staples Retailing                                               | 77.30     | 
| 2015 | Food & Staples Retailing                                               | 70.60     | 
| 2016 | Food & Staples Retailing                                               | 0.50      | 
| 2015 | Gas Utilities                                                          | 61.00     | 
| 2013 | Household & Personal Products                                          | 0.00      | 
| 2013 | Materials                                                              | 4177.35   | 
| 2014 | Materials                                                              | 1513.56   | 
| 2016 | Materials                                                              | 1401.06   | 
| 2017 | Materials                                                              | 11217.74  | 
| 2013 | Media                                                                  | 2411.25   | 
| 2014 | Media                                                                  | 2411.25   | 
| 2015 | Media                                                                  | 479.75    | 
| 2016 | Media                                                                  | 602.67    | 
| 2014 | Retailing                                                              | 6.33      | 
| 2015 | Retailing                                                              | 5.50      | 
| 2014 | Semiconductors & Semiconductor Equipment                               | 16.67     | 
| 2016 | Semiconductors & Semiconductor Equipment                               | 2.00      | 
| 2015 | Semiconductors & Semiconductors Equipment                              | 1.00      | 
| 2013 | Software & Services                                                    | 1.50      | 
| 2014 | Software & Services                                                    | 29.20     | 
| 2015 | Software & Services                                                    | 1523.73   | 
| 2016 | Software & Services                                                    | 2538.44   | 
| 2017 | Software & Services                                                    | 690.00    | 
| 2013 | Technology Hardware & Equipment                                        | 1053.45   | 
| 2014 | Technology Hardware & Equipment                                        | 1780.44   | 
| 2015 | Technology Hardware & Equipment                                        | 1895.66   | 
| 2016 | Technology Hardware & Equipment                                        | 65.25     | 
| 2017 | Technology Hardware & Equipment                                        | 788.34    | 
| 2013 | Telecommunication Services                                             | 52.00     | 
| 2014 | Telecommunication Services                                             | 45.75     | 
| 2015 | Telecommunication Services                                             | 45.75     | 
| 2015 | Tires                                                                  | 1011.00   | 
| 2015 | Tobacco                                                                | 1.00      | 
| 2015 | Trading Companies & Distributors and Commercial Services & Supplies    | 39.83     | 
| 2013 | Utilities                                                              | 61.00     | 
| 2016 | Utilities                                                              | 61.00     | 

