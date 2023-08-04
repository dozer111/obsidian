`@mixin` - тег, який вказує на те що клас Б володіє всіма публічними методами і властивостями класа А(при цьому не наслідуючи його)

загалом, це використовується в усіляких ORM, і т.п де робочий код підставляється походу

стаття: https://freek.dev/1482-the-mixin-php-docblock

```php
class ClassA  
{  
    public function methodOfClassA(): string  
    {  
        return 'This is classA';  
    }  
}  
  
/** @mixin ClassA */  
class ClassB  
{  
    public function methodOfClassB(): string  
    {  
        return 'This is classB';  
    }  
  
    public function __call($name, $arguments)  
    {  
        (new ClassA())->$name(...$arguments);  
    }  
}
```

![[Pasted image 20230804152420.png]]