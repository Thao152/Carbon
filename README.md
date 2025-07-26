# Carbon
```
select
product_name,
carbon_footprint_pcf
from product_emissions
order by carbon_footprint_pcf desc
limit 10                                                                              
```
| product_name                                                                                                                       | carbon_footprint_pcf | 
| ---------------------------------------------------------------------------------------------------------------------------------: | -------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044              | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187              | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608              | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625              | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687               | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000               | 
| TCDE                                                                                                                               | 99075                | 
| TCDE                                                                                                                               | 99075                | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000                | 
| Electric Motor                                                                                                                     | 87589                | 

2. What are the industry groups of these products?

There are industry group of top 10 products contribute the most to carbon emissions:
```
select
  prod.product_name,
  ins.industry_group,
  avg(prod.carbon_footprint_pcf) as carb_footprint
from product_emissions prod
  left join industry_groups ins
  on prod.industry_group_id = ins.id
group by prod.product_name, ins.industry_group
order by avg(prod.carbon_footprint_pcf) desc
limit 10
```
| product_name                                                                                                                       | industry_group                     | carb_footprint | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------------------------: | -------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 3718044.0000   | 
| Wind Turbine G132 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 3276187.0000   | 
| Wind Turbine G114 2 Megawats                                                                                                       | Electrical Equipment and Machinery | 1532608.0000   | 
| Wind Turbine G90 2 Megawats                                                                                                        | Electrical Equipment and Machinery | 1251625.0000   | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | Automobiles & Components           | 191687.0000    | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | Materials                          | 167000.0000    | 
| TCDE                                                                                                                               | Materials                          | 99075.0000     | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | Automobiles & Components           | 91000.0000     | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | Automobiles & Components           | 85000.0000     | 
| Mercedes-Benz SL (SL 350)                                                                                                          | Automobiles & Components           | 72000.0000     | 


cau 3
```
select i.industry_group, sum(p.carbon_footprint_pcf) as "Total Pcf"
from product_emissions p
left join industry_groups i on p.industry_group_id = i.id
group by 1
order by 2 desc
limit 10
```

| industry_group                                   | Total Pcf | 
| -----------------------------------------------: | --------: | 
| Electrical Equipment and Machinery               | 9801558   | 
| Automobiles & Components                         | 2582264   | 
| Materials                                        | 577595    | 
| Technology Hardware & Equipment                  | 363776    | 
| Capital Goods                                    | 258712    | 
| "Food, Beverage & Tobacco"                       | 111131    | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 72486     | 
| Chemicals                                        | 62369     | 
| Software & Services                              | 46544     | 
| Media                                            | 23017     | 

cau 4
```
select c.company_name, sum(p.carbon_footprint_pcf) as "Total Pcf"
from product_emissions p
left join companies c on p.company_id = c.id
group by 1
order by 2 desc
limit 10
```
| company_name                            | Total Pcf | 
| --------------------------------------: | --------: | 
| "Gamesa Corporación Tecnológica, S.A."  | 9778464   | 
| Daimler AG                              | 1594300   | 
| Volkswagen AG                           | 655960    | 
| "Mitsubishi Gas Chemical Company, Inc." | 212016    | 
| "Hino Motors, Ltd."                     | 191687    | 
| Arcelor Mittal                          | 167007    | 
| Weg S/A                                 | 160655    | 
| General Motors Company                  | 137007    | 
| "Lexmark International, Inc."           | 132012    | 
| "Daikin Industries, Ltd."               | 105600    | 


cau 5
```
select co.country_name, sum(p.carbon_footprint_pcf) as "Total Pcf"
from product_emissions p
left join countries co on p.country_id = co.id
group by 1
order by 2 desc
limit 5
```
| country_name | Total Pcf | 
| -----------: | --------: | 
| Spain        | 9786130   | 
| Germany      | 2251225   | 
| Japan        | 653237    | 
| USA          | 518381    | 
| South Korea  | 186965    | 


cau 6
```
select year, sum(carbon_footprint_pcf) as carb_footprint
from product_emissions
group by 1
order by 1 asc
```
| year | carb_footprint | 
| ---: | -------------: | 
| 2013 | 503857         | 
| 2014 | 624226         | 
| 2015 | 10840415       | 
| 2016 | 1640182        | 
| 2017 | 340271         | 

```
select p.year, i.industry_group, sum(p.carbon_footprint_pcf) as "Total PCF"
from product_emissions p
join industry_groups i
on p.industry_group_id=i.id
group by 1,2
order by 2 asc, 1 asc
```
| year | industry_group                                                         | Total PCF | 
| ---: | ---------------------------------------------------------------------: | --------: | 
| 2015 | "Consumer Durables, Household and Personal Products"                   | 931       | 
| 2013 | "Food, Beverage & Tobacco"                                             | 4995      | 
| 2014 | "Food, Beverage & Tobacco"                                             | 2685      | 
| 2015 | "Food, Beverage & Tobacco"                                             | 0         | 
| 2016 | "Food, Beverage & Tobacco"                                             | 100289    | 
| 2017 | "Food, Beverage & Tobacco"                                             | 3162      | 
| 2015 | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 8909      | 
| 2015 | "Mining - Iron, Aluminum, Other Metals"                                | 8181      | 
| 2013 | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 32271     | 
| 2014 | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 40215     | 
| 2015 | "Textiles, Apparel, Footwear and Luxury Goods"                         | 387       | 
| 2013 | Automobiles & Components                                               | 130189    | 
| 2014 | Automobiles & Components                                               | 230015    | 
| 2015 | Automobiles & Components                                               | 817227    | 
| 2016 | Automobiles & Components                                               | 1404833   | 
| 2013 | Capital Goods                                                          | 60190     | 
| 2014 | Capital Goods                                                          | 93699     | 
| 2015 | Capital Goods                                                          | 3505      | 
| 2016 | Capital Goods                                                          | 6369      | 
| 2017 | Capital Goods                                                          | 94949     | 
| 2015 | Chemicals                                                              | 62369     | 
| 2013 | Commercial & Professional Services                                     | 1157      | 
| 2014 | Commercial & Professional Services                                     | 477       | 
| 2016 | Commercial & Professional Services                                     | 2890      | 
| 2017 | Commercial & Professional Services                                     | 741       | 
| 2013 | Consumer Durables & Apparel                                            | 2867      | 
| 2014 | Consumer Durables & Apparel                                            | 3280      | 
| 2016 | Consumer Durables & Apparel                                            | 1162      | 
| 2015 | Containers & Packaging                                                 | 2988      | 
| 2015 | Electrical Equipment and Machinery                                     | 9801558   | 
| 2013 | Energy                                                                 | 750       | 
| 2016 | Energy                                                                 | 10024     | 
| 2015 | Food & Beverage Processing                                             | 141       | 
| 2014 | Food & Staples Retailing                                               | 773       | 
| 2015 | Food & Staples Retailing                                               | 706       | 
| 2016 | Food & Staples Retailing                                               | 2         | 
| 2015 | Gas Utilities                                                          | 122       | 
| 2013 | Household & Personal Products                                          | 0         | 
| 2013 | Materials                                                              | 200513    | 
| 2014 | Materials                                                              | 75678     | 
| 2016 | Materials                                                              | 88267     | 
| 2017 | Materials                                                              | 213137    | 
| 2013 | Media                                                                  | 9645      | 
| 2014 | Media                                                                  | 9645      | 
| 2015 | Media                                                                  | 1919      | 
| 2016 | Media                                                                  | 1808      | 
| 2014 | Retailing                                                              | 19        | 
| 2015 | Retailing                                                              | 11        | 
| 2014 | Semiconductors & Semiconductor Equipment                               | 50        | 
| 2016 | Semiconductors & Semiconductor Equipment                               | 4         | 
| 2015 | Semiconductors & Semiconductors Equipment                              | 3         | 
| 2013 | Software & Services                                                    | 6         | 
| 2014 | Software & Services                                                    | 146       | 
| 2015 | Software & Services                                                    | 22856     | 
| 2016 | Software & Services                                                    | 22846     | 
| 2017 | Software & Services                                                    | 690       | 
| 2013 | Technology Hardware & Equipment                                        | 61100     | 
| 2014 | Technology Hardware & Equipment                                        | 167361    | 
| 2015 | Technology Hardware & Equipment                                        | 106157    | 
| 2016 | Technology Hardware & Equipment                                        | 1566      | 
| 2017 | Technology Hardware & Equipment                                        | 27592     | 
| 2013 | Telecommunication Services                                             | 52        | 
| 2014 | Telecommunication Services                                             | 183       | 
| 2015 | Telecommunication Services                                             | 183       | 
| 2015 | Tires                                                                  | 2022      | 
| 2015 | Tobacco                                                                | 1         | 
| 2015 | Trading Companies & Distributors and Commercial Services & Supplies    | 239       | 
| 2013 | Utilities                                                              | 122       | 
| 2016 | Utilities                                                              | 122       | 

