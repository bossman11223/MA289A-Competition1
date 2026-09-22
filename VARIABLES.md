# Data Dictionary

## Identification

- `Id`: Unique identifier for each house.

## Sale Information

- `SaleCondition`: Condition of sale.
- `SaleType`: Type of sale.

## Location

- `Neighborhood`: Physical location within Ames.
- `MSSubClass`: Type of dwelling.
- `MSZoning`: General zoning classification.

## Lot Characteristics

- `LotFrontage`: Linear feet of street connected to property.
- `LotArea`: Lot size in square feet.
- `LotShape`: General shape of property.
- `LandContour`: Flatness of property.
- `Utilities`: Type of utilities available.
- `LotConfig`: Lot configuration.
- `LandSlope`: Slope of property.

## Exterior

- `BldgType`: Type of dwelling.
- `HouseStyle`: Style of dwelling.
- `OverallQual`: Overall material and finish quality.
- `OverallCond`: Overall condition rating.
- `YearBuilt`: Original construction date.
- `YearRemodAdd`: Remodel date.
- `RoofStyle`: Type of roof.
- `RoofMatl`: Roof material.
- `Exterior1st`, `Exterior2nd`: Exterior covering.
- `MasVnrType`: Masonry veneer type.
- `MasVnrArea`: Masonry veneer area.

## Foundation and Basement

- `Foundation`: Type of foundation.
- `BsmtQual`, `BsmtCond`: Basement quality and condition.
- `BsmtExposure`: Walkout or garden level walls.
- `BsmtFinType1`, `BsmtFinType2`: Finished basement areas.
- `BsmtFinSF1`, `BsmtFinSF2`: Finished square footage.
- `BsmtUnfSF`: Unfinished square footage.
- `TotalBsmtSF`: Total basement square footage.

## Heating and Electrical

- `Heating`: Heating type.
- `HeatingQC`: Heating quality.
- `CentralAir`: Central air conditioning.
- `Electrical`: Electrical system.

## Interior

- `1stFlrSF`, `2ndFlrSF`: First and second floor square footage.
- `LowQualFinSF`: Low quality finished area.
- `GrLivArea`: Above-ground living area.
- `FullBath`, `HalfBath`: Bathrooms above grade.
- `BsmtFullBath`, `BsmtHalfBath`: Basement bathrooms.
- `BedroomAbvGr`: Bedrooms above grade.
- `KitchenAbvGr`: Kitchens above grade.
- `KitchenQual`: Kitchen quality.
- `TotRmsAbvGrd`: Total rooms above grade.
- `Functional`: Home functionality.

## Fireplace and Garage

- `Fireplaces`: Number of fireplaces.
- `FireplaceQu`: Fireplace quality.
- `GarageType`: Garage location.
- `GarageYrBlt`: Year garage built.
- `GarageFinish`: Interior finish.
- `GarageCars`: Size of garage in car capacity.
- `GarageArea`: Garage size in square feet.
- `GarageQual`, `GarageCond`: Garage quality and condition.

## Outdoor Amenities

- `PavedDrive`: Paved driveway.
- `WoodDeckSF`: Wood deck area.
- `OpenPorchSF`: Open porch area.
- `EnclosedPorch`: Enclosed porch area.
- `3SsnPorch`: Three-season porch area.
- `ScreenPorch`: Screen porch area.
- `PoolArea`: Pool area.
- `PoolQC`: Pool quality.
- `Fence`: Fence quality.
- `MiscFeature`: Miscellaneous feature.
- `MiscVal`: Value of miscellaneous features.

## Time and Target

- `MoSold`: Month sold.
- `YrSold`: Year sold.
- `SalePrice`: Target variable, present in the training set only.
