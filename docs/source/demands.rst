=====================
2. Demand projections
=====================

Demand curves are obtained outside the OSeMOSYS model and then given to it as input. A demand workbook has been defined to obtain the energy service demand values for each sector. An overview of the data sources and the assumptions behind the demand workbook is given in the following. Section 2.1 describes how the initial values, for 2019, have been obtained. Section 2.2 illustrates the available demand drivers and Section 2.3 outlines more in detail how each sectorial demand has been defined and projections have been done.


2.1 Current energy balance
==========================

An energy balance tracks the flow of energy within a geographical area in a given period . This sheet gives a breakdown of the different fuels in terms of supply defined as the Total Energy Supply (TES) and consumption defined as the Total final consumption (TFC). 
The Total energy supply (TES) was given as a sum of what was produced locally in the country, imports (+), exports (-), marine and aviation bunkers treated as exports and stock changes that could be positive or negative. The TFC was given as a sum total of transfers (change in commodity balance through a change in use) that could be positive or negative, statistical differences indicating differences between supply and demand (positive or negative), Transformation processes which excluded all fuels used for the process and includes the product of transformation, that was given as a sum of Electricity plants (main producers – generating electricity for sale as their main business), Electricity plants (autoproducers – generating electricity for their own needs but could sell any surplus), Other transformation that does not include electricity, energy industry own use for example consumption of electricity in power plants (-) and losses occurring during transmission and distribution of electricity and gas (-) .
The energy balance was based on the International Energy Agency (IEA) 2019 energy balance for Kenya. The unit of energy was converted from thousand tonnes of oil equivalent (ktoe) to petajoules (PJ)
Consumption for each fuel is broken down into various sectors that added up to the total final consumption computed for the specific fuel.
The sectors included: Residential, Industry, Commerce & Service, Agriculture, Fisheries, Other, Transport, Non-Energy Use


2.2 Demand projections
======================

The energy service demand projections was done drawn from each sector represented from the 2019 energy balance. The relevant projection drivers included population (Mln people for three different scenarios – High, Central and Low), urbanization share, urban and rural household occupancy, household electricity use (Central and Low scenarios), Gross Domestic Product (GDP – High, Central, Low scenarios), Gross Value Added (GVA – High, Central, Low scenarios) contribution per relevant sector.   
The table shows how each projection driver was applied to the service demands described.

.. csv-table:: 
   :file: ./data/projections.csv
   :widths: 30, 30, 30, 70
   :header-rows: 1


2.3 Sectors
===========

Agriculture
-----------

Fuel consumption from the energy balance was aggregated for the three sectors and sub divided in % shares into relevant energy service demands per fuel category: Electrical appliances, Machinery. This was then calculated into energy service demands in PJ and an efficiency amount applied to derive useful energy demand per fuel category. 

Commercial sector
-----------------

Total fuel consumption is derived from the energy balance and sub-divided in % shares into relevant energy service demand per fuel category: Electrical Appliances, Low heat appliances. This was then calculated into energy service demands in PJ and an efficiency amount was applied to derive useful energy demand per fuel category

Industry
--------

The fuel consumption was subdivided into three different sub-subsectors in the energy balance. The % shares were calculated for each fuel category from the total allocations: Industry - Non-metallic minerals (cement), Industry - F&D, Industry – Other. Each sub-sector was further divided into relevant energy service demand and given a percentage share. Electrical Appliances (motive power), High heat, Low heat. 
The service demand in PJ was computed from this share and an efficiency value applied to it. This then gave the useful energy service demand per fuel category. A total amount for each useful service demand was computed within the industry sector.


Residential sector
------------------

A split between Urban and Rural fuel consumption was given. The split was done in percentage vales for each fuel and added up to 100%. From this split consumption for the relevant fuel was calculated in PJ from the total consumption for the residential sector
Consumption by fuel was further subdivided into energy service demands. Each allocation was given a percentage split that summed up to a total 100%
The energy service demands given under the urban and rural splits were: Cooking, Heating (low heat), Lighting, Cooling, Other electrical appliances
The consumption for each service demand by fuel was calculated for each allocation from the total fuel use given for the split between the urban and rural areas 
Efficiency was applied for the allocations to derive useful energy service demand


Transports
----------

The total consumption for each fuel was derived from the energy balance. This was then apportioned in % shares to different energy service demands relevant to the sector. The shares for each service demand by fuel category added up to 100%
The energy service demand under transport included: Motorcycles, Cars, Buses, Heavy Duty Vehicles (HDVs), Light Duty Vehicles (LDVs), Aviation, Shipping and Rail
The service demand was then calculated from each share in PJ. Their totals by fuel category summed up to the aggregate total consumption in the transport sector derived from the energy balance equivalent to each fuel. A check for whether the two totals sums up was provided for in the energy balance sheet
Efficiency values for each service demand were given per fuel category to calculate useful energy per service demand.
