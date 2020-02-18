# VE-STATE Tutorial
----


## VESTATE

VE-STATE is an extension of RSPM models, namely VERSPM, which enables users to apply the model for statewide applications. In order to develop VE-STATE, VE-RSPM modules has been tested and modified to confirm that they will work in a statewide application.
The main difference between VE-RSPM models and VE-STATE models is that VE-STATE has been adjusted for a level of detail expected with a statewide view.  Essentially VE-STATE models run at a higher level of abstraction than VE-RSPM models, that is the most detailed geographic detail (Bzones) that are inputs in VE-RSPM, are synthesized in VE-State from inputs at the Azone (typically county) and MArea (full metropolitan area, census urbanized area) levels.  This greatly simplifies the user inputs on the demographic and land use inputs.  Additionally, all VE-RSPM Bzone inputs, instead use an "area-type" classification in VE-State.  Example inputs include parking and travel demand management policy actions. Once at a common geography, VE-State used the same methods, many (non-Bzone) of the same inputs and the same outputs as VE-RSPM. 

## Area Types in VESTATE

Area types are designated based on a combination of activity density and destination accessibility levels. Each is split into 4 levels. Area type is determined by 16 combinations of those levels.

Following are the activity density level definitions:
 * Very Low :  0 to 0.5 household and jobs per acre
 * Low :  0.5 to 5 household and jobs per acre
 * Moderate :  5 to 10 household and jobs per acre
 * High :  more than 10 household and jobs per acre
 
Following are the destination accessibility level definitions:
 * Very Low :  0 to 2000 units
 * Low :   2,000 to 10,000 units
 * Moderate :   10,000 to 50,0000 units
 * High :   more than 50,000 units
 
 Following table classifies area types by activity density and destination accessibility levels. Rows represent activity density and columns represent destination accessibility levels.

|       	  | Very Low       | Low        | Moderate   | High |
| ----------- | -------------- | ---------- | ---------- | ---------- |
| Very Low    | fringe  | fringe         | outer     | outer |
| Low  | fringe  | outer         | outer      | inner |
| Moderate     | outer  | outer         | inner      |inner|
| High   | outer  | inner         | center      |center|

# VESTATE Vs. VERSPM

The main difference between VE-RSPM models and VE-STATE models is that a number of VE-RSPM inputs are specified at the Bzone leve. The following diagrams show how these two model differes at the early stages.
VESTATE uses simulation methods to generate land use and housing input in Bzone level.

	*** VERSPM


<img align="center" width="600" border=1 src="images/VE-RSPM.png">

	*** VESTATE


<img align="center" width="600" border=1 src="images/VE-State.png">

 
Bzone level attributes are required by a number of modules so methods need to be developed for synthesizing a representative set of Bzones and their characteristics from policies and attributes specified at the Azone and Marea levels. Something like this is done in the GreenSTEP model where a likely distribution of neighborhood population density is synthesized from the overall metropolitan area density. Azone level inputs are provided for base year population and area by development type (metropolitan, town, rural), population growth by development type, and the ratio of urban area growth to population growth. From these inputs, average density is calculated by Azone and development type and a model is applied to synthesize a distribution of neighborhood densities from the average density. 
All of the VE-RSPM modules which assign Bzone characteristics are contained in the VELandUse package. The modules that are developed to synthesize Bzones and their characteristics will be placed in a VESimLandUse package. When a VE-STATE model is run, the modules in the VESimLandUse package will be run instead of the modules in the VELandUse package. Otherwise the model setup will be almost the same for VE-STATE and VE-RSPM.

- Note :  Advanced users can use the VESimLandUse modules in non-statewide applications. For example, the VE-State methods might allow users to simulate Bzones in a VE-RSPM application, enabling metropolitan area planners to more easily define and model alternative land use scenarios as is done in RPAT (Rapid Policy Analysis Tool) applications

# VE-State Bzone Synthesis 

Land use modeling in VE-RSPM is more complex than in the RSPM. There are two reasons for this. First, modules were designed to produce datasets needed to run the new multi-modal travel model. This module require several activity density, diversity (i.e. activity mixing), and destination accessibility measures that in turn require households and employment to be located at the Bzone level to calculate those measures. In addition, a few multi-modal network and service level measures need to be calculated. Second, locating jobs at the Bzone level opened up opportunities for significant improvements to the travel demand management (TDM) and parking pricing modules to establish more realistic relationships between policies and the households they would affect. It was a simple extension to locate household workers at job sites and then use that information of translate job site TDM and parking policies back to households. Finally, is how simulated households are assigned to Bzones. In VE-RSPM a numbers of single family and multifamily dwelling units are assigned to Bzones as inputs along with the relative income distribution of households in each Bzone. VE-RSPM models the housing choice of each household based on the overall supply of housing of each type in the Azone and the household characteristics. Then the model assigns each household to a Bzone based on the household’s housing choice and income, and on the relative supplies of housing of the type and household income distribution in the Bzone. The Bzone attributes that need to be synthesized are: 

-  Destination accessibility (i.e. accessibility to jobs and housing) measured consistent as it is used in the multi-modal travel model – This information is one of the 5D measured used in the new RSPM multi-modal travel model. In the RSPM it is calculated from numbers of households and jobs and zone centroid locations. Since synthetic zones won’t have physical locations, it can’t be calculated simply from households and employment by zone
-  Number of households proportional split of dwelling units between single family and multifamily – Number of households and dwelling unit split by Bzone is needed in order to assign households to Bzones. 
-  Number of jobs by sector (retail, service, other) is used in calculating several diversity measures used in the RSPM multi-modal travel model. The number of jobs is also used to associate household workers with workplace Bzones
-  Area type and development type – Some practical system of zonal development classification is needed for organizing policy inputs. In VERSPM, 3 development types are used. These are called metropolitan, town, and rural. It is proposed that a classification system merge these development types with the place type system used in RPAT where place types are defined as a combination of area types and development types (see [Area Types in VESTATE](#AreaTypesinVESTATE) ). Policies such as travel demand management policies will be specified by Azone and area type and/or development type. These designations will also be used in the calculation of the design and distance to transit ‘5D’ measure categories that are used in the RSPM multi-modal travel model

# Approach for Synthesizing Bzones and their Attributes 

1. The user provides inputs on:  
-  Azone proportional split of dwelling units by location type (metropolitan, town and rural) 
-  Azone proportional split of workers by job site location types  (For example proportions of rural residents in the Azone who work in rural locations, town locations, or the metropolitan area) 
-  Marea proportional split of Marea employment among Azones


2. Total activity – numbers of households and jobs –  determine the number of SimBzones in the Azone. SimBzones have equal amounts of activity and unequal areas since activity density varies among SimBzones. An appropriate average SimBzone activity value is be determined through evaluation of the Smart Location Database (SLD)

3. Models are be applied to select a destination accessibility value for each Bzone. For metropolitan type development, the model creates a distribution of destination accessibility values that is consistent with the overall activity density in the metropolitan area. Random sampling from the distribution is used to assign destination accessibility values to metropolitan SimBzones. Models are developed for town and rural types.

4. Activity density of each SimBzones is determined as a function of the destination accessibility of each zone (because destination accessibility is a measure of activity density at a larger geographic scale). A model is estimated from the SLD which creates a distribution of zone densities as a function of destination accessibility. An adjustment process, such as an iterative proportional fitting process (IPF), is used to adjust densities and destination accessibilities so that the overall activity density of all the zones in a metropolitan area is equal to the input value

5. Further subdivision of the metropolitan area into area types are done as a function of the destination accessibility and activity density of each zone. 4 such area types are proposed which meld the RPAT types with GreenSTEP/EERPAT location types: urban core, close in community, and suburban/town, low density/rural. The final typology and the relationship of area types to destination accessibility and activity density are developed through examination of the SLD dataset. It is envisioned that area types are defined as fuzzy sets rather than crisp sets.  Although some SimBzones may be wholly one type, many SimBzones have degrees of membership in several types. Using fuzzy sets is a more realistic recognition of the nature of area types and avoids aberrations resulting from threshold effects. 

6. The total activity in each SimBzone is split into households and jobs using a model which relates zonal mixing to destination accessibility, activity density, and area type. This model is specified and estimated based on investigations using the SLD data. It is anticipated that the model produces distributions of activity splits from which values will be drawn. IPF or some other adjustment process is used to adjust values so that the aggregation of the splits for all the SimBzones in an Azone is consistent with the Azone inputs. This model needs to specify the split of land area between households and jobs. 

7. Once the number of households is determined for each SimBzone, the split of dwelling units by housing type (single family, multifamily) as a function of activity density. The SLD and census data are used to develop this model. IPF or some other adjustment process are used to fit the distribution of SimBzone values to Azone level control totals. This allows users to specify Azone ratios as policy inputs. 

8. A variant of the VE-RSPM housing model is applied to assign households to housing types and to Bzones. One thing to be worked out is whether the allocation to SimBzones considers household income or not. In the RSPM, relative Bzone income distributions are input and these are used in the process of allocating households to Bzones. Something similar could be done by Azone and area type for VE-STATE. This would enable VE-STATE users to model general relationships of income to parts of the metropolitan area (e.g. the effect of gentrification in the urban core). 

9. Jobs in each SimBzone is split into numbers of retail, service, and other jobs. The approach for doing this is yet to be determined. SimBzone splits is constrained so that they total to Azone splits that are inputs. The model is a function of the destination accessibility, employment density, and mixing of households and employment in the SimBzone. The SLD data is used to develop and estimate this model. Thought is given as to whether there should be control totals on the mix for a metropolitan area.  If so, IPF or some other adjustment process would need to be used to match the totals. 

10. Workers are assigned to SimBzone job sites. How this is done is yet to be determined. It is proposed that an agile development approach be used where the first iteration of the model will be a random assignment of workers to job sites. Other extensions that could be considered if there is time/budget investigation could be done using LEHD data and SLD data to look for relationships between worker residence by area type and worker job site by area type. Relative income could also be considered.

11. Once numbers of households and numbers of jobs by type are assigned to SimBzones, all the remaining density and diversity measures can be calculated. 

12. The distance to transit measure is modeled for metropolitan SimBzones as a function of the metropolitan-level transit supply measure and the SimBzone attributes for destination 

13. Development type, like the RPAT development types (e.g. residential, employment, mixed, transit-oriented development, greenfield), is assigned to SimBzones based on the density, diversity, and distance to transit measures. These development types, like the area types may be fuzzy sets. The SLD is used to create the development type specifications. The design enables model users to input Marea goals for the proportional split of development types. The model adjusts the allocation of development types consistent with the goals but constrained to plausible levels. 

14. Network design measures used by the RSPM multi-modal travel model (e.g. multi-modal network density, pedestrian network density) is applied based on inputs related to area and development type. The SLD is used to identify ranges of values by area and development type. Users specify in inputs goals relative to these ranges by Azone, development type and area type.

15.  The parking pricing, travel demand management, and car service inputs are specified by Azone, area type, and development type. These are then translated to the SimBzone based on the SimBzone area type and development type. After that is done, the AssignDemandManagement, AssignParkingRestrictions, and AssignCarSvcAvailability modules can run as they currently do. Thought will be given as to how to simplify inputs so that users are not required to provide inputs for every combination of Azone, area type and development type.

For more information on simuling Bzones process see [here](https://github.com/VisionEval/VisionEval-Dev/blob/master/sources/modules/VESimLandUse/inst/module_docs/CreateSimBzones.md)


## Sections
This tutorial contains the following sections:

* [Modules and Outputs](Modules_and_Outputs.md): a detailed identification Modules and their inputs and outputs
* [Inputs and Parameters](Inputs_and_Parameters.md): a detailed descriptiopn of model inputs modification
* [Running the Model](Running_VESTATE.md): step by step manual to run the model;
* [Performance Metrics](Performance.md): an overview of the model outcomes;

