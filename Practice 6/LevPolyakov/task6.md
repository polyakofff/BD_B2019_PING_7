# Задание 6 #
#### 1) #
Для Олимпийских игр 2004 года сгенерируйте список (год рождения, количество игроков, количество золотых медалей), содержащий годы, в которые родились игроки, количество игроков, родившихся в каждый из этих лет, которые выиграли по крайней мере одну золотую медаль, и количество золотых медалей, завоеванных игроками, родившимися в этом году.
``` sql
select extract(year from p.birthdate), 
       count(distinct p.player_id), 
       count(*)
from Players p
    join Results r on r.player_id = p.player_id
    join Events e on e.event_id = r.event_id
    join Olympics o on o.olympic_id = e.olympic_id
where o.year = 2004 and r.medal = 'GOLD'
group by extract(year from p.birthdate);
```

#### 2) #
Перечислите все индивидуальные (не групповые) соревнования, в которых была ничья в счете, и два или более игрока выиграли золотую медаль.
``` sql
select e.event_id
from Events e
    join Results r on r.event_id = e.event_id
where e.is_team_event = 0 and r.medal = 'GOLD'
group by e.event_id
having count(*) > 1;
```

#### 3) #
Найдите всех игроков, которые выиграли хотя бы одну медаль (GOLD, SILVER и BRONZE) на одной Олимпиаде. (player-name, olympic-id).
``` sql
select distinct (p.name, e.olympic_id)
from Players p
    join Results r on r.player_id = p.player_id
    join Events e on e.event_id = r.event_id
where r.medal in ('GOLD', 'SILVER', 'BRONZE');
```

#### 4) #
В какой стране был наибольший процент игроков (из перечисленных в наборе данных), чьи имена начинались с гласной?
``` sql
with country_perc as (
    select c.country_id,
           sum(case when p.name ~* '^[aeiou]' then 1 else 0 end)::decimal / count(p) as perc
    from Countries c
        join Players p on p.country_id = c.country_id
    group by c.country_id

), country_perc_desc as (
    select cp.country_id,
           rank() over (order by cp.perc desc) rnk
    from country_perc cp
    
)
select cpd.country_id
from country_perc_desc cpd
where cpd.rnk = 1;
```

#### 5) #
Для Олимпийских игр 2000 года найдите 5 стран с минимальным соотношением количества групповых медалей к численности населения.
``` sql
with team_event as (
    select e.event_id, e.olympic_id, p.country_id
    from Events e
        join Results r on r.event_id = e.event_id
        join Players p on p.player_id = r.player_id
    where e.is_team_event = 1
    group by e.event_id, e.olympic_id, r.medal, p.country_id

)
select c.country_id
from Countries c
    join team_event te on te.country_id = c.country_id
    join Olympics o on o.olympic_id = te.olympic_id
where o.year = 2000
group by c.country_id, c.population
order by count(*)::decimal / c.population
limit 5;
```
