# Carbon


cau 3
select i.industry_group, sum(p.carbon_footprint_pcf) as "Total Pcf"
from product_emissions p
left join industry_groups i on p.industry_group_id = i.id
group by 1
order by 2 desc
limit 10
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
select c.company_name, sum(p.carbon_footprint_pcf) as "Total Pcf"
from product_emissions p
left join companies c on p.company_id = c.id
group by 1
order by 2 desc
limit 10
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
select co.country_name, sum(p.carbon_footprint_pcf) as "Total Pcf"
from product_emissions p
left join countries co on p.country_id = co.id
group by 1
order by 2 desc
limit 5
| country_name | Total Pcf | 
| -----------: | --------: | 
| Spain        | 9786130   | 
| Germany      | 2251225   | 
| Japan        | 653237    | 
| USA          | 518381    | 
| South Korea  | 186965    | 
