Bulk Claims for Value Based Care
--------------------------------

This is a public repository describing the "Bulk Claims for Value Based Care" initiative in North Carolina.  Its is overseen by the "Duke-Margolis Center for Health Policy". This public repository contains general information about the project such as links to relevant standards and sample data.  All project participants may contribute to this repository or its wiki. See CONTRIBUTING.MD for more details. 


Objectives
----------

* To create a standard way for health providers to download claims information from payers (insurance providers). Payer to provider data flow is the initial focus.
* To adopt or profile existing standards and profiles to facilitate risk stratification.

Ongoing Work
------------

* Identify exactly what fields are needed for risk stratification models.

Dignosis\conditions and comorbidities are the most common\important data elements used in most risk stratification models. Age, gender(sex), maritial status, and other demographic data are also used in some models. 

* Answer this question. Are fields needed for risk stratification already covered in the CPCDS format and corresponding FHIR profile? Use the table below to support your answer.


| Risk Statification Model                | Key Elements                | Links  |
| --------------------------------------- | ---------------------------:| ------:|
| Hierarchical Condition Categories (HCCs)| Diagnosis/Conditions | https://www.cms.gov/Medicare/Health-Plans/MedicareAdvtgSpecRateStats/Risk-Adjustors.html |
| Adjusted Clinical Groups (ACG)          | Diagnosis/Conditions  | https://www.hopkinsacg.org/ |
| Chronic Comorbidity Count (CCC)         | Diagnosis/Conditions   | https://www.ncbi.nlm.nih.gov/pubmed/21473661 |
| Elder Risk Assessment (ERA)             | Diagnosis/conditions, age, gender, marital status, number of hospital days over the prior two years, and selected comorbid medical illness  |  https://www.ncbi.nlm.nih.gov/pubmed/21441764 |
| Minnesota Tiering (MN)                  | Diagnosis/Conditions    | https://www.health.state.mn.us/facilities/hchomes/legreport/docs/hch2016report.pdf |
| Charlson Comorbidity Measure            | Diagnosis/Conditions    | https://www.sciencedirect.com/science/article/pii/0021968187901718 | 
|Vermont Blueprint for Health|Diagnosis/Conditions| https://blueprintforhealth.vermont.gov/|

Sample Data
-----------

* 100 Patients in North Carolina. https://videntityshare.s3.amazonaws.com/nc-samples-100.zip (includes CPCDS csv and Bulk FHIR output.)

We will continue to improve the sample data to make it as complete and realistic as possible. If you encounter any issues or want the data adjusted please reach out.  Check back here for updates / additional data samples.


Links to Relevant Technical Documentation
-----------------------------------------

* FHIR Bulk Data Access (Flat FHIR) - https://build.fhir.org/ig/HL7/bulk-data-export/
* Consumer-Directed Payer Data Exchange (CARIN Blue Button) - https://build.fhir.org/ig/HL7/carin-bb/index.html
* Beneficiary Claims Data API (CMS) - https://bcda.cms.gov/
* Claim and Claim Line Feed (CCLF) - https://www.cms.gov/Medicare/Medicare-Fee-for-Service-Payment/sharedsavingsprogram/Downloads/2019-CCLF-file-data-elements-resource.pdf
* Transformed Medicaid Statistical Information System (T-MSIS) - https://www.medicaid.gov/medicaid/data-and-systems/macbis/tmsis/index.html
* T-MSIS Data Dictionary - https://www.medicaid.gov/medicaid-chip-program-information/by-topics/data-and-systems/downloads/t-msis-data-dictionary.zip
* DaVinci Data Exchange For Quality Measures Implementation Guide https://build.fhir.org/ig/HL7/davinci-deqm/



Participants
------------

The Duke-Margolis Center for Health Policy functions as convener of participants. The participants are:

* UNC Health Care
* Wellcare/Centene
* Blue Cross Blue Shield of North Carolina
* North Carolina Department of Health and Human Services
* AmeriHealth Caritas
* Optum/United Healthcare
* Duke Health
