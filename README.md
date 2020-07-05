# iv-hafta-odevi
*  Geri dönen bilgiye göre yeşil renkte onay mesajı gösterilmesi. (örneğin:view bag)

*  AddMVC - AddMVCCore - AddDateAnnotations nedir? Nerelerde eklenmelidir?

 * Shanpshot nedir? nasıl değişir? neden alınır?

*  Jquery Calender--> [Datapicker](https://jqueryui.com/datepicker/) --> DueAt'i takvim tipinde eklemek nasıl yapılır? Araştırınız. (DateTimeUffset tipinden atamalar oluşucak)

*  First- FirstOrDefault ve Single- SingleOrDefault nedir? Aralarındaki farkı araştırınız.

*  En kısa null check nasıl yapılır?

* partial view nedir?

* Farklı authentication bulup,aynı işleri farklı yollar ile yapanları araştırınız.

* Ödev- Razor Pages/MVC Projects karşılaştırmasını yapınız.



## Bilgiye Göre Onay Mesajı

Bunu eğer bir JavaScript metodu ile yaparsak Ajax,Fetch vs. geri dönmek inanılmaz basittir. Success kısmına bir **Alert** kullanılarak veyahut [Notiflix](https://www.notiflix.com/) gibi bir çok eklenti ile kolayca yapabilirsiniz. Ama işlem kontroller kısmında yapılır ise bu bilgiyi view kısmına aktarmanın bazı yolları vardır. En basit hali ile **ViewBag** ile çözülebilir örneğin;
```cs
ViewBag.SuccessMessage = "<p>Success!</p>"; // Controller 
if(ViewBag.SuccessMessage != null)          // View 
{
     <div>@ViewBag.SuccessMessage</div>
}
```
**TempData** ile hemen hemen aynı şekilde istenildiği gibi kullanılabilir.
```cs
TempData["Message"] = "Operation successful!";   // Controller
@TempData["Message"]                             // View
```

## AddMVC - AddMVCCore - AddDataAnnotations

Bir ASP.NET Core projesi oluştururken, hizmetlerinizi ve pipeline yapılandırmak için genellikle bir Startup.cs dosyası görürsünüz. Bu Yöntemler
ConfigureServices(IServiceCollection services) ve Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory) içindir.

**ConfigureServices** hizmetlerinizi yapılandırdıkça kullanılmaya hazırlıyor. Aynı zamanda bağımlılıklarınızı eklemek için bir yerdir.

### AddMVC
services.AddMvc() yönteminin kaynak kodunu inceleyip görebileceğiniz gibi, MVC için gereken tüm temel hizmetleri kendi yapılandırabilir. Örnek; JsonFormatter, DataAnnotations gibi bağımlılıklar dahil. Özetle tüm dependencyleri ekler.

### AddMVCCore
services.AddMvcCore() yöntemi bağımlılık enjeksiyon kapsayıcısına yalnızca gerekli MVC hizmetlerini ekler. Yani MVC'nin **Minimum Dependecy** ile çalışması için gerekli olanları ekler. Eğer bunu ekleyip bir json dönmek isterseniz, hata verir çünkü herşeyi kendi yapmaz bunu biraz daha manuel düşünmelisiniz. :)

### AddDataAnnotations
MVC'nin tasarımdan biri **Kendini Tekrarlama**. ASP.NET Core MVC, işlevselliği veya davranışı yalnızca bir kez belirtmenizi ve bir uygulamada her yerde yansıtıldığını önerir. Bu, yazmanız gereken kod miktarını azaltır ve daha az hata yazmanızı, daha kolay test yapmayı ve bakımını daha kolay hale getirir. Bir modelinizin propertylerine kural koymak istiyorsunuz, hemen annotationslar imdadınıza yetişiyor. Örnek; Modelimin iki propertysine annotations ekliyorum :smile:
```cs
    [Display(Name = "Release Date")]
    [DataType(DataType.Date)]
    public DateTime ReleaseDate { get; set; }

    [Range(1, 100)]
    [DataType(DataType.Currency)]
    [Column(TypeName = "decimal(18, 2)")]
    public decimal Price { get; set; }
```

## Snapshot Nedir?
<DbContext>Snapshot.cs. Bu dosya, geçerli bir şemanın snapshotunu içerir. Modelinizi veritabanı şemasına çeviren tek bir sınıf gibidir.
      [Snapshot Nedir? Nasıl Değişir? Neden Alınır?](https://softdevpractice.com/blog/entity-framework-core-snapshot/) çok temiz anlatılmış, güzel makale.

## Jquery Calender
Soruyu anlayamadım yada internette yanlış aratıyorum hiç birşey bulamadım. :shipit:

## First - FirstOrDefault vs Single - SingleOrDefault ?

#### SingleOrDefault ve Single
- **SingleOrDefault**: Dizi içerisinden sadece bir tane çift sayı seçilmek isteniyor ve seçim şartımız sağlanmıyorsa, bu durumda int tipinin varsayılan değeri olan 0(sıfır) döndürülmesi sağlanacak ise SingleOrDefault seçimininin kullanılması gerekir.
- **Single**: Eğer seçimimiz sonucunda sadece bir tane eleman geleceği garanti ise bu durumda Single kullanılabilir. Eğer şart sonucunda; hiçbir eleman dönmez ise veya şartı sağlayan birden falza eleman dönerse; bu durumda hata ile karşılaşılacaktır.

#### FirstOrDefault ve First
- **FirstOrDefault**: Bu seçimde de mantık SingleOrDefault ile aynıdır. Ancak seçimde ilk eleman seçilir. Yani eğer dizide 2den büyük bir sayı seçilecekse; bu elemanda 2 den büyük “ilk” eleman seçilir.
- **First**: Mantık Single ile aynıdır. Ancak ilk elaman seçilir

##  En Kısa Null Check
```cs
   if(myObject){}
   if(myObject != null){}
```

## Partial View Nedir?
Bir işlemi birden fazla kez yapacaksak bir kalıp kullanırız. Öğreğin oluşturacağımız bir resim galerisini web sitesinde birden fazla sayfada kullanacağımızı düşünelim. Aynı galeriyi her sayfa için tekrar tekrar oluşturmak gereksiz ve zaman kaybıdır. Tam da burada Partial View  imdadımıza yetişiyor. Partial View kendi başına hiçbir işlevi olmayan bir yapıdır.
```cs
   <!-- Aşağıda bulunan kod örneği layout içinde yazmamız gereken koddur --> 
   @Html.Action("PartialViewSample", "Home")
```

## Authentications
- Login ile ilgili ASP.Net Core'un bize sağladığı sistem ile ilgili --> [Güzel Bir Örnek](http://cagatayyildiz.com/net-core-mvc-login-islemi/)
- Jwt Authentication sistemi günümüzde çok kullanılıyor. Token Bazlı buyrun bir makale --> [JWT Auth](https://medium.com/bili%C5%9Fim-hareketi/asp-net-core-ile-jwt-authentication-web-api-uyg-66a7d3fecb6f)
- Evet ASP.Net Core'un token bazlı oAuth middleware sistemi --> [oAuth](https://developer.okta.com/blog/2019/07/12/secure-your-aspnet-core-app-with-oauth)

# Razor Pages vs MVC Projects?

## Nedir bu Razor Pages?

ASP.NET Core 2.0 ile beraber hayatımıza giren Razor Pages, ASP.NET Core MVC alt yapısında, sayfa bazlı web uygulamaları geliştirebileceğimiz bir programlama modeli. 
Tamamen MVC alt yapısı üzerine geliştirilmiş bir kabuk olarak düşünebilirsiniz. MVC template’lerindeki klasör sayısını azaltmak, sayfa bazlı uygulamaları daha kolay geliştirmek için tasarlanmış yeni bir model.
> Altını çizerek belirtmek isterim ki, MVC’ye alternatif ya da onun yerini alacak bir model değildir.

## ASP.NET MVC ?
Geliştirilen web uygulamalarındaki bölümlerin artmasıyla beraber yazılan kodlarda artmaktadır.
Yazılan kodların artması, geliştirilen uygulama için uygun bir mimarinin seçilmemesi kodların karmaşıklaşmasına, kod bakım süresinin uzamasına neden olur.
Microsoft bu sorunu çözmek için web uygulamalarında sıklıkla kullanılan MVC mimarisini ASP.NET içerisine entegre etmiştir.<p>MVC yani <strong>M</strong>odel-<strong>V</strong>iew-<strong>C</strong>ontroller en basit şekilde geliştirilen uygulamaların parçalara ayrılmasıdır.</p>
<p>Parçalara ayrılmasındaki neden SOC <strong>S</strong>eparation <strong>O</strong>f <strong>C</strong>oncerns yani sorumlulukların ayrılması prensibidir.</p>Her bir parçanın kendine göre görevleri vardır.
<ul><li><strong>Model</strong> – Uygulamada kullanılacak verilerin bulunduğu, veritabanı ile ilgili bağlantının yapıldığı katmandır.</li><li><strong>View</strong> – Model içerisindeki verilerin görselleştirilmesinden sorumlu katmandır.</li><li><strong>Controller</strong> – Model ile View arasındaki bağlantıyı sağlayan katmandır. View’dan gelen ekleme, silme, güncelleme vb. isteklere cevap verir.</li></ul>

## Karşılaştıralım

ASP.Net Core Razor Page, ASP.NET MVC'nin görünüm sayfalarına çok benzer. Sözdizimi ve işlevsellikte MVC ile benzerlik gösterir. En büyük fark, bir MVC uygulama modelinde ve denetleyici kodunun Görünüm sayfalarına eklenmesi veya bağlanmasıdır.

Razor sayfaları, sayfa uzantısı dışında yapı bağlamında ASP.Net web formlarına benzer.
ASP.Net web formlarında, UI için .aspx ve arkasında kod için .aspx.cs dosyası vardı, ASP.Net Razor sayfalarında UI için .cshtml ve arkasında kod için .cshtml.cs var.

> Yani, Razor sayfalarının MVC'ye göre daha organize olduğunu söyleyebiliriz. MVC'de çok sayıda yönlendirme, Controller içindeki Model, Denetleyici ve Eylemlere dahil olur. Ancak Razor sayfalarında durum böyle değil.

Razor sayfalarının MVC gibi bir yapısı yoktur. Tüm Razor sayfaları çok temel bir yapıya sahip Pages klasörü altında bulunur. Aşağıdaki ekran görüntüsünü görebilirsiniz. Ayrıca, proje yapınızı işlevselliğinize göre düzenleyebilirsiniz.
Aşağıdaki ekran görüntüsü, .Net Core Razor sayfalarının proje yapısı ile MVC arasındaki farkları açıklayacaktır.
Razor sayfalarını MVC yapısına karşı aşağıdaki görüntüden anlayın.

![mvcrazor](https://1.bp.blogspot.com/-8G1LL9mwx4Q/XaC1-cAhY-I/AAAAAAAACYo/Ac9TmL4T-7EcLZfcwx9BW3rKVnIH2SniwCNcBGAsYHQ/s400/del.png)

# ÖZET

Razor sayfaları geleneksel ASP.Net WebForms'un bir sonraki evrimidir. MVC, çok sayıda dinamik sunucu sayfası, REST API'leri ve AJAX çağrısı olan web uygulamaları için iyidir.
> Hangisinin daha iyi olduğuna karar vermek için birçok tartışma olabilir.

**RAZOR**: Temel web sayfaları ve basit kullanıcı giriş formları için statik sayfalarla veya birkaç dinamik sayfa içeren bir web sitesi oluşturmak istiyorsanız, Razor'ın iyi bir seçim olduğunu düşünüyorum.<br />
**MVC**: Ancak REST tabanlı bir API projesi veya çok sayıda dinamik sayfa oluşturuyorsanız, MVC ile yola devam etmelisiniz. :smile:

**ASP.Net Core'da Razor sayfaları ve MVC öğrenmenin tadını çıkarın.**

<p align="center"><strong>Hüseyin Karacif tarafından :heart: ile hazırlandı.</strong></p>
