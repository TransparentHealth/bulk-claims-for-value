API Options and Examples
========================


These APIs are created for illustration and discussion purposes.  The data they serve is the synthetic data presented in README.  The different transport protocols in play are:

Transport Protocols
-------------------

* HTTP (on top of TCP/IP and protected by OAuth2)
* SFTP (on to of TCP/IP and protected by public/private keypairs)
* MLLP (a socket on top of TCP/IP and protected by point-to-point VPN)

We want to get consensus from the group to move to a single transport protocol, HTTP, for this project. Are our parties in agreement?

Data Formats
------------

As far as data formats go, the following formats are being used/exchanged/considrered by our group.

* HL7 FHIR (2, 3, and 4), including CPCDS Profile and `ClaimResponse` Resource. This includes Bulk FHIR which is in NDJSON format.
* HL7 v 2.5 messages including ADTs.
* CSV files of various formats (please share details as your organizations are able).
* HL7 CDA/CCDA XML

We want to get consensus on the subset of these formats that help achieve our collective objectives.


API Examples
------------


For ease of evaluation, some of these APIs do not require authentication. For the use cases described here, a production implementation **would** require authentication.  Others that do require an OAuth2 access token. I will assisit you/your organization in creating access tokens and or registering client applications.  Just shoot me (alan) an email.

The command-line tool web client `curl` is used an example, but you could instead use Postman, or any htyp client.  


The command line tool `sftp` is also used as an example, but any SFTP client should work.  `curl` and `sftp` will already be installed on most MacOS and Linux systems and many equivilents exist for Microsoft Windows.

There are two flavors of APIs here.

1. Static Content APIs - information is sitting on a SFTP and/or S3 content-delivery network.  There is no database.
2. Dynamic Content APs - Data may be queried.  A database is used in the background to process queries and respond to API requests.

Static Content APIs
-------------------

Get all patient, claim, and coverage data from S3 as static.


    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/Patient.ndjson
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/ExplanationOfBenefit.ndjson
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/Claim.ndjson
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/CPCDS_Patients.csv
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/CPCDS_Claims.csv
    curl https://s3.amazonaws.com/sftp.bulk-claims.transparenthealth.org/Wellcare/latest/CPCDS_Coverages.csv


Get all patient, claim, and coverage data from SFTP (same data bucket as S3).

Please note that any SFTP client can be used. The SFTP hostname is `s-992885016a6f47159.server.transfer.us-east-1.amazonaws.com` and the sample username is `unc-health-care`. This server does not support passwords. Instead it relies on RSA keys. Place the RSA key into a text file called `sftp-priv.key` before trying out the following sftp commands. 
Please ask me for the sample private key.


    sftp -i ./sftp-priv.key unc-health-care@s-992885016a6f47159.server.transfer.us-east-1.amazonaws.com


Followed by the SFTP commands for downloading...


    get Wellcare/latest/Patient.ndjson
    get Wellcare/latest/ExplanationOfBenefit.ndjson
    get Wellcare/latest/Claim.ndjson
    get Wellcare/latest/CPCDS_Patients.csv
    get Wellcare/latest/CPCDS_Claims.csv
    get Wellcare/latest/CPCDS_Coverages.csv
    
 
 
Dynamic Content APIs
-------------------

While these APIs do return FHIR (json), Bulk FHIR(ndjson), and CSV, the URLs do not map to 
the FHIR specification.  For lack of a better term we can call these "FHIR light".

Get all patients in Durham County as a CSV


    curl https://nc.oauth2.org/djm/read/api/public/duke-margolis-bulk-claims/CPCDS_Patients-csv/Patients.csv?County=Durham%20County

 
Get all patients in Durham County as a JSON


    curl https://nc.oauth2.org/djm/read/api/public/duke-margolis-bulk-claims/CPCDS_Patients-csv/Patients.json?County=Durham%20County


 
Get all patients in Durham County as a NDJSON (Not FHIR)


    curl https://bulk-claims-api.transparenthealth.org/djm/read/api/public/duke-margolis-bulk-claims/CPCDS_Patients-csv/Patients.ndjson?County=Durham%20County


Get all claims in NDJSON FHIR format for patient with the Patient FHIR id of `a39e3c49-a036-485c-aad8-5f1589b23a86`.


    curl https://bulk-claims-api.transparenthealth.org/djm/read/api/custom/public/patient-claim?---patient-fhir-id---=a39e3c49-a036-485c-aad8-5f1589b23a86


OAuth2 Examples
---------------

See https://nc.oauth2.org    for some additional API examples.

If you want an account so that you can register client applications and generate sample OAuth2 tokens, please do so here:
https://id.oauth2.org  Register for an agent account. If you have questions send me an email or call me.


Supply the OAuth2 Bearer token `some-b2b-token` in the header. Please replace this with an actual access token.  (I can provide a sample via email).


Get all Claims of a particular condition of Childhood Asthma (SNOMED CODE 233678006) as FHIR (JSON):

    curl -H "Authorization: Bearer some-b2b-token" "https://nc.oauth2.org/djm/read/api/oauth2/duke-margolis-bulk-claims/Condition-fhir/Condition.json?code.coding.code=233678006"


Get all Claims of a particular condition of Childhood Asthma (SNOMED CODE 233678006) as Bulk FHIR (NDJSON):


    curl -H "Authorization: Bearer some-b2b-token" "https://nc.oauth2.org/djm/read/api/oauth2/duke-margolis-bulk-claims/Condition-fhir/Condition.ndjson?code.coding.code=233678006"


Get all claims of with the particilar condition of hypertension as a CPCDS CSV:


    curl -H "Authorization: Bearer some-b2b-token" "https://nc.oauth2.org/djm/read/api/public/duke-margolis-bulk-claims/CPCDS_Claims-csv/claims.csv?Diagnosis_code=59621000"
    
