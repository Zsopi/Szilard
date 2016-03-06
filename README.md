#
Learning about political trouble
This code implements an estimation of “political trouble” in a given year in a given country my machine learning methods. One country-year is one record.
Variable definitions and data sources
“Political trouble” is a binary variable, defined as either of the following happening in the given year: coup, attempted coup, self-coup, rebels ousting executive, interregnum periods (as defined by code -77 in the Polity IV database, see here), civil war or violence, ethnic war or violence. The civil violence data is described here and the data sources is here. The estimate uses the “CIVTOT” variable, but only with an intensity code of at least 3. This is to exclude long running, often low intensity cases like ethnic strife in China or Thailand that is still ongoing. The definition of “political trouble” includes only domestic events and excludes cases of external wars. The source of political variables is the Center for Systemic Peace.
The features (or independent variables) are:  
•	(The natural log of) GDP per capita at purchasing power in 2011 USA dollars. Source: IMF World Economic Outlook Database or the Maddison Project.
•	(Lagged) GDP growth rate 5 years up to the year prior to the year examined, % annualized (this is to exclude reverse causation). Source: own calculations from above sources.
•	Ratio of “young” population in the adult population. Source: own calculation based on UN demographic data. For definition of “young” see below – this was the result of a grid search.
•	Growth rate of young population, % per annum. Source: same as above.
•	Growth rate of total population, % per annum. Source: same as above.
•	Political system variable (“polity2”). Denotes how authoritarian or democratic is in the country in the given year. Source: Polity IV:  Regime Authority Characteristics and Transitions Datasets from the Center for Systemic Peace.
•	Dummy variable for resource economies (“resdummy”). Takes values of 1 if resource rents  where resource rent minus “forest rent” is larger than 20% of GDP in 2013 or latest available, otherwise 0. Source: World Bank.
•	Youth ratio and polity2 interaction terms:  the product of the two variables above.
•	Youth ratio and GDP per capita interaction terms:  the product of the two variables above.

Some political scientist make a connection between the ratio of young people in the total or adult population and political violence. The basic idea is that the higher the ratio of young people, the more political (and criminal) violence because youth has both the opportunity and the motive to be violent. (See for example: Urdal 2012, Yair 2016). But their definition of “young” is usually arbitrary, something like ages between 15-24 or 15-29. In the following I will attempt to calibrate what age bracket is best to forecast political violence by using machine learning algorithms. I will run Random Forest, GBM and Deep Learning algorithms and will use AUC (“area under the curve”) measure to compare age cutoffs.

Then I will use grid search to estimate the best models, and take the average of probability forecast of the three models as the final prediciton.

