# Building and evaluation of a PBPK model for Dabigatran in healthy adults

| Version                                         | master-OSP12.2                                                   |
| ----------------------------------------------- | ------------------------------------------------------------ |
| based on *Model Snapshot* and *Evaluation Plan* | https://github.com/Open-Systems-Pharmacology/Dabigatran-Model/releases/tag/vmaster |
| OSP Version                                     | 12.2                                                          |
| Qualification Framework Version                 | 3.5                                                          |

This evaluation report and the corresponding PK-Sim project file are filed at:

https://github.com/Open-Systems-Pharmacology/OSP-PBPK-Model-Library/

# Table of Contents

 * [1 Introduction](#intro)
 * [2 Methods](#methods)
   * [2.1 Modeling Strategy](#strategy)
   * [2.2 Data](#data)
     * [2.2.1 In vitro / physico-chemical Data ](#invitro-and-physico-chemical-data)
     * [2.2.2 Clinical Data  ](#clinical-data)
       * [2.2.2.1 Model Building ](#model-building)
       * [2.2.2.2 Model Verification ](#model-verification)
   * [2.3 Model Parameters and Assumptions](#assumptions)
     * [2.3.1 Absorption ](#model-parameters-and-assumptions-absorption)
     * [2.3.2 Distribution ](#model-parameters-and-assumptions-distribution)
     * [2.3.3 Metabolism and Elimination ](#model-parameters-and-assumptions-metabolism-and-elimination)
     * [2.3.4 Automated Parameter Identification ](#model-parameters-and-assumptions-parameter-identification)
 * [3 Results and Discussion](#results)
   * [3.1 Final input parameters](#parameters)
   * [3.2 Diagnostic Plots](#plots)
   * [3.3 Concentration-Time Profiles](#profiles)
     * [3.3.1 Model Building](#training)
     * [3.3.2 Model Verification](#test)
 * [4 Conclusion](#conclusion)
 * [5 References](#references)

# 1 Introduction<a id="intro"></a>

Dabigatran is an oral direct thrombin inhibitor administered as the pharmacologically inactive prodrug dabigatran etexilate. Following its absorption, dabigatran etexilate undergoes enzymatic hydrolysation via the carboxylesterases CES1 in the liver and CES2 in the intestine to produce the active moiety dabigatran. The processes involved in the absorption, distribution, metabolism and excretion for dabigatran result in low oral bioavailability (~6–7%) and moderate interindividual variability.

Following the activation of the prodrug to dabigatran (or following intravenous administration of dabigatran itself), dabigatran undergoes glucuronidation to dabigatran acylglucuronide, which contributes to total active exposure. Therefore, often the sum of dabigatran + dabigatran glucuronide = "total dabigatran" is reported. Absorption of the prodrug dabigatran etexilate is strongly influenced by P-glycoprotein (Pgp), making Pgp activity a key determinant of systemic dabigatran exposure and drug–drug interaction (DDI) potential.

The presented whole-body PBPK model is based on the model developed by [Moj et al. 2019](#main-references) and includes dabigatran etexilate, dabigatran and the pharmacologically active metabolite dabigatran acylglucuronide. It was established to be used for DDI prediction, because dabigatran etexilate is a widely used Pgp substrate in clinical DDI studies.  

The herein presented model building and evaluation report evaluates the performance of the PBPK model for dabigatran in healthy adults. 

# 2 Methods<a id="methods"></a>

## 2.1 Modeling Strategy<a id="strategy"></a>

The general concept of building a PBPK model has previously been described by Kuepfer et al. ([Kuepfer 2016](#main-references)). Data regarding the relevant anthropometric (height, weight) and physiological parameters (e.g. blood flows, organ volumes, binding protein concentrations, hematocrit, cardiac output) in adults was gathered from the literature and has been previously published ([PK-Sim Ontogeny Database](#main-references)). This information was incorporated into PK-Sim® and was used as default values for the simulations in adults.

The applied activity and variability of plasma proteins and active processes that are integrated into PK-Sim® are described in the publicly available PK-Sim® Ontogeny Database or otherwise referenced for the specific process ([Schlender 2016](#main-references)).

The dabigatran PBPK model was developed using a stepwise modeling strategy. First, an intravenous dabigatran model was established to describe distribution and elimination processes, including UGT2B15-mediated glucuronidation of dabigatran to dabigatran glucuronide as well as the renal clearance of both entities. 

As many clinical reports provide "total dabigatran" = (dabigatran + dabigatran glucuronide) plasma concentrations instead of dabigatran glucuronide measurements, an observer for "dabigatran sum" was incorporated and used in parameter identifications. In addition, observers for fraction excreted to urine following intravenous administration of dabigatran (for dabigatran glucuronide) and fraction excreted to urine following oral administration of dabigatran etexilate (for dabigatran and dabigatran glucuronide) were implemented. 

Then, the model was extended to include the orally administered prodrug dabigatran etexilate. This step required incorporation of Pgp-mediated transport affecting its absorption and CES1/CES2-mediated prodrug activation to produce dabigatran. 

The respective contributions of CES1 and CES2 were informed by data from the RE-LY trial ([Paré 2013](#main-references)), reporting that patients carrying 2 minor CES1 alleles (modeled as complete loss of CES1 activity) show a 28% reduction of their total dabigatran plasma concentration trough values (dabigatran + dabigatran glucuronide). 

While the original model considered data of 2 different clinical DDI studies (rifampicin-mediated Pgp induction ([Härtter 2012](#main-references)) and clarithromycin-mediated Pgp inhibition ([Delavenne 2012](#main-references))), data of 7 further clinical DDI trials were included for the model update, adding Pgp inhibition by rifampicin (n=2), itraconazole (n=1), verapamil (n=1), and additional clarithromycin studies (n=3). 

Unknown parameters were identified using the PK‑Sim® Parameter Identification module. Model evaluation included comparison of predicted versus observed concentration–time profiles, goodness-of-fit plots, and geometric mean fold error (GMFE) analysis.

Details about input data (physico-chemical, *in vitro* and clinical) can be found in [Section 2.2](#methods-data).

Details about the structural model and its parameters can be found in [Section 2.3](#model-parameters-and-assumptions).

## 2.2 Data<a id="data"></a>

### 2.2.1 In vitro / physico-chemical Data <a id="invitro-and-physico-chemical-data"></a>

A literature search was performed to collect available information on physico-chemical properties of dabigatran etexilate, dabigatran and dabigatran glucuronide. The obtained information from literature is summarized in the table below. 

#### Dabigatran etexilate 
| **Parameter**   | **Unit** | **Value** | Source                                     | **Description**                                 |
| :-------------- | -------- | --------- | ------------------------------------------ | ----------------------------------------------- |
| MW              | g/mol    | 627.73          | [Moj 2019](#main-references)               | Molecular weight                                |
| pK<sub>a</sub>  |          | 4.0, 6.7          | [Zhao 2014](#main-references)         | Acid dissociation constant                      |
| Solubility (pH) | mg/mL         | 1.8 (7.0)         | [Moj 2019](#main-references)               | Aqueous Solubility                |
| logP            |          | 3.8          | [Zhao 2014](#main-references) | Partition coefficient between octanol and water |
| fu              | %        | 7          | [Moj 2019](#main-references)                | Fraction unbound in plasma                      |

#### Dabigatran  
| **Parameter**   | **Unit** | **Value** | Source                                     | **Description**                                 |
| :-------------- | -------- | --------- | ------------------------------------------ | ----------------------------------------------- |
| MW              | g/mol    | 471.51          | [Moj 2019](#main-references)               | Molecular weight                                |
| pK<sub>a</sub>  |          | 4.1, 4.4, 12.4           | [Zhao 2014](#main-references)         | Acid dissociation constant                      |
| Solubility (pH) | mg/mL         | 0.017 (7.0)          | [Moj 2019](#main-references)               | Aqueous Solubility                 |
| logP            |          | -2.2          | [Zhao 2014](#main-references) | Partition coefficient between octanol and water |
| fu              | %        | 65          | [Moj 2019](#main-references)                | Fraction unbound in plasma                      |
| B/P ratio       |          | 0.67          | [Moj 2019](#main-references)                | Blood to plasma ratio                           |

#### Dabigatran glucuronide 
| **Parameter**   | **Unit** | **Value** | Source                                     | **Description**                                 |
| :-------------- | -------- | --------- | ------------------------------------------ | ----------------------------------------------- |
| MW              | g/mol    | 647.23          | [Moj 2019](#main-references)               | Molecular weight                                |
| pK<sub>a</sub>  |          | 4.1, 4.4, 12.4          | [Moj 2019](#main-references)         | Acid dissociation constant                      |
| logP            |          | -4.15          | [Moj 2019](#main-references) (in-silico) | Partition coefficient between octanol and water |
| fu              | %        | 65          | [Moj 2019](#main-references)                | Fraction unbound in plasma                      |

### 2.2.2 Clinical Data  <a id="clinical-data"></a>

A search was performed to collect available clinical data on dabigatran in healthy adults.

#### 2.2.2.1 Model Building <a id="model-building"></a>

The following studies were used for model building (training data):

| Source                      | Arm / Treatment / Information used for model building |
| :-------------------------- | :---------------------------------------------------- |
| 1160-0005 internal clinical trial report 2001 | Intravenous infusion of 0.1 mg (single dose)          |
| 1160-0005 internal clinical trial report 2001 | Intravenous infusion of 1.0 mg (single dose)          |
| 1160-0005 internal clinical trial report 2001 | Intravenous infusion of 5.0 mg (single dose)          |
| 1160-0061 internal clinical trial report 2006 | Oral capsule administration of 110 mg and 150 mg (twice daily)          |
| 1160-0194 internal clinical trial report 2014 | Oral solution administration of 150 mg (twice daily)          |
| 1160-0194 internal clinical trial report 2014 | Oral capsule administration of 150 mg (twice daily)          |
| [Blech 2008](#main-references) | Oral solution administration of 200 mg (single dose)           |
| [Härtter 2012](#main-references) | Oral capsule administration of 150 mg (single dose)           |

#### 2.2.2.2 Model Verification <a id="model-verification"></a>

The following studies were used for model verification (test data):

| Source                      | Arm / Treatment / Information used for model verification |
| :-------------------------- | :---------------------------------------------------- |
| 1160-0074 internal clinical trial report 2009 | Oral capsule administration of 150 mg (single dose)           |
| 1160-0082 internal clinical trial report 2008 | Oral capsule administration of 150 mg (single dose)           |
| [Delavenne 2012](#main-references) | Oral capsule administration of 300 mg (single dose)           |

## 2.3 Model Parameters and Assumptions<a id="assumptions"></a>

### 2.3.1 Absorption <a id="model-parameters-and-assumptions-absorption"></a>

Absorption of dabigatran etexilate is influenced by intestinal permeability and Pgp transport. The calculated value was used for `Specific intestinal permeability`. The value for Pgp kcat was estimated, informed by Rifampicin-Dabigatran Pgp-induction DDI data. 

The dissolution of capsules was implemented via an empirical Weibull function, using the Weibull parameters from the original model by [Moj et al. 2019](#main-references). 

### 2.3.2 Distribution <a id="model-parameters-and-assumptions-distribution"></a>

After testing the available organ-plasma partition coefficient and cell permeability calculation methods built in PK-Sim, observed clinical data was best described by choosing the partition coefficient calculation by `Rodgers and Rowland` and cellular permeability calculation by `PK-Sim Standard` for all three compounds. 
For the model parameter `Specific organ permeability` the calculated values were used for all three compounds, with the `Lipophilicity` values optimized to best match clinical data (see [Section 2.3.4](#model-parameters-and-assumptions-absorption)). 

### 2.3.3 Metabolism and Elimination <a id="model-parameters-and-assumptions-metabolism-and-elimination"></a>

- For dabigatran etexilate the final model includes transport by Pgp, prodrug ester cleavage by CES1 and CES2 and passive renal filtration (trace amounts excreted in urine following oral administration). 
- For dabigatran the final model includes glucuronidation by UGT2B15 and renal excretion (70.6-76.2% excreted in urine following intravenous, 4.3% excreted in urine following oral administration). 
- For dabigatran glucuronide the final model includes renal excretion only, implemented with the GFR fraction parameter value from the original model by [Moj et al. 2019](#main-references). Dabigatran glucuronide in urine is not meaningful in clinical practice (2.7-6.4% excreted in urine following intravenous, 0.4% excreted in urine following oral administration) and there is little data to inform the estimation of dabigatran glucuronide GFR fraction. 

### 2.3.4 Automated Parameter Identification <a id="model-parameters-and-assumptions-parameter-identification"></a>

These are the results of the two final sequential parameter identifications.
1. iv: 

| Model Parameter      | Optimized Value | Unit |
| -------------------- | --------------- | ---- |
| `Dabigatran logP` | 1.1436481967                |      |
| `Dabigatran UGT2B15 kcat` | 4.2993761606                | 1/min     |
| `Dabigatran GFR fraction` | 1.2278243749                |      |
| `Dabigatran glucuronide logP` | -0.80                |      |
| `Dabigatran glucuronide GFR fraction` | 6.36 (fixed)                |      |

2. oral: 

| Model Parameter      | Optimized Value | Unit |
| -------------------- | --------------- | ---- |
| `Dabigatran etexilate logP` | 1.8088312812                |      |
| `Dabigatran etexilate Pgp kcat` | 0.46                | 1/min     |
| `Dabigatran etexilate CES1 kcat` | 10.8149677921                | 1/min     |
| `Dabigatran etexilate CES2 kcat` | 0.7209978528                | 1/min     |
| `Dabigatran etexilate GFR fraction` | 1.00 (fixed)                |      |

# 3 Results and Discussion<a id="results"></a>

The PBPK model for dabigatran was developed and verified using clinical pharmacokinetic data from the studies listed in [Section 2.2.2](#clinical-data). 
In addition, 9 different Pgp-DDI studies were used to qualify the model for its application as Pgp substrate in DDI predictions. 

The model was evaluated covering data from studies including: 
* intravenous (infusion) and oral administration (solution and capsules, single and multiple dose)
* a dose range of 0.1 to 300 mg 

The model includes Pgp transport and CES1/CES2-mediated hydrolysation of the prodrug dabigatran etexilate, UGT2B15-mediated glucuronidation of dabigatran, and renal secretion of dabigatran glucuronide. 

The next sections show:
1. the final model parameters for the building blocks: [Section 3.1](#final-input-parameters)
2. the overall goodness of fit: [Section 3.2](#plots)
3. simulated versus observed concentration-time profiles for the clinical studies used for model building and for model verification: [Section 3.3](#profiles) 

## 3.1 Final input parameters<a id="parameters"></a>

The compound parameter values of the final PBPK model are illustrated below.

### Compound: DabiEtex

#### Parameters

Name                                       | Value                  | Value Origin                                                                                                                             | Alternative | Default
------------------------------------------ | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------
Solubility at reference pH                 | 1.8 mg/ml              |                                                                                                                                          | Measurement | True   
Reference pH                               | 7                      |                                                                                                                                          | Measurement | True   
Lipophilicity                              | 1.8088312812 Log Units | Parameter Identification-Parameter Identification-Value updated from '#11 - P-gp 0.46, DabiGluc logP -0.80, CESlink' on 2026-03-05 10:32 | Measurement | True   
Fraction unbound (plasma, reference value) | 0.07                   |                                                                                                                                          | Measurement | True   
Is small molecule                          | Yes                    |                                                                                                                                          |             |        
Molecular weight                           | 627.73 g/mol           |                                                                                                                                          |             |        
Plasma protein binding partner             | Albumin                |                                                                                                                                          |             |        

#### Calculation methods

Name                    | Value              
----------------------- | -------------------
Partition coefficients  | Rodgers and Rowland
Cellular permeabilities | PK-Sim Standard    

#### Processes

##### Transport Protein: ABCB1-FIT

Molecule: ABCB1

###### Parameters

Name                      | Value        | Value Origin                                                                                                                            
------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------
Transporter concentration | 1 µmol/l     |                                                                                                                                         
Vmax                      | 0 µmol/l/min |                                                                                                                                         
Km                        | 0.08 µmol/l  |                                                                                                                                         
kcat                      | 0.46 1/min   | Parameter Identification-Parameter Identification-Value updated from '#11 - P-gp 0.46, DabiGluc logP -0.80, CESlink' on 2026-03-05 10:32

##### Metabolizing Enzyme: CES1-FIT

Molecule: CES1

Metabolite: Dabigatran

###### Parameters

Name                               | Value                      | Value Origin                                                                                                                            
---------------------------------- | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------
In vitro Vmax for liver microsomes | 0 pmol/min/mg mic. protein |                                                                                                                                         
Km                                 | 24.9 µmol/l                |                                                                                                                                         
kcat                               | 10.8149677921 1/min        | Parameter Identification-Parameter Identification-Value updated from '#11 - P-gp 0.46, DabiGluc logP -0.80, CESlink' on 2026-03-05 10:32

##### Metabolizing Enzyme: CES2-FIT

Molecule: CES2

Metabolite: Dabigatran

###### Parameters

Name                               | Value                      | Value Origin                                                                                                                            
---------------------------------- | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------
In vitro Vmax for liver microsomes | 0 pmol/min/mg mic. protein |                                                                                                                                         
Km                                 | 5.5 µmol/l                 |                                                                                                                                         
kcat                               | 0.7209978528 1/min         | Parameter Identification-Parameter Identification-Value updated from '#11 - P-gp 0.46, DabiGluc logP -0.80, CESlink' on 2026-03-05 10:32

##### Systemic Process: Glomerular Filtration-DabiEtex

Species: Human

###### Parameters

Name         | Value | Value Origin
------------ | -----:| ------------:
GFR fraction |     1 |             

### Compound: DabiGluc

#### Parameters

Name                                       | Value          | Value Origin                                                                                                                             | Alternative | Default
------------------------------------------ | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------
Solubility at reference pH                 | 1.8 mg/ml      |                                                                                                                                          | Measurement | True   
Reference pH                               | 7              |                                                                                                                                          | Measurement | True   
Lipophilicity                              | -0.8 Log Units | Parameter Identification-Parameter Identification-Value updated from '#11 - P-gp 0.46, DabiGluc logP -0.80, CESlink' on 2026-03-04 18:22 | Measurement | True   
Fraction unbound (plasma, reference value) | 0.65           |                                                                                                                                          | Measurement | True   
Is small molecule                          | Yes            |                                                                                                                                          |             |        
Molecular weight                           | 647.23 g/mol   |                                                                                                                                          |             |        
Plasma protein binding partner             | Albumin        |                                                                                                                                          |             |        

#### Calculation methods

Name                    | Value              
----------------------- | -------------------
Partition coefficients  | Rodgers and Rowland
Cellular permeabilities | PK-Sim Standard    

#### Processes

##### Systemic Process: Glomerular Filtration-DabiGluc

Species: Human

###### Parameters

Name         | Value | Value Origin
------------ | -----:| ------------:
GFR fraction |  6.36 |             

### Compound: Dabigatran

#### Parameters

Name                                       | Value                  | Value Origin                                                                                                                      | Alternative | Default
------------------------------------------ | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------
Solubility at reference pH                 | 0.017 mg/ml            |                                                                                                                                   | Measurement | True   
Reference pH                               | 7                      |                                                                                                                                   | Measurement | True   
Lipophilicity                              | 1.1436481967 Log Units | Parameter Identification-Parameter Identification-Value updated from '#7 - iv (logP, logP, UGT, GFR)_best iv' on 2025-08-30 15:56 | Measurement | True   
Fraction unbound (plasma, reference value) | 0.65                   |                                                                                                                                   | Measurement | True   
Is small molecule                          | Yes                    |                                                                                                                                   |             |        
Molecular weight                           | 471.51 g/mol           |                                                                                                                                   |             |        
Plasma protein binding partner             | Albumin                |                                                                                                                                   |             |        

#### Calculation methods

Name                    | Value              
----------------------- | -------------------
Partition coefficients  | Rodgers and Rowland
Cellular permeabilities | PK-Sim Standard    

#### Processes

##### Metabolizing Enzyme: UGT2B15-FIT

Molecule: UGT2B15

Metabolite: DabiGluc

###### Parameters

Name                               | Value                      | Value Origin                                                                                                                     
---------------------------------- | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------
In vitro Vmax for liver microsomes | 0 pmol/min/mg mic. protein |                                                                                                                                  
Km                                 | 512 µmol/l                 |                                                                                                                                  
kcat                               | 4.2993761606 1/min         | Parameter Identification-Parameter Identification-Value updated from '#7 - iv (logP, logP, UGT, GFR)_best iv' on 2025-08-30 15:56

##### Systemic Process: Glomerular Filtration-Dabi

Species: Human

###### Parameters

Name         |        Value | Value Origin                                                                                                                     
------------ | ------------:| ---------------------------------------------------------------------------------------------------------------------------------
GFR fraction | 1.2278243749 | Parameter Identification-Parameter Identification-Value updated from '#7 - iv (logP, logP, UGT, GFR)_best iv' on 2025-08-30 15:56

### Formulation: DabiEtex_Capsule

Type: Weibull

#### Parameters

Name                             | Value      | Value Origin
-------------------------------- | ---------- | ------------:
Dissolution time (50% dissolved) | 1.0579 min |             
Lag time                         | 0 min      |             
Dissolution shape                | 0.2628     |             
Use as suspension                | No         |             

## 3.2 Diagnostic Plots<a id="plots"></a>

Below you find the goodness-of-fit visual diagnostic plots for the PBPK model performance of all data used presented in [Section 2.2.2](#clinical-data).

The first plot shows observed versus simulated plasma concentration, the second weighted residuals versus time. 

<a id="table-3-1"></a>

**Table 3-1: GMFE for Goodness of fit plot for concentration in plasma**

|Group                               |GMFE |
|:-----------------------------------|:----|
|Intravenous infusion                |1.14 |
|Oral capsule                        |1.24 |
|Oral capsule - Verification dataset |1.76 |
|Oral solution                       |1.80 |
|All                                 |1.42 |

<br>
<br>

<a id="figure-3-1"></a>

![](images/006_section_Results/008_section_Plots/2_gof_plot_predictedVsObserved.png)

**Figure 3-1: Goodness of fit plot for concentration in plasma**

<br>
<br>

<a id="figure-3-2"></a>

![](images/006_section_Results/008_section_Plots/3_gof_plot_residualsOverTime.png)

**Figure 3-2: Goodness of fit plot for concentration in plasma**

<br>
<br>

## 3.3 Concentration-Time Profiles<a id="profiles"></a>

Simulated versus observed concentration-time profiles of all data listed in [Section 2.2.2](#clinical-data) are presented below.

### 3.3.1 Model Building<a id="training"></a>

<a id="figure-3-3"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/1_time_profile_plot_Dabigatran_1160_0005___0_1_mg_iv.png)

**Figure 3-3: 1160-0005 - Dabigatran iv 0.1 mg - log**

<br>
<br>

<a id="figure-3-4"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/2_time_profile_plot_Dabigatran_1160_0005___1_0_mg_iv.png)

**Figure 3-4: 1160-0005 - Dabigatran iv 1.0 mg - log**

<br>
<br>

<a id="figure-3-5"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/3_time_profile_plot_Dabigatran_1160_0005___5_0_mg_iv.png)

**Figure 3-5: 1160-0005 - Dabigatran iv 5.0 mg - log**

<br>
<br>

<a id="figure-3-6"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/4_time_profile_plot_Dabigatran_1160_0061___110_150_mg_BID.png)

**Figure 3-6: 1160-0061 - Dabigatran 110+150 mg BID - lin**

<br>
<br>

<a id="figure-3-7"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/5_time_profile_plot_Dabigatran_1160_0194___150_mg_Capsule.png)

**Figure 3-7: 1160-0194 - Dabigatran 150 mg Capsule - lin**

<br>
<br>

<a id="figure-3-8"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/6_time_profile_plot_Dabigatran_1160_0194___150_mg_Solution.png)

**Figure 3-8: 1160-0194 - Dabigatran 150 mg Solution - lin**

<br>
<br>

<a id="figure-3-9"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/7_time_profile_plot_Dabigatran_Blech_2008___200_mg_Solution.png)

**Figure 3-9: Blech 2008 - Dabigatran 200 mg Solution - log**

<br>
<br>

<a id="figure-3-10"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/11_time_profile_plot_Dabigatran_Hartter_2012___DDI_Control.png)

**Figure 3-10: Härtter 2012 - Dabigatran DDI Control - lin**

<br>
<br>

### 3.3.2 Model Verification<a id="test"></a>

<a id="figure-3-11"></a>

![](images/006_section_Results/009_section_Profiles/011_section_Test/8_time_profile_plot_Dabigatran_Delavenne_2012___DDI_Control.png)

**Figure 3-11: Delavenne 2012 - Dabigatran DDI Control - lin**

<br>
<br>

<a id="figure-3-12"></a>

![](images/006_section_Results/009_section_Profiles/011_section_Test/9_time_profile_plot_Dabigatran_1160_0074___DDI_Control.png)

**Figure 3-12: 1160-0074 - Dabigatran DDI Control - lin**

<br>
<br>

<a id="figure-3-13"></a>

![](images/006_section_Results/009_section_Profiles/011_section_Test/10_time_profile_plot_Dabigatran_1160_0082___DDI_Control.png)

**Figure 3-13: 1160-0082 - Dabigatran DDI Control - lin**

<br>
<br>

# 4 Conclusion<a id="conclusion"></a>

The herein presented PBPK model adequately describes the pharmacokinetics of dabigatran etexilate, dabigatran, and dabigatran glucuronide in healthy adults.

In particular, it quantitatively reproduces the impact of Pgp on the absorption of dabigatran etexilate, which was qualified against the clinical data of 9 different Pgp DDI studies. Thus the model is fit for purpose to be applied for the investigation of drug-drug interactions with regard to dabigatran etexilate Pgp transport. 

# 5 References<a id="references"></a>

**Blech 2008** Blech S, Ebner T, Ludwig-Schwellinger E, Stangier J, Roth W. The metabolism and disposition of the oral direct thrombin inhibitor, dabigatran, in humans. Drug Metab Dispos. 2008 Feb;36(2):386–399. doi: 10.1124/dmd.107.019083.  

**Delavenne 2012** Delavenne X, Ollier E, Basset T, Bertoletti L, Accassat S, Garcin A, Laporte S, Zufferey P, Mismetti P. A semi-mechanistic absorption model to evaluate drug–drug interaction with dabigatran: application with clarithromycin. Br J Clin Pharmacol. 2013 Jul;76(1):107–113. doi: 10.1111/bcp.12055.  

**Härtter 2012** Härtter S, Koenen-Bergmann M, Sharma A, Nehmiz G, Lemke U, Timmer W, Reilly PA. Decrease in the oral bioavailability of dabigatran etexilate after co-medication with rifampicin. Br J Clin Pharmacol. 2012 Sep;74(3):490–500. doi: 10.1111/j.1365-2125.2012.04218.x.  

**Kuepfer 2016** Kuepfer L, Niederalt C, Wendl T, Schlender JF, Willmann S, Lippert J, Block M, Eissing T, Teutonico D. Applied Concepts in PBPK Modeling: How to Build a PBPK/PD Model.CPT Pharmacometrics Syst Pharmacol. 2016 Oct;5(10):516-531. doi: 10.1002/psp4.12134. 	

**Moj 2019** Moj D, Maas H, Schaeftlein A, Hanke N, Gómez‑Mantilla JD, Lehr T. A Comprehensive Whole‑Body PBPK Model of Dabigatran Etexilate, Dabigatran and Dabigatran Glucuronide in Healthy Adults and Renally Impaired Patients. Clin Pharmacokinet. 2019. doi: 10.1007/s40262-019-00776-y.  

**Paré 2013** Paré G, Eriksson N, Lehr T, Connolly S, Eikelboom J, Ezekowitz MD, Axelsson T, Haertter S, Oldgren J, Reilly P, Siegbahn A, Syvanen AC, Wadelius C, Wadelius M, Zimdahl-Gelling H, Yusuf S, Wallentin L. Genetic Determinants of Dabigatran Plasma Levels and Their Relation to Bleeding. Circulation. 2013 Apr;127(13):1404–12. doi: 10.1161/CIRCULATIONAHA.112.001233.  

**PK-Sim Ontogeny Database** ([https://github.com/Open-Systems-Pharmacology/OSPSuite.Documentation/blob/master/PK-Sim%20Ontogeny%20Database.pdf](https://github.com/Open-Systems-Pharmacology/OSPSuite.Documentation/blob/master/PK-Sim%20Ontogeny%20Database.pdf)) 

**PK-Sim Open Systems Pharmacology Suite** PK-Sim® and MoBi® Documentation. ([https://github.com/Open-Systems-Pharmacology/OSPSuite.Documentation](https://github.com/Open-Systems-Pharmacology/OSPSuite.Documentation)) 

**Schlender 2016** Schlender JF, Meyer M, Thelen K, Krauss M, Willmann S, Eissing T, Jaehde U. Development of a Whole-Body Physiologically Based Pharmacokinetic Approach to Assess the Pharmacokinetics of Drugs in Elderly Individuals. Clin Pharmacokinet. 2016 Dec;55(12):1573-1589. doi: 10.1007/s40262-016-0422-3. 

**Zhao 2014** Zhao Y, Hu ZY. Physiologically based pharmacokinetic modelling and in vivo [I]/K(i) accurately predict P-glycoprotein-mediated drug-drug interactions with dabigatran etexilate. Br J Pharmacol. 2014 Feb;171(4):1043-53. doi: 10.1111/bph.12533.

