# Laravel İpuçları
> Sürekli güncel :arrows_counterclockwise:

## Başlıklar
- [Teorik Bilgiler](https://github.com/mahammad/laravel-ipuclari#teorik)
- [Model](https://github.com/mahammad/laravel-ipuclari#model)
- Request
- [Blade](https://github.com/mahammad/laravel-ipuclari#blade)
- [Controller](https://github.com/mahammad/laravel-ipuclari#controller)
    - Increments and Decrements (Artışlar ve Azalmalar)   
- Helper

## Model
> Model yapısıyla alakalı ipuçları

#### `$fillable` 
Model aracılığıyla kayıt oluşturmada kolon belirleme. İstekten (örnek: `$request->all()`) gelen tüm veriyi kayıt için gönderdiğimizde belirlemiş olduğumuz kolonlara karşılık gelen veriler kayıt edilecek.

```php
protected $fillable = [
	'id',
	'name',
	'surname',
	'password'
];
```

#### `$hidden`
Model aracılığıyla çekmiş olduğunuz veride kolon gizleme (örnek: `password`).

```php
protected $hidden = [
	'password'
];
```

#### `$dateFormat`
Model aracılığıyla Tarih/Saat Biçimini Değiştirmek

```php
protected $dateFormat = 'U';
```

#### `$timestamps` Varsayılan Kayıt tarihi(`created_at`) ve(veya) Güncelleme(`updated_at`) kolonlarının yönetimi.
- Kolonların kullanılmadığı durumunda
    ```php
    public $timestamps = false;
    ```
- Kolonlara varsayılan isim belirlenmesi
    ```php
    const CREATED_AT = 'created';
    const UPDATED_AT = 'updated';
    ```
    
#### `$casts` kolonlorın formatlanması
> daha fazlası için [laravel döküman](https://laravel.com/docs/8.x/eloquent-mutators#attribute-casting)

* `array` olarak tanımlanan kolonun array olarak döndüşünü sağlar
* `string` kolonun string olarak formatlama
* `float` ondalıklı sayı olarak formatlama
* `int` tam sayı olarak formatlama 
* `datetime` tarih formatlama
    ```php
    protected $casts = [
        'id' => 'string',
        'amount' => 'float',
        'quantity' => 'integer',
        'content' => 'array',
        'created_at' => 'datetime:d-m-Y H:si',
        'updated_at' => 'datetime:d-m-Y',
    ];
    ```

## Blade
>Blade için ipuçları

### Tanımsız değişken kullanımı
> örnek için bir blade faklı konumlarda kullanılıyorsa ve bazı veriler her yerde göndermiyor ola bilirsiniz önerilen iki ipuçu

```php
// 1. yöntem
{{ $data ?? null }}

// 2. yöntem
{{ @$data }}
```

## Controller
> Genel itibariyler controller tarafında veya genel kullanımlar

#### Increments and Decrements (Artışlar ve Azalmalar) 
> örnek: stok artış veya azalması
```php

$product = Product::find(1);  // id'si 1 olan ürün verisi

// stok artışı genel kullanım
$product->stock++;
$product->save();

// stok artışı için önerilen ipuçu
$product->increment('stock');
// 10 lu artım, 1. parametre kolon ismi 2. parametre ise artış değeri
$product->increment('stock',10); 

// stok azalması için genel kullanım
$product->stock--;
$product->save();

// stok azalması için önerilen ipuçu
$product->decrement('stock');
```

## Teorik :warning:

* Route dosyaları middleware'dan önce çalışır
* config klasöründe bulunan dosyalar en önce yüklenir. (Örneğin: Dil fonksiyonu app.php 'de çalışmaz )