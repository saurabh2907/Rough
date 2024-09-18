Actual_NBM = 
VAR SalesOfAll =
    CALCULATE (
        [NBM Selected_Actual],
        REMOVEFILTERS ( 'Product Names' )
    )
RETURN
    IF (
        NOT ISINSCOPE ( 'Product Names'[Products] ),
 
        -- Calculation for a group of products
        SalesOfAll,
 
        -- Calculation for one product name
        VAR ProductsToRank = [TopN Value]
        VAR SalesOfCurrentProduct = [NBM Selected_Actual]
        VAR IsOtherSelected =
            SELECTEDVALUE ( 'Product Names'[Products] ) = "Others"
        RETURN
            IF (
                NOT IsOtherSelected,
 
                -- Calculation for a regular product
                SalesOfCurrentProduct,
 
                -- Calculation for Others
                VAR VisibleProducts =
                    CALCULATETABLE (
                        VALUES ( 'Product Names' ),
                        ALLSELECTED ( 'Product Names'[Products] )
                    )
                VAR ProductsWithSales =
                    ADDCOLUMNS (
                        VisibleProducts,
                        "@SalesAmount", [NBM Selected_Actual]
                    )
                VAR SalesOfTopProducts =
                    SUMX (
                        TOPN (
                            ProductsToRank,
                            ProductsWithSales,
                            [@SalesAmount]
                        ),
                        [@SalesAmount]
                    )
                VAR SalesOthers =
                    SalesOfAll - SalesOfTopProducts
                RETURN
                    SalesOthers
            )
    )
