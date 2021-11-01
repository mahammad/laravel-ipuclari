# Laravel İpuçları

## Başlıklar
- Model
- Request
- Blade
- Controller
- Helper

### Model
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
* `array` olarak tanımlanan kolonun array olarak döndüşünü sağlar
* `string` kolonun string olarak formatlama
* `float` ondalıklı sayı olarak formatlama
* `int` tam sayı olarak formatlama 
* `datetime` tarih formatlama
```php
protected $casts = [
    'id' => 'string',
    'amount' => 'float',
    'quantity' => 'int',
    'content' => 'array',
    'created_at' => 'datetime:d-m-Y H:si',
    'updated_at' => 'datetime:d-m-Y',
];
```