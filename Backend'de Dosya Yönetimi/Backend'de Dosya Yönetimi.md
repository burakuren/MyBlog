# Backend'de Dosya Yönetimi

Merhabalar, şimdiye kadar okuduğum başlangıç seviyesi tüm yazılar dosya yönetimi hakkında ya mevcut kütüphane'nin ilgili dosya-ilişkili field'ını kullanıyor ya da basitçe projeninde içerisinde bulunduğu dosyaların arasına kayıt yapmayı öğretiyor.

Bu blog post'umun amacı sizlere benim de production ortamında kullandığım bir dosya yönetim biçimini göstermek.

Projemizde aslında yüklenen dosyalar için ihtiyaçlarımız şu şekilde:

1. Dosyayı kimin yüklediğini, ne zaman yüklendiğini, dosyanının şuanda nerede olduğunu vb. bilmemizi sağlayacak bir tablo yapısı yaratmak.
2. Dosyaların sağlıklı bir biçimde upload olabilmesini sağlamak.
3. Dosyalarının silinebilmesini sağlamak.
4. Dosyamızın silinmesi durumunda hem db'den ilişkili kaydının hem de dosyanın asıl bulunduğu yerden silinmesini sağlayacak trigger yapısı kurmak.
5. Dosyalar üzerinde yapılacak askiyonları tek bir yerden yönetebilmemizi sağlamak için geliştireceğimiz methodları barındıran bir class yazmak.

Normalde prod ortamında dosyalarımızı nereye kayıt ettiğimiz değişebilir. Bu yazıda ben, mevcut uygulamanın çalıştığı yerde bir klasör içerisine kayıt edeceğim lakin kuracağımız tablo yapısı ve FileRecordsManager sayesinde bu dosyaları dilerseniz Amazon S3'e dilerseniz [on-prem](https://en.wikipedia.org/wiki/On-premises_software) sunucunuzun diskine kayıt edin. Her halükarda bunu kolaylıkla yapabilir hatta süreç içerisinde bu tercihinizi değiştirseniz dahi en azından bu konu hakkında oldukça kontrollü ve az sayıda değişiklik yapabilir durumda olucaksınız.


