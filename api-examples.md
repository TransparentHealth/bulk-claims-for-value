API Examples
============


These APIs are created for illustration and discussion purposes.  The data they serve is the synthetic data presented in README.

For easy of evaluation, some APIs do not require authentication. A production implemenation would require authentication. 
APIs requiring authentication will indicate so.

There are two flavors of APIs here.


1. Static Content APIs  - information is sitting on a SFTP and/or S3 content-delivery network.  There is no database.
2. Dynamic Content APs   - Data may be queried.  A database is used in the background to process queries and respond to API requests.


Static Content APIs
-------------------

Get all patient, claim, and coverage data from S3.


    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/Patient.ndjson
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/ExplanationOfBenefit.ndjson
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/Claim.ndjson
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/CPCDS_Patients.csv
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/CPCDS_Claims.csv
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/CPCDS_Coverages.csv


Get all patient, claim, and coverage data from SFTP (same data bucket as S3).

Please note that any SFTP client can be used.  This server does not support passwords.  It instead relies on RSA keys.
Place the RSA key into a text file called `sftp-priv.key` before trying out the following sftp commands. 
Please ask me for the sample private key.


    sftp -i ./sftp-priv.key unc-health-care@s-992885016a6f47159.server.transfer.us-east-1.amazonaws.com


Followed By the SFTP commands for downloading...


    get Wellcare/latest/Patient.ndjson
    get Wellcare/latest/ExplanationOfBenefit.ndjson
    get Wellcare/latest/Claim.ndjson
    get Wellcare/latest/CPCDS_Patients.csv
    get Wellcare/latest/CPCDS_Claims.csv
    get Wellcare/latest/CPCDS_Coverages.csv
    
 
 
Dynamic Content APIs
-------------------

A FHIR server would qualify as one of these APIs but we havn't established one for this project yet.
While these APIs do return FHIR (json), Bulk FHIR(ndjson), and CSV, the URLs so not map to 
the FHIR specification.  For lack of a better term we can call these "FHIR light".

Get all patients in Durham County as a CSV


    curl https://bulk-claims-api.transparenthealth.org/djm/read/api/public/duke-margolis-bulk-claims/CPCDS_Patients-csv/Patients.csv?County=Durham%20County

 
Get all patients in Durham County as a JSON


    curl https://bulk-claims-api.transparenthealth.org/djm/read/api/public/duke-margolis-bulk-claims/CPCDS_Patients-csv/Patients.csv?County=Durham%20County


 
Get all patients in Durham County as a NDJSON (Not FHIR)


    curl https://bulk-claims-api.transparenthealth.org/djm/read/api/public/duke-margolis-bulk-claims/CPCDS_Patients-csv/Patients.csv?County=Durham%20County


Get all claims in NDJSON FHIR format for patient with the Patient FHIR id of `a39e3c49-a036-485c-aad8-5f1589b23a86`.


    curl https://bulk-claims-api.transparenthealth.org/djm/read/api/custom/public/patient-claim?---patient-fhir-id---=a39e3c49-a036-485c-aad8-5f1589b23a86


OAuth2 Examples
```````````````

Supply the Oauth2 Bearer token `sample-token-abababdfdf123dfcbc` in the header.


Get all Claims of a particular condition of Childhood Asthma (SNOMED CODE 233678006) as FHIR JSON


    curl -H "Authorization: Bearer sample-token-abababdfdf123dfcbc" "https://bulk-claims-api.transparenthealth.org/djm/read/api/oauth2/duke-margolis-bulk-claims/Condition-fhir/Condition.json?code.coding.code=233678006"


Get same as Bulk FHIR (NDJSON)


    curl -H "Authorization: Bearer sample-token-abababdfdf123dfcbc" "https://bulk-claims-api.transparenthealth.org/djm/read/api/oauth2/duke-margolis-bulk-claims/Condition-fhir/Condition.ndjson?code.coding.code=233678006"


Get all claims of a particilar condition of hypertension as as a CPCDS CSV


    curl -H "Authorization: Bearer sample-token-abababdfdf123dfcbc" "https://bulk-claims-api.transparenthealth.org/djm/read/api/public/duke-margolis-bulk-claims/CPCDS_Claims-csv/claims.csv?Diagnosis_code=59621000"
 