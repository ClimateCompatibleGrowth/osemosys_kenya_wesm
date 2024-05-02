==============
3. Data inputs
==============
This section gives an overview of the data sources used in the model and how it was implemented.

3.1 Main data sources
=====================
The following table lists the main data sources used to populate the model. Where available, Kenyan data sources have been used, either directly in the model or, if not in the right format, to validate the data already in the model. It is the case of the technologies in the agricultural, commercial, and industrial sectors, for which the level of detail could be improved. The power sector heavily relies on data provided by the LCPDP team. Data for the residential sector has been also provided by Nuvoni, a Kenyan consultancy firm currently working at the national e-cooking strategy to be published in the next months. 

.. csv-table:: 
   :file: ./data/data_sources.csv
   :header-rows: 1


3.2 Global parameters
=====================

Global parameters are parameters influencing the model as a whole.

DiscountRate
------------
An annual discount rate of 9% is applied throughout the model.

YearSplit
---------
Year split is the parameter where the length of timeslices is given. The length of each timeslice is given by the combination of season, day type and portion of the day. Kenya's weather is characterized by a dry season, two wet ones, and an intermediate one. The length of each season is given in the following table, as well as the corresponding fraction of the year. The distinction between weekdays and weekends, as well as dividing each single day in 6 time bands, is driven by an analysis of Kenya's power demand curve. As for seasons, for each day type and time band the corresponding fraction of the total (resepctively 7 days and 24 hours) is computed. Each of the 48 timeslices is given by a unique combination of season, day type and time band, and the corresponding fraction of the year is obtained by multiplying the single fractions of each component.

.. table:: 
   :align: left
   
   +--------+-------+-------+-----------+-------------+
   | Season | Start | End   | N of days | Fraction    |
   +========+=======+=======+===========+=============+
   | Dry    | 01/01 | 31/03 | 90        | 0.246575342 |
   +--------+-------+-------+-----------+-------------+
   | Wet 1  | 01/04 | 31/05 | 61        | 0.167123288 |
   +--------+-------+-------+-----------+-------------+
   | Int    | 01/06 | 30/09 | 122       | 0.334246575 |
   +--------+-------+-------+-----------+-------------+
   | Wet 2  | 01/10 | 31/12 | 92        | 0.252054795 |
   +--------+-------+-------+-----------+-------------+

.. table:: 
   :align: left
   
   +----------+-----------+-------------+
   | Day type | N of days | Fraction    |
   +==========+===========+=============+
   | Weekday  | 5         | 0.714285714 |
   +----------+-----------+-------------+
   | Weekend  | 2         | 0.285714286 |
   +----------+-----------+-------------+

.. table:: 
   :align: left
   
   +------------+------------+-------------+
   | Time slice | N of hours | Fraction    |
   +============+============+=============+
   | 00-06      | 6          | 0.25        |
   +------------+------------+-------------+
   | 06-09      | 3          | 0.125       |
   +------------+------------+-------------+
   | 09-15      | 6          | 0.25        |
   +------------+------------+-------------+
   | 15-19      | 4          | 0.166666667 |
   +------------+------------+-------------+
   | 19-21      | 2          | 0.083333333 |
   +------------+------------+-------------+
   | 21-00      | 3          | 0.125       |
   +------------+------------+-------------+
   

3.3 Demand
==========

The procedure used to determine the annual demand, and the demand types per each sector are introduced in the dedicated Section 2. Demands are then added in the model in two possible ways. In case demand is only given as an annual value, without any information on the demand profile trhoughout the year, then the parameter of choice is AccumulatedAnnualDemand. In case a profile is given, then the demand is represented through two parameters:SpecifiedAnnualDemand, where the total annual demand is given, and SpecifiedDemandProfile, where the profile is. Currently in the model demand the demand profile is specified for the residential sector, while all other sector only have an AccumulatedAnnualDemand profile defined.


3.4 Performance
===============

This section deals with parametrs used to describe the performance and availability of the technologies available in the model. Where not explicitly reported, the specific values for each technology can be obtained from the data file of the model.

CapacityToActivityUnit
----------------------
This parameter is used to define the relationship between capacity and activity level of the technologies, based on the units of measure considered. In the power sector, it represents the relationship between power, expressed in GW, and energy, expressed in PJ. 1 GW of constant power throughout the year corresponds to 31.536 PJ, which is the value considered for power plants. The same goes for all other technologies for which activity is given in terms of PJ and capacity in GW. Different is the case for technologies where demand is not expressed in PJ, but in other units of measure, as, for example, the transport sector, where demand is expressed in billion vehicle-kilometers (bvkm). In this case, the capacity unit is expressed in bvkm/year, and hence the CapacityToActivityUnit parameter is 1.

CapacityFactor
--------------
Capacity factors are highly dependent on the technology considered, down to the single power plant level. For each technology, capacity factors are defined for each timeslice. All capacity factors in the power sector have been provided by the LCPDP team, whil eoutside of the power sector all capacity factors are set to 1.

AvailabilityFactor
------------------
This parameter represents the portion of the year during which a certain technology is available. As for the capacity factor, it is used only for the power sector. Different availabilities factors are defined for different technologies, based on data provided by the LCPDP team or from values commonly used in the literature when the former where not available. For all other sectors the availability factor is set to 1. 

OperationalLife
---------------
The operational life represent the number of years for which a certain technology is available before it has to be substituted (e.g. a new investment is needed). It is defined on a technology basis and the values considered have been obtained from different sources, depending on the sector, as outlined in Section 3.1, where the major data sources are listed.

InputActivityRatio and OutputActivityRatio
------------------------------------------
Input and output activity ratios represent, respectively, the rate of use or output of a technology, a ratio of the rate of activity. The ratio between output and input hence represents the efficiency of a certain technology, defined with the resulting unit of measure. The convention adopted in the model is that the output activity ratio is set to 1 for all technologies. As a consequence, the input activity ratio is the reciprocal of the efficiency:

.. math::

   OAR = \frac{1}{\eta}

ResidualCapacity
----------------
Residual capacity is used to represent the current capacity mix and the residual amount of years each technology has before reaching its end-of-life. In the WESM model, the residual capacity is only used in the power sector, and the required values have been obtained from the LCPDP. In all other sectors the current mix is enforced a lower limit on annual activity, through the TotalAnnualActivityLowerLimit parameter. 

TotalAnnualMin/MaxCapacity
--------------------------
Lower and upper limits on the annual capacity are used in combination to introduce different types of constraint on the technologies available in the power sector. Lower limits are used to ensure that planned power plants are selected by the model, while upper limits to ensure that technologies not yet available are considered only when appropriate and gradually introduced in the model.

TotalAnnualActivityLower/UpperLimit
-----------------------------------
These parameters serve a scope similar to the capacity limits, but are set on an activity basis. Lower activity limits are used to constrain the current capacity mix in all end use sectors, and then are progressively removed to leave the model with more freedom to select the cost optimal options.

ReserveMargin and ReserveMarginTagTechnology
--------------------------------------------
Reserve margin is a power sector specific-parameter, and represents the extra firm capacity that is needed in the system as backup. An extra 9% on the total capacity is considered each year. Not all technologies can contribute to the reserve margin, while some technologies are only considered to contribute with a fraction of their capacity. The parameter that allows to regulate the contribution of each technology to the reserve margin is the ReserveMarginTagTechnology. A list of the contribution from each parameter is given in the following.

+----------------------+--------------+
| Technology           | Contribution |
+======================+==============+
| Biomass              | 1.00         |
+----------------------+--------------+
| Coal                 | 1.00         |
+----------------------+--------------+
| Geothermal           | 1.00         |
+----------------------+--------------+
| Heavy fuel oil       | 1.00         |
+----------------------+--------------+
| Hydro (dam)          | 1.00         |
+----------------------+--------------+
| Hydro (run of river) | 0.00         |
+----------------------+--------------+
| Light fuel oil       | 1.00         |
+----------------------+--------------+
| Natural gas          | 1.00         |
+----------------------+--------------+
| Solar                | 0.00         |
+----------------------+--------------+
| Nuclear              | 1.00         |
+----------------------+--------------+
| Wind                 | 0.25         |
+----------------------+--------------+


3.5 Costs
=========

CapitalCost
------------
Capital costs are expressed in MUSD/capacity unit and are defined on a technology basis. All costs have been obtained from the main data sources listed in Section 3.1.

FixedCost
---------
Fixed costs represent the annual costs associated to a technology, regardless of the activity, and are expressed as a function of the installed capacity MUSD/capacity unit/year.

VariableCost
------------
Variable costs represents the annual costs associated to the activity of a certain technology, and are expressed in MUSD/activity unit/year. Variable costs can hence be used to account for fuel expenditure. To allow for competition between different sectors, fuel costs are defined at a primary commodity level, hence associated to either MIN technologies (local production) or IMP technologies (imports). Additional sector-specific fuels costs are accounted for in the FTE technologies of each sector.

3.6 Emissions
=============
Currently, emissions in the model are limited to CO\ :sub:`2` emissions. As shown in Section 1.2, emissions are double counted to facilitate the post processing of the results.

EmissionActivityRatio
---------------------
Emissions are modelled through the emission activity ratio parameter, that defines the amount of tons of CO\ :sub:`2` associated to a unit of activity, PJ. General emissions are accounted at a primary commodity level, while sectorial specific emissions are associated to FTE technologies. A summary of the emissions per fuel type is given in the following table.

+----------------+--------------------+
| Fuel           | Emission [Mton/PJ] |
+================+====================+
| Coal           | 0.10               |
+----------------+--------------------+
| Diesel         | 0.07               |
+----------------+--------------------+
| Gasoline       | 0.07               |
+----------------+--------------------+
| Heavy fuel oil | 0.08               |
+----------------+--------------------+
| Jet fuel       | 0.07               |
+----------------+--------------------+
| Kerosene       | 0.07               |
+----------------+--------------------+
| Light fuel oil | 0.07               |
+----------------+--------------------+
| Natural gas    | 0.06               |
+----------------+--------------------+