[https://cbua-us.alma.exlibrisgroup.com/SAML](https://cbua-us.alma.exlibrisgroup.com/SAML)

### Ejercicios planteados en el Curso

SIGB.jml. Devoluciones desde una máquina de autopréstamo realizadas en 2022 clasificadas por grupo de usuario
``` sql
SELECT
   0 s_0,
   "Fulfillment"."Patron Details"."Patron Group" s_1,
   "Fulfillment"."Loan"."Returns" s_2,
   REPORT_SUM("Fulfillment"."Loan"."Returns" BY ) s_3
FROM "Fulfillment"
WHERE
(("Return Circulation Desk"."Has Self Check" = 1) AND ("Return Date"."Return Year" = '2022'))
ORDER BY 3 DESC NULLS LAST, 2 ASC NULLS FIRST
FETCH FIRST 10000001 ROWS ONLY
```


SIGB.jml. Ejemplares de la B. de Educación con signaturas que empiecen por "K S " o "K S2 " y que no estén en Depósito
```sql
SELECT
   0 s_0,
   "Physical Items"."Bibliographic Details"."Title" s_1,
   "Physical Items"."Location"."Location Name" s_2,
   "Physical Items"."Physical Item Details"."Item Call Number" s_3,
   "Physical Items"."Physical Item Details"."Physical Item Id" s_4,
   "Physical Items"."Physical Item Details"."Receiving Date (Calendar)" s_5
FROM "Physical Items"
WHERE
(("Library Unit"."Library Name" = 'B Educación') AND (("Physical Item Details"."Item Call Number" LIKE 'K S %' OR "Physical Item Details"."Item Call Number" LIKE 'K S2 %')) AND ("Location"."Location Name" <> 'Depósito'))
ORDER BY 6 DESC NULLS LAST, 5 ASC NULLS FIRST, 4 ASC NULLS FIRST, 3 ASC NULLS FIRST, 2 ASC NULLS FIRST
FETCH FIRST 10000001 ROWS ONLY
```


SIGB.jml. Líneas de pedido correspondientes al año fiscal 2021, por proveedores, por biblioteca y por estado
```sql
SELECT
   0 s_0,
   "Funds Expenditure"."Library Unit"."Library Name" s_1,
   "Funds Expenditure"."PO Line"."PO Line Reference" s_2,
   "Funds Expenditure"."PO Line"."Status (Active)" s_3,
   "Funds Expenditure"."PO Line"."Status" s_4,
   "Funds Expenditure"."Vendor"."Vendor Name" s_5
FROM "Funds Expenditure"
WHERE
("Fiscal Period"."Fiscal Period Description" = '01/01/2021 - 31/12/2021')
ORDER BY 2 ASC NULLS FIRST, 5 ASC NULLS FIRST, 6 ASC NULLS FIRST, 3 ASC NULLS FIRST, 4 ASC NULLS FIRST
FETCH FIRST 10000001 ROWS ONLY
```

SIGB.jml. Los 20 libros más prestados en los últimos 365 días en la Biblioteca
```sql
SELECT
   0 s_0,
   "Fulfillment"."Bibliographic Details"."Title" s_1,
   "Fulfillment"."Item Location at time of loan"."Library Name" s_2,
   "Fulfillment"."Physical Item Details"."Barcode" s_3,
   "Fulfillment"."Physical Item Details"."Item Call Number" s_4,
   "Fulfillment"."Physical Item Details"."Material Type" s_5,
   "Fulfillment"."Physical Item Details"."Physical Item Id" s_6,
   "Fulfillment"."Loan"."Loans (Not In House)" s_7
FROM "Fulfillment"
WHERE
(("Physical Item Details"."Material Type" = 'Book') AND ("Loan Date"."Loan Date Filter" = 'Last 365 Days') AND (TOPN("Loan"."Loans (Not In House)",20) <= 20))
ORDER BY 8 DESC NULLS LAST, 3 ASC NULLS FIRST, 7 ASC NULLS FIRST, 4 ASC NULLS FIRST, 5 ASC NULLS FIRST, 2 ASC NULLS FIRST, 6 ASC NULLS FIRST
FETCH FIRST 10000001 ROWS ONLY
```

SIGB.jml. Número de ejemplares recibidos por biblioteca en 2022
```sql
SELECT
   0 s_0,
   "Physical Items"."Location"."Library Name" s_1,
   "Physical Items"."Physical Item Details"."Num of Items (Deleted + In Repository)" s_2
FROM "Physical Items"
WHERE
(YEAR("Physical Item Details"."Receiving Date (Calendar)") = 2022)
ORDER BY 2 ASC NULLS FIRST
FETCH FIRST 10000001 ROWS ONLY
```

SIGB.jml. Portfolios creados en 2022 que están en repositorio y son bibliografía recomendada para la titulación "Grado en Economía"
```sql
SELECT
   0 s_0,
   "E-Inventory"."Bibliographic Details"."Local Param 05" s_1,
   "E-Inventory"."Bibliographic Details"."MMS Id" s_2,
   "E-Inventory"."Bibliographic Details"."Title" s_3,
   "E-Inventory"."Portfolio Creation Date"."Portfolio Creation Date" s_4,
   "E-Inventory"."Portfolio"."Lifecycle" s_5,
   "E-Inventory"."Portfolio"."Portfolio Id" s_6
FROM "E-Inventory"
WHERE
(("Portfolio Creation Date"."Portfolio Creation Year" = '2022') AND ("Portfolio"."Lifecycle" = 'In Repository') AND ("Bibliographic Details"."Local Param 05" LIKE '%Grado en Economía%'))
ORDER BY 7 ASC NULLS FIRST, 6 ASC NULLS FIRST, 5 ASC NULLS FIRST, 3 ASC NULLS FIRST, 4 ASC NULLS FIRST, 2 ASC NULLS FIRST
FETCH FIRST 10000001 ROWS ONLY
```