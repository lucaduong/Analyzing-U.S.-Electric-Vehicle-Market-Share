-- 3. market share analysis 

-- 3.1. percentage of vehicles in each state are EVs, PHEVs, HEVs, and gasoline

with total_vehicle_data as
(
select *,
(ev + phev + hev + biodiesel + e85 + cng + propane + hydrogen + methanol + gasoline + diesel + unknown_fuel) as total_vehicle
from vehicle_data_2
),
percentage_data as 
(
select
state, 
round((ev/total_vehicle *100),2) as ev_percentage,
round((phev/total_vehicle *100),2) as phev_percentage,
round((hev/total_vehicle *100),2) as hev_percentage,
round((gasoline/total_vehicle *100),2) as gas_percentage
from total_vehicle_data
)

-- 3.2. identify the top 5 states with the highest EV adoption rate

select state, ev_percentage
from percentage_data
-- order by ev_percentage desc
-- limit 5

-- 3.3. compare EV adoption in California vs. other large states (e.g., Texas, Florida, New York)

where state in ('California', 'Texas', 'Florida', 'New York')
order by ev_percentage desc
;

-- 3.4. alternative fuels (biodiesel, ethanol, hydrogen) have meaningful presence vs. niche usage

with alt_fuels as
(
select
sum(biodiesel) as total_biodiesel,
sum(e85) as total_e85,
sum(hydrogen) as total_hydrogen,
sum(ev + phev + hev + biodiesel + e85 + cng + propane + hydrogen + methanol + gasoline + diesel + unknown_fuel) as total_vehicle
from vehicle_data_2
)
select 
total_biodiesel,
round(total_biodiesel / total_vehicle * 100,2) as biodiesel_percentage,
total_e85,
round(total_e85 / total_vehicle * 100,2) as e85_percentage,
total_hydrogen,
round(total_hydrogen / total_vehicle * 100,2) as hydrogen_percentage,
total_vehicle
from alt_fuels
;
