# Laravel İpuçları

## Başlıklar

- Model
- Request
- Blade
- Controller
- Helper


### Model

* Model dosyalarınızda `fillable` `hidden` özellikleri neden var? 
    - `fillable` veritabanına Model aracılığıyla oluşturacağınız kayıt esnasında request'ten gelecek olan tüm veriyi(örn: `$request->all()`) gönderme durumunda sizi koruyan çok güzel bir önlem
    
        ```php    
            protected $fillable = [
                'id',
                'name',
                'surname',
                'password'
            ];
        ```

    - `hidden` Model aracılığıyla çekmiş olduğunuz verilerde gözükmesini veya bulunmasını istemediğiniz kolanlar (örn:`password`). Bazı veriler sorgularda sadece yük

        ```php    
            protected $hidden = [
                'password'
            ];
        ``` 