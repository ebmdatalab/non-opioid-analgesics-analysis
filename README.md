# non-opioid-analgesics-analysis

Draft SQL data extraction
```
-- non-opioid analgesics
SELECT 
  year,
  bnf_code,
  Para_current,
  Chemical_current,
  sum(itemsper1000) as items_per_1000, 
  sum(quantityper1000) as quantity_per_1000,
  sum(Infl_corr_Cost_per1000) as cost_per_1000
FROM ebmdatalab.helen.trends_from_pca_final_2017 p

WHERE 
SUBSTR(bnf_code,1,6) IN 
('040701', -- non-opioid analgesics
'100101', -- NSAIDs
'040703') -- neuropathic pain
OR SUBSTR(bnf_code,1,9) IN 
('0403010B0', --amytriptyline
'0403010V0', -- nortriptyline
'0408010AE', -- pregabalin
'0408010G0') -- gabapentin
OR bnf_code LIKE '1502010J0%EL' -- lidocaine patches

GROUP BY 
  year,
  bnf_code,
  para_current,
  chemical_current
  
ORDER BY year,para_current
```
