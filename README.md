# Insurando
It is coded with pure javascript to be able to facilitate the connetion with the APIs. There is no addiction. Create instance for "InsurandoAPI", before request sent.
``` js
// API Object Example   
var api = new InsurandoAPI('<baseUrl>/api/', '<username>', '<password>');
```
We can send requests via described object above.
## Postal Code
### All Postal codes
``` js
// Retrieve all postal codes  
api.PostCode(function (response) {
    if (response.readyState != 4) return;

    if (response.status == 200) {
        var data = JSON.parse(response.responseText);
        console.log(data);
    }
});
```
Response
``` js
[1000,1003,1004,1005,...]
```
### Searching postal codes
Search for postal codes which are start with given parameter. Can be used with Autocomplate,Typeahead etc. plugins.

E.g. Search for postal codes which are start with "100"
``` js
// Postal codes which are start with "100"    
var postCodeStartWithSearchTerm = 100;
api.PostCode(postCodeStartWithSearchTerm, function (response) {
    if (response.readyState != 4) return;

    if (response.status == 200) {
        var data = JSON.parse(response.responseText);
        console.log(data);
    }
});
```
Response
``` js
[1000,1003,1004,1005,1006,1007,1008,1009]
```
## Region
Gets regions which are related with postal code.
You have to send a valid postal code value.
``` js 
// Gets all postal codes    
api.PostCode(function (response) {
    if (response.readyState != 4) return;

    if (response.status == 200) {
        var data = JSON.parse(response.responseText);
        console.log(data);
    }
});
```
Response
``` js
[
    {
        "regionId": 3,
        "label": "Lausanne - Lausanne",
        "grade": 1,
        "region": "Lausanne",
        "zone": "Lausanne",
        "canton": "VD",
        "postCode": 1000
    },
    {
        "regionId": 2,
        "label": "Lausanne - Lausanne 25",
        "grade": 1,
        "region": "Lausanne 25",
        "zone": "Lausanne",
        "canton": "VD",
        "postCode": 1000
    },
    {
        "regionId": 1,
        "label": "Lausanne - Lausanne 26",
        "grade": 1,
        "region": "Lausanne 26",
        "zone": "Lausanne",
        "canton": "VD",
        "postCode": 1000
    },
    {
        "regionId": 0,
        "label": "Lausanne - Lausanne 27",
        "grade": 1,
        "region": "Lausanne 27",
        "zone": "Lausanne",
        "canton": "VD",
        "postCode": 1000
    }
]
```
## Insurance Company
It is used for reaching the insurance companies which are registerd in Insurando system.
``` js
//Gets all health insurance companies   
api.Company.Health(function (response) {
    if (response.readyState != 4) return;

    if (response.status == 200) {
        var data = JSON.parse(response.responseText);
        console.log(data);
    }
});
```
Response
``` js 

[
    {
        "label": "Agrisano",
        "value": "1560"
    },
    {
        "label": "AMB",
        "value": "1507"
    },
    {
        "label": "Aquilana",
        "value": "32"
    },
        ...
]
```
## Lead
It registers the Lead object to Insurando system and gets the registered lead's id.
Lead nesnesini Insurando sisteminee kaydeder ve geriye kaydedilen lead'in Id'sini döner
``` js
// lead object
var leadObject = {
    "FirstName": "TestFirstName",
    "LastName": "TestLastName",
    "Gender": "F",
    "Email": "test@gmail.com",
    "StreetName": "Am Zopfbach",
    "BuildingNumber": "15",
    "PhoneNo": "071 555 55 55",
    "Region": 1,
    "CurrentHealthInsuranceProviderId": 3073,
    "BirthDate": "2019-01-01",
    "Franchise": "600",
    "Message": "Lorem Ipsum ist ein einfacher Demo-Text für die Print- und Schriftindustrie.",
    "WhatIsImportantForYou": ["Günstige Prämien", "Volle Abdeckung", "Zahnzusatzversicherung"],
    "PersonInHouseHold": 3,
    "Language": "DE"
};

// Add lead
api.Lead(leadObject, function (response) {
    if (response.readyState != 4) return;

    if (response.status == 201) {
    var data = JSON.parse(response.responseText);
    console.log(data);
    }
});
```

<table class="table table-bordered">
    <thead>
        <tr>
            <th>Name</th>
            <th>Requirement</th>
            <th>Desciription</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>FirstName</th>
            <td>Not mandadory</td>
            <td>
                <p>Maximum 50 characters</p>
            </td>
        </tr>
        <tr>
            <th>LastName</th>
            <td>Mandatory</td>
            <td>
                <p>Maximum 50 characters</p>
            </td>
        </tr>
        <tr>
            <th>Gender</th>
            <td>Not mandatory</td>
            <td>
                <p>Can get value as "M" or "F" , "M" Male, "F" Female</p>
            </td>
        </tr>
        <tr>
            <th>Email</th>
            <td>Mandatory</td>
            <td>
                <p>Maximum 75 characters</p>
            </td>
        </tr>
        <tr>
            <th>BirthDate</th>
            <td>Not mandatory</td>
            <td>
                <p>Date must be formatted with ISO standarts as yyyy-MM-dd</p>
            </td>
        </tr>
        <tr>
            <th>StreetName</th>
            <td>Mandatory</td>
            <td>
                <p>Maximum 4000 characters</p>
            </td>
        </tr>
        <tr>
            <th>BuildingNumber</th>
            <td>Mandatory</td>
            <td>
                <p>Maximum 25 characters</p>
            </td>
        </tr>
        <tr>
            <th>Region</th>
            <td>Mandatory</td>
            <td>
                <p>get "regionId" which is retrieved from Region API </p>
            </td>
        </tr>
        <tr>
            <th>PhoneNo</th>
            <td>Mandatory</td>
            <td>
                <p>Maximum 50 characters</p>
                <p>have to start with city/operator code</p>
                <p>have to be \"0XX XXX XX XX\" format</p>
                <p>validation regex: "(0)(/21|22|24|26|27|31|32|33|41|43|52|56|61|62|71|81|91)sd{3}sd{2}sd{2}"</p>
            </td>
        </tr>
        <tr>
            <th>CurrentHealthInsuranceProviderId</th>
            <td>Not mandatory</td>
            <td>
                <p>can get a value which is taken from Company API</p>
            </td>
        </tr>
        <tr>
            <th>Language</th>
            <td>Mandatory</td>
            <td>
                <p>Can be "DE","FR","IT"</p>
                <p>"DE" German</p>
                <p>"FR" French</p>
                <p>"IT" Italian</p>
            </td>
        </tr>
        <tr>
            <th>PersonInHouseHold</th>
            <td>Mandatory</td>
            <td>
                <p>can get value between 1 to 10,must be at least 1</p>
            </td>
        </tr>
        <tr>
            <th>Franchise</th>
            <td>Not mandatory</td>
            <td>
                <p>flexible according to date of birth</p>
                <p>Age between 0-18 can get [0, 200, 300, 400, 500, 600] values</p>
                <p>if age is above 18 can get [300, 500, 1000, 1500, 2000, 2500] values</p>
                <p>All the values are acceptible if date of birth is not sent</p>
            </td>
        </tr>
        <tr>
            <th>TariffType</th>
            <td>Not mandatory</td>
            <td>
                <p>"TAR-BASE", Can take \"TAR-BASE\", \"TAR-DIV\", \"TAR-HAM\", \"TAR-HMO\" values.</p>
                <p>"TAR-BASE" : Standard</p>
                <p>"TAR-DIV" : Telmed</p>
                <p>"TAR-HAM" : Hausarzt</p>
                <p>"TAR-HMO" : HMO</p>
            </td>
        </tr>
        <tr>
            <th>Message</th>
            <td>Not mandatory</td>
            <td>
                <p>Message written by customer</p>
            </td>
        </tr>
        <tr>
            <th>WhatIsImportantForYou</th>
            <td>Not mandatory</td>
            <td>
                <p>Given answer by the customer for "What is important for you?" question</p>
                <p>gets string serie value</p>
            </td>
        </tr>
    </tbody>
</table>
