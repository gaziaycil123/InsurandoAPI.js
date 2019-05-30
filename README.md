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

{% raw %}
deneme
{% endraw %}
