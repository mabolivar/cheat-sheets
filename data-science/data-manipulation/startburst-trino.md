
## How to unnest array (json) elements?

**Preferred**
```sql
with cte as (
    select 
        order_id, 
        cast(json_parse(json_element) as row (productId bigint, rating integer, ratingEvaluation varchar)) as row_element
    from "delta"."central_ratings_odp"."ratings"
    cross join unnest (rated_products) AS t (json_element)
    where cardinality(rated_products) >= 1 and p_creation_date between date '2024-09-29' and date '2024-09-29'
)
select 
    order_id,
    row_element.productId as product_id,
    row_element.rating as rating,
    row_element.ratingEvaluation as rating_evaluation
from cte;
```

**Alternative**
```sql
SELECT
order_id
, JSON_EXTRACT_SCALAR(JSON_ELEMENT, '$.productId') AS product_id
, JSON_EXTRACT_SCALAR(JSON_ELEMENT, '$.rating') AS rating
, JSON_EXTRACT_SCALAR(JSON_ELEMENT, '$.ratingEvaluation') AS ratingEvaluation
FROM "delta"."central_ratings_odp"."ratings"
CROSS JOIN UNNEST (rated_products) AS t (JSON_ELEMENT)
WHERE JSON_ARRAY_LENGTH(CAST(rated_products AS JSON)) >= 1
AND p_creation_date BETWEEN DATE '2024-09-29' AND DATE '2024-09-29'
```