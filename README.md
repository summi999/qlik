Store:
Load * Inline [
StoreID, StoreName
1, Store A
2, Store B
];

Calendar:
Load MonthID As DateID, Month Inline [
MonthID, Month
1, Jan
2, Feb
];

Product:
Load * Inline [
ProductID, Product
1, Product A
2, Product B
];

Sales:
LOAD StoreID & ProductID as SalesBudgetID,
* INLINE [
    DateID, StoreID, ProductID, SaleQty, SaleValue
    1, 1, 1, 2, 23
    1, 1, 2, 4, 24
    2, 1, 1, 4, 33
    2, 1, 2, 3, 28
    1, 2, 1, 2, 21
    1, 2, 2, 4, 30
    2, 2, 1, 3, 25
];

Budget:
LOAD StoreID & ProductID as SalesBudgetID,* INLINE [
    StoreID, ProductID, BudgetQty, BudgetValue
    1, 1, 5, 50
    1, 2, 6, 47
    2, 1, 5, 41
    2, 2, 4, 27
];


KeyTable:


load 
StoreID & ProductID as SalesBudgetID,
StoreID, 
ProductID
Resident Sales;

Concatenate

load 
StoreID & ProductID as SalesBudgetID,
StoreID,
ProductID
Resident Budget;

drop Fields StoreID,ProductID from Sales;

drop Fields StoreID,ProductID from Budget;

