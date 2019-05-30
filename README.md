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


