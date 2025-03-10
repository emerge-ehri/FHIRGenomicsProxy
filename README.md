# FHIR Genomics Proxy
Deployed a secure FHIR Genomics Proxy instance and configured an authorization access role for Baylor College of Medicine (BCM) users to send FHIR bundles from BCM into the Johns Hopkins cloud-based ancillary genomics system.

## Overview
At Johns Hopkins University (JHU), we implemented the [Azure API for FHIR](https://azure.microsoft.com/en-us/services/azure-api-for-fhir/) (MS FHIR API), a secure and scaleable cloud-based FHIR service for FHIR version R4 and DTSU3.  We then modified and deployed a secure FHIR Proxy service ([FHIRProxy](https://github.com/microsoft/health-architectures/tree/master/FHIR/FHIRProxy)).

In summary, the FHIRProxy ties in Azure Active Directory and Key Vault, allowing for direct authentication/authorization tie-ins to institutions with Microsoft login implementations.  In addition, it allows for the creation of service accounts, making automated data upload and analysis seamless and secure.
 
For the FHIR Genomics Proxy, we created a service account for the Baylor College of Medicine (BCM) FHIRClient.  With proper authentication parameters and role assignments, BCM Data can obtain an authorization token, to access the FHIR Server.  With the token, BCM Data sends lab reports (i.e., FHIR transaction bundles) to the FHIR Genomics Proxy.  The FHIR Genomics Proxy processes the bundles and stores them in the MS FHIR API.

## Modifications to FHIRProxy and FHIRClient
The batch bundles require additional processing in order to maintain associations between the bundled resources.  This required changes to be made to both the FHIRProxy and FHIRClient to include association information into the submissions to the MS FHIR API. Once we made these changes, we were able to retrieve associated resources from the MS FHIR API using standard FHIR query parameters.
 
## Acknowledgements
This work as part of the eMERGE Network was initiated and funded in part by the NIH NHGRI through the Johns Hopkins subcontract under the following grant U01HG8679 (Geisinger). Johns Hopkins is also part of Microsoft’s Partner Network, which provides enhanced services to the university. The content is solely the responsibility of the authors and does not necessarily represent the official views of the NIH or Microsoft.
