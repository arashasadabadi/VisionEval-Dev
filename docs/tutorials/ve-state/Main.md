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


## Sections
This tutorial contains the following sections:

* [Model Description](Model_Overview.md): a description of the VESTATE model and a broad comparison with VERSPM model;
* [Modules and Outputs](Modules_and_Outputs.md): a detailed identification Modules and their inputs and outputs
* [Inputs and Parameters](Inputs_and_Parameters.md): a detailed descriptiopn of model inputs modification
* [Running the Model](Running_VESTATE.md): step by step manual to run the model;
* [Performance Metrics](Performance.md): an overview of the model outcomes;

