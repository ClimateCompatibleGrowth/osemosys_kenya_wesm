==================
1. Model structure
==================

A description of how the Kenya WESM model is structured is given in the following. Section 1.1 briefly introduces the general structure of the model, while Section 1.2 looks at how OSeMOSYS sets have been defined for the Kenyan model, including a list of all commodities, technologies, and emissions considered. Technologies an commodities are combined to the define the reference energy system (RES), introduced in Section 1.3 and analysed more in detail, sector by sector, in Section 1.4.

1.1 General model structure 
===========================

The general model structure is represented in the following figure. Primary energy can be either imported or extracted locally. Kenya hs abundant renewable energy sources - like solar, wind, hydro and geothermal - that feed into the power system to provide electricity to the end use sectors. Bioenergy can be directly used in end use sectors, as in the case of wood fuel for cooking, or converted to secondary fuels, like electricity, charcoal, bioethanol or biomethane. Kenya's scarce fossil fuel resources are not considered in the analysis, as  the country does not currently have any local production or refineries, nor plans to start extraction activities in the foreseeable future. Fossil fuels are hence only imported, and distributed to the different sectors. The energy demand of each sector is converted into energy service demands, to allow the model to identify the cost optimal technology mix for each sector.

.. image:: ./img/general_structure.svg
  :width: 1200
  :alt: Simplified Reference energy system

1.2 Model configuration - Sets
==============================

Sets shape the general model structure and contain information on the temporal and geographical coordinates of the model, as well as the fuels, technologies and typology of emissions included.

Region and years
----------------
The model is a single node national model for the whole country, meaning that no internal energy fluxes between different regions are considered. The time horizon is between 2019 and 2050, with one year increments. Years between 2019 and 2022 are used for calibration and checked with available data.

Timeslices
----------
Timeslices constitue the representation of time within a single year in the model. The Kenya WESM uses 48 timeslices, given by the combination of 4 seasons, 2 day types (weekday and week end days), and 6 time intervals within one day.

Fuels
-----
Fuels include all commodities considered in the model, being it primary or secondary. Generally speaking, primary and secondary commodities can be both produced locally or imported. In the case of Kenya, no fossil fuel local production is considered, and the only domestic resources corresponds to the potential of renewable energy sources as biomass, geothermal, solar, wind and hydro. Imported fossil fuels can be employed in one or more sectors and include coal, heavy and light fuel oil, natural gas, diesel fuel, gasoline, kerosene, jet fuel and LPG. Charcoal, bioethanol and biogas are locally produced, the first two from biomass, the latter from residual waste not accounted for in the model. Electricity is produced by the available power plants or imported from Ethiopia and Uganda and is represented by three different fuels, corresponding to electricity before transmission, between transmission and distribution and after distribution. To facilitate the analysis of the results, sector-specific fuels are defined and linked to the generic fuels through dummy technologies named fuel-technology mix technologies (FTE). Finally, demands are represented by fuels as well and identified by the prefix DEM.

.. csv-table:: 
   :file: ./data/fuels.csv
   :widths: 30, 70
   :header-rows: 1

Technologies and modes of operation
-----------------------------------
All technologies considered in the model are listed in the technologies set. Imported resources and fuels (IMP) and local resources (MIN) are characterized by technologies with only an output fuel. The power sector is represented at a single power plant level (PWR technologies). The transmission (PWRTRN) and distribution PWRDIST) grids are represented by a single technology, to account for losses. Each sector is delimitated by the fuel-technology mix technologies (FTE), one per each fuel available to the sector. The function of FTE technologies is to facilitate the postprocessing of the results, as well as to account for sector-specific costs and efficiencies not explicitly modelled. Each sector has then its own technologies, identified by a specific prefix, that convert the available fuels in the relevant sectoral demand. Currently, only one mode of operation is considered per each technology.

.. csv-table:: 
   :file: ./data/technologies.csv
   :widths: 30, 70
   :header-rows: 1


Emissions
---------
The current version of the model only accounts for CO\ :sub:`2` emissions. The set includes both a generic CO\ :sub:`2` emission entry, as well as sectoral specific CO\ :sub:`2` emissions.

.. csv-table:: 
   :file: ./data/emissions.csv
   :widths: 30, 70
   :header-rows: 1



1.3 Reference energy system
===========================

An overview of the entire reference energy system is given in the following figure. Starting from the left hand-side, each block represents one or two technologies, depending if the commodity is locally extracted or imported. The top part of the scheme describes the power sector. Each block can represent up to thirty power plants, as in the model they are described at a single plant level. Power imports and exports are at a transmission level, while the electricity is distributed to the different sectors after the transmission and distribution grids, where losses are accounted for. Beneath the uranium imports the fuels only used at end sector are listed, as well as the upstream charcoal and ethanol technologies, that represent the conversion from raw biomass to the end fuel. Each sector is then represented singularly, each one bounded by the  FTE technologies, with its sectoral-sepcific fuels, the relevant technologies and its energy service demands.

.. image:: ./img/wesm_res.svg
  :width: 1200
  :alt: Reference energy system

 
1.4 Sectors
===========

Agriculture
-----------

The only demand type considered for the agricultural sector is a generic demand type, representing fuel cconsumption to operate the agricultural machinery. There is one technology option per fuel type, and fuels considered are diesel, gasoline and heavy fuel oil.

.. image:: ./img/wesm_agriculture.svg
  :width: 1200
  :alt: Agricultural sector

Commercial sector
-----------------

A generic demand is also considered for the commercial sector. In this case, only electrical appliances are considered as a technology option to cover the demand, as the generic demand only consists of electricity.

.. image:: ./img/wesm_commercial.svg
  :width: 1200
  :alt: Commercial sector
  
Industry
--------

The industrial sector is slightly more complex than the first two. Three different types of demand are considered: non metals and cement, food processing, and other processes. The demand for the non metals and cement subsector can only be covered by technologies using coal as fuel. Similarly, only electricty is considered as an option for the food processing subsector. The other processes subsector includes several different processes, including steel production. Technologies considered are based on various fuels inputs, including coal, electricity, diesel, hevy fuel oil and kerosene.

.. image:: ./img/wesm_industry.svg
  :width: 1200
  :alt: Industrial sector

Residential sector
------------------

The residential sector is the most complex sector included in the model, as it also represents the highest share of the final energy consumption in the country. Demands are divided between lighting, cooling, cooking and other. Each demand is split between urban and rural areas, to account for the significant differences in the two areas. Cooling and other demands can only be satisfied by technologies using electricity as an input fuel. Lighting options include both electricity and kerosene. Finally, the cooking sector offers numerous technology options, including diffent ones for the same type of fuel. For examples, e-cooking technologies considered are coil, induction and electric pressure cookers, while wood stoves can be either traditional or improved, as in the case of charcoal.

.. image:: ./img/wesm_residential.svg
  :width: 1200
  :alt: Residential sector
  
Transports
----------

Transports include national aviation and shipping, the railway system and road transport. The latter is divided between buses, cars, freight, light commercial vehicles, and two- and three-wheelers. Each of the subsector of road transport has three technology options, namely diesel, gasoline, and electricity, with the excpetion of freight transport, where only diesel and gasoline are considered. Aviation demand can only be satisfied by technologies using jet fuel, shipping by technologies using heavy fuel oil and only electric trains are considered.

.. image:: ./img/wesm_transports.svg
  :width: 1200
  :alt: Transport sector