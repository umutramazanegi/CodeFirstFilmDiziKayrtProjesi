# CodeFirstFilmDiziKayrtProjesi 🎬

Bu proje, .NET Framework üzerinde C# ve Windows Forms kullanılarak geliştirilmiş, Entity Framework **Code First** yaklaşımıyla basit bir Film/Dizi ve Kategori kayıt yönetim uygulamasıdır.

## 🚀 Genel Bakış

Uygulama, kod içerisinde tanımlanan varlık (Entity) sınıflarından (`Category.cs`, `Movie.cs`) yola çıkarak veritabanını ve tablolarını oluşturur (Code First). Kullanıcıların kategorileri ve bu kategorilere ait film/dizi bilgilerini yönetmesine olanak tanır. Temel CRUD (Create, Read, Update, Delete) işlemleri her iki varlık için ayrı formlarda sunulmuştur.

## ✨ Özellikler

*   **Entity Framework Code First:** Veritabanı şeması, kodda tanımlanan `Category` ve `Movie` sınıfları ile `MovieContext` üzerinden oluşturulur.
*   **EF Migrations:** Veritabanı şemasındaki değişiklikleri yönetmek için Entity Framework Migrations kullanılmıştır (`Migrations` klasörü).
*   **Kategori Yönetimi (`Form1`):**
    *   Yeni kategori ekleme (`Create`).
    *   Mevcut kategorileri listeleme (`Read`).
    *   Kategori bilgilerini güncelleme (`Update`).
    *   Kategori silme (`Delete`).
    *   Kategori adına göre arama yapma (`Search`).
*   **Film/Dizi Yönetimi (`FrmMovie`):**
    *   Yeni film/dizi ekleme (`Create`) - Kategori seçimi `ComboBox` ile yapılır.
    *   Mevcut filmleri/dizileri listeleme (`Read`).
    *   Film/Dizi bilgilerini güncelleme (`Update`).
    *   Film/Dizi silme (`Delete`).
    *   Film/Dizi adına göre arama yapma (`Search`).
    *   Kategorileri `ComboBox` içerisine yükleme (`FrmMovie_Load`).
    *   Filmleri/Dizileri kategori adlarıyla birlikte listeleme (LINQ `Join` kullanarak - `btnMovieWithCategory_Click`).

## 🛠️ Kullanılan Teknolojiler

*   **Programlama Dili:** C#
*   **Framework:** .NET Framework 4.7.2
*   **Arayüz:** Windows Forms (WinForms)
*   **Veri Erişimi:** Entity Framework 6 (Code First)
*   **Veritabanı:** Microsoft SQL Server

## 💾 Kurulum ve Çalıştırma

Bu proje Entity Framework Code First yaklaşımını kullandığı için veritabanı, uygulama ilk çalıştığında veya Migration komutu ile otomatik olarak oluşturulabilir.

1.  **Gereksinimler:**
    *   Visual Studio 2019 veya üzeri (.NET Framework 4.7.2 desteği ile)
    *   Microsoft SQL Server (Express, Developer veya başka bir sürüm) - Uygulamanın bağlanabileceği bir instance çalışıyor olmalı.

2.  **Projeyi Klonlama:**
    ```bash
    git clone https://github.com/kullanici-adiniz/CodeFirstFilmDiziKayrtProjesi.git
    ```
    *(kullanici-adiniz kısmını kendi GitHub kullanıcı adınızla değiştirin)*

3.  **Bağlantı Dizesini Ayarlama:**
    *   `CodeFirstFilmDiziKayrtProjesi` projesindeki `App.config` dosyasını açın.
    *   `connectionStrings` bölümündeki `MovieContext` adlı bağlantı dizesini bulun.
    *   `data source=UMUT\SQLEXPRESS` kısmını kendi SQL Server sunucu adınızla değiştirin (örn: `.` , `(localdb)\mssqllocaldb`, `YOUR_PC_NAME\SQLEXPRESS` vb.).
    *   `initial catalog=FilmDiziKayrtDb` kısmındaki veritabanı adını isterseniz değiştirebilirsiniz. Bu veritabanı SQL Server'da mevcut olmasa bile EF Code First tarafından oluşturulacaktır.
    *   Eğer SQL Server'ınız Windows Authentication (integrated security=true) kullanmıyorsa, bağlantı dizesini SQL Server Authentication'a göre düzenlemeniz gerekir (User ID=...;Password=...;).

    ```xml
     <connectionStrings>
       <add name="MovieContext" connectionString="data source=YOUR_SERVER_NAME;initial catalog=FilmDiziKayrtDb;integrated security=true;" providerName="System.Data.SqlClient" />
     </connectionStrings>
    ```

4.  **Veritabanını Oluşturma (EF Migrations):**
    *   Visual Studio'da `CodeFirstFilmDiziKayrtProjesi.sln` dosyasını açın.
    *   NuGet Paket Yöneticisi Konsolu'nu açın (`Tools -> NuGet Package Manager -> Package Manager Console`).
    *   Açılan konsolda `Default project` olarak `CodeFirstFilmDiziKayrtProjesi` projesinin seçili olduğundan emin olun.
    *   Aşağıdaki komutu çalıştırarak veritabanını oluşturun ve mevcut migration'ları uygulayın:
        ```powershell
        Update-Database
        ```
    *   Bu komut, `App.config`'deki bağlantı dizesini kullanarak SQL Server'a bağlanacak, `FilmDiziKayrtDb` veritabanını (eğer yoksa) oluşturacak ve `Migrations` klasöründeki tanımlara göre tabloları (`Categories`, `Movies`) yaratacaktır.

5.  **Uygulamayı Çalıştırma:**
    *   Projeyi derleyin (Build -> Build Solution).
    *   Uygulamayı başlatın (Debug -> Start Debugging veya F5). Ana form olarak `FrmMovie` açılacaktır.

## 📝 Code First Yaklaşımı Hakkında

Bu projede veritabanı önceden oluşturulmaz. Bunun yerine:

1.  **Entity Sınıfları:** `DAL/Entities` klasöründe `Category.cs` ve `Movie.cs` sınıfları veritabanı tablolarını temsil eder.
2.  **DbContext:** `DAL/Context/MovieContext.cs` sınıfı, veritabanı bağlantısını ve tablolarla (`DbSet`) etkileşimi yönetir.
3.  **Migrations:** `Migrations` klasörü, kodda yapılan model değişikliklerinin veritabanına nasıl yansıtılacağını takip eder. `Update-Database` komutu bu değişiklikleri uygular.

Bu README, Entity Framework Code First kullanarak basit bir WinForms uygulamasının nasıl yapılandırıldığını ve çalıştırıldığını anlamanıza yardımcı olacaktır.
