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
 * [2 Methodsduction](#methods)
   * [2.1 Strategyduction](#strategy)
   * [2.2 Dataduction](#data)
   * [2.3 Assumptionsduction](#assumptions)
 * [3 Resultsduction](#results)
   * [3.1 Parametersduction](#parameters)
   * [3.2 Plotsduction](#plots)
   * [3.3 Profilesduction](#profiles)
     * [3.3.1 Trainingduction](#training)
     * [3.3.2 Testduction](#test)
 * [4 Conclusionduction](#conclusion)
 * [5 Referencesduction](#references)

# 1 Introduction<a id="intro"></a>

COMPOUND is an active, highly selective ... (Information about Pharmacology)

COMPOUND is ...  (Information about relevant Pharmacokinetics)

The herein presented model building and evaluation report evaluates the performance of the PBPK model for COMPOUND in (healthy) adults.

The presented COMPOUND PBPK model as well as the respective evaluation plan and evaluation report are provided open-source ([https://github.com/Open-Systems-Pharmacology/COMPOUND-Model](https://github.com/Open-Systems-Pharmacology/COMPOUND-Model)).

Alfentanil is a potent analgesic synthetic opioid. It is fast but short-acting and used for anesthesia during surgery. Alfentanil is metabolized solely by CYP3A4 (Phimmasone 2001). Like midazolam, alfentanil is not a substrate for P-gp (Wandel 2002) and less than 1% of an alfentanil dose is excreted unchanged in urine (Meuldermans 1988).

Although in clinical use alfentanil is always administered intravenously (iv), some DDI studies published plasma concentration-time profiles of alfentanil following oral ingestion. The presented alfentanil model was established using clinical PK data of 8 publications, covering iv and oral (po) administration and a dosing range from 0.015 to 0.075 mg/kg as well as absolute doses of 1 mg iv and 4 mg po. The established model is based on the model developed by Hanke et al. (Hanke 2018) and applies metabolism by CYP3A4 and glomerular filtration.

# 2 Methodsduction<a id="methods"></a>

## 2.1 Strategyduction<a id="strategy"></a>

## 2.2 Dataduction<a id="data"></a>

## 2.3 Assumptionsduction<a id="assumptions"></a>

# 3 Resultsduction<a id="results"></a>

## 3.1 Parametersduction<a id="parameters"></a>

## 3.2 Plotsduction<a id="plots"></a>

<a id="table-3-1"></a>

**Table 3-1: GMFE for Goodness of fit plot for concentration in plasma**

|Group                      |GMFE |
|:--------------------------|:----|
|Intravenous administration |1.16 |

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

## 3.3 Profilesduction<a id="profiles"></a>

### 3.3.1 Trainingduction<a id="training"></a>

<a id="figure-3-3"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/comparison_time_profile_iv___0_1_mg_1.png)

**Figure 3-3: iv - 0.1 mg**

<br>
<br>

<a id="figure-3-4"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/comparison_time_profile_iv___5_0_mg_2.png)

**Figure 3-4: iv - 5.0 mg**

<br>
<br>

<a id="figure-3-5"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/1_time_profile_plot_Dabigatran_1160_0005_0_1mg_iv_update_PI.png)

**Figure 3-5: Analysis**

<br>
<br>

<a id="figure-3-6"></a>

![](images/006_section_Results/009_section_Profiles/010_section_Training/2_time_profile_plot_Dabigatran_1160_0005_5_0mg_iv_update_PI.png)

**Figure 3-6: Analysis**

<br>
<br>

### 3.3.2 Testduction<a id="test"></a>

# 4 Conclusionduction<a id="conclusion"></a>

# 5 Referencesduction<a id="references"></a>

