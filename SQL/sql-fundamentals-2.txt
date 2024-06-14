-- first just get rows using the between function
-- only shows those that have an enddate
select dates.datekey, employees.startdate, employees.enddate, count(1)
from employees cross join dates
where dates.datekey BETWEEN employees.startdate and employees.enddate
group by dates.datekey, employees.startdate, employees.enddate

-- add check using if statement for those without end-dates
select dates.datekey, employees.startdate, if(employees.enddate is null, "9999-12-31", employees.enddate) edate, employees.*
from employees cross join dates
where dates.datekey >= employees.startdate
and (dates.datekey <= employees.enddate
    OR
    employees.enddate is null)

-- group by month
select DATE_TRUNC(dates.datekey, "month") as mnt, count(1)
from employees cross join dates
where dates.datekey >= employees.startdate
and (dates.datekey <= employees.enddate
    OR
    employees.enddate is null)
group by DATE_TRUNC(dates.datekey, "month")



-- but it's counting everyone every day, so 30x the actual number
-- so typically we choose the end of the month

 select 
    dates.datekey,
    DATE_TRUNC(dates.datekey, "month") month,
    DATE_ADD(DATE_TRUNC(dates.datekey, "month"), 1, "month") next_month,
    DATE_ADD(DATE_ADD(DATE_TRUNC(dates.datekey, "month"), 1, "month"), -1, "day") eomonth

 from dates
 limit 10;



-- now let's use that to get the active count on that day


WITH `dl` AS (
 select DISTINCT
    CAST(DATE_ADD(DATE_ADD(DATE_TRUNC(dates.datekey, "month"), 1, "month"), -1, "day") AS DATE) eomonth
 from dates
)
select dl.eomonth, count(1)
from employees cross join `dl` AS dl
where dl.eomonth >= employees.startdate
and (dl.eomonth <= employees.enddate
    OR
    employees.enddate is null)
group by dl.eomonth
order by dl.eomonth