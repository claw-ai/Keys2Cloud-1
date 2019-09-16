# API Implementation and Reuse

## Overview
In this hands-on lab you will extend itineraries API implementation by reusing aircrafts API.  The current itineraries API responds with reservation, passenger, flight and status details.  We want to also include aircraft details.  

### Get Started

Start by signing into TIBCO Cloud and opening API Specs.  There are many ways to navigate to API Spec but let’s start with this.

1)	Start at Welcome to your TIBCO Cloud.
2)	Select Integration.
3)	Select Flogo.

### Import Application
We are going to use a prebuilt application for that hands-on lab and extend it by reusing flights API. 

1)	Select Create.
2)	Give your new app a name, v1_itineraries_todo and select create.
3)	Select Create a TIBCO Flogo App.
4)	Select +Import app.
5)	Navigate to where you extracted the connected customer experience artifacts and choose drag CustomerExperienceAirport/TCI/v1_itineraries_todo.json into upload files and select Upload. 
6)	Press continue when you get the warning dialog for passwords.
7)	You now ready to extend this API with aircraft details.
  
### Extend and Reuse API
Let’s extend the itineraries API to include aircrafts details.

1)	Select V1Itineraries_reservationid_GET.  GET /itineraries/{reservationid} implementation will be opened.  Here you see the orchestration that invokes reservations, passengers, flights, statuses APIs.  You are now going invoke an API call to aircrafts in the next steps.
2)	Hover your mouse over the gray line and select the + to add a new activity.
3)	From Add Activity, scroll down, select General, select Invoke REST Service. 
4)	Drag the InvokeRESTService to the right of Status.
5)	Now let’s configure the Invoke Rest Service activity.  
6)	Let’s rename this activity.  Select InvokeRESTService, hover your mouse over the name InvokeRESTService and select the edit icon.  
7)	Rename InvokeRESTService Aircraft.
8)  Select setting and past the following URL in URL.
  https://integration.cloud.tibcoapps.com:443/wz3dr4zotkxmqg5au6yhc526iw2otlc2/v1/aircrafts/{aircraftid}
9)  Now let’s map activity input.  Select Input, expand pathParams and select aircraftid.   Expand Upstream Output->Reservation->responseBody->reservation and select aircraftid.
10) Configure the Output settings.  Select Output Settings and past the following schema into Response Schema.
```
{"aircraft":
    {"aircraftid":"111",
    "type":"767",
    "seatcapacity":"280"}
}
```