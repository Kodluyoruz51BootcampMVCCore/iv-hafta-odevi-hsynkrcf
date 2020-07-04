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
