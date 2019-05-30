# Insurando

Apilere bağlantıyı kolaylaştırmak için pure javascript ile yazılmıştır. Herhangi bir bağımlılığı yoktur.
Request'ler gönderilmeden önce "InsurandoAPI" nesnesinin örneği alınmalıdır.
``` js
// API nesne örneği   
var api = new InsurandoAPI('<baseUrl>/api/', '<kullanıcı adı>', '<şifre>');
```
Yukarıda tanımlanan nesne üzerinden request'lerimizi gönderebiliriz.
## Posta Kodu
### Tüm Posta Kodları
``` js
// Tüm posta kodlarını getir  
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
### Posta Kodu Arama
Gönderilen parametre ile başlayan posta kodlarını arar. Autocomplate,Typeahead vb. plugin'lerde kullanılabilir.

Örneğin 100 ile başlayan posta kodlarını arayalım
``` js
// "100" ile başlayan posta kodlarını   
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
## Bölge
Posta koduna ait bölgeleri getirir
Geçerli bir posta kodu değeri göndermeniz gerekmektedir.
``` js 
// Tüm posta kodlarını getir   
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
## Sigorta Şirketi
Insurando sisteminde kayıtlı olan sigorta şirketlerine erişmek için kullanılır
``` js
// Tüm sağlık branşındaki sigorta şirketlerini getirir   
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
Lead nesnesini Insurando sisteminee kaydeder ve geriye kaydedilen lead'in Id'sini döner
``` js
// lead nesnesi
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

// lead ekle
api.Lead(leadObject, function (response) {
    if (response.readyState != 4) return;

    if (response.status == 200) {
    var data = JSON.parse(response.responseText);
    console.log(data);
    }
});
```

<table class="table table-bordered"><thead><tr><th>İsim</th> <th>Gereklilik</th> <th>Açıklama</th></tr></thead> <tbody><tr><th>FirstName</th> <td>Zorunlu Değil</td> <td><p>Maksimum 50 karakter</p></td></tr><tr><th>LastName</th> <td>Zorunlu</td> <td><p>Maksimum 50 karakter</p></td></tr><tr><th>Gender</th> <td>Zorunlu Değil</td> <td><p>"M" veya "F" değeri alabilir, "M" Erkek, "F" Kadın</p></td></tr><tr><th>Email</th> <td>Zorunlu</td> <td><p>Maximum 75 karakter</p></td></tr><tr><th>BirthDate</th> <td>Zorunlu Değil</td> <td><p>ISO standardında tarih formatı gönderilmeli yyyy-MM-dd</p></td></tr><tr><th>StreetName</th> <td>Zorunlu</td> <td><p>Maximum 4000 karakter</p></td></tr><tr><th>BuildingNumber</th> <td>Zorunlu</td> <td><p>Maximum 25 karakter</p></td></tr><tr><th>Region</th> <td>Zorunlu</td> <td><p>Region apisinden dönen "regionId" değeri alabilir</p></td></tr><tr><th>PhoneNo</th> <td>Zorunlu</td> <td><p>Maximum 50 karakter</p><p>Geçerli şehir/operatör kodu ile başlamak zorunda</p><p>"0XX XXX XX XX" formatında olmak zorunda</p><p>valaidasyon regex: "(0)(/21|22|24|26|27|31|32|33|41|43|52|56|61|62|71|81|91)sd{3}sd{2}sd{2}"</p></td></tr><tr><th>CurrentHealthInsuranceProviderId</th> <td>Zorunlu Değil</td> <td><p>Company apisinden dönen değerlerden birini alabilir</p></td></tr><tr><th>Language</th> <td>Zorunlu</td> <td><p>"DE","FR","IT" değerlerinden birini alabilir</p><p>"DE" Almance</p><p>"FR" Fransızca</p><p>"IT" İtalyanca</p></td></tr><tr><th>PersonInHouseHold</th> <td>Zorunlu</td> <td><p>1 ile 10 arasında bir değer alır, En az 1 gönderilmelidir</p></td></tr><tr><th>Franchise</th> <td>Zorunlu Değil</td> <td><p>Doğum tarihine göre değişkenlik gösterir</p><p>Yaş 0-18 aralığında [0, 200, 300, 400, 500, 600] değerlerini alır</p><p>Yaş &gt; 18 ise [300, 500, 1000, 1500, 2000, 2500] değerlerini alır</p><p>Doğum tarihi gönderilmez ise tüm değerler kabul edilir</p></td></tr><tr><th>TariffType</th> <td>Zorunlu Değil</td> <td><p>"TAR-BASE", "TAR-DIV", "TAR-HAM", "TAR-HMO" değerlerini alabilir.</p><p>"TAR-BASE" : Standart</p><p>"TAR-DIV" : Telmed</p><p>"TAR-HAM" : Hausarzt</p><p>"TAR-HMO" : HMO</p></td></tr><tr><th>Message</th> <td>Zorunlu Değil</td> <td><p>Müşteriden alınacak mesaj</p></td></tr><tr><th>WhatIsImportantForYou</th> <td>Zorunlu Değil</td> <td><p>Müşteriden alınacak olan "sizin için önemli olan ne" sorusunun cevabı</p><p>String dizi değeri alır</p></td></tr></tbody></table>
