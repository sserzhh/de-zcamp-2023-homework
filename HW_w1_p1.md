--Q1
docker build --help
;

--Q2
pip list
;

--Q3
select count(*) cnt
from public.green_taxi
where lpep_pickup_datetime >= '2019-01-15' and lpep_pickup_datetime < '2019-01-16'
;


--Q4
select lpep_pickup_datetime, trip_distance, row_number() over(order by trip_distance desc) trip_dist_rnk
from public.green_taxi
limit 1
;


--Q5
select passenger_count, count(*) cnt
from public.green_taxi
where lpep_pickup_datetime >= '2019-01-01' and lpep_pickup_datetime < '2019-01-02'
group by passenger_count
;


--Q6
select zpu."Zone" puzone, zdo."Zone" dozone, trp.tip_amount,
	row_number() over(order by trp.tip_amount desc) tip_amount_rnk
from 
	public.green_taxi trp
		LEFT JOIN public.zones zpu
		ON trp."PULocationID" = zpu."LocationID"
			LEFT JOIN public.zones zdo
			ON trp."DOLocationID" = zdo."LocationID"
where
	zpu."Zone" = 'Astoria'
limit 1
;