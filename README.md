# Target_RA_Model
Economic model in Simul8 which accompanies the publication 'Targeted anti-CCP testing to identify people at risk of rheumatoid arthritis in primary care: an early economic evaluation'
________________________________________
# 1. Overview
This repository contains documentation for an economic evaluation model used to assess alternative testing scenarios for identifying patients at risk of rheumatoid arthritis (RA) in primary care, from a UK context. The conceptual model structure, assumptions, parameter values, and analytical methods are fully described in the accompanying journal publication.

This README provides instructions for configuring, running, and reproducing model results, including the base-case probabilistic sensitivity analyses and additional sensitivity analyses. 
________________________________________
# 2. License and Use
This model is distributed under the MIT License.

The model is provided for academic and research purposes. If you use this model in a project or publication, please cite:
A. F Smith, B. Shinkins, E. M. A Hensor, M. Wilson, A. Anderson, R. Stack, P Emery, K Mankia, H. J. Siddle. "Targeted anti-CCP testing to identify people at risk of rheumatoid arthritis in primary care: an early economic evaluation." *Rheumatology Advances in Practice*. [Under Review].

The analyses reported in the publication were generated using the model version archived in this repository.
________________________________________
# 3. Model Version and Provenance
•	Model name: Target_RA_Model

•	Repository version: v1.0

•	GitHub commit hash: a79cd56

Users are encouraged to reference the specific repository version or release tag when reproducing or citing results.
________________________________________
# 4. Software and System Requirements
•	Software: Simul8 software

The model provided in this repository (Target_RA_Model) was created with Simul8 simulation software. To open, run, or modify these files, you require a separately obtained, valid Simul8 licence. Simul8 is a proprietary software and is not included in this repository. 
________________________________________
# 5. Model Scenarios
The model includes the following comparator and intervention scenarios:

**1.	No Test (base-case comparator)**
   
**2.	Anti-CCP testing, for randomly selected proportion of patients:**

o	10%

o	20%

o	30%

o	40%

o	50%

o	75%

**3.	Anti-CCP testing for all individuals (100%)**
   
**4.	COBRA (“COuld it Be RA”) prediction model, with anti-CCP testing for individuals who are COBRA-positive**

The published base-case analysis corresponds to the No Test scenario. All other strategies are evaluated in comparison to this comparator.
________________________________________
# 6. Selecting the Base-Case Scenario
Model scenarios are selected by modifying global data values in the Information Store (go to: Build → Data Store → Numbers).

For each model scenario, the global data that requires changing are outlined below. 


**6.1 No Test (Base-Case Comparator)**

•	Set Intervention_Arm to: aCCP_Test_some

•	Set SET_aCCP_strategies_prop_tested content value to: 0


**6.2 Anti-CCP Testing Scenarios (10%–100%)**

•	Set Intervention_Arm to: aCCP_Test_some

•	Set SET_aCCP_strategies_prop_tested content value to the required testing proportion e.g. 10% → 0.1, 20% → 0.2, 100% → 1.0.


**6.3 COBRA Prediction Model Scenario**

•	Set Intervention_Arm to: COBRA

•	Set SET_COBRA_threshold to: 11

In this scenario, individuals identified as positive by the COBRA model undergo anti-CCP testing.
________________________________________
# 7. Selecting sensitivity analyses/ scenarios
The below model sensitivity analyses (7.1, 7.2, 7.3 and 7.4) require changes to global data values, as outlined below. After running a sensitivity analysis/ scenario, ensure the relevant global data values are re-set to the base-case values in each case. 

**7.1 COBRA Prediction Model alternative threshold**

•	Set Intervention_Arm to: COBRA

•	Set SET_COBRA_threshold to: 8 (base-case value = 11)

7.2 Weibull parameterisation for delay variables  

•	Set SET_TTE_Parameterisation to: 1 (base-case value = 2)

**7.3 Alternative (cheaper) costs for primary care tests**

•	Set cost_CRP to: 4.37 (base-case value = 8.74)

•	Set cost_RF to: 2.18 (base-case value = 8.74)

•	Set cost_aCCP to: 5.55 (base-case value = 8.74)

**7.4 50% of primary care appointments conducted by first contact physician (FCP) Physiotherapist**

•	Set SET_p_GP_vs_Physio to: 0.5 (base-case value = 1)

The below model sensitivity/ scenario analyses (7.5, 7.6) require changes to the model visual logic code. The required changes are outlined below. After running a sensitivity analysis/ scenario, ensure the relevant section of visual logic code is re-set to the base-case code in each case. 

**7.5 Halving rate of persistent symptoms** 

•	Go to On Reset logic: Visual logic tab → Time → On Reset

•	Change On Reset logic to include ‘/2’ for required data from the PSA_Inputs spreadsheet: 

o	SET Var_sympt_persist_aCCP_pos  =  PSA_Inputs[7,SET_SOUR] / 2

o	SET Var_sympt_persist_aCCP_neg  =  PSA_Inputs[8,SET_SOUR] / 2

•	Once you have completed the sensitivity analysis, remember to return the code to its original state (remove the ‘/2’)

**7.6 Doubling rate of persistent symptoms**

•	Go to On Reset logic: Visual logic tab → Time → On Reset

•	Change On Reset logic to include ‘*2’ for required data from the PSA_Inputs spreadsheet: 

o	SET Var_sympt_persist_aCCP_pos  =  PSA_Inputs[7,SET_SOUR] * 2

o	SET Var_sympt_persist_aCCP_neg  =  PSA_Inputs[8,SET_SOUR] * 2

•	Once you have completed the sensitivity analysis, remember to return the code to its original state (remove the ‘*2’)

________________________________________
# 8. Probabilistic Sensitivity Analysis (PSA)
**8.1 PSA Setup**

To enable probabilistic sensitivity analysis, update the following Global Data items:

•	Set SET_Run_PSA to: 1

•	Set SET_PSA_Number to: 5000

•	Set SET_SOUR content number to: 2 (Leave the “On reset” field blank)

**8.2 PSA Execution**

1.	Navigate to the Home tab.

2.	Click the Reset button to initiate the PSA. The model will run the specified number of Monte Carlo iterations.

**8.3 Randomness and Reproducibility**

This model using random sampling as part of the probabilistic sensitivity analysis (PSA). To ensure reproducibility, the random number seed for each PSA run is set to the PSA run number (i.e. SET_SOUR). This is done in the visual logic code, On Reset visual logic. 

The same set of seeds is used consistently across all scenario runs. This means that differences between scenarios reflect changes in model inputs or structure, rather than differences in random sampling. Using fixed and documented seeds ensures that all PSA results can be reproduced. 

The number of PSA iterations used in the published analysis was 5,000.
________________________________________
# 9. Model Outputs
Model outputs are stored automatically in the following worksheets: PSA_Outputs

•	Go to:  Build  →  Spreadsheets  →  PSA_Outputs 

Definitions of outcomes, valuation methods, and discounting assumptions are provided in the accompanying publication.
________________________________________
# 10. Reproducing Published Results
To reproduce the main results reported in the publication:

1.	Open the model file.

2.	Select the No Test base-case scenario (follow the steps outlined in Section 6).

3.	Enable PSA and set the number of iterations to 5,000 (follow the steps outlined in Section 8).

4.	Click Reset to run the model.

5.	Extract results from the PSA_Results worksheet.

6.	Repeat steps 2–5 for alternative scenarios (see Section 7) to generate incremental comparisons.
________________________________________
# 12. Contact
For questions regarding the model or its use, please contact:

•	Alison F. Smith, Associate Professor at the University of Leeds, Leeds, UK. Email: a.f.c.smith@leeds.ac.uk 
________________________________________
# Final Note
This README is intended to support transparency and reproducibility. It should be read in conjunction with the accompanying publication, which provides full methodological and conceptual details.
