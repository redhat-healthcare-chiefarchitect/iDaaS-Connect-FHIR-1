# Open-iDaaS-Connect-FHIR
iDAAS has several key components that provide many capabilities. iDAAS Connect is intended ONLY
to enable iDAAS connectivity. iDAAS-Connect-FHIR specifically ONLY deals with enabling 
iDAAS to process the healthcare industry standard FHIR based resources ONLY. Here is the 
<a href="https://www.hl7.org/fhir/resourcelist.html" target="_blank">current FHIR Resource List</a> 
It will process over 60+ of the currently available resources - around 40 clinical FHIR 
resources, all the financial public health and research/evidence based medicine/and quality
reporting and testing resources. You can also find a list of the 
<a href="http://connectedhealth-idaas.io/home/SupportedTransactions" target="_blank">platforms supported transactions</a> 

This solution contains three supporting directories. The intent of these artifacts to enable
resources to work locally: <br/>
1. platform-addons: needed software to run locally. This currently contains Kafka 2.6)<br/>
2. platform-scripts: support running kafka, building and running the solution as well. All the scripts are named to describe their capabilities <br/>
3. platform-testdata: sample transactions to leverage for using the platform. 

For this particular repository it has been tested and works with multiple FHIR servers. <br/>
<a href="https://github.com/hapifhir/hapi-fhir-jpaserver-starter" target="_blank">HAPI FHIR JPA Server</a><br/> 
<a href="https://github.com/IBM/FHIR" target="_blank">IBM FHIR Server</a><br/>
<a href="https://github.com/microsoft/fhir-server" target="_blank">Microsoft Azure FHIR Server</a><br/>

Which ever FHIR server you implement you will need to follow the specific install instructions from each vendor. 
While we have tested with all three of them there could be a need to reconfigure the connectivity details to it. 

## Scenario: Integration 
This repository follows a very common general facility based implementation. The implementation
is of a facility, we have named MCTN for an application we have named MMS. This implementation 
specifically defines one FHIR endpoint per FHIR resource.

### Integration Data Flow Steps
 
1. This respository acts as an HTTP/HTTP(s) secure endpoint for processing FHIR Data. Each FHIR Resource has a 
specifically defined URL endpoint. It posts the transactions and gets a response back.
2. iDAAS Connect FHIR will do the following actions:<br/>
    a. Receive the FHIR message. Internally, it will audit the data it received to 
    a specifically defined topic.<br/>
    b. The FHIR message will then be processed to a specifically defined topic for this implementation. There is a 
    specific topic pattern -  for the facility and application each data type has a specific topic define for it.
    For example: MCTN_MMS_AdverseEvent, MCTN_MMS_Consent, etc. <br/>
    c. If the code is enabled then the FHIR resource data can be sent to an external FHIR server. If and external 
    FHIR server is configured the respomse from it will then be sent back to the FHIR client.<br/>
    d. The response is also sent to the auditing topic location.<br/>
    
## Builds
This section will cover both local and automated builds.

### Local Builds
Within the code base you can find the local build commands in the /platform-scripts directory
1.  Run the build-solution.sh script
It will run the maven commands to build and then package up the solution. The package will use the usual settings
in the pom.xml file. It pulls the version and concatenates the version to the output jar it builds.

### Automated Builds
Automated Builds are going to be done in Azure Pipelines

## Ongoing Enhancements
We maintain all enhancements within the Git Hub portal under the 
<a href="https://github.com/Open-iDaaS/Open-iDaaS-Connect-FHIR/projects" target="_blank">projects tab</a>

## Defects/Bugs
All defects or bugs should be submitted through the Git Hub Portal under the 
<a href="https://github.com/Open-iDaaS/Open-iDaaS-Connect-FHIR/issues" target="_blank">issues tab</a>

## Chat and Collaboration
You can always leverage <a href="https://redhathealthcare.zulipchat.com" target="_blank">Red Hat Healthcare's ZuilpChat area</a>
and find all the specific areas for iDAAS-Connect-FHIR. We look forward to any feedback!!

If you would like to contribute feel free to, contributions are always welcome!!!! 

Happy using and coding....

