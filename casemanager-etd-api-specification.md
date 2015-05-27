# ETD - IIZUKA Case Manager API Specification


## Contents

1. [Intended Audience](#intendedAudience)
2. [Conventions](#conventions)
3. [Protocol and Format](#protocol)
4. [Authentication Mechanism](#authentication)
5. [Using The Case Manager API](#using)

<a href="#intendedAudience"></a>
### (1) Intended Audience

This document has been designed to define the interface between the IIZUKA Case Manager system and the ETD web form application in order to submit ETD applications to the case manager system. 

This interface will be agreed and maintained by both the ETD and the IIZUKA teams. 

This is a low level technical document that details the HTTP requests and responses.

The canonical home of this document is as part of the github repository that contains the documentation for the ETD project. Access to this is controlled by the ETD team and can be granted on an individual basis.


<a href="#conventions"></a>
### (2) Conventions

* [JSON](http://en.wikipedia.org/wiki/JSON) data structures will be illustrated by use of indentation:

        {
            "key" : " value"
        }

* The service will be available only on HTTPS

* No authentication details are provided on any example API calls. That will be provided as an specific section ([Authentication Mechanism](#authentication))
 
<a href="#protocol"></a>
### (3) Protocol and Format

* As communication between the ETD application and the Case Manager will be done through the Internet, **HTTPS** will be used as the communications protocol to to transfer encrypted information.

* **JSON** is the prefered data format. It is a  lightweight text-data interchange format -smaller than XML, and faster and easier to parse. It is also language independent - it uses javascript syntax for describing data objects, but indenpended of any language.   


<a href="#authentication"></a>
### (4) Authentication Mechanism

**TBD**

<a href="#using"></a>
### (5) Using the Case Manager API

IIZUKA Case Manager provides a [JSON](http://en.wikipedia.org/wiki/JSON) based API. It accepts and responds with JSON only. We required that clients correctly set the [Accepts Header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html). The correct value for this header as defined in [RFC4627](http://www.ietf.org/rfc/rfc4627.txt) is as follows:

    Accept: application/json

Also we require that submissions require the [Content Type Header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html). This must be set to 

    Content-Type: application/json; charset=utf-8

Additionally the default character encoding for the API is UTF-8. As defined in the JSON RFC above.

The IIZUKA Case Manager API has the following possible interactions

* [Posting an ETD application.](#applicationPost)
* [Posting payment details.](#paymentPost) [**TBD**]

<a href="#applicationPost"></a>
#### Posting an ETD application.

To push the ETD application details, the API call is as follows:

* URL: https://[case-manager-api-url]/application
* HTTP Method: POST
* Required Headers:
    - **TBD**

##### Example request:

	{
		"etdApp": {
	   		"appDetails" : {
	       		"title" : "Mr",
	        	"forenames" : "John",
	        	"surname" : "Smith",
	        	"other" : [
	        		{
	        	  		"forenames" : "Samuel",
	        	  		"surname" : "Jackson"
	        	  	}
	        	],
				"address" : {
		       		"numberAndStreet": "125 Kingsway",
		        	"town": "London",
		          	"postcode": "SW112DR",
		          	"country": "England"
		      	},	
		      	"birthDate": "1995-03-02",
		       	"birthCity": "London",
		       	"birthCountry": "England",
		       	"contactPhone": "07799779977",
		       	"homePhone": "07799779978",
	          	"email": "john@example.com"
	       },
	       "etdReason" : {
	       		"reason" : "stolen",
	       		"other" : ""
	       },
	       "passportDetails" : {
	       		"passwordIssuedInUK" : "y",
	       		"countryOfIssue" : "",
	       		"cityOfIssue" : "", 	
	       		"docNumber" : "",
	       		"dateOfIssue" : "",
	       		"nationality" : "",
	       		"passportApplicant" : {
		   			"title" : "Mr",
		        	"forenames" : "John",
		        	"surname" : "Smith",
		      		"birthDate": "1995-03-02",
		       		"birthCity": "London",
		       		"birthCountry": "England",
					"relationship" : ""
	       		}
			},
	    	"lostStolenDetails"	: {
	    		"place" :"",
	       		"date" : "",
	       		"country" : "",
	       		"circumstances" : "",
	       		"policeNotification" : "y",
	       		"policeDetails" : {
	       			"reportedDate" : "",
	       			"policeStation" : "",
	       			"policeReportNumber" : "",
	       			"prevReported" : "",
	       			"prevReportedDetails" : ""
	       		}
	   		},
	    	"journeyDetails" : {
	       		"departDate" : "",
	       		"arrivalDate" : "",
	       		"transitCountries" : [ "country1", "country2" ],
	       		"transportModes": [ "car", "plane"],
	       		"otherTransportMode" : "",
	       		"destCountry" : "",
	       		"travelPurpose" : "",
	       		"returnJourney" : "y",
	       		"returnJourneyDetails" : {
		       		"departDate" : "",
	       			"transitCountries" : [ "country1", "country2" ],
	       			"arrivalDate" : ""
	       		}
	    	},
	    	"furtherInformation" : {
	       		"BNOHongKongIdCard" : "",
	       		"registeredApplicant" : "",
	       		"applicationReasons" : "",
	       		"courtName" : "",
	       		"countryCourt" : "",
	       		"otherInfo" : ""
	    	},
	    	"firstTimeApp" : {
	       		"HMPOPassportApp" : "y",
	       		"HMPORefNumber" : "",
	       		"appDate" : "",
	       		"applicantInfo" : {
	       			"birthRegistered" : "",
	       			"britishConsulate" : "",
	       			"regAsBritish" : "y",
	       			"docNumber" : "",
	       			"placeOfIssue" : "",
	       			"dateOfIssue" : ""
	       		},
	       		"parentDetails" : {
	       			"fatherDetails" : {
	       				"fullName" : "",
	       				"birthCountry" : "",
	       				"birthTown" : "",
	       				"birthDate" : "",
	       				"citizenShip" : "",
	       				"immigrationStatus" : "",
	       				"passport" : {
	       					"docNumber" : "",
	       					"placeOfIssue" : "",
	       					"dateOfIssue" : ""
	       				},
	       				"citizenship" : {
	       					"docNumber" : "",
	       					"placeOfIssue" : "",
	       					"dateOfIssue" : ""
	       				}
	       			},
	       			"motherDetails" : {
	       				"fullName" : "",
	       				"birthCountry" : "",
	       				"birthTown" : "",
	       				"birthDate" : "",
	       				"citizenShip" : "",
	       				"immigrationStatus" : "",
	       				"passport" : {
	       					"docNumber" : "",
	       					"placeOfIssue" : "",
	       					"dateOfIssue" : ""
	       				},
	       				"citizenship" : {
	       					"docNumber" : "",
	       					"placeOfIssue" : "",
	       					"dateOfIssue" : ""
	       				}
	       			},
	       			"parentsMarriageDate" : "",
	       			"parentsMarriagePlace" : ""
	       		},
	       		"countersignature" : {
	       			"fullName" : "",
	       			"years" : "x",
	       			"country" : "",
	       			"numberAndStreet": "125 Kingsway",
		          	"town": "London",
		          	"postcode": "SW112DR",
		          	"email" : "",
		          	"contactphone" : "",
		          	"relationship" : "",
		          	"nationality" : "",
		          	"profession" : ""
	       		}
	     	}
		}
	}

	
##### Description of API request:

##### Applicant details block (appDetails)

|Field name|Description|Format|Mandation|Maximum length|
|-------------|-------------|-------------|-------------|-------------|
|title|Title|[Mr, Mrs, <b>TBD</b>]|required|N/A (range of values)|
|forenames|Forenames (first and middle names)|Text|required|<b>TBD</b>|
|surname|Surname|Text|required|<b>TBD</b>|
|other|Other names used by the applicant|Array[<i>OtherName</i>]|Optional|N/A (array of JSON objects)|
|<i>OtherName</i>.forenames|Forenames for "other name"|Text|required (only if "other names" has been selected)|<b>TBD</b>|
|<i>OtherName</i>.surname|Surname for "other name"|Text|required (only if "other names" has been selected)|<b>TBD</b>|
|address|Residential address|<i>Address</i>|required|N/A (depends on Address object)|
|<i>Address</i>.numberAndStreet|House name/number & street name|Text|required|<b>TBD</b>|
|<i>Address</i>.town|Town/City|Text|required|<b>TBD</b>|
|<i>Address</i>.postcode|Postcode|Postcode Regex|required|9|
|<i>Address</i>.country|Country|Text|required|<b>TBD</b>|
|birthDate|Date of birth|Date ('yyyy-mm-dd')|required|10|
|birthCity|Place of birth (city)|Text|required|<b>TBD</b>|
|birthCountry|Place of birth (country)|Text|required|<b>TBD</b>|
|contactPhone|Contact telephone number|Text|required|<b>TBD</b>|
|homePhone|Home telephone number|Text|optional|<b>TBD</b>|
|email|Contact email|Email Regex|optional|<b>TBD</b>|



##### Reason to apply for an ETD block (etdReason)

|Field name|Description|Format|Mandation|Maximum length|
|-------------|-------------|-------------|-------------|-------------|
|reason|Reason to apply|['Lost','Stolen','Expired','Defaced/Damaged','Other']|required|N/A (range of values)|
|other|Information about that other reason|Text|optional (required if 'reason' == 'Other')|<b>TBD</b>|

##### Passport details block (passportDetails)

|Field name|Description|Format|Mandation|Maximum length|
|-------------|-------------|-------------|-------------|-------------|
|passwordIssuedInUK|Was the Passport issued in the UK?|Boolean ['y','n']|required|1|
|countryOfIssue|Country of issue|Text|optional (required if 'passwordIssuedInUK' == 'n')|<b>TBD</b>|
|cityOfIssue|City of issue|Text|optional (required if 'passwordIssuedInUK' == 'n')|<b>TBD</b>|
|docNumber|Passport document number|Passport Regex|optional|Passport Regex|
|dateOfIssue|Date of issue|Date ('yyyy-mm-dd')|optional|10|
|nationality|Nationality|Text|optional|<b>TBD</b>|
|passportApplicant|Passport applicant|<i>PassportApplicant</i>|optional|N/A|
|<i>PassportApplicant</i>.title|Title|[Mr, Mrs, <b>TBD</b>]|required (if passportApplicant is needed)|N/A (range of values)|
|<i>PassportApplicant</i>.forenames|Forenames (first and middle names)|Text|required (if passportApplicant is needed)|<b>TBD</b>|
|<i>PassportApplicant</i>.surname|Surname for passport applicant|Text|required (if passportApplicant is needed)|<b>TBD</b>|
|<i>PassportApplicant</i>.birthDate|Date of birth|Date ('yyyy-mm-dd')|required (if passportApplicant is needed)|10|
|<i>PassportApplicant</i>.birthCity|Place of birth (city)|Text|required (if passportApplicant is needed)|<b>TBD</b>|
|<i>PassportApplicant</i>.birthCountry|Place of birth (country)|Text|required (if passportApplicant is needed)|<b>TBD</b>|
|<i>PassportApplicant</i>.relationship|Relationship to applicant|Text|required (if passportApplicant is needed)|<b>TBD</b>|

##### Details of where and when lost/stolen passport last seen block(lostStolenDetails)

|Field name|Description|Format|Mandation|Maximum length|
|-------------|-------------|-------------|-------------|-------------|
|place|Place of loss/theft|Text|required|<b>TBD</b>|
|date|Date of loss/theft|Date ('yyyy-mm-dd')|required|10|
|country|Country of loss/theft|Text|required|<b>TBD</b>|
|circumstances|Circumstances of loss/theft|Text|required|<b>TBD</b>|
|policeNotification|Have local police been notified?|Boolean ['y','n']|required|1|
|policeDetails|Police details|<i>PoliceDetails</i>|optional (required if 'policeNotification' == 'y')|N/A|
|<i>PoliceDetails</i>.reportedDate|Date reported to Police|Date ('yyyy-mm-dd')|optional (required if 'policeNotification' == 'y')|10|
|<i>PoliceDetails</i>.policeStation|Police station|Text|optional (required if 'policeNotification' == 'y')|<b>TBD</b>|
|<i>PoliceDetails</i>.policeReportNumber|Police report number|Text|optional (required if 'policeNotification' == 'y')|<b>TBD</b>|
|<i>PoliceDetails</i>.prevReported|Have you previously reported your/any passport lost or stolen?|Boolean ['y','n']|optional (required if 'policeNotification' == 'y')|1|
|<i>PoliceDetails</i>.prevReportedDetails|Previously reported details|Text|optional (required if 'policeNotification' == 'y' and 'prevReported' == 'y')|<b>TBD</b>|

##### Details of journey block (journeyDetails)

|Field name|Description|Format|Mandation|Maximum length|
|-------------|-------------|-------------|-------------|-------------|
|departDate|Departure date|Date ('yyyy-mm-dd')|required|10|
|arrivalDate|Arrival date|Date ('yyyy-mm-dd')|required|10|
|transitCountries|Countries transited|Array[String]|optional|Up to 5 countries|
|transportModes|Mode(s) of transport|Array['Plane','Train','Boat',<br>'Car','Coach','Other']|required|N/A|
|otherTransportMode|Other transport mode|Text|Optional (required if transportModes includes 'Other')|<b>TBD</b>|
|destCountry|Country of final destination|Text|required|<b>TBD</b>|
|travelPurpose|Purpose of travel|Text|required|<b>TBD</b>|
|returnJourney|Return journey?|Boolean ['y','n']|required|1|
|returnJourneyDetails|Return journey details|<i>ReturnJourney</i>|optional (required if 'returnJourney' == 'y')|N/A|
|<i>ReturnJourney</i>.departDate|Departure date|Date ('yyyy-mm-dd')|optional (required if 'returnJourney' == 'y')|10|
|<i>ReturnJourney</i>.transitCountries|Countries transited|Array[String]|optional (required if 'returnJourney' == 'y')|Up to 5 countries|
|<i>ReturnJourney</i>.arrivalDate|Arrival date|Date ('yyyy-mm-dd')|optional (required if 'returnJourney' == 'y')|10|

##### Further information block (furtherInformation)

|Field name|Description|Format|Mandation|Maximum length|
|-------------|-------------|-------------|-------------|-------------|
|BNOHongKongIdCard|Card number if the applicant is a British National (Overseas) with a Hong Kong permanent identity card|Text|optional|<b>TBD</b>|
|registeredApplicant|Has the applicant been Naturalised or Registered?|Boolean ['y','n']|required|1|
|applicationReasons|Reasons for making this application for an Emergency Travel Document|Text|optional|<b>TBD</b>|
|courtName|Court name (when applying by authority from the court)|Text|optional|<b>TBD</b>|
|countryCourt|Country court (when applying by authority from the court)|Text| optional|<b>TBD</b>|
|otherInfo|Other information|Text|optional|<b>TBD</b>|

##### First time applicant block (firstTimeApp)

|Field name|Description|Format|Mandation|Maximum length|
|-------------|-------------|-------------|-------------|-------------|
|HMPOPassportApp|Has the applicant lodged a full validity passport application with HM Passport Office?|Boolean ['y','n']|required (if first applicant)|1|
|HMPORefNumber|HM Passport Office reference number|Text|optional (required if 'HMPOPassportApp' == 'y')|<b>TBD</b>|
|appDate|Date application lodged|Date ('yyyy-mm-dd')|optional (required if 'HMPOPassportApp' == 'y')|10|
|applicantInfo|Applicant information|<i>ApplicantInfo</i>|optional (required if 'HMPOPassportApp' == 'n')|N/A|
|<i>ApplicantInfo</i>.birthRegistered|Was the birth registered at a British Consulate?|Boolean ['y','n']|optional (required if 'HMPOPassportApp' == 'n')|1|
|<i>ApplicantInfo</i>.britishConsulate|British Consulate|Text|optional (required if 'HMPOPassportApp' == 'n')|<b>TBD</b>|
|<i>ApplicantInfo</i>.regAsBritish|Was the applicant registered as a British citizen, British Dependent/Overseas Territories citizen,British Overseas citizen, British subject or British protected person?|Boolean ['y','n']|optional (required if 'HMPOPassportApp' == 'n')|1|
|<i>ApplicantInfo</i>.docNumber|Document number|Text|optional (required if 'HMPOPassportApp' == 'n' and 'regAsBritish' == 'y')|N/A|
|<i>ApplicantInfo</i>.placeOfIssue|Place of issue|Text|optional (required if 'HMPOPassportApp' == 'n' and 'regAsBritish' == 'y')||
|<i>ApplicantInfo</i>.dateOfIssue|Date of issue|Date ('yyyy-mm-dd')|optional (required if 'HMPOPassportApp' == 'n' and 'regAsBritish' == 'y')|10|
|parentDetails|Parent details|<i>ParentDetails</i>|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.fatherDetails|Father details|<i>FatherDetails</i>|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<i><br>FatherDetails</i>.fullName|Father's full name|Text|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.birthCountry|Father's country of birth|Text|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.birthTown|Father's town of birth|Text|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.birthDate|Father's date of birth|Date ('yyyy-mm-dd')|<b>TBD</b>|10|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.citizenship|Father's citizenship at the time of the applicant’s birth|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.immigrationStatus|Father's immigration status|Text|<b>TBD</b>|10|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.passport|Father's passport details|<i>Passport</i>|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.<i>Passport</i>.docNumber|Father's passport document number|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.<i>Passport</i>.placeOfIssue|Father's passport place of issue|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.<i>Passport</i>.dateOfIssue|Father's passport date of issue|Date ('yyyy-mm-dd')|<b>TBD</b>|10|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.citizenship|Father's citizenship|<i>Citizenship</i>|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.<i>Citizenship</i>.docNumber|Father's citizenship document number|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.<i>Citizenship</i>.placeOfIssue|Father's citizenship place of issue|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>FatherDetails</i>.<i>Citizenship</i>.dateOfIssue|Father's citizenship date of issue|Date ('yyyy-mm-dd')|<b>TBD</b>|10|
|<i>ParentDetails</i>.MotherDetails|Mother details|<i>MotherDetails</i>|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.fullName|Mother's full name|Text|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.birthCountry|Mother's country of birth|Text|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.birthTown|Mother's town of birth|Text|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.birthDate|Mother's date of birth|Date ('yyyy-mm-dd')|<b>TBD</b>|10|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.citizenship|Mother's citizenship at the time of the applicant’s birth|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.immigrationStatus|Mother's immigration status|Text|<b>TBD</b>|10|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.passport|Mother's passport details|<i>Passport</i>|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.<i>Passport</i>.docNumber|Mother's passport document number|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.<i>Passport</i>.placeOfIssue|Mother's passport place of issue|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.<i>Passport</i>.dateOfIssue|Mother's passport date of issue|Date ('yyyy-mm-dd')|<b>TBD</b>|10|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.citizenship|Mother's citizenship|<i>Citizenship</i>|<b>TBD</b>|N/A|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.<i>Citizenship</i>.docNumber|Mother's citizenship document number|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.<i>Citizenship</i>.placeOfIssue|Mother's citizenship place of issue|Text|<b>TBD</b>|<b>TBD</b>|
|<i>ParentDetails</i>.<br><i>MotherDetails</i>.<i>Citizenship</i>.dateOfIssue|Mother's citizenship date of issue|Date ('yyyy-mm-dd')|<b>TBD</b>|10|
|<i>ParentDetails</i>.parentsMarriageDate|Parents' marriage date|Date ('yyyy-mm-dd')|<b>TBD</b>|10|
|<i>ParentDetails</i>.parentsMarriagePlace|Parents' marriage place|Text|<b>TBD</b>|<b>TBD</b>|
|countersignature|Countersignature|<i>Countersignature</i>|<b>TBD</b>|N/A|
|<i>Countersignature</i>.fullName|Counter signatory's full name|Text|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.years|Number of years|Number|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.country|Counter signatory's country|Text|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.numberAndStreet|Counter signatory's House name/number & street name|Text|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.town|Counter signatory's town/city|Text|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.postcode|Counter signatory's postcode|Postcode Regex|<b>TBD</b>|<b>9</b>|
|<i>Countersignature</i>.email|Counter signatory's email|Email|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.contactphone|Counter signatory's contact telephone number|Text|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.relationship|Counter signatory's relationship to applicant|Text|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.nationality|Counter signatory's nationality|Text|<b>TBD</b>|<b>TBD</b>|
|<i>Countersignature</i>.profession|Counter signatory's profession|Text|<b>TBD</b>|<b>TBD</b>|


##### Example response:

	 * 200 for successful responses

    	{	
       		"appRefNumber": "12345"
    	}
    
    * 422 for validation errors.

        {
            "errors" : [
                {
                    "birthDate" : "Invalid format"
                }
            ]
        }

    * 500 for server errors

        {
            "error" : "Internal Server Error"
        }

    
    

##### Invalid record validation error messages / general error cases

    * Error block defined as:

            {
                "errors" : [
                    {
                        "field" : "message"
                    }
                ]
            }

    * Error messages

        * Required: when a required field is missing
        * Maximum length exceeded (xxx): Max length of field has been exceed.
          Max length included in parenthesis.
        * Invalid format: Format is incorrect

    * Example

        {
            "errors" : [
                    { "appDetails.birthDate" : "Invalid format" },
                    { "appDetails.surname" : "Required" }
            ]
        }


<a href="#paymentPost"></a>
#### Posting payment details.

**TBD**
