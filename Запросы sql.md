with unfiltred_1 as (SELECT part_id, ((rpm * adjusted_watt) / size) as quality

    FROM ( SELECT part_id, rpm, watt + (select avg(watt) from enom_gilpane) as adjusted_watt, size

        FROM enom_gilpane)),
        
unfiltred_2 as (SELECT part_id, ((rpm * adjusted_watt) / size) as quality

    FROM ( SELECT part_id, rpm, watt + (select avg(watt) from castle_loctus) as adjusted_watt, size

        FROM castle_loctus)),

unfiltred_3 as (SELECT part_id, ((rpm * adjusted_watt) / size) as quality

    FROM ( SELECT part_id, rpm, watt + (select avg(watt) from honpan_bilopsa) as adjusted_watt, size

        FROM honpan_bilopsa)),

unfiltred_4 as (SELECT part_id, ((rpm * adjusted_watt) / size) as quality

    FROM ( SELECT part_id, rpm, watt + (select avg(watt) from yurnol_qoltam) as adjusted_watt, size

        FROM yurnol_qoltam)),

quality_table as (

    select * from unfiltred_1

    where quality > (select avg(quality) from unfiltred_1)

union all

    select * from unfiltred_2

    where quality > (select avg(quality) from unfiltred_2)

union all

    select * from unfiltred_3

    where quality > (select avg(quality) from unfiltred_3)

union all

    select * from unfiltred_4

    where quality > (select avg(quality) from unfiltred_4))

select part_id, avg(quality) as avg_quality from quality_table

group by part_id

order by avg_quality desc;