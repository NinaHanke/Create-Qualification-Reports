# Building and evaluation of a PBPK model for COMPOUND in healthy adults

| Version                                         | master-OSP12.2                                                   |
| ----------------------------------------------- | ------------------------------------------------------------ |
| based on *Model Snapshot* and *Evaluation Plan* | https://github.com/Open-Systems-Pharmacology/COMPOUND-Model/releases/tag/vmaster |
| OSP Version                                     | 12.2                                                          |
| Qualification Framework Version                 | 3.5                                                          |

This evaluation report and the corresponding PK-Sim project file are filed at:

https://github.com/Open-Systems-Pharmacology/OSP-PBPK-Model-Library/

# Table of Contents

 * [1 Introduction](#intro)
 * [2 Methods](#methods)
   * [2.1 Modeling Strategy](#strategy)
   * [2.2 Data](#data)
   * [2.3 Model Parameters and Assumptions](#assumptions)
 * [3 Results and Discussion](#results)
   * [3.1 Final input parameters](#parameters)
   * [3.2 Diagnostic Plots](#plots)
   * [3.3 Concentration-Time Profiles](#profiles)
     * [3.3.1 Model Building](#training)
     * [3.3.2 Model Verification](#test)
 * [4 Conclusion](#conclusion)
 * [5 References](#references)

# 1 Introduction<a id="intro"></a>

COMPOUND is an active, highly selective ... (Information about Pharmacology)

COMPOUND is ...  (Information about relevant Pharmacokinetics)

The herein presented model building and evaluation report evaluates the performance of the PBPK model for COMPOUND in (healthy) adults.

The presented COMPOUND PBPK model as well as the respective evaluation plan and evaluation report are provided open-source ([https://github.com/Open-Systems-Pharmacology/COMPOUND-Model](https://github.com/Open-Systems-Pharmacology/COMPOUND-Model)).

Alfentanil is a potent analgesic synthetic opioid. It is fast but short-acting and used for anesthesia during surgery. Alfentanil is metabolized solely by CYP3A4 (Phimmasone 2001). Like midazolam, alfentanil is not a substrate for P-gp (Wandel 2002) and less than 1% of an alfentanil dose is excreted unchanged in urine (Meuldermans 1988).

Although in clinical use alfentanil is always administered intravenously (iv), some DDI studies published plasma concentration-time profiles of alfentanil following oral ingestion. The presented alfentanil model was established using clinical PK data of 8 publications, covering iv and oral (po) administration and a dosing range from 0.015 to 0.075 mg/kg as well as absolute doses of 1 mg iv and 4 mg po. The established model is based on the model developed by Hanke et al. (Hanke 2018) and applies metabolism by CYP3A4 and glomerular filtration.

# 2 Methods<a id="methods"></a>

## 2.1 Modeling Strategy<a id="strategy"></a>

## 2.2 Data<a id="data"></a>

## 2.3 Model Parameters and Assumptions<a id="assumptions"></a>

# 3 Results and Discussion<a id="results"></a>

## 3.1 Final input parameters<a id="parameters"></a>

### Compound: DabiEtex

#### Parameters

Name                                             | Value                  | Value Origin                                                                                                                             | Alternative | Default
------------------------------------------------ | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------
Solubility at reference pH                       | 1.8 mg/ml              |                                                                                                                                          | Measurement | True   
Reference pH                                     | 7                      |                                                                                                                                          | Measurement | True   
Lipophilicity                                    | 1.8088312812 Log Units | Parameter Identification-Parameter Identification-Value updated from '#11 - P-gp 0.46, DabiGluc logP -0.80, CESlink' on 2026-03-05 10:32 | Measurement | True   
Fraction unbound (plasma, reference value)       | 0.07                   |                                                                                                                                          | Measurement | True   
Permeability                                     | NaN cm/min             |                                                                                                                                          | FIT         | False  
Specific intestinal permeability (transcellular) | 1.85E-07 cm/min        | Unknown                                                                                                                                  | Fit         | True   
Is small molecule                                | Yes                    |                                                                                                                                          |             |        
Molecular weight                                 | 627.73 g/mol           |                                                                                                                                          |             |        
Plasma protein binding partner                   | Albumin                |                                                                                                                                          |             |        

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
Permeability                               | NaN cm/min     |                                                                                                                                          | FIT         | False  
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

Name                                       | Value                   | Value Origin                                                                                                                      | Alternative | Default
------------------------------------------ | ----------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------
Solubility at reference pH                 | 17 mg/l                 |                                                                                                                                   | Measurement | True   
Reference pH                               | 7                       |                                                                                                                                   | Measurement | True   
Lipophilicity                              | 1.1436481967 Log Units  | Parameter Identification-Parameter Identification-Value updated from '#7 - iv (logP, logP, UGT, GFR)_best iv' on 2025-08-30 15:56 | Measurement | True   
Fraction unbound (plasma, reference value) | 0.65                    |                                                                                                                                   | Measurement | True   
Permeability                               | 4.6547688496E-06 dm/min | Parameter Identification-Parameter Identification-Value updated from '#1 update' on 2025-08-14 16:39                              | FIT         | False  
Is small molecule                          | Yes                     |                                                                                                                                   |             |        
Molecular weight                           | 471.51 g/mol            |                                                                                                                                   |             |        
Plasma protein binding partner             | Albumin                 |                                                                                                                                   |             |        

#### Calculation methods

Name                    | Value              
----------------------- | -------------------
Partition coefficients  | Rodgers and Rowland
Cellular permeabilities | PK-Sim Standard    

#### Processes

##### Systemic Process: Glomerular Filtration-Dabi

Species: Human

###### Parameters

Name         | Value | Value Origin
------------ | -----:| ------------:
GFR fraction |     1 |             

##### Metabolizing Enzyme: UGT2B15-FIT

Molecule: UGT2B15

Metabolite: DabiGluc

###### Parameters

Name                               | Value                      | Value Origin                                                                                                                     
---------------------------------- | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------
In vitro Vmax for liver microsomes | 0 pmol/min/mg mic. protein |                                                                                                                                  
Km                                 | 512 µmol/l                 |                                                                                                                                  
kcat                               | 4.2993761606 1/min         | Parameter Identification-Parameter Identification-Value updated from '#7 - iv (logP, logP, UGT, GFR)_best iv' on 2025-08-30 15:56

## 3.2 Diagnostic Plots<a id="plots"></a>

<a id="table-3-1"></a>

**Table 3-1: GMFE for Goodness of fit plot for concentration in plasma**

|Group                               |GMFE |
|:-----------------------------------|:----|
|Intravenous infusion                |1.16 |
|Oral capsule                        |1.35 |
|Oral capsule - Verification dataset |1.83 |
|Oral solution                       |1.92 |
|All                                 |1.50 |

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

**Figure 3-10: Härtter 2012 - Dabigatran DDI Rifampicin - lin**

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

# 5 References<a id="references"></a>

