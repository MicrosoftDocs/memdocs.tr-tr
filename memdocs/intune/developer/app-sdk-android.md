---
title: Android için Microsoft Intune Uygulama SDK’sı geliştirici kılavuzu
description: Android için Microsoft Intune Uygulama SDK’sı, Intune mobil uygulama yönetimini (MAM) Android uygulamanıza eklemenizi sağlar.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 0100e1b5-5edd-4541-95f1-aec301fb96af
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5b29043956a86934f7b1be18606d0b78f25dc50
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608452"
---
# <a name="microsoft-intune-app-sdk-for-android-developer-guide"></a>Android için Microsoft Intune Uygulama SDK’sı geliştirici kılavuzu

> [!NOTE]
> Öncelikle, SDK’nın geçerli özelliklerini kapsayan ve desteklenen her platformda tümleştirmeye nasıl hazırlandığını açıklayan [Intune Uygulama SDK’sına genel bakış](app-sdk.md) bölümünü okumanız önerilir.
>
> SDK 'yı indirmek için bkz. [SDK dosyalarını indirme](../developer/app-sdk-get-started.md#download-the-sdk-files).

Android için Microsoft Intune Uygulama SDK’sı, Intune uygulama koruma ilkelerini (**APP** veya MAM ilkeleri olarak da bilinir) yerel Android uygulamanıza eklemenizi sağlar. Intune ile yönetilen bir uygulama, Intune Uygulama SDK’sı ile tümleşik bir uygulamadır. Intune uygulamayı etkin bir şekilde yönetirken, Intune yöneticileri uygulama koruma ilkelerini Intune ile yönetilen uygulamanıza kolayca dağıtabilir.


## <a name="whats-in-the-sdk"></a>SDK’nın kapsamı

Intune Uygulama SDK’sı aşağıdaki dosyalardan oluşur:

* **Microsoft.Intune.MAM.SDK.aar**: Destek Kitaplığı JAR dosyaları dışındaki SDK bileşenleri.
* **Microsoft.Intune.MAM.SDK.Support.v4.jar**: Android v4 destek kitaplığını kullanan uygulamalarda MAM özelliğini etkinleştirmek için gereken sınıflar.
* **Microsoft.Intune.MAM.SDK.Support.v7.jar**: Android v7 destek kitaplığını kullanan uygulamalarda MAM özelliğini etkinleştirmek için gereken sınıflar.
* **Microsoft.Intune.MAM.SDK.Support.v17.jar**: Android v17 destek kitaplığını kullanan uygulamalarda MAM özelliğini etkinleştirmek için gereken sınıflar. 
* **Microsoft.Intune.MAM.SDK.Support.Text.jar**: `android.support.text` paketindeki Android destek kitaplığı sınıflarını kullanan uygulamalarda MAM özelliğini etkinleştirmek için gereken sınıflar.
* **Microsoft. Intune. mam. SDK. Downlevelsaplamalar. AAR**: Bu AAR, yalnızca daha yeni cihazlarda bulunan ancak içindeki metotlar tarafından başvurulan Android sistem sınıfları için yer tutucular içerir `MAMActivity` . Daha yeni cihazlarda bu saplama sınıfları yoksayılır. Bu AAR, yalnızca uygulamanız ' den türetilen sınıflarda yansıma gerçekleştirdiğinde `MAMActivity` ve çoğu uygulamanın bu uygulamayı içermesi gerekmiyorsa gereklidir. AAR, tüm sınıflarını hariç tutmak için ProGuard kuralları içerir.
* **com.microsoft.intune.mam.build.jar**: [SDK'yi tümleştirmeye yardımcı olan](#build-tooling) bir Gradle eklentisi.
* **Changelog.MD**: her SDK sürümünde yapılan değişikliklerin kaydını sağlar.
* **THIRDPARTYNOTICES.TXT**:  Uygulamanıza derlenecek üçüncü taraf ve/veya OSS kodunu tanıyan bir öznitelik bildirimi.


## <a name="requirements"></a>Gereksinimler

### <a name="android-versions"></a>Android sürümleri
SDK, Android API 29 (Android 10,0) aracılığıyla Android API 21 ' i (Android 5,0) tam olarak destekler. Bu, en fazla 14 kadar Android mini SDK sürümü olan bir uygulamada yerleşik olarak bulunabilir, ancak bu eski işletim sistemi sürümlerinde Intune Şirket Portalı uygulamasını yüklemek veya MAM ilkelerini kullanmak imkansız olur.

### <a name="company-portal-app"></a>Şirket Portalı uygulaması
Android için Intune Uygulama SDK’sı, uygulama koruma ilkelerini etkinleştirmek için cihazda [Şirket Portalı](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) uygulamasının varlığına bağımlıdır. Şirket Portalı uygulama koruma ilkelerini Intune hizmetinden alır. Uygulama başlatıldığında, ilkeyi ve ilkenin zorlanmasına yönelik kodu Şirket Portalı’dan yükler.

> [!NOTE]
> Cihazda Şirket Portalı uygulaması olmadığında, Intune ile yönetilen bir uygulama Intune uygulama koruma ilkelerini desteklemeyen normal bir uygulama gibi davranır.

Cihaz kaydı olmadan uygulama koruması için kullanıcının Şirket Portalı uygulamasını kullanarak cihazını kaydetmesi gerekli _**değildir**_.

## <a name="sdk-integration"></a>SDK tümleştirmesi

### <a name="sample-app"></a>Örnek uygulama
Intune uygulama SDK 'Sı ile nasıl tümleştirileceğini bir örnek [GitHub](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App)' da bulunabilir. Bu örnek [Gradle Build eklentisini](#gradle-build-plugin)kullanır.

### <a name="referencing-intune-app-libraries"></a>Intune Uygulama kitaplıklarına başvurma

Intune Uygulama SDK'sı dış bağımlılıkları olmayan standart bir Android kitaplığıdır. **Microsoft.Intune.MAM.SDK.aar**, hem uygulama koruma ilkesi etkinleştirmesi için gereken arabirimleri hem de Microsoft Intune Şirket Portalı uygulamasıyla birlikte çalışma için gereken kodu içerir.

**Microsoft.Intune.MAM.SDK.aar** bir Android kitaplık başvurusu olarak belirtilmelidir. Bunu yapmak için, uygulama projenizi Android Studio’da açın, **Dosya > Yeni > Yeni modül**’e gidin ve **.JAR/.AAR Paketini İçeri Aktar**’ı seçin. Ardından, için bir modül oluşturmak üzere Microsoft. Intune. MAM. SDK. AAR Android arşiv paketimizi seçin *. AAR* dosya türü. Uygulama kodunuzu içeren modüle veya modüllere sağ tıklayın ve **Modül ayarları**  >  **Bağımlılıklar Sekmesi**  >  **+ simge**  >  **Modül bağımlılığı** ' na gidin > **Tamam**> SDK AAR modülünü seçin. Bu, projenizi derlediğinizde modülünüzün MAM SDK’sı ile derlendiğinden emin olmanızı sağlar.

Ayrıca **Microsoft.Intune.MAM.SDK.Support.XXX.jar** kitaplıkları, ilgili `android.support.XXX` kitaplıklarının Intune çeşitlerini içerir. Uygulamanın destek kitaplıklarına bağımlı olmasının istenmediği durumlarda olabileceği için Microsoft.Intune.MAM.SDK.aar'de yerleşik olarak bulunmaz.

#### <a name="proguard"></a>ProGuard

Bir derleme adımı olarak [ProGuard](http://proguard.sourceforge.net/) (veya başka bir daraltma/gizleme mekanizması) kullanılırsa, SDK'nın dahil edilmesi gereken ek yapılandırma kuralları vardır. Dahil olmak üzere *. Yapımızda AAR* , kurallarımız Proguard adımla otomatik olarak tümleştirilir ve gerekli sınıf dosyaları tutulur.

Azure Active Directory Authentication Library’lerin (ADAL) kendi ProGuard kısıtlamaları olabilir. Uygulamanız ADAL ile tümleştiriliyorsa, bu kısıtlamalarla ilgili olarak ADAL belgelerine bakmalısınız.

### <a name="policy-enforcement"></a>İlke zorlama
Intune Uygulama SDK'sı, uygulamanızın Intune ilkelerini yaptırmasını desteklemeyi ve buna katılımda bulunmayı sağlayan bir Android kitaplığıdır. 

Çoğu ilke yarı otomatik olarak zorlanır, ancak bazı ilkeler [uygulamanızdan zorla zorlamak için açık katılım](#enable-features-that-require-app-participation)gerektirir.
Kaynak tümleştirmesi gerçekleştirmenizi veya tümleştirme için yapı araçları 'nı kullanmayı, açık katılım gerektiren ilkelerin için kodlanmış olması gerekir.

Otomatik olarak zorlanan ilkeler için, uygulamaların MAM eşdeğerlerine devralmayla çeşitli Android temel sınıflarından devralım ve benzer şekilde belirli Android sistem hizmeti sınıflarına yapılan çağrıları MAM eşdeğerleri ile değiştirmesine izin vermek gerekir. Gerekli olan değişiklikler [aşağıda](#class-and-method-replacements) ayrıntılıdır ve kaynak tümleştirmeyle el ile gerçekleştirilebilir veya derleme araçları aracılığıyla otomatik olarak gerçekleştirilebilir.

### <a name="build-tooling"></a>Derleme araçları
SDK, derleme araçları (Gradle derlemeleri için bir eklenti ve Gradle derlemeleri için bir komut satırı aracı) ile otomatik olarak MAM eşdeğer değişiklikler gerçekleştirir. Bu araçlar, Java derlemesi tarafından üretilen sınıf dosyalarını dönüştürür ve asıl kaynak kodu değiştirmez.

Araçlar yalnızca [doğrudan değiştirme](#class-and-method-replacements) işlemleri gerçekleştirir. [Farklı Kaydetme İlkesi](#enable-features-that-require-app-participation), [Çoklu Kimlik](#multi-identity-optional), [Uygulama WE kaydı](#app-protection-policy-without-device-enrollment), [AndroidManifest değişiklikleri](#manifest-replacements) veya [ADAL yapılandırması](#configure-azure-active-directory-authentication-library-adal) gibi başka hiçbir karmaşık SDK tümleştirmesi yapmadığından, uygulamanızın tam olarak Intune özellikli hale gelmesi önce bunların tamamlanması gerekir. Uygulamanızı ilgilendiren tümleştirmeye ilişkin noktalar için lütfen belgelerin geri kalanını dikkatle inceleyin.

> [!NOTE]
> Aracın, MAM SDK'sının kısmı veya tam kaynak tümleştirmesi daha önce elle yapılan değiştirmelerle gerçekleştirilmiş bir projede çalıştırılmasında bir sorun yoktur. Ancak MAM SDK'sının yine de projenizde bir bağımlılık olarak listelenmesi gerekir.

### <a name="gradle-build-plugin"></a>Gradle Derleme Eklentisi
Uygulamanız Gradle ile derlenmiyorsa [Komut Satırı Aracı ile tümleştirme](#command-line-build-tool) bölümüne atlayın. 

Uygulama SDK'sı eklentisi **GradlePlugin/com.microsoft.intune.mam.build.jar** adıyla SDK'nın bir parçası olarak dağıtılır. Gradle'ın eklentiyi bulabilmesi için eklentinin derleme betiği sınıf yoluna eklenmesi gerekir. Eklenti, kendisi de eklenmesi gereken [Javassist](https://jboss-javassist.github.io/javassist/)'e bağımlıdır. Bunları sınıf yoluna eklemek için aşağıdakileri uygulamanızın kök dizinine ekleyin `build.gradle`

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.javassist:javassist:3.22.0-GA"
        classpath files("$PATH_TO_MAM_SDK/GradlePlugin/com.microsoft.intune.mam.build.jar")
    }
}
```

Ardından APK projenizin `build.gradle` dosyasına eklentiyi şu şekilde eklemeniz yeterlidir:

```groovy
apply plugin: 'com.microsoft.intune.mam'
```

Eklenti varsayılan olarak **yalnızca**`project` bağımlılıkları üzerinde çalışır.
Test derlemesi bundan etkilenmez. Listeye yapılandırma sağlanabilir
* Dışlanacak projeler
* [Dahil edilecek dış bağımlılıklar](#usage-of-includeexternallibraries) 
* İşlemin dışında tutulacak belirli sınıflar
* İşlemin dışında tutulacak çeşitler. Bunlar tam bir çeşit adı veya tek bir çeşitleme olabilir. Örneğin:
  * uygulamanızı {`savory`, `sweet`} ve {`vanilla`, `chocolate`} çeşitleri olan `debug` ve `release` derleme türleri varsa
  * `savory` belirterek uygun türde tüm çeşitleri, `savoryVanillaRelease` belirterek yalnızca tam çeşitleri dışlayabilirsiniz.

#### <a name="example-partial-buildgradle"></a>Örnek kısmi derleme.gradle

```groovy

apply plugin: 'com.microsoft.intune.mam'

dependencies {
    implementation project(':product:FooLib')
    implementation project(':product:foo-project')
    implementation fileTree(dir: "libs", include: ["bar.jar"])
    implementation fileTree(dir: "libs", include: ["zap.jar"])
    implementation "com.contoso.foo:zap-artifact:1.0.0"
    implementation "com.microsoft.bar:baz:1.0.0"
    implementation "com.microsoft.qux:foo:2.0"

    // Include the MAM SDK
    implementation files("$PATH_TO_MAM_SDK/Microsoft.Intune.MAM.SDK.aar")
}
intunemam {
    excludeProjects = [':product:FooLib']
    includeExternalLibraries = ['bar.jar', "com.contoso.foo:zap-artifact", "com.microsoft.*", "!com.microsoft.qux*"]
    excludeClasses = ['com.contoso.SplashActivity']
    excludeVariants=['savory']
}
```

Bu, şu sonuçları üretir:
* `:product:FooLib`, `excludeProjects` içinde bulunduğundan yeniden yazılmaz
* `:product:foo-project`, `excludeClasses` içinde olduğundan atlanan `com.contoso.SplashActivity` dışında yeniden yazılır
* `bar.jar`, `includeExternalLibraries` içine dahil edildiğinden yeniden yazılır
* `zap.jar`, bir proje olmadığı ve `includeExternalLibraries` içine dahil edilmediğinden yeniden **yazılmaz**
* `com.contoso.foo:zap-artifact:1.0.0`, `includeExternalLibraries` içine dahil edildiğinden yeniden yazılır
* `com.microsoft.bar:baz:1.0.0`, bir joker karakterle `includeExternalLibraries` içine dahil edildiğinden (`com.microsoft.*`) yeniden yazılır.
* `com.microsoft.qux:foo:2.0` , bir olumsuzlama düzeniyle açıkça dışlandığı için, önceki öğeyle aynı joker karakterle eşleşip eşleşmese de bu geri yazılır.

#### <a name="usage-of-includeexternallibraries"></a>includeExternalLibraries kullanımı

Eklenti varsayılan olarak yalnızca (genellikle `project()` işlevinin sağladığı) proje bağımlılıkları üzerinde işlem yaptığından, `fileTree(...)` tarafından belirtilen veya Maven ya da ("`com.contoso.bar:baz:1.2.0`" gibi) başka paket kaynaklarından elde edilen tüm bağımlılıkların, aşağıda açıklanan ölçütlere göre MAM ile işlenmesi gerekiyorsa `includeExternalLibraries` özelliğine sağlanması gerekir. Joker karakterler ("*") desteklenir. İle başlayan bir öğe `!` değildir ve başka bir joker karakterle dahil edilecek kitaplıkları hariç tutmak için kullanılabilir.

Yapıt gösterimi ile dış bağımlılıklar belirtilirken `includeExternalLibraries` değerindeki sürüm bileşeninin çıkarılması önerilir. Sürümü eklerseniz, tam bir sürüm olması gerekir. Dinamik sürüm belirtimleri (örneğin `1.+`) desteklenmez.

`includeExternalLibraries` içindeki kitaplıkları dahil etmeniz gerekip gerekmediğini belirlemek için kullanmanız gereken genel kural iki soruya dayanır:
1. Kitaplıkta MAM eşdeğerleri olan sınıflar var mı? Örnekler: `Activity`, `Fragment`, `ContentProvider`, `Service` vs.
2. Yanıt evet ise, uygulamanız söz konusu sınıfları kullanıyor mu?

Her iki soruyu da 'evet' ile yanıtlıyorsanız, bu kitaplığı `includeExternalLibraries` içine dahil etmeniz gerekir. 

| Senaryo | Dahil edilsin mi? |
|--|--|
| Uygulamanıza bir PDF görüntüleyici kitaplığı dahil ediyor ve görüntüleyicinin `Activity` sınıfını kullanıcılarınız PDF'leri görüntülemeye çalıştığında uygulamanızda kullanıyorsunuz | Yes |
| Gelişmiş Web performansı için bir HTTP kitaplığını uygulamanıza dahil ediyorsunuz | Hayır |
| `Activity`, `Application` ve `Fragment` sınıflarından türetilmiş sınıfları olan React Native gibi bir kitaplığı dahil ediyor ve bu sınıfları uygulamanızda kullanıyor veya bunlardan başka sınıflar türetiyorsunuz | Yes |
| `Activity`, `Application` ve `Fragment` sınıflarından türetilmiş sınıflar içeren React Native gibi bir kitaplığı dahil ediyor, ancak yalnızca statik yardımcıları veya hizmet sınıflarını kullanıyorsunuz | Hayır |
| `TextView` sınıfından türetilmiş görünüm sınıfları içeren bir kitaplığı dahil ediyor ve bu sınıfları uygulamanızda kullanıyor veya bunlardan başka sınıflar türetiyorsunuz | Yes |

#### <a name="reporting"></a>Raporlama
Yapı eklentisi, yaptığı değişikliklerin HTML raporunu oluşturabilir. Bu raporun oluşturulmasını istemek için `report = true` yapılandırma bloğunda ' i belirtin `intunemam` . Oluşturulduysa, rapor `outputs/logs` derleme dizinine yazılır.

```groovy
intunemam {
    report = true
}
```

#### <a name="verification"></a>Doğrulama
Derleme eklentisi, işleme sınıflarında olası hataları aramak için ek doğrulama çalıştırabilir. Bunu istemek için yapılandırma bloğunda ' i belirtin `verify = true` `intunemam` . Bu, eklentinin görevinin aldığı zamana birkaç saniye ekleyebileceğini unutmayın.

```groovy
intunemam {
    verify = true
}
```


#### <a name="incremental-builds"></a>Artımlı derlemeler
Artımlı oluşturma desteğini etkinleştirmek için `incremental = true` yapılandırma bloğunda ' ı belirtin `intunemam` .  Bu, yalnızca değişmiş olan giriş dosyalarını işleyerek derleme performansını artırmaya yönelik deneysel bir özelliktir.  Varsayılan yapılandırma `false` .

```groovy
intunemam {
    incremental = true
}
```


#### <a name="dependencies"></a>Bağımlılıklar

Gradle eklentisini [Javassist](https://jboss-javassist.github.io/javassist/)'e bağımlıdır ve bunun (yukarıda açıklandığı gibi) Gradle'ın bağımlılık çözümlemesinde bulunması gerekir. Javassist yalnızca derleme zamanında, eklenti çalıştırılırken kullanılır. Uygulamanıza hiçbir Javassist kodu eklenmeyecektir.

> [!NOTE] 
> Android Gradle eklentisinin 3.0 veya daha yeni bir sürümünü ve Gradle'ın 4.1 veya daha yeni bir sürümünü kullanmalısınız.

### <a name="command-line-build-tool"></a>Komut Satırı Derleme Aracı
Derlemeniz Gradle kullanıyorsa, [sonraki bölüme](#class-and-method-replacements) atlayın.

Komut satırı derleme aracı SDK yüklemesinin `BuildTool` klasöründe bulunabilir. Ayrıntıları yukarıda verilen Gradle eklentisi ile aynı işlevi görür, ancak özel ve Gradle dışı derleme sistemleriyle tümleştirilebilir. Daha genel amaçlı olduğundan çağırmak daha karmaşıktır, bu nedenle mümkün olan durumlarda Gradle eklentisi kullanılmalıdır.

#### <a name="using-the-command-line-tool"></a>Komut satırı aracını kullanma

Komut satırı aracı, dizinde bulunan belirtilen yardımcı betikler kullanılarak çağrılabilir `BuildTool\bin` .

Araç aşağıdaki parametreleri bekler.

| Parametre | Açıklama |
| -- | -- |
| `--input` | Değiştirilecek JAR dosyalarının ve sınıf dosyası dizinlerinin noktalı virgülle ayrılmış listesi. Bu liste, yeniden yazmayı düşündüğünüz tüm JAR dosyalarını/dizinleri içermelidir. |
| `--output` | Değiştirilen sınıfların depolanacağı JAR dosyalarının ve dizinlerin noktalı virgülle ayrılmış bir listesi. Her girdi için bir çıktı olmalı ve bunlar sırayla listelenmelidir. |
| `--classpath` | Derleme sınıf yolu. Bu, hem jar dosyaları dışındaki hem de sınıf dizinleri içerebilir. |
| `--excludeClasses`| Yeniden yazma dışında bırakılması gereken sınıf adlarını içeren noktalı virgülle ayrılmış bir liste. |

`--excludeClasses` dışındaki tüm parametreler isteğe bağlıdır.

> [!NOTE]
> UNIX benzeri sistemlerde noktalı virgül, bir komut ayırıcısıdır. Kabuğun komutları bölünmesini önlemek için, her noktalı virgül ' i ile kaçış \' veya tam parametreyi tırnak işaretleriyle sardığınızdan emin olun.

#### <a name="example-command-line-tool-invocation"></a>Örnek komut satırı aracı çağırma

``` batch
> BuildTool\bin\BuildTool.bat --input build\product-foo-project;libs\bar.jar --output mam-build\product-foo-project;mam-build\libs\bar.jar --classpath build\zap.jar;libs\Microsoft.Intune.MAM.SDK\classes.jar;%ANDROID_SDK_ROOT%\platforms\android-27\android.jar --excludeClasses com.contoso.SplashActivity
```

Bu, şu sonuçları üretir:

* `product-foo-project` dizini `mam-build\product-foo-project` dizinine yeniden yazılır
* `bar.jar`, `mam-build\libs\bar.jar` dosyasına yeniden yazılır
* `zap.jar`, yalnızca `--classpath` parametresinde listelendiğinden yeniden **yazılmaz**
* `com.contoso.SplashActivity` sınıfı, `--input` parametresinde olsa bile yeniden **yazılmaz**

> [!NOTE] 
> Derleme aracı şu anda AAR dosyalarını desteklememektedir. Yapı sisteminiz AAR dosyalarını işlerken `classes.jar` dosyasını daha önceden ayıklamıyorsa, bunu derleme aracını çağırmadan önce sizin yapmanız gerekir.


## <a name="class-and-method-replacements"></a>Sınıf ve yöntem değişiklikleri
> [!NOTE] 
> Uygulamalar, bu değişiklikleri otomatik olarak gerçekleştirecek SDK [derleme araçları](#build-tooling)ile *tümleşmelidir* ( [bildirim değişiklikleri](#manifest-replacements) dışında).

Android temel sınıflarının, Intune yönetimini etkinleştirmek için ilgili MAM eşdeğerleriyle değiştirilmeleri gerekir. SDK sınıfları, Android temel sınıfı ile uygulamanın söz konusu sınıftan türettiği sürüm arasında çalışır. Örneğin bir uygulama geliştirme etkinliği şuna benzer bir devralma hiyerarşisiyle sonuçlanabilir: `Activity` > `MAMActivity` >
`AppSpecificActivity`. MAM katmanı, uygulamanıza dünyanın yönetilen bir görünümünü sorunsuz bir şekilde sağlamak için, sistem işlemlerine yapılan çağrıları filtreler.

Temel sınıflara ek olarak, uygulamanızın türetmesiz kullanabileceği bazı sınıfların (örneğin `MediaPlayer`) gerekli MAM eşdeğerleri vardır ve [bazı yöntem çağrıları da değiştirilmelidir](#wrapped-system-services). Tam ayrıntılar aşağıda verilmiştir.

> [!NOTE] 
> Uygulamanız SDK [Yapı Araçları](#build-tooling)ile tümleştirildiğinde, aşağıdaki sınıf ve Yöntem değişiklikleri otomatik olarak gerçekleştirilir.

| Android temel sınıf | Intune Uygulama SDK'sı karşılığı |
|--|--|
| android.app.Activity | MAMActivity |
| android.app.ActivityGroup | MAMActivityGroup |
| android.app.AliasActivity | MAMAliasActivity |
| android.app.Application | MAMApplication |
| Android. app. Iletişim kutusu | MAMDialog Iletişim kutusu |
| Android. app. AlertDialog. Builder | Mamalcertdialogbuilder |
| android.app.DialogFragment | MAMDialogFragment |
| android.app.ExpandableListActivity | MAMExpandableListActivity |
| android.app.Fragment | MAMFragment |
| android.app.IntentService | MAMIntentService |
| android.app.LauncherActivity | MAMLauncherActivity |
| android.app.ListActivity | MAMListActivity |
| android.app.ListFragment | MAMListFragment |
| android.app.NativeActivity | MAMNativeActivity |
| android.app.PendingIntent | MAMPendingIntent (bkz. [Pending Intent](#pendingintent)) |
| android.app.Service | MAMService |
| android.app.TabActivity | MAMTabActivity |
| android.app.TaskStackBuilder | MAMTaskStackBuilder |
| android.app.backup.BackupAgent | MAMBackupAgent |
| android.app.backup.BackupAgentHelper | MAMBackupAgentHelper |
| android.app.backup.FileBackupHelper | MAMFileBackupHelper |
| android.app.backup.SharePreferencesBackupHelper | MAMSharedPreferencesBackupHelper |
| android.content.BroadcastReceiver | MAMBroadcastReceiver |
| android.content.ContentProvider | MAMContentProvider |
| android.os.Binder | MAMBinder (Yalnızca Bağlayıcı, Android Arabirimi Tanım Dili (AIDL) arabiriminden oluşturulmadığında gereklidir) |
| android.media.MediaPlayer | MAMMediaPlayer |
| android.media.MediaMetadataRetriever | MAMMediaMetadataRetriever |
| android.provider.DocumentsProvider | MAMDocumentsProvider |
| android.preference.PreferenceActivity | MAMPreferenceActivity |
| android.support.multidex.MultiDexApplication | MAMMultiDexApplication |
| android.widget.TextView | MAMTextView |
| android.widget.AutoCompleteTextView | MAMAutoCompleteTextView |
| android.widget.CheckedTextView | MAMCheckedTextView |
| android.widget.EditText | MAMEditText |
| android.inputmethodservice.ExtractEditText | MAMExtractEditText |
| android.widget.MultiAutoCompleteTextView | MAMMultiAutoCompleteTextView |


> [!NOTE]
> Uygulamanıza türetilen kendi `Application` sınıfı gerekmiyor olsa da, [aşağıdaki `MAMApplication` bölümüne bakın](#mamapplication)

### <a name="microsoftintunemamsdksupportv4jar"></a>Microsoft.Intune.MAM.SDK.Support.v4.jar:

| Android Sınıfı | Intune Uygulama SDK'sı karşılığı |
|--|--|
| android.support.v4.app.DialogFragment | MAMDialogFragment
| android.support.v4.app.FragmentActivity | MAMFragmentActivity
| android.support.v4.app.Fragment | MAMFragment
| android.support.v4.app.JobIntentService | MAMJobIntentService
| android.support.v4.app.TaskStackBuilder | MAMTaskStackBuilder
| android.support.v4.content.FileProvider | MAMFileProvider
| android.support.v4.content.WakefulBroadcastReceiver | MAMWakefulBroadcastReceiver

### <a name="microsoftintunemamsdksupportv7jar"></a>Microsoft.Intune.MAM.SDK.Support.v7.jar:

|Android Sınıfı | Intune Uygulama SDK'sı karşılığı |
|--|--|
| Android. support. v7. app. AlertDialog. Builder | Mamalcertdialogbuilder |
| android.support.v7.app.AppCompatActivity | MAMAppCompatActivity |
| android.support.v7.widget.AppCompatAutoCompleteTextView | MAMAppCompatAutoCompleteTextView |
| android.support.v7.widget.AppCompatCheckedTextView | MAMAppCompatCheckedTextView |
| android.support.v7.widget.AppCompatEditText | MAMAppCompatEditText |
| android.support.v7.widget.AppCompatMultiAutoCompleteTextView | MAMAppCompatMultiAutoCompleteTextView |
| android.support.v7.widget.AppCompatTextView | MAMAppCompatTextView |

### <a name="microsoftintunemamsdksupportv17jar"></a>Microsoft.Intune.MAM.SDK.Support.v17.jar:
|Android Sınıfı | Intune Uygulama SDK'sı karşılığı |
|--|--|
| android.support.v17.leanback.widget.SearchEditText | MAMSearchEditText |

### <a name="microsoftintunemamsdksupporttextjar"></a>Microsoft.Intune.MAM.SDK.Support.Text.jar:
|Android Sınıfı | Intune Uygulama SDK'sı karşılığı |
|--|--|
| android.support.text.emoji.widget.EmojiAppCompatEditText | MAMEmojiAppCompatEditText |
| android.support.text.emoji.widget.EmojiAppCompatTextView | MAMEmojiAppCompatTextView |
| android.support.text.emoji.widget.EmojiEditText | MAMEmojiEditText |
| android.support.text.emoji.widget.EmojiTextView | MAMEmojiTextView |

### <a name="renamed-methods"></a>Yeniden Adlandırılan Yöntemler

Birçok durumda, Android sınıfında kullanılabilir olan bir yöntem, MAM değiştirme sınıfında kesin olarak işaretlenmiştir. Bu durumda, MAM değiştirme sınıfı benzer ada sahip olup (genellikle `MAM` son ekini alır) geçersiz kılmanız gereken bir yöntem sağlar. Örneğin, `MAMActivity`’i geçersiz kılıp `onCreate()` çağırmak yerine `super.onCreate()`’den türetilirken, `Activity`, `onMAMCreate()`’i geçersiz kılmalı ve `super.onMAMCreate()` çağırmalıdır. Java derleyicisi, MAM eşdeğeri yerine özgün metodun yanlışlıkla geçersiz kılınmasını önleyen kesin kısıtlamalar uygulamalıdır.

### <a name="mamapplication"></a>MAMApplication
Uygulamanız bir `android.app.Application` alt sınıfı oluşturursa bunun yerine bir `com.microsoft.intune.mam.client.app.MAMApplication` alt sınıfı oluşturmanız **gerekir**. Uygulamanız `android.app.Application` alt sınıfı oluşturmazsa AndroidManifest.xml’in `<application>` etiketinde `"android:name"` özniteliği olarak `"com.microsoft.intune.mam.client.app.MAMApplication"` ayarlamanız **gerekir**.

### <a name="pendingintent"></a>PendingIntent
`PendingIntent.get*` yerine `MAMPendingIntent.get*` yöntemini kullanmanız gerekir. Bundan sonra her zamanki gibi `PendingIntent` sonucunu kullanabilirsiniz.

### <a name="wrapped-system-services"></a>Sarmalanmış Sistem Hizmetleri
Bazı sistem hizmet sınıflarında, istenen bir yöntemi hizmet örneğinde doğrudan çağırmak yerine bir MAM sarmalayıcı sınıfının statik bir yöntemini çağırmak gerekir. Örneğin bir `getSystemService(ClipboardManager.class).getPrimaryClip()` çağrısı bir `MAMClipboardManager.getPrimaryClip(getSystemService(ClipboardManager.class)` çağrısı haline gelmelidir. Bu değişikliklerin elle yapılması önerilmez. Bu işlemi BuildPlugin ile yapın.

| Android Sınıfı | Intune Uygulama SDK'sı karşılığı |
|--|--|
| android.content.ClipboardManager | MAMClipboard |
| Android. Content. ContentProviderClient | MAMContentProviderClientManagement |
| Android. Content. ContentResolver | MAMContentResolverManagement |
| android.content.pm.PackageManager | MAMPackageManagement |
| android.app.DownloadManager | MAMDownloadManagement |
| Android. Print. PrintManager | MAMPrintManagement |
| Android. support. v4. Print. PrintHelper | MAMPrintHelperManagement |
| Android. View. View | MAMViewManagement |
| Android. View. DragEvent | MAMDragEventManagement |
| Android. app. NotificationManager | MAMNotificationManagement |
| Android. support. v4. app. NotificationManagerCompat | MAMNotificationCompatManagement |

Bazı sınıfların çoğu yöntemlerinin büyük bir kısmı sarmalanır, örneğin,,, `ClipboardManager` `ContentProviderClient` `ContentResolver` ve `PackageManager` diğer sınıfların yalnızca bir veya iki yöntemi sarmalanmış olsa da `DownloadManager` `PrintManager` `PrintHelper` `View` `DragEvent` `NotificationManager` ,,,,, ve `NotificationManagerCompat` . BuildPlugin kullanmazsanız, lütfen tam Yöntem için MAM denk sınıflar tarafından kullanıma sunulan API 'Lere başvurun.

### <a name="manifest-replacements"></a>Bildirim Değişiklikleri
Hem bildirimde hem de Java kodunda yukarıdaki sınıf değişikliklerinden bazılarını yapmanız gerekebilir. Özel not:
* `android.support.v4.content.FileProvider` için olan bildirim başvuruları `com.microsoft.intune.mam.client.support.v4.content.MAMFileProvider` ile değiştirilmelidir.

## <a name="androidx-libraries"></a>AndroidX Kitaplıkları
Android P ile Google, AndroidX adlı yeni (yeniden adlandırılmış) bir destek kitaplıkları kümesini duyurdu ve sürüm 28 mevcut android.support kitaplıklarının son önemli sürümü.

Android destek kitaplıklarından farklı olarak AndroidX kitaplıklarının MAM çeşitlerini sunmuyoruz. AndroidX herhangi bir dış kitaplık gibi değerlendirilmeli ve derleme eklentisi/aracı tarafından yeniden yazılmak üzere yapılandırılmalıdır. Gradle derlemeleri için, bu, `androidx.*` `includeExternalLibraries` eklenti yapılandırması alanına eklenerek yapılabilir. Komut satırı aracının çağırmaları tüm jar dosyalarını açıkça listemalıdır.

### <a name="pre-androidx-architecture-components"></a>Ön AndroidX mimari bileşenleri
Oda, ViewModel ve WorkManager dahil pek çok Android mimarisi bileşeni AndroidX için yeniden paketlenmiştir. Uygulamanız bu kitaplıkların pre-AndroidX türevlerini kullanıyorsa, `android.arch.*` eklenti yapılandırması alanına dahil ederek yeniden bağlanma uygulamasının uygulanmasını sağlayın `includeExternalLibraries` . Alternatif olarak, kitaplıkları AndroidX eşdeğerlerine güncelleştirin.

### <a name="troubleshooting-androidx-migration"></a>AndroidX geçiş sorunlarını giderme
SDK ile tümleşik uygulamanızı AndroidX 'e geçirirken aşağıdakiler gibi bir hatayla karşılaşabilirsiniz:

```log
incompatible types: android.support.v7.app.ActionBar cannot be converted to androidx.appcompat.app.ActionBar
```

Bu hatalar, uygulamanız MAM destek sınıflarına başvurduğundan oluşabilir. MAM destek sınıfları, AndroidX 'e taşınan Android destek sınıflarını kaydırır. Bu tür hatalara karşı, tüm MAM destek sınıfı başvurularını AndroidX eşdeğerleriyle değiştirin. Bu, önce Gradle derleme dosyalarınızda MAM destek kitaplığı bağımlılıklarını kaldırarak elde edilebilir. Söz konusu satırlar aşağıdakine benzer şekilde görünür:

```Gradle
implementation "com.microsoft.intune.mam:android-sdk-support-v4:$intune_mam_version"
implementation "com.microsoft.intune.mam:android-sdk-support-v7:$intune_mam_version"
```

Ardından, ve paketlerdeki MAM sınıflardaki tüm başvuruları `com.microsoft.intune.mam.client.support.v7` AndroidX eşdeğerleriyle değiştirerek ortaya çıkan derleme zamanı hatalarını düzeltir `com.microsoft.intune.mam.client.support.v4` . Örneğin, başvuruları `MAMAppCompatActivity` AndroidX 'in olarak değiştirilmelidir `AppCompatActivity` . Yukarıda açıklanan şekilde, MAM derleme eklentisi/Aracı, AndroidX kitaplıklarına sınıfları derleme zamanında uygun MAM eşdeğerlerine göre otomatik olarak yeniden oluşturur.

## <a name="sdk-permissions"></a>SDK izinleri

Intune uygulama SDK'sı, tümleştirildiği uygulamalarda üç [Android sistem izni](https://developer.android.com/guide/topics/security/permissions.html) gerektirir:

* `android.permission.GET_ACCOUNTS` (gerekirse çalışma zamanında istenir)

* `android.permission.MANAGE_ACCOUNTS`

* `android.permission.USE_CREDENTIALS`

Bu izinler, Azure Active Directory Kimlik Doğrulama Kitaplığı ([ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/)) tarafından aracılık edilen kimlik doğrulaması gerçekleştirmek üzere istenir. Bu izinler uygulamaya sağlanmazsa veya kullanıcı tarafından kaldırılırsa, aracı (Şirket Portalı uygulaması) gerektiren kimlik doğrulama akışları devre dışı bırakılır.

## <a name="logging"></a>Günlüğe kaydetme

Günlüğe kaydedilen verilerden en iyi şekilde yararlanmak için günlüğün erken başlatılması gerekir. `Application.onMAMCreate()` normalde günlüğü başlatmak için en iyi konumdur.

Uygulamanıza MAM günlüklerini almak için, [Java İşleyicisi](https://docs.oracle.com/javase/7/docs/api/java/util/logging/Handler.html) oluşturun ve bunu `MAMLogHandlerWrapper` konumuna ekleyin. Bu, her günlük iletisi için uygulama işleyicisinde `publish()` çağrısı yapar.

```java
/**
 * Global log handler that enables fine grained PII filtering within MAM logs.  
 *
 * To start using this you should build your own log handler and add it via
 * MAMComponents.get(MAMLogHandlerWrapper.class).addHandler(myHandler, false);  
 *
 * You may also remove the handler entirely via
 * MAMComponents.get(MAMLogHandlerWrapper.class).removeHandler(myHandler);
 */
public interface MAMLogHandlerWrapper {
    /**
     * Add a handler, PII can be toggled.
     *
     * @param handler handler to add.
     * @param wantsPII if PII is desired in the logs.    
     */
    void addHandler(final Handler handler, final boolean wantsPII);

    /**
     * Remove a handler.
     *
     * @param handler handler to remove.
     */
    void removeHandler(final Handler handler);
}
```

## <a name="diagnostics-information"></a>Tanılama bilgileri
Uygulamalar, `MAMPolicyManager.showDiagnostics(context)` Şirket portalı günlüklerini toplamak ve Mam tanılamayı görüntülemek için Kullanıcı arabirimi görüntüleyen bir etkinliği Başlatan yöntemi çağırabilir.
Bu, hata ayıklamaya yardımcı olabilecek isteğe bağlı bir özelliktir.

Cihaza Şirket Portalı yüklü olmadığında, bu bilgilerin şu anda kullanılabilir durumda olduğunu kullanıcıya bildirmek için bir iletişim kutusu istenir. Uygulamalar MAM ilkesi tarafından yönetildiğinde, ayrıntılı MAM ilke ayarları görüntülenir.

## <a name="mam-strict-mode"></a>MAM katı mod
MAM katı mod, MAM API 'lerinin veya MAM kısıtlı platform API 'lerinin uygulama kullanımında "Smells" öğesini algılamaya yönelik bir mekanizma sağlar. Android 'in StrictMode 'dan sonra gevşek bir şekilde desenli ve başarısız olduklarında hata veren bir denetim kümesi çalıştırırlar. Üretim yapılarında etkinleştirilmeye yönelik değildir, ancak uygulamanızın iç geliştirme, hata ayıklama ve/veya doggıda Derlemelerinizde kullanılması *önemle* önerilir.

Etkinleştirmek, çağırmak için

```java
MAMStrictMode.enable();
```
 uygulama başlatılırken erken (ör. `Application.onCreate` ). 

MAM katı mod denetimi başarısız olduğunda, uygulamanızın uygulamanızda düzeltilenler veya hatalı pozitif bir sorun olup olmadığını belirlemeyi deneyin. Bunun yanlış pozitif olduğunu düşünüyorsanız veya emin değilseniz lütfen Intune MAM ekibinin bilmesini sağlayın. Bu, yanlış pozitif belirlemele anlaşıyoruz ve gelecekteki sürümler için algılamayı geliştirmeyi denemek için size izin verir. Hatalı pozitifleri gizlemek için başarısız denetimi devre dışı bırakın (daha fazla bilgi).

### <a name="handling-violations"></a>Ihlalleri işleme
Bir denetim başarısız olduğunda, çalışır `MAMStrictViolationHandler` . Varsayılan işleyici, `Error` uygulamanın kilitlenmesi beklenen bir oluşturur. Bu, hatalara olabildiğince gürültülü hale getirmek ve üretim yapılarında katı modunun etkinleştirilmemelidir.

Uygulamanız ihlalleri farklı şekilde işlemek istiyorsanız şunu çağırarak kendi işleyicisini sağlayabilirsiniz:

```java
MAMStrictMode.global().setHandler(handler);
```

`handler`şunları uygular `MAMStrictViolationHandler` :

```java
public interface MAMStrictViolationHandler {
    /**
     * Called when a MAM Strict Mode check fails.
     *
     * @param check
     *         the check that failed
     * @param detail
     *         additional detail. Note that this might contain usernames or filepaths.
     * @param error
     *         error containing a stack trace. The default implementation throws this error
     */
    void checkFailed(@NonNull MAMStrictCheck check, @NonNull String detail, @NonNull Error error);
}
```

### <a name="suppressing-checks"></a>Denetimleri gizleme
Uygulamanızın hiçbir şey yanlış bir durumda olmadığı bir denetim başarısız olursa, lütfen yukarıda belirtilen şekilde bildirin. Ancak, bazı zamanlarda, en azından güncelleştirilmiş bir SDK için beklerken, yanlış pozitif bir pozitif ve bu denetimi devre dışı bırakmanız gerekebilir. Başarısız olan denetim varsayılan işleyici tarafından oluşturulan hatada gösterilir veya ayarlandıysa özel bir işleyiciye geçirilir.

Gizleme genel olarak yapılabilir, ancak belirli bir çağrı sitesinde iş parçacığı başına geçici olarak devre dışı bırakılması tercih edilir. Aşağıdaki örneklerde devre dışı bırakılacak çeşitli yollar gösterilmektedir `MAMStrictCheck.IDENTITY_NO_SUCH_FILE` (mevcut olmayan bir dosyayı korumak için bir girişimde bulunulduğunda tetiklenir).


#### <a name="per-thread-temporary-suppression"></a>Iş parçacığı başına geçici gizleme
Bu, tercih edilen gizleme mekanizmasıdır.
```java
try (StrictScopedDisable disable = MAMStrictMode.thread().disableScoped(MAMStrictCheck.IDENTITY_NO_SUCH_FILE)) {
    // Perform the operation which raised a violation here
}
// The check is no longer disabled once the block exits
```

#### <a name="per-thread-permanent-suppression"></a>Iş parçacığı başına kalıcı gizleme
```java
MAMStrictMode.thread().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```

#### <a name="global-process-wide-suppression"></a>Küresel (Işlem genelinde) gizleme
```java
MAMStrictMode.global().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```



## <a name="enable-features-that-require-app-participation"></a>Uygulama katılımı gerektiren özellikleri etkinleştirme

SDK’nın kendi başına uygulayamayacağı çeşitli uygulama koruma ilkeleri vardır. Uygulama bu özellikleri sağlamak için aşağıdaki `AppPolicy` arabiriminde bulabileceğiniz çeşitli API’ler kullanarak davranışını denetleyebilir. Bir `AppPolicy` örneği almak için `MAMPolicyManager.getPolicy` kullanın.

```java
/**
 * External facing application policies.
 */
public interface AppPolicy {

/**
 * Restrict where an app can save personal data.
 * This function is now deprecated. Use getIsSaveToLocationAllowed(SaveLocation, String) instead
 * @return True if the app is allowed to save to personal data stores; false otherwise.
 */
@Deprecated
boolean getIsSaveToPersonalAllowed();

/**
 * Check if policy prohibits saving to a content provider location.
 *
 * @param location
 *            a content URI to check
 * @return True if location is not a content URI or if policy does not prohibit saving to the content location.
 */
boolean getIsSaveToLocationAllowed(Uri location);

/**
 * Determines if the SaveLocation passed in can be saved to by the username associated with the cloud service.
 *
 * @param service
 *           The SaveLocation the data will be saved to.
 * @param username
 *           The AAD UPN associated with the cloud service being saved to. Use null if a mapping between
 *           the AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the location can be saved to by the identity, false if otherwise.
 */
boolean getIsSaveToLocationAllowed(SaveLocation service, String username);

/**
 * Determines if data from the OpenLocation can be opened for the username associated with the data.
 *
 * @param location
 *      The OpenLocation that the data will be opened from.
 * @param username
 *      The AAD UPN associated with the location the data is being opened from. Use null if a mapping between the
 *      AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the data can be opened from the location for the identity, false if otherwise.
 */
boolean getIsOpenFromLocationAllowed(@NonNull OpenLocation location, @Nullable String username);

/**
 * Checks whether any activities which could handle the given intent are allowed by policy. Returns false only if all
 * activities which could otherwise handle the intent are blocked. If there are no activities which could handle the intent
 * regardless of policy, returns true. If some activities are allowed and others blocked, returns true. Note that it is not
 * necessary to use this method for policy enforcement. If your app attempts to launch an intent for which there are no
 * allowed activities, MAM will display a dialog explaining the situation to the user.
 *
 * @param intent
 *         intent to check
 *
 * @return whether any activities which could handle this intent are allowed.
*/
boolean areIntentActivitiesAllowed(Intent intent);

/**
 * Whether the SDK PIN prompt is enabled for the app.
 *
 * @return True if the PIN is enabled. False otherwise.
 */
boolean getIsPinRequired();

/**
 * Whether the Intune Managed Browser is required to open web links.
 * @return True if the Managed Browser is required, false otherwise
 */
boolean getIsManagedBrowserRequired();

/**
 * Check if policy allows taking screenshots.
 *
 * @return True if screenshots will be blocked, false otherwise
 */
boolean getIsScreenCaptureAllowed();

/**
 * Check if policy allows Contact sync to local contact list.
 *
 * @return True if Contact sync is allowed to save to local contact list; false otherwise.
 */
boolean getIsContactSyncAllowed();

/**
 * Get the notification restriction. If {@link NotificationRestriction#BLOCKED BLOCKED}, the app must not show any notifications
 * for the user associated with this policy. If {@link NotificationRestriction#BLOCK_ORG_DATA BLOCK_ORG_DATA}, the app must show
 * a modified notification that does not contain organization data. If {@link NotificationRestriction#UNRESTRICTED
 * UNRESTRICTED}, all notifications are allowed.
 *
 * @return The notification restriction.
 */
NotificationRestriction getNotificationRestriction();

/**
 * This method is intended for diagnostic/telemetry purposes only. It can be used to discover whether file encryption is in use.
 * File encryption is transparent to the app and the app should not need to make any business logic decisions based on this.
 * @return True if file encryption is in use.
 */
boolean diagnosticIsFileEncryptionInUse();

/**
 * Return the policy in string format to the app.
 *  
 * @return The string representing the policy.
 */
String toString();

}
```

> [!NOTE]
> Cihaz veya uygulama bir Intune yönetim ilkesi altında olmasa bile `MAMPolicyManager.getPolicy` her zaman null olmayan bir Uygulama İlkesi döndürür.

### <a name="example-determine-if-pin-is-required-for-the-app"></a>Örnek: Uygulama için PIN’in gerekli olup olmadığını belirleme

Uygulamanın kendi PIN kullanıcı deneyimi varsa, BT yöneticisi SDK’yı uygulama PIN’ini isteyecek şekilde yapılandırdıysa, uygulamanın deneyimini devre dışı bırakmak isteyebilirsiniz. BT yöneticisinin bu uygulamada uygulama PIN ilkesini dağıtıp dağıtmadığını belirlemek için, geçerli son kullanıcı için aşağıdaki yöntemi çağırın:

```java

MAMPolicyManager.getPolicy(currentActivity).getIsPinRequired();
```

### <a name="example-determine-the-primary-intune-user"></a>Örnek: Birincil Intune kullanıcısını belirleme

AppPolicy’de gösterilen API’lere ek olarak, `MAMUserInfo` arabirimi içinde tanımlanan `getPrimaryUser()` API’si tarafından kullanıcı asıl adı (**UPN**) da gösterilir. UPN’yi almak için aşağıdaki çağrıyı yapın:

```java
MAMComponents.get(MAMUserInfo.class).getPrimaryUser();
```

MAMUserInfo arabiriminin tam tanımı şöyledir:

```java
/**
 * External facing user information.
 *
 */
public interface MAMUserInfo {
       /**
        * Get the primary user name.
        *
        * @return the primary user name or null if neither the device nor app is enrolled.
        */
       String getPrimaryUser();
}
```

### <a name="example-data-transfer-between-apps-and-device-or-cloud-storage-locations"></a>Örnek: uygulamalar ile cihaz veya bulut depolama konumları arasında veri aktarımı

Birçok uygulama, son kullanıcının yerel dosya depolama veya bulut depolama hizmetlerine veri kaydetmesine veya bu verileri açmasını sağlayan özellikler uygular.
Intune uygulama SDK 'Sı, BT yöneticilerinin, kuruluşlarında sığdırma yaparken, ilke kısıtlamaları uygulayarak veri giriş ve sızıntılara karşı koruma sağlamasına olanak tanır.

**Özelliği etkinleştirmek için uygulama katılımı gereklidir.**
Uygulamanız kişisel veya bulut konumlarına doğrudan uygulama üzerinden kaydetmeye izin veriyorsa *veya* verilerin doğrudan uygulamaya açılmasına izin VERIYORSA, BT yöneticisinin bir konumdan kaydetmeye/buradan açmaya izin verilip verilmediğini denetlemesini sağlamak için ilgili özelliği uygulamanız gerekir.

#### <a name="saving-to-device-or-cloud-storage"></a>Cihaza veya bulut depolamaya kaydetme

Aşağıdaki API, uygulamanın, geçerli Intune yönetici ilkesi tarafından kişisel bir depolama alanına kaydetmeye izin verilip verilmediğini bilmesini sağlar.

İlkenin zorunlu tutulup tutulmadığını belirlemek için aşağıdaki çağrıyı yapın:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(
SaveLocation service, String username);
```

`service`Parametre aşağıdaki değerlerden biri olmalıdır `SaveLocation` :

* `SaveLocation.ONEDRIVE_FOR_BUSINESS`
* `SaveLocation.SHAREPOINT`
* `SaveLocation.LOCAL`
* `SaveLocation.ACCOUNT_DOCUMENT`
* `SaveLocation.OTHER`

`ACCOUNT_DOCUMENT` `OTHER` `getIsSaveToLocationAllowed` Daha fazla bilgi için [Bilinmeyen veya listelenmemiş konumları](#unknown-or-unlisted-locations) görmek üzere veya geçirilmesi gerekip gerekmediğini belirlemek için.

Parametresi için `username` , daha fazla bilgi için bkz. [veri aktarımı Için Kullanıcı adı](#username-for-data-transfer) .

Kullanıcının ilkesinin çeşitli konumlara veri kaydetmesine izin verip vermediğini belirlemeye yönelik önceki yöntem, aynı **AppPolicy** sınıfındaki `getIsSaveToPersonalAllowed()` yöntemiydi.
Bu işlev artık **kullanım dışı bırakılmıştır** ve kullanılmamalıdır; aşağıdaki çağrı `getIsSaveToPersonalAllowed()` ile eşdeğerdir:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(SaveLocation.LOCAL, null);
```

#### <a name="opening-data-from-a-local-or-cloud-storage-location"></a>Yerel veya bulut depolama konumundan veri açma

Aşağıdaki API, uygulamanın, geçerli Intune yöneticisinin ilkesi tarafından kişisel bir mağazadan açmaya izin verilip verilmediğini bilmesini sağlar.

İlkenin zorunlu tutulup tutulmadığını belirlemek için aşağıdaki çağrıyı yapın:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsOpenFromLocationAllowed(
OpenLocation location, String username);
```

`location`Parametre aşağıdaki değerlerden biri olmalıdır `OpenLocation` :

* `OpenLocation.ONEDRIVE_FOR_BUSINESS`
* `OpenLocation.SHAREPOINT`
* `OpenLocation.CAMERA`
* `OpenLocation.LOCAL`
* `OpenLocation.ACCOUNT_DOCUMENT`
* `OpenLocation.OTHER`

`OpenLocation.CAMERA`Uygulama, kameradan verileri açarken konum geçirilmesi gerekir.
`OpenLocation.LOCAL`Uygulama, yerel cihazdaki dış depolamadan veri açarken konum geçirilmelidir.
Uygulama, uygulamada `OpenLocation.ACCOUNT_DOCUMENT` oturum açan BIR AAD hesabına ait verileri açarken konum geçirilmelidir.

`ACCOUNT_DOCUMENT` `OTHER` `getIsOpenFromLocationAllowed` Daha fazla bilgi için [Bilinmeyen veya listelenmemiş konumları](#unknown-or-unlisted-locations) görmek üzere veya geçirilmesi gerekip gerekmediğini belirlemek için.

Parametresi için `username` , daha fazla bilgi için bkz. [veri aktarımı Için Kullanıcı adı](#username-for-data-transfer) .

#### <a name="unknown-or-unlisted-locations"></a>Bilinmeyen veya listelenmemiş konumlar

İstenen konum `SaveLocation` veya numaralandırmalar içinde listelenmediyse `OpenLocation` veya bu `service` / `location` parametre bilinmiyorsa, ve parametreleri için `ACCOUNT_DOCUMENT` iki seçenek vardır `OTHER` .
`ACCOUNT_DOCUMENT` veriler uygulamada oturum açan bir AAD hesabına ait olduğunda, ancak `ONEDRIVE_FOR_BUSINESS` `SHAREPOINT` Bu durum yoksa, `OTHER` Bu durumda kullanılması gerekir.

Yönetilen hesap ile yönetilen hesabın UPN 'sini paylaşan bir hesap arasında ayrım yapmak önemlidir.
Örneğin, "" UPN 'si ile yönetilen bir hesap, user@contoso.com OneDrive 'da oturum açmış "" UPN 'sine sahip bir hesapla aynı değildir user@contoso.com .
Yönetilen hesapta oturum açarak bilinmeyen veya listelenmemiş bir hizmete erişiliyorsa (ör. " user@contoso.com " OneDrive 'da oturum açıldı), konum tarafından temsil edilmelidir `ACCOUNT_DOCUMENT` .
Bilinmeyen veya listelenmemiş hizmet başka bir hesapta oturum açarsa (ör. " user@contoso.com " Dropbox 'ta oturum açıldı), yönetilen bir hesapla konuma erişmez ve konum tarafından temsil edilmelidir `OTHER` .

#### <a name="username-for-data-transfer"></a>Veri aktarımı için Kullanıcı adı

Kayıt ilkesini denetlerken, `username` kaydedilen bulut hizmeti ile ILIŞKILI UPN/Kullanıcı adı/e-posta olması gerekir (Bu, kaydedilmekte olan*not* kullanıcıyla aynı olması gerekmez).
`SaveLocation.LOCAL` bir bulut hizmeti değil, her zaman bir `null` Kullanıcı adı parametresiyle birlikte kullanılmalıdır.

Açık ilke denetlenirken, `username` açılan bulut hizmeti ile ILIŞKILI UPN/Kullanıcı adı/e-posta olmalıdır.
`OpenLocation.LOCAL` ve `OpenLocation.CAMERA` bulut hizmeti konumları değildir ve bu nedenle her zaman bir `null` Kullanıcı adı parametresiyle birlikte kullanılmalıdır.

Aşağıdaki konumlar her zaman AAD UPN ve Cloud Service Kullanıcı adı arasında bir eşleme içeren bir Kullanıcı adı bekler: `ONEDRIVE_FOR_BUSINESS` , `SHAREPOINT` ve `ACCOUNT_DOCUMENT` .

AAD UPN ile bulut hizmeti Kullanıcı adı arasında bir eşleme yoksa veya Kullanıcı adının bilinen kullanım alanı yoksa `null` .

#### <a name="sharing-blocked-dialog"></a>Paylaşım engellendi iletişim kutusu

SDK, kullanıcıya bir veri aktarımı eyleminin MAM ilkesi tarafından engellendiğini bildiren bir iletişim kutusu sağlar.

`isSaveToAllowedForLocation`Veya `isOpenFromAllowedForLocation` API çağrısı, engellenen Kaydet/Aç eylemi ile sonuçlanırsa, iletişim kutusu kullanıcıya görüntülenmelidir.
İletişim kutusu genel bir ileti görüntüler ve bu iletiyi `Activity` çıkarıldığında çağıran öğesine döndürür.

İletişim kutusunu göstermek için aşağıdaki çağrıyı yapın:

``` java
MAMUIHelper.showSharingBlockedDialog(currentActivity)
```

### <a name="allow-for-file-sharing"></a>Dosya paylaşımına izin ver

Ortak depolama konumlarına kaydetmeye izin verilmiyorsa, uygulamanız hala [uygulama özel depolama alanına](https://developer.android.com/training/data-storage) indirerek ve sonra bunları sistem seçiciyle açarak kullanıcının dosyaları görüntülemesine izin vermeyi sağlamalıdır.

### <a name="example-determine-if-notifications-with-organization-data-need-to-be-restricted"></a>Örnek: kuruluş verilerine sahip bildirimlerin kısıtlanması gerekip gerekmediğini belirleme

Uygulamanız bildirimleri görüntülüyorsa, bildirimi göstermeden önce bildirimle ilişkili kullanıcı için bildirim kısıtlama ilkesini denetlemeniz gerekir. İlkenin uygulanıp uygulanmadığını anlamak için aşağıdaki çağrıyı yapın.

```java
NotificationRestriction notificationRestriction =
    MAMPolicyManager.getPolicyForIdentity(notificationIdentity).getNotificationRestriction();
```

Kısıtlama ise `BLOCKED` , uygulamanın bu ilkeyle ilişkili kullanıcı için herhangi bir bildirim göstermemelidir. İse `BLOCK_ORG_DATA` , uygulamanın kuruluş verileri içermeyen bir değiştirilmiş bildirim göstermesi gerekir. Varsa `UNRESTRICTED` , tüm bildirimlere izin verilir.

`getNotificationRestriction`Çağrılmadığından, mam SDK, tek kimlik uygulamaları için bildirimleri otomatik olarak kısıtlamak için en iyi çabayı yapar. Otomatik engelleme etkin ve `BLOCK_ORG_DATA` ayarlandıysa, bildirim hiç gösterilmez. Daha ayrıntılı denetim için, değerini denetleyin `getNotificationRestriction` ve uygulama bildirimlerini uygun şekilde değiştirin.

## <a name="register-for-notifications-from-the-sdk"></a>SDK’dan gelen bildirimlere kaydolma

### <a name="overview"></a>Genel bakış
Intune Uygulama SDK’sı uygulamanıza seçmeli silme gibi bazı ilkelerin (bu ilkeler BT yöneticisi tarafından dağıtıldığında) davranışını denetleme izni verir. BT yöneticisi böyle bir ilke dağıttığında, Intune hizmeti SDK’ya bir bildirim gönderir.

Uygulamanızın `MAMNotificationReceiver` oluşturup `MAMNotificationReceiverRegistry` ile kaydederek SDK’dan gelen bildirimlere kaydolması gerekir. Bu işlem, aşağıdaki örnekte gösterildiği gibi alıcı ve `App.onCreate` öğesinde istenen bildirim türü belirtilerek yapılır:

```java
@Override
public void onCreate() {
  super.onCreate();
  MAMComponents.get(MAMNotificationReceiverRegistry.class)
    .registerReceiver(
      new ToastNotificationReceiver(),
      MAMNotificationType.WIPE_USER_DATA);
}
```

### <a name="mamnotificationreceiver"></a>MAMNotificationReceiver

`MAMNotificationReceiver` arabirimi yalnızca Intune hizmetinden bildirimleri alır. Bazı bildirimler doğrudan SDK tarafından işlenirken, bazıları uygulamanın katılımını gerektirir. Bir uygulamanın, bildirimden true veya false değeri döndürmesi **gerekir**. Bildirim sonucunda uygulamayı denediği bazı eylemler başarısız olmadığı sürece, uygulama her zaman true değerini döndürmelidir.

* Bu hata Intune hizmetine bildirilebilir. BT yöneticisi bir silme işlemi başlattıktan sonra uygulamanın kullanıcı verilerini silmekte başarısız olması rapor edilecek bir senaryoya örnek olarak verilebilir.

>[!NOTE]
> `MAMNotificationReceiver.onReceive` öğesinin engellenmesi güvenlidir; çünkü geri çağırma işlemi, kullanıcı arabirimi iş parçacığı üzerinde çalışmamaktadır.

SDK’da tanımlanan `MAMNotificationReceiver` arabirimi aşağıya eklenmiştir:

```java
/**
 * The SDK is signaling that a MAM event has occurred.
 *
 */
public interface MAMNotificationReceiver {

    /**
     * A notification was received.
     *
     * @param notification
     *            The notification that was received.
     * @return The receiver should return true if it handled the
     *   notification without error (or if it decided to ignore the
     *   notification). If the receiver tried to take some action in
     *   response to the notification but failed to complete that
     *   action it should return false.
     */
    boolean onReceive(MAMNotification notification);
}
```

### <a name="types-of-notifications"></a>Bildirim türleri

Aşağıdaki bildirimler uygulamaya gönderilir ve bazıları uygulama katılımını gerektirebilir:

* **WIPE_USER_DATA**: Bu bildirim bir `MAMUserNotification` sınıfında gönderilir. Bu bildirim alındığında, uygulamanın yönetilen kimlikle ilişkili tüm verileri (Kimden) silmesi *gerekir* `MAMUserNotification.getUserIdentity()` . Bildirim, uygulamanızın çağrı yaptığı zaman, bir `unregisterAccountForMAM` BT Yöneticisi bir silme işlemi başlattığında veya yönetici tarafından gerekli koşullu erişim ilkeleri karşılanmadığı durumlarda da dahil olmak üzere çeşitli nedenlerle meydana gelebilir. Uygulamanız bu bildirime kaydolmaz, varsayılan silme davranışı gerçekleştirilir. Varsayılan davranış tek kimlikli bir uygulama için tüm dosyaları veya çok kimlikli bir uygulama için yönetilen kimlikle etiketlenmiş tüm dosyaları siler. Bu bildirim, Kullanıcı arabirimi iş parçacığı üzerinde hiçbir şekilde gönderilmeyecektir.

* **WIPE_USER_AUXILIARY_DATA**: Uygulamalar Intune Uygulama SDK’sının varsayılan seçmeli silme davranışını gerçekleştirmesini ve diğer yandan silme gerçekleştirildiğinde bazı yardımcı verilerin kaldırılmasını isterse bu bildirime kaydolabilir. Bu bildirim tek kimlik uygulamaları için kullanılamaz; yalnızca çoklu kimlik uygulamalarına gönderilir. Bu bildirim, Kullanıcı arabirimi iş parçacığı üzerinde hiçbir şekilde gönderilmeyecektir.

* **REFRESH_POLICY**: Bu bildirim bir `MAMUserNotification` içinde gönderilir. Bu bildirim alındığında, uygulamanız tarafından önbelleğe alınan tüm Intune ilkesi kararları geçersiz kılınmalıdır ve güncelleştirilir. Uygulamanız herhangi bir ilke varsayımsını depolamaz bu bildirime kaydolmamalıdır. Bu bildirimin gönderileceği iş parçacığı olarak hiçbir garanti yapılmaz.

* **REFRESH_APP_CONFIG**: Bu bildirim bir içinde gönderilir `MAMUserNotification` . Bu bildirim alındığında, önbelleğe alınan tüm uygulama yapılandırma verileri geçersiz kılınmalıdır ve güncelleştirilir. Bu bildirimin gönderileceği iş parçacığı olarak hiçbir garanti yapılmaz.

* **MANAGEMENT_REMOVED**: Bu bildirim `MAMUserNotification` içinde gönderilir ve uygulamaya, yönetilmeyen bir uygulamaya dönüşmek üzere olduğunu bildirir. Yönetilmeyen duruma gelince, artık şifreli dosyaları okuyamayacak, MAMDataProtectionManager ile şifrelenmiş verileri okuyamayacak, şifrelenmiş panoyla etkileşim kuramayacak veya başka bir şekilde yönetilen uygulama ekosistemine katılamayacaktır. Daha ayrıntılı bilgi için aşağıdaki ayrıntılara bakın. Bu bildirim, Kullanıcı arabirimi iş parçacığı üzerinde hiçbir şekilde gönderilmeyecektir.

* **MAM_ENROLLMENT_RESULT**: Bu bildirim, uygulamayı bir `MAMEnrollmentNotification` App-we kayıt denemesinin tamamlandığını bilgilendirmek ve bu girişimin durumunu sağlamak için bir ile gönderilir. Bu bildirimin gönderileceği iş parçacığı olarak hiçbir garanti yapılmaz.

* **COMPLIANCE_STATUS**: Bu bildirim bir `MAMComplianceNotification` Uyumluluk Düzeltme denemesinin sonucunu uygulamayı bilgilendirmek için bir ile gönderilir. Bu bildirimin gönderileceği iş parçacığı olarak hiçbir garanti yapılmaz.

> [!NOTE]
> Bir uygulamanın hiçbir zaman hem `WIPE_USER_DATA` hem de `WIPE_USER_AUXILIARY_DATA` bildirimleri için kaydı olmamalıdır.

### <a name="management_removed"></a>MANAGEMENT_REMOVED

`MANAGEMENT_REMOVED`Bildirim, daha önce ilkeyle yönetilen bir kullanıcının artık ıNTUNE mam ilkesi tarafından yönetilmeyeceğini gösterir. Bu, Kullanıcı verilerini silme veya Kullanıcı oturumu kapatma gerektirmez (bir temizleme gerekliyse bir `WIPE_USER_DATA` bildirim gönderilir). Birçok uygulamanın bu bildirimi hiç işlemesi gerekmez, ancak kullanan uygulamalar `MAMDataProtectionManager` [Bu bildirimin özel durumunu göz önünde](#data-protection)tutabilmelidir.

MAM, uygulamanın `MANAGEMENT_REMOVED` alıcısını çağırdığında aşağıdakiler doğru olacaktır:
* MAM, uygulamaya ait olan önceden şifrelenmiş dosyaların (ancak korunmayan veri arabelleklerinin) şifresini zaten çözüldü. Sdcard üzerinde, doğrudan uygulamaya ait olmayan (örn. belgeler veya Indirme klasörleri) ortak konumlardaki dosyalar şifresi çözülür.
* Alıcı yöntemi tarafından oluşturulan yeni dosyalar veya korumalı veri arabellekleri (ya da alıcı başladıktan sonra çalışan başka bir kod) şifrelenmeyecektir.
* Uygulamanın hala şifreleme anahtarlarına erişimi vardır. bu nedenle, şifre çözme veri arabellekleri gibi işlemler başarılı olur.

Uygulamanızın alıcısı döndüğünde, artık şifreleme anahtarlarına erişemez.

## <a name="configure-azure-active-directory-authentication-library-adal"></a>Azure Active Directory Kimlik Doğrulama Kitaplığı'nı (ADAL) Yapılandırma

> [!NOTE]
> 30 Haziran 2020 ' den başlayarak Active Directory Authentication Library (ADAL) için yeni özellikler ekleyemeyecektir. Teknik destek ve güvenlik güncelleştirmeleri sağlamaya devam edeceğiz, ancak artık Özellik Güncelleştirmesi sağlamayız. Uygulamaların, Microsoft kimlik doğrulama kitaplığı 'na (MSAL) ve Microsoft Graph yükseltilmesi gerekir. [Android belgesi Için adal msal geçiş kılavuzu](https://docs.microsoft.com/azure/active-directory/develop/migrate-android-adal-msal) ' nda ek bilgiler bulunabilir


İlk olarak, lütfen [GitHub’da ADAL deposu](https://github.com/AzureAD/azure-activedirectory-library-for-android) konusunda bulunan ADAL tümleştirme yönergelerini okuyun.

SDK; [kimlik doğrulaması](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) ve koşullu başlatma senaryolarında, uygulamaların [Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-whatis/) ile yapılandırılmasını gerektiren [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) özelliğini kullanır. Yapılandırma değerleri, AndroidManifest meta verileri üzerinden SDK’ya iletilir.

Uygulamanızı yapılandırmak ve uygun kimlik doğrulamasını sağlamak için AndroidManifest.xml içindeki uygulama düğümüne aşağıdakileri ekleyin. Bu yapılandırmalardan bazıları, yalnızca uygulamanız genel olarak kimlik doğrulaması için ADAL kullanıyorsa gereklidir; bu durumda, uygulamanızın kendisini AAD’ye kaydetmek için kullandığı değerleri kullanmanız gerekir. Bu işlem, AAD’nin iki ayrı kayıt değerini (biri uygulamadan, biri SDK’dan) tanıması nedeniyle son kullanıcıdan kimlik doğrulamasının iki kez istenmesini önlemek amacıyla yapılır.

```xml
<meta-data
    android:name="com.microsoft.intune.mam.aad.Authority"
    android:value="https://AAD authority/" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.ClientID"
    android:value="your-client-ID-GUID" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.NonBrokerRedirectURI"
    android:value="your-redirect-URI" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.SkipBroker"
    android:value="[true | false]" />
```

### <a name="adal-metadata"></a>ADAL meta verileri

* **Yetkili**, kullanımdaki AAD yetkilisidir. Bu değer yoksa AAD ortak ortamı kullanılır.
    > [!NOTE]
    > Uygulamanız bağımsız bulut kullanıyorsa bu alanı ayarlamayın.

* **ClientID** , kullanılacak AAD ClientID 'Dir (uygulama kimliği olarak da bilinir). Azure AD 'ye kaydolduysanız veya ADAL tümleştirmemişse [varsayılan kayıttan](#default-enrollment-optional) yararlanmak için kendi uygulamanızın ClientID kullanmanız gerekir.

* **NonBrokerRedirectURI**, aracısız durumlarda kullanılacak AAD yeniden yönlendirme URI’sidir. Hiçbiri belirtilmemişse, varsayılan `urn:ietf:wg:oauth:2.0:oob` değeri kullanılır. Bu varsayılan değer, çoğu uygulamaya uygundur.

  * NonBrokerRedirectURI yalnızca SkipBroker "true" olduğunda kullanılır.

* **Skipbroker** varsayılan adal SSO katılım davranışını geçersiz kılmak için kullanılır. SkipBroker yalnızca bir ClientID belirten **ve** aracılı kimlik doğrulaması/CIHAZ genelinde SSO 'yu desteklemeyen uygulamalar için belirtilmelidir. Bu durumda, "true" olarak ayarlanmalıdır. Çoğu uygulama SkipBroker parametresini ayarlanmamalıdır.

  * Bir SkipBroker değeri belirtmek için bildirimde bir **ClientID belirtilmelidir** .

  * Bir ClientID belirtildiğinde, varsayılan değer "false" dır.

  * SkipBroker "true" olduğunda, NonBrokerRedirectURI kullanılacaktır. ADAL (ve bu nedenle ClientID) tümleştirmesiz uygulamalar, varsayılan olarak "true" olarak değişir.

### <a name="common-adal-configurations"></a>Yaygın ADAL yapılandırmaları

Aşağıda, uygulamanın ADAL ile yapılandırılabilmesinin yaygın yolları açıklanmıştır. Uygulamanızın yapılandırmasını bulun ve ADAL meta veri parametrelerini (yukarıda açıklanan parametreler) gerekli değerlere ayarladığınızdan emin olun. Her durumda, varsayılan olmayan ortamlar için isteniyorsa, yetkili belirlenebilir. Belirtilmemişse, genel üretim AAD yetkilisi kullanılacaktır.

#### <a name="1-app-does-not-integrate-adal"></a>1. uygulama ADAL 'yi tümleştirmez
ADAL meta **verileri bildirimde bulunmamalıdır.**

#### <a name="2-app-integrates-adal"></a>2. uygulama ADAL ile tümleşir

|Gerekli ADAL parametresi| Değer |
|--|--|
| ClientID | Uygulamanın İstemci Kimliği (uygulama kaydedilirken Azure AD tarafından oluşturulur) |

Gerekirse yetkili belirtilebilir.

Uygulamanızı Azure AD 'ye kaydetmeniz ve uygulamanıza uygulama koruma ilkesi hizmeti erişimi sağlamanız gerekir:
* Bkz. hızlı başlangıç: Azure AD ile uygulama kaydetme hakkında bilgi için [Microsoft Identity platformu ile uygulama kaydetme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications) .
* Android uygulama izinlerinizi uygulama koruma ilkesi (APP) hizmetine verme adımlarının izlendiğinden emin olun. "Uygulamanızın Intune uygulama koruma hizmeti 'ne erişmesine izin verin (isteğe bağlı)" altındaki [Intune SDK 'sını](../developer/app-sdk-get-started.md#next-steps-after-integration) kullanmaya başlama yönergelerini kullanın. 

Ayrıca aşağıdaki [Koşullu Erişim](#conditional-access) gereksinimlerini inceleyin.


#### <a name="3-app-integrates-adal-but-does-not-support-brokered-authenticationdevice-wide-sso"></a>3. uygulama ADAL ile tümleşir, ancak aracılı kimlik doğrulaması/cihaz genelinde SSO 'yu desteklemez

|Gerekli ADAL parametresi| Değer |
|--|--|
| ClientID | Uygulamanın İstemci Kimliği (uygulama kaydedilirken Azure AD tarafından oluşturulur) |
| SkipBroker | **True** |

Gerekirse Yetkili ve NonBrokerRedirectURI belirtilebilir.


### <a name="conditional-access"></a>Koşullu Erişim
Koşullu Erişim (CA), AAD kaynaklarına erişimi denetlemek için kullanılabilen bir Azure Active Directory [özelliğidir](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer). Intune yöneticileri yalnızca Intune tarafından yönetilen cihazlar veya uygulamalardan kaynak erişimine izin veren [CA kurallarını tanımlayabilir](../protect/conditional-access.md). Uygulamanızın uygun olduğunda kaynaklara erişebildiğinden emin olmak için aşağıdaki adımları izlemeniz gerekir. Uygulamanız herhangi bir AAD erişim belirteci gerektirmiyorsa veya yalnızca CA ile korunamayan kaynaklara erişiyorsa bu adımları atlayabilirsiniz.

1. [ADAL tümleştirme yönergelerini](https://github.com/AzureAD/azure-activedirectory-library-for-android#how-to-use-this-library) izleyin. 
   Aracı kullanımı için özellikle 11. Adıma bakın.
2. [Uygulamanızı Azure Active Directory ile kaydedin](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration). 
   Yeniden yönlendirme URI’si, yukarıdaki ADAL tümleştirme kılavuzlarında bulunabilir.
3. Yukarıda [Yaygın ADAL yapılandırmaları](#common-adal-configurations), öğe 2 için bildirim meta veri parametrelerini ayarlayın.
4. [Azure portalından](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExchangeConnectorMenu/aad/connectorType/2)[cihaz tabanlı CA](../protect/conditional-access-intune-common-ways-use.md)’yı etkinleştirerek her şeyin doğru yapılandırıldığını sınayıp doğrulayın
    - Uygulamanızda oturum açmak için Intune Şirket Portalı’nı yüklemeniz ve buraya kaydolmanız istenir
    - Kayıttan sonra uygulamanızda oturum açma başarıyla tamamlanır.
5. Uygulamanız Intune uygulama SDK 'Sı tümleştirmesini gönderdikten sonra, msintuneappsdk@microsoft.com [uygulama tabanlı koşullu erişim](https://docs.microsoft.com/intune/conditional-access-intune-common-ways-use#app-based-conditional-access) için onaylanan uygulamalar listesine eklenecek kişi
6. Uygulamanız onaylananlar listesine eklendikten sonra, [Uygulama tabanlı CA’yı yapılandırarak](../protect/app-based-conditional-access-intune-create.md) doğrulayın ve uygulamanıza oturum açmanın başarıyla tamamlandığından emin olun.

## <a name="app-protection-policy-without-device-enrollment"></a>Cihaz kaydı olmadan uygulama koruma ilkesi

### <a name="overview"></a>Genel bakış
Cihaz kaydı olmadan Intune uygulama koruma ilkesi (APP-WE veya MAM-WE olarak da bilinir), uygulamaların Intune MDM’ye kaydedilmeden Intune tarafından yönetilmesine izin verir. APP-WE, hem cihaz kaydıyla hem de cihaz kaydı olmadan çalışır. Şirket Portalı’nın yine cihaza yüklenmiş olması gerekir, ancak kullanıcının Şirket Portalı’nda oturum açması ve cihazı kaydetmesi gerekmez.

> [!NOTE]
> Tüm uygulamaların cihaz kaydı olmadan uygulama koruma ilkesini desteklemesi gerekir.

### <a name="workflow"></a>İş akışı

Uygulama yeni bir kullanıcı hesabı oluşturduğunda, hesabı Intune Uygulama SDK’sıyla yönetim için kaydetmelidir. Uygulamayı APP-WE hizmetine kaydetme işleminin ayrıntılarını SDK gerçekleştirir; hatalar olması durumunda gerekirse tüm kayıtları uygun aralıklarla yeniden dener.

Uygulama ayrıca, kayıtlı bir kullanıcının durumunu Intune Uygulama SDK’sında sorgulayıp kullanıcının şirket içeriğine erişimini engellemenin gerekip gerekmediğini de saptayabilir. Yönetim için birden çok hesap kaydedilebilir, ancak şu anda APP-WE hizmetiyle bir kerede tek bir hesap etkin olarak kaydedilebilmektedir. Bu da, bir kerede tek bir hesabın uygulama koruma ilkesini alabildiği anlamına gelir.

Uygulamanın, SDK adına Azure Active Directory Authentication Library’den (ADAL) uygun erişim belirtecini almak için bir geri çağırma sağlaması gerekir. Uygulamanın kimlik doğrulaması yapmak ve kendi erişim belirteçlerini almak için zaten ADAL kullandığı varsayılır.

Uygulama bir hesabı tamamen kaldırdığında, uygulamanın söz konusu kullanıcı için artık ilke uygulamayacağını belirtmek üzere o hesabın kaydını kaldırmalıdır. Kullanıcı MAM hizmetine kaydedilmişse, kullanıcının kaydı kaldırılır ve uygulama temizlenir.


### <a name="overview-of-app-requirements"></a>Uygulama gereksinimlerine genel bakış

APP-WE tümleştirmesini gerçekleştirmek için, uygulamanız kullanıcı hesabını MAM SDK ile kaydetmelidir:

1. Uygulamanın, bir `MAMServiceAuthenticationCallback` arabirimi örneğini gerçekleştirmesi ve kaydetmesi _gerekir_. Geri çağırma örneği, uygulamanın yaşam döngüsünde mümkün olduğunca erken bir aşamada kaydedilmelidir (normalde uygulama sınıfının `onMAMCreate()` yönteminde).

2. Kullanıcı hesabı oluşturulduğunda ve kullanıcı başarıyla ADAL oturumu açtığında, uygulama `registerAccountForMAM()` çağrısı _yapmalıdır_.

3. Kullanıcı hesabı kaldırıldığında, uygulamanın hesabı Intune yönetiminden kaldırmak için `unregisterAccountForMAM()` çağrısı yapması gerekir.

    > [!NOTE]
    > Kullanıcı uygulama oturumunu geçici olarak kapattıysa, uygulamanın `unregisterAccountForMAM()` çağrısı yapması gerekmez. Çağrı, kullanıcıdan şirket verilerini tümüyle kaldırmak için bir temizleme başlatabilir.


### <a name="mamenrollmentmanager"></a>MAMEnrollmentManager

Tüm gerekli kimlik doğrulama ve kayıt API’leri `MAMEnrollmentManager` arabiriminde bulunabilir. Bir `MAMEnrollmentManager` başvurusu şu şekilde alınabilir:

```java
MAMEnrollmentManager mgr = MAMComponents.get(MAMEnrollmentManager.class);

// make use of mgr
```

Döndürülen `MAMEnrollmentManager` örneğinin null olmaması garanti edilir. API yöntemleri iki kategoriye ayrılır: **kimlik doğrulaması** ve **hesap kaydı**.

```java
package com.microsoft.intune.mam.policy;

public interface MAMEnrollmentManager {
    public enum Result {
        AUTHORIZATION_NEEDED,
        NOT_LICENSED,
        ENROLLMENT_SUCCEEDED,
        ENROLLMENT_FAILED,
        WRONG_USER,
        MDM_ENROLLED,
        UNENROLLMENT_SUCCEEDED,
        UNENROLLMENT_FAILED,
        PENDING,
        COMPANY_PORTAL_REQUIRED;
    }

    //Authentication methods
    interface MAMServiceAuthenticationCallback {
        String acquireToken(String upn, String aadId, String resourceId);
    }
    void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
    void updateToken(String upn, String aadId, String resourceId, String token);

    //Registration methods
    void registerAccountForMAM(String upn, String aadId, String tenantId);
    void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
    void unregisterAccountForMAM(String upn);
    Result getRegisteredAccountStatus(String upn);
}
```

### <a name="account-authentication"></a>Hesap kimlik doğrulaması

Bu bölümde, `MAMEnrollmentManager` içindeki kimlik doğrulama API yöntemleri ve bunların nasıl kullanıldığı açıklanır.

```java
interface MAMServiceAuthenticationCallback {
    String acquireToken(String upn, String aadId, String resourceId);
}
void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
void updateToken(String upn, String aadId, String resourceId, String token);
```

1. SDK’nın verili kullanıcı ve kaynak kimliği için ADAL isteğinde bulunmasına olanak tanımak üzere uygulama `MAMServiceAuthenticationCallback` gerçekleştirmelidir. `registerAuthenticationCallback()` yöntemi çağrılarak `MAMEnrollmentManager` için geri çağırma örneği sağlanmalıdır. Kayıt yeniden denemeleri ve uygulama koruma ilkesi yenileme iadeleri için uygulama yaşam döngüsünün erken bir aşamasında belirteç gerekebilir; dolayısıyla geri çağırma kaydı için ideal konum, uygulamanın `MAMApplication` alt sınıfının `onMAMCreate()` yöntemidir.

2. `acquireToken()` yöntemi, verili kullanıcının istenen kaynak kimliği için erişim belirtecini almalıdır. İstenen belirteci almazsa, null değeri döndürmelidir.

    > [!NOTE]
    > `resourceId`Doğru belirtecin alınması için uygulamanızın geçirilen ve parametrelerini kullandığından emin olun `aadId` `acquireToken()` .

    ```java
    class MAMAuthCallback implements MAMServiceAuthenticationCallback {
        public String acquireToken(String upn, String aadId, String resourceId) {
            return mAuthContext.acquireTokenSilentSync(resourceId, ClientID, aadId).getAccessToken();
        }
    }
    ```

3. SDK `acquireToken()` çağrısı yaptığında uygulamanın belirteci sağlayamaması durumunda (örneğin, sessiz kimlik doğrulaması başarısız olursa ve UI göstermek için uygun bir zaman değilse), uygulama daha sonraki bir aşamada `updateToken()` yöntemini çağırarak belirteci sağlayabilir. `updateToken()` çağrısına, önceki `acquireToken()` çağrısında istenen aynı UPN, AAD ID ve kaynak kimliğinin yanı sıra sonunda alınan belirteç de geçirilmelidir. Uygulamanın, sağlanan geri çağırmadan null döndürüldükten sonra, mümkün olan en kısa sürede bu yöntemi çağırması gerekir.

    > [!NOTE]
    > SDK, belirteci almak için düzenli aralıklarla `acquireToken()` yöntemini çağırır; dolayısıyla `updateToken()` çağrısı yapmak kesin olarak gerekli değildir. Ancak, kayıtların ve uygulama koruma ilkesi iadelerinin zamanında tamamlanmasını sağlamak için kesinlikle önerilir.


### <a name="account-registration"></a>Hesap Kaydı

Bu bölümde, `MAMEnrollmentManager` içindeki hesap kaydı API yöntemleri ve bunların nasıl kullanıldığı açıklanır.

```java
void registerAccountForMAM(String upn, String aadId, String tenantId);
void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
void unregisterAccountForMAM(String upn);
Result getRegisteredAccountStatus(String upn);
```

1. Hesabı yönetime kaydetmek için, uygulamanın `registerAccountForMAM()` yöntemini çağırması gerekir. Kullanıcı hesabı hem UPN değeriyle hem de AAD kullanıcı kimliğiyle tanımlanır. Kayıt verilerini kullanıcının AAD kiracısıyla ilişkilendirmek için kiracı kimliği de gereklidir. Kullanıcının yetkisi, belirli bir bağımsız bulutlara karşı kayda izin vermek için de sağlanmış olabilir; daha fazla bilgi için bkz. [Sovereign bulutu kaydı](#sovereign-cloud-registration).  SDK, verili kullanıcı için MAM hizmetinde uygulamayı kaydetme girişiminde bulunabilir; kayıt başarısız olursa, hesabın kaydı kaldırılana kadar kaydetme işlemini düzenli aralıklarla yeniden dener. Yeniden denemeler normalde 12-24 saatte bir yapılır. SDK, bildirimler yoluyla kayıt girişimlerinin durumunu zaman uyumsuz olarak sağlar.

2. AAD kimlik doğrulaması gerekli olduğundan, kullanıcı hesabını kaydetmek için en uygun zaman, kullanıcının uygulamada oturum açmasından ve ADAL kullanarak başarıyla kimliğini doğrulamasından sonraki bir zamandır. Kullanıcının AAD KIMLIĞI ve kiracı KIMLIĞI, ADAL kimlik doğrulama çağrısından nesnenin bir parçası olarak döndürülür [`AuthenticationResult`](https://github.com/AzureAD/azure-activedirectory-library-for-android) .
    * Kiracı kimliği `AuthenticationResult.getTenantID()` yönteminden gelir.
    * Kullanıcı hakkındaki bilgiler `AuthenticationResult.getUserInfo()` çağrısından gelen `UserInfo` türündeki bir alt nesnede bulunur ve AAD kullanıcı kimliği `UserInfo.getUserId()` çağrısı yapılarak o nesneden alınır.

3. Intune yönetiminden bir hesabın kaydını kaldırmak için, uygulamanın `unregisterAccountForMAM()` yöntemini çağırması gerekir. Hesap başarıyla kaydedilmiş ve yönetilmişse, SDK hesabın kaydını kaldırır ve verilerini temizler. Hesap için düzenli aralıklarla yapılan kayıt yeniden denemeleri durdurulur. SDK, bildirim aracılığıyla kayıt kaldırma isteğinin durumunu zaman uyumsuz olarak sağlar.

### <a name="sovereign-cloud-registration"></a>Bağımsız Bulut Kaydı

[Bağımsız bulut kullanan uygulamalar, `authority` öğesini `registerAccountForMAM()` öğesine ](https://www.microsoft.com/trustcenter/cloudservices/nationalcloud) **sağlamalıdır**.  Bu ADAL'ın [1.14.0+](https://github.com/AzureAD/azure-activedirectory-library-for-android/releases/tag/v1.14.0) acquireToken extraQueryParameters içinde `instance_aware=true` sağlayıp AuthenticationCallback AuthenticationResult üzerinde `getAuthority()` çağrılarak alınabilir.

```java
mAuthContext.acquireToken(this, RESOURCE_ID, CLIENT_ID, REDIRECT_URI, PromptBehavior.FORCE_PROMPT, "instance_aware=true",
        new AuthenticationCallback<AuthenticationResult>() {
            @Override
            public void onError(final Exception exc) {
                // authentication failed
            }

            @Override
            public void onSuccess(final AuthenticationResult result) {
                mAuthority = result.getAuthority();
                // handle other parts of the result
            }
        });
```

> [!NOTE]
> `com.microsoft.intune.mam.aad.Authority`AndroidManifest.xml meta veri öğesini ayarlamayın.

> [!NOTE]
> `MAMServiceAuthenticationCallback::acquireToken()` yönteminizde yetkilinin doğru ayarlandığından emin olun.

#### <a name="currently-supported-sovereign-clouds"></a>Şu Anda Desteklenen Bağımsız Bulutlar

1. Azure ABD kamu bulutu
2. 21Vianet tarafından işletilen Microsoft Azure (Azure Çin)


### <a name="important-implementation-notes"></a>Önemli uygulama notları

#### <a name="authentication"></a>Kimlik Doğrulaması

* Uygulama `registerAccountForMAM()` çağrısı yaptığında, bundan kısa süre sonra farklı bir iş parçacığında `MAMServiceAuthenticationCallback` arabiriminde bir geri çağırma alabilir. İdeal olarak, uygulama, istenen belirtecin alımını hızlandırmak için hesabı kaydetmeden önce ADAL 'dan kendi belirtecini almış. Uygulama geri aramadan geçerli bir belirteç döndürürse, kayıt devam eder ve uygulama bir bildirim aracılığıyla nihai sonucu alır.

* Uygulama geçerli bir AAD belirteci döndürmezse, kayıt girişiminin nihai sonucu `AUTHORIZATION_NEEDED` olur. Uygulama bu sonucu bildirim aracılığıyla alırsa, daha önceden istenen kullanıcı ve kaynak için belirteci alarak kayıt işlemini hızlandırmak `acquireToken()` ve `updateToken()` kayıt işlemini yeniden başlatmak için yöntemi çağırmak önemle önerilir.

* Uygulama kaydı, `MAMServiceAuthenticationCallback` düzenli uygulama koruma ilkesi yenileme iadelerinin bir belirtecini almak için de çağrılır. Uygulama istendiğinde bir belirteç sağlayamadığında bildirim almaz, ancak `updateToken()` iade sürecini hızlandırmak için bir sonraki uygun zamanda bir belirteç edinmeyi ve çağırmayı denemelidir. Belirteç sağlanmazsa, geri çağırma bir sonraki iade girişiminde yine de çağrılır.

* Bağımsız bulutlar için destek, yetkilinin sağlanmasını gerektirir.

#### <a name="registration"></a>Kayıt

* Size kolaylık sağlamak açısından, kayıt yöntemleri eşgüçlüdür; örneğin, `registerAccountForMAM()` yöntemi yalnızca bir hesabı kaydeder ve hesap henüz kaydedilmediyse uygulama kaydı yapmayı dener ve `unregisterAccountForMAM()` yöntemi de şu anda kaydedilmiş durumdaysa hesabın kaydını kaldırır. Birbirini izleyen çağrılar çalışmaz; dolayısıyla bu yöntemlerin birden çok kez çağrılmasının bir zararı olmaz. Buna ek olarak, bu yöntemlere yapılan çağrılar arasındaki iletişim ve sonuç bildirimleri garanti edilmez: şöyle ki, zaten kayıtlı olan bir kimlik için `registerAccountForMAM()` çağrılırsa, söz konusu kimlik için yeniden bildirim gönderilmeyebilir. SDK arka planda kayıtları düzenli aralıklarla deneyebildiğinden ve Intune hizmetinden alınan silme isteklerinin tetiklediği kayıt kaldırma işlemleri olabildiğinden, bu yöntemlere yapılan çağrılardan hiçbirine karşılık gelmeyen bildirimlerin gönderilmesi de mümkündür.

* Kayıt yöntemleri istenen sayıda farklı kimlik için çağrılabilir, ama şu anda yalnızca bir kullanıcı hesabı başarılı bir şekilde kaydedilebilir. Intune lisansı olan ve uygulama koruma ilkesi tarafından hedeflenen birden çok kullanıcı hesabı aynı anda veya birbirine çok yakın zamanda kaydedilirse, yarışı hangisinin kazanacağı konusunda bir garanti verilemez.

* Son olarak, belirli bir hesabın kaydedilip kaydedilmediğini görmek ve geçerli durumunu almak için `getRegisteredAccountStatus()` yöntemini kullanarak `MAMEnrollmentManager`‘ı sorgulayabilirsiniz. Sağlanan hesap kaydedilmediyse, bu yöntem **null** döndürür. Hesap kayıtlıysa, bu yöntem `MAMEnrollmentManager.Result` sabit listesinin üyelerinden biri olarak hesabın durumunu döndürür.

### <a name="result-and-status-codes"></a>Sonuç ve durum kodları

Hesap ilk kez kaydedildiğinde, `PENDING` durumunda başlar. Bu, ilk MAM hizmeti kayıt girişiminin tamamlanmadığı anlamına gelir. Kayıt girişimi tamamlandığında, aşağıdaki tabloda yer alan Dönüş kodlarından biriyle bir bildirim gönderilir. Buna ek olarak, `getRegisteredAccountStatus()` yöntemi hesabın durumunu döndürür ve böylelikle uygulama, söz konusu kullanıcı için kurumsal içeriğe erişimin engellenip engellenmediğini her zaman saptayabilir. Kayıt girişimi başarısız olursa, SDK arka planda kaydı yeniden denediğinden hesabın durumu zaman içinde değişebilir.

|Sonuç kodu | Açıklama |
| -- | -- |
| `AUTHORIZATION_NEEDED` | Bu sonuç, bir belirtecin uygulamanın kayıtlı örneği tarafından sağlandığını `MAMServiceAuthenticationCallback` veya belirtilen belirtecin geçersiz olduğunu gösterir.  Uygulama mümkünse geçerli bir belirteç almalı ve `updateToken()` yöntemini çağırmalıdır. |
| `NOT_LICENSED` | Kullanıcı Intune’da lisanslı değildir veya Intune MAM hizmetiyle iletişim kurma girişimi başarısız olmuştur.  Uygulamanın yönetilmeyen (normal) durumda çalışmaya devam etmesi ve kullanıcının engellenmemesi gerekir.  Kullanıcının gelecekte lisanslı duruma gelme olasılığına karşı, kayıt işlemleri düzenli aralıklarla yeniden denenecektir. |
| `ENROLLMENT_SUCCEEDED` | Kayıt girişimi başarılı olmuştur ve kullanıcı kaydedilmiştir.  Başarılı bir kayıt söz konusu olduğunda, bu bildirimden önce ilke yenileme bildirimi gönderilir.  Kurumsal verilere erişim izni verilmelidir. |
| `ENROLLMENT_FAILED` | Kayıt girişimi başarısız olmuştur.  Diğer ayrıntılar, cihaz günlüklerinde bulunabilir.  Daha önce kullanıcının Intune için lisanslı olduğunu belirlediğinden, uygulamanın bu durumda kurumsal verilere erişim izni olmaması gerekir.|
| `WRONG_USER` | Cihaz başına yalnızca bir kullanıcı MAM hizmetiyle uygulamayı kaydedebilir. Bu sonuç, bu sonucun teslim edildiği kullanıcının (ikinci Kullanıcı) MAM ilkesi ile hedeflendiğini, ancak farklı bir kullanıcının zaten kayıtlı olduğunu gösterir. İkinci Kullanıcı için MAM ilkesi zorlanamadığından, bu kullanıcı için kayıt kaydı daha sonra başarılı olmadığı sürece uygulamanız bu kullanıcının verilerine erişime izin vermelidir (muhtemelen Kullanıcı uygulamanızdan kaldırılır). Bu sonucu sunmaya eşzamanlı `WRONG_USER` olarak, mam var olan hesabı kaldırma seçeneğiyle istemde yer alacak. İnsan kullanıcısı bir süre içinde yanıt verdiği zaman, ikinci kullanıcıyı kısa bir süre sonra kaydetmek mümkün olacaktır. İkinci Kullanıcı kayıtlı kaldığı sürece, MAM kaydı düzenli aralıklarla yeniden dener. |
| `UNENROLLMENT_SUCCEEDED` | Kaydın kaldırılması başarılı olmuştur.|
| `UNENROLLMENT_FAILED` | Kayıt kaldırma isteği başarısız olmuştur.  Diğer ayrıntılar, cihaz günlüklerinde bulunabilir. Genel olarak, uygulama geçerli bir (null ya da boş) UPN 'yi geçirmiş olduğu sürece bu durum oluşmaz. Uygulamanın gidebilmesine yönelik doğrudan, güvenilir bir düzeltme yoktur. Bu değer geçerli bir UPN kaydı silinirken alınmışsa, lütfen Intune MAM ekibine hata olarak bildirin.|
| `PENDING` | Kullanıcı için ilk kayıt denemesi devam etmektedir.  Kayıt sonucu bilinir duruma gelene kadar uygulama kurumsal verilere erişimi engelleyebilir ama bunu yapması zorunlu değildir. |
| `COMPANY_PORTAL_REQUIRED` | Kullanıcının Intune lisansı vardır ama cihaza Şirket Portalı uygulaması yüklenene kadar uygulama kaydedilemez. Intune Uygulama SDK’sı verili kullanıcı için uygulamaya erişimi engellemeyi dener ve kullanıcıyı Şirket Portalı uygulamasını yüklemeye yönlendirir (ayrıntılar için aşağıya bakın). |


### <a name="company-portal-requirement-prompt-override-optional"></a>Şirket Portalı gereksinimi istemini geçersiz kılma (isteğe bağlı)

`COMPANY_PORTAL_REQUIRED` Sonucu alınırsa, SDK kendisi için kayıt istenen kimliğin kullanıldığı etkinliklerin kullanımını engeller. Bunun yerine, SDK bu etkinliklerin Şirket Portalı’nı indirme istemi görüntülemesine neden olur. Uygulamanızda bu davranışı engellemek istiyorsanız, etkinlikler `MAMActivity.onMAMCompanyPortalRequired` gerçekleştirebilir.

Bu yöntem, SDK varsayılan engelleme UI’sini görüntülemeden önce çağrılır. Uygulama etkinlik kimliğini değiştirirse veya kaydolmaya çalışan kullanıcının kaydını kaldırırsa, SDK etkinliği engellemez. Bu durumda, kurumsal verilerin sızdırılmasını önlemek uygulamanın tercihine bağlı olur. Yalnızca çok kimlikli uygulamalar (sonraki bölümlerde ele alınacaktır) etkinlik kimliğini değiştirebilir.

`MAMActivity` sınıfını (derleme araçları bu değişikliği yapacağı için) açık olarak devralmıyorsanız, ancak yine de bu bildirimi işlemeniz gerekiyorsa, bunun yerine `MAMActivityBlockingListener` sınıfını uygulayabilirsiniz.

### <a name="notifications"></a>Bildirimler

Uygulama **MAM_ENROLLMENT_RESULT**tür bildirimleri için kaydolduğunda, `MAMEnrollmentNotification` uygulamayı kayıt isteğinin tamamlandığını bilgilendirmek için bir gönderilir. `MAMEnrollmentNotification`, [SDK’dan gelen bildirimlere kaydolma](#register-for-notifications-from-the-sdk) bölümünde açıklandığı gibi `MAMNotificationReceiver` arabirimi üzerinden alınır.

```java
public interface MAMEnrollmentNotification extends MAMUserNotification {
    MAMEnrollmentManager.Result getEnrollmentResult();
}
```

`getEnrollmentResult()` yöntemi, kayıt isteğinin sonucunu döndürür.  `MAMEnrollmentNotification``MAMUserNotification`‘ın kapsamını genişlettiğinden, kayıt girişiminde bulunulan kullanıcının kimliği de sağlanır. Uygulama, [SDK’dan gelen bildirimlere kaydolma](#register-for-notifications-from-the-sdk) bölümünde ayrıntılarıyla açıklandığı gibi, bu bildirimleri almak için `MAMNotificationReceiver` arabirimini gerçekleştirmelidir.

Kayıtlı Kullanıcı hesabının durumu bir kayıt bildirimi alındığında değişebilir, ancak her durumda değişmeyecektir (örneğin, bildirim, gibi `AUTHORIZATION_NEEDED` daha bilgilendirici bir sonuçtan sonra alınmışsa `WRONG_USER` , hesabın durumu olarak daha bilgilendirici sonuç olur).  Hesap başarıyla kaydedildikten sonra, `ENROLLMENT_SUCCEEDED` hesabın kaydı geri alınana veya temizlenmeden sonra durum olarak kalır.


## <a name="app-ca-with-policy-assurance"></a>Ilke güvencesi olan uygulama CA 'sı

### <a name="overview"></a>Genel bakış
Ilke güvencesi ile uygulama CA 'sı (koşullu erişim) ile, kaynaklara erişim Intune Uygulama Koruması Ilkelerinin uygulama üzerinde koşullanar.  AAD, Ilke güvencesi korumalı kaynağı ile bir uygulama CA 'sına bir belirteç vermeden önce uygulamanın uygulama tarafından kaydedilmesini ve yönetilmesini zorunlu kılarak bunu zorunlu kılar.  Uygulamanın, belirteç alımı için ADAL Aracısı 'nı kullanması gerekir ve kurulum yukarıda [koşullu erişim](#conditional-access)bölümünde açıklananla aynıdır.

### <a name="adal-changes"></a>ADAL değişiklikleri
ADAL kitaplığı, uygulamayı bir belirteç alma hatasının uygulama yönetimiyle uyumsuz olduğunu bildiren yeni bir hata koduna sahiptir.  Uygulama bu hata kodunu alırsa, uygulamayı kaydederek ve ilkeyi uygulayarak uyumluluğu düzeltmeye çalışmak için SDK 'Yı çağırmalıdır. ADAL yöntemi tarafından bir özel durum alınır `onError()` `AuthenticationCallback` ve hata kodu olacaktır `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED` .  Bu durumda, özel durum, uyumluluk düzeltme aşamasında `IntuneAppProtectionPolicyRequiredException` kullanılmak üzere başka parametrelerin ayıklanabileceği bir öğesine dönüşebilir (Aşağıdaki kod örneğine bakın). Düzeltme başarılı olduktan sonra, uygulama ADAL üzerinden belirteç alımı yeniden deneyebilir.

> [!NOTE]
> Bu yeni hata kodu ve Ilke güvencesi içeren uygulama CA 'sı için diğer destek, ADAL kitaplığı 'nın sürüm 1.15.0 (veya üstü) gerektirir.

### <a name="mamcompliancemanager"></a>Mamkarmaşıancemanager

`MAMComplianceManager`Arabirim, adal 'dan ilke gerekli hatası alındığında kullanılır.  `remediateCompliance()`Uygulamayı uyumlu duruma koymaya çalışmak için çağrılması gereken yöntemi içerir. Bir `MAMComplianceManager` başvurusu şu şekilde alınabilir:

```java
MAMComplianceManager mgr = MAMComponents.get(MAMComplianceManager.class);

// make use of mgr
```

Döndürülen `MAMComplianceManager` örneğinin null olmaması garanti edilir.

```java
package com.microsoft.intune.mam.policy;

public interface MAMComplianceManager {
    void remediateCompliance(String upn, String aadId, String tenantId, String authority, boolean showUX);
}
```

`remediateCompliance()`Yöntemi, istenen belirteci vermek IÇIN AAD 'nin koşullarını karşılamak üzere uygulamayı yönetim altına koymaya çalışmak üzere çağırılır.  İlk dört parametre ADAL yöntemi tarafından alınan özel durumdan ayıklanabilir `AuthenticationCallback.onError()` (Aşağıdaki kod örneğine bakın).  Son parametre, uyumluluk girişimi sırasında bir UX gösterilip gösterilmeyeceğini denetleyen bir Boole değeri.  Bu işlem sırasında özelleştirilmiş UX gösterme gereksinimi olmayan uygulamalar için varsayılan olarak sunulan basit bir engelleme ilerleme stil arabirimidir.  Yalnızca uyumluluk düzeltmesi devam ederken engellenecek ve nihai sonucu göstermeyecektir.  Uygulama, uyumluluk düzeltme girişiminin başarısını veya başarısızlığını işlemek için bir bildirim alıcısı kaydetmelidir (aşağıya bakın).

`remediateCompliance()`Yöntemi, uyumluluk oluşturma kapsamında BIR mam kaydı olabilir.  Uygulama, kayıt bildirimleri için bir bildirim alıcısı kaydettirirse bir kayıt bildirimi alabilir.  Uygulamanın kayıtlı yöntemi, `MAMServiceAuthenticationCallback` `acquireToken()` mam kaydı için bir belirteç almak üzere çağırılır. `acquireToken()` uygulama kendi belirtecini elde etmeden önce çağrılacaktır, bu nedenle uygulamanın başarılı bir belirteç alımı sonrasında kullandığı tüm muhasebe veya hesap oluşturma görevleri henüz yapılmamış olabilir.  Geri çağırma bu durumda bir belirteç elde edebilmelidir.  Öğesinden bir belirteç döndüremiyorum `acquireToken()` , uyumluluk düzeltme girişimi başarısız olur.  `updateToken()`İstenen kaynak için daha sonra geçerli bir belirteçle çağrı yaparsanız, uyumluluk düzeltmesi verilen belirteçle hemen yeniden denenir.

> [!NOTE]
> `acquireToken()`Kullanıcı aracıyı yüklemek ve hata alınmadan önce cihazı kaydetmek için zaten Kılavuzlu için sessiz belirteç alma işlemi yine de mümkün olacaktır `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED` .  Bu, aracıda, istenen belirtecin sessiz Alım işleminin başarılı olmasına izin veren, önbelleğinde geçerli bir yenileme belirteci olmasına neden olur.

İlke için gerekli hata alma örneği `AuthenticationCallback.onError()` ve `MAMComplianceManager` hatayı işlemek için çağrısı aşağıda verilmiştir.

```java
public void onError(@Nullable Exception exc) {
    if (exc instanceof AuthenticationException && 
        ((AuthenticationException) exc).getCode() == ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED) {

        final IntuneAppProtectionPolicyRequiredException policyRequiredException = 
            (IntuneAppProtectionPolicyRequiredException) ex;

        final String upn = policyRequiredException.getAccountUpn();
        final String aadId = policyRequiredException.getAccountUserId();
        final String tenantId = policyRequiredException.getTenantId();
        final String authority = policyRequiredException.getAuthorityURL();

        MAMComplianceManager complianceManager = MAMComponents.get(MAMComplianceManager.class);
        complianceManager.remediateCompliance(upn, aadId, tenantId, authority, showUX);
    }
}
```

### <a name="status-notifications"></a>Durum bildirimleri

Uygulama **COMPLIANCE_STATUS**tür bildirimleri için kaydolduktan sonra, `MAMComplianceNotification` uygulamayı uyumluluk düzeltme denemesinin son durumuna bildirmek için bir gönderilir. `MAMComplianceNotification`, [SDK’dan gelen bildirimlere kaydolma](#register-for-notifications-from-the-sdk) bölümünde açıklandığı gibi `MAMNotificationReceiver` arabirimi üzerinden alınır.

```java
public interface MAMComplianceNotification extends MAMUserNotification {
    MAMCAComplianceStatus getComplianceStatus();
    String getComplianceErrorTitle();
    String getComplianceErrorMessage();
}
```

`getComplianceStatus()`Yöntemi, uyumluluk düzeltme denemesinin sonucunu, numaralandırıcıdan bir değer olarak döndürür `MAMCAComplianceStatus` .

|Durum kodu | Açıklama |
| -- | -- |
| BILINMEYEN | Durum bilinmiyor. Bu, beklenmeyen bir hata nedenini gösterebilir. Şirket Portalı günlüklerinde ek bilgiler bulunabilir. |
| Uyumluluk | Uyumluluk düzeltmesi başarılı oldu ve uygulama artık ilkeyle uyumlu. ADAL belirteci alımı yeniden denenmelidir. |
| NOT_COMPLIANT | Uyumluluğun düzeltilmesi girişimi başarısız oldu.  Uygulama uyumlu değil ve ADAL belirteci alma, hata koşulu düzeltilene kadar yeniden denenmemelidir.  Ek hata bilgileri MAMComplianceNotification ile gönderilir. |
| SERVICE_FAILURE | Intune hizmetinden uyumluluk verileri alınmaya çalışılırken bir hata oluştu. Şirket Portalı günlüklerinde ek bilgiler bulunabilir. |
| NETWORK_FAILURE | Intune hizmetine bağlanılırken bir hata oluştu. Uygulama, ağ bağlantısı geri yüklendiğinde belirteç alımı ' nı yeniden denemelidir. |
| CLIENT_ERROR | İstemciyle ilgili bazı nedenlerle uyumluluğu düzeltme girişimi başarısız oldu.  Örneğin, belirteç yok veya yanlış Kullanıcı. Ek hata bilgileri MAMComplianceNotification ile gönderilir. |
| PENDING | Durum yanıtı, zaman sınırı aşıldığında hizmetten henüz alınmadığı için uyumluluğu düzeltme girişimi başarısız oldu. Uygulama, belirteç alımı daha sonra tekrar denemelidir. |
| COMPANY_PORTAL_REQUIRED | Uyumluluk düzeltmesinin başarılı olabilmesi için Şirket Portalı cihazda yüklü olmalıdır.  Şirket Portalı cihazda zaten yüklüyse, uygulamanın yeniden başlatılması gerekir.  Bu durumda, kullanıcıdan uygulamayı yeniden başlatmasını isteyen bir iletişim kutusu gösterilir. |

Uyumluluk durumu ise `MAMCAComplianceStatus.COMPLIANT` , uygulamanın özgün belirteç alma işlemini (kendi kaynağı için) yeniden başlatması gerekir. Uyumluluk Düzeltme girişimi başarısız olursa, `getComplianceErrorTitle()` ve `getComplianceErrorMessage()` yöntemleri uygulamanın seçtiği son kullanıcıya görüntüleyeceği yerelleştirilmiş dizeleri döndürür.  Çoğu hata durumu uygulama tarafından etkilenmez, bu nedenle genel durumda hesap oluşturma veya oturum açma işlemi başarısız olabilir ve kullanıcının daha sonra tekrar denemesini sağlayabilirsiniz.  Bir hata kalıcısa, MAM günlükleri sorunun belirlenmesine yardımcı olabilir.  Son Kullanıcı günlükleri gönderebilir. Daha fazla bilgi için bkz. [yükleme ve e-posta günlükleri](../user-help/send-logs-to-your-it-admin-by-email-android.md).

`MAMComplianceNotification`Genişlettiğinden `MAMUserNotification` , düzeltmenin denendiği kullanıcının kimliği de kullanılabilir.

Bu, Mamnotificationahize arabirimini uygulamak için anonim sınıf kullanarak bir alıcıyı kaydetmenin bir örneğidir:

```java
final MAMNotificationReceiverRegistry notificationRegistry = MAMComponents.get(MAMNotificationReceiverRegistry.class);
// create a receiver
final MAMNotificationReceiver receiver = new MAMNotificationReceiver() {
    public boolean onReceive(MAMNotification notification) {
        if (notification.getType() == MAMNotificationType.COMPLIANCE_STATUS) {
            MAMComplianceNotification complianceNotification = (MAMComplianceNotification) notification;
            
            // take appropriate action based on complianceNotification.getComplianceStatus()
            
            // unregister this receiver if no longer needed
            notificationRegistry.unregisterReceiver(this, MAMNotificationType.COMPLIANCE_STATUS);
        }
        return true;
    }
};
// register the receiver
notificationRegistry.registerReceiver(receiver, MAMNotificationType.COMPLIANCE_STATUS);
```

> [!NOTE]
> Bildirimin `remediateCompliance()` kaçırılması ile sonuçlanmasına neden olabilecek bir yarış durumundan kaçınmak için çağrılmadan önce bildirim alıcısı kaydedilmelidir.

### <a name="implementation-notes"></a>Uygulama notları

> [!NOTE]
> **Önemli değişiklik!**  <br>
> Uygulamanın `MAMServiceAuthenticationCallback.acquireToken()` yöntemi, yeni bayrağı için *yanlış* geçmelidir `forceRefresh` `acquireTokenSilentSync()` .
> Daha önce, aracıdan belirteçleri yenileme ile ilgili bir sorunu gidermek için *doğru* geçirilmesi önerilir, ancak bu bayrak *true*olduğunda bazı senaryolarda BELIRTEÇLERI alma engelleyebilen adal ile ilgili bir sorun bulundu.
```java
AuthenticationResult result = acquireTokenSilentSync(resourceId, clientId, userId, /* forceRefresh */ false);
```

> [!NOTE]
> Düzeltme girişimi sırasında özel bir engelleme UX 'i göstermek istiyorsanız, showUX parametresi için *false* olarak geçmelisiniz `remediateCompliance()` . ' İ çağırmadan önce UX 'nizi gösterdiğinizden ve bildirim dinleyicinizi kaydetmeniz gerekir `remediateCompliance()` .  Bu, çok hızlı bir şekilde başarısız olursa bildirimin kaçırıldığı bir yarış durumu önler `remediateCompliance()` .  Örneğin, `onCreate()` `onMAMCreate()` bir etkinlik alt sınıfının or yöntemi, bildirim dinleyicisini kaydetmek ve sonra çağırmak için ideal bir yerdir `remediateCompliance()` .  Parametreleri, `remediateCompliance()` UX veya amaç ek ekstraları olarak geçirilebilir.  Uyumluluk durumu bildirimi alındığında, sonucu görüntüleyebilir veya yalnızca etkinliği tamamaktarabilirsiniz.

> [!NOTE]
> `remediateCompliance()` hesabı kaydeder ve kaydı deneyecektir.  Ana belirteç alındıktan sonra, çağırma `registerAccountForMAM()` gerekli değildir, ancak bunu yapmakla bir sorun yoktur. Diğer taraftan, uygulama, Kullanıcı hesabını kaldırmak için belirtecini ve dileklerini elde kuramazsa, `unregisterAccountForMAM()` hesabı kaldırmak ve arka plan kaydı yeniden denemelerini engellemek için çağrı yapılmalıdır.

## <a name="protecting-backup-data"></a>Yedekleme verilerini koruma

Android Marshmallow (API 23) sürümünden itibaren Android’deki bir uygulama, verileri iki yolla yedekleyebilir. Her bir seçenek uygulamanızda kullanılabilir ve Intune veri korumasının doğru bir şekilde uygulandığından emin olmak için farklı adımlar gerektirir. Doğru veri koruma davranışı için gerekli olan ilgili eylemler için aşağıdaki tabloyu gözden geçirebilirsiniz.  Yedekleme yöntemleri hakkında daha fazla bilgi için bkz. [Android API kılavuzu](https://developer.android.com/guide/topics/data/backup.html).

### <a name="auto-backup-for-apps"></a>Uygulamalar için Otomatik Yedekleme

Android, Android Marshmallow cihazlarındaki uygulamalar için Google Drive’a, uygulamanın hedef API’sinden bağımsız olarak [otomatik tam yedeklemeler](https://developer.android.com/guide/topics/data/autobackup.html) sunmaya başlamıştır. AndroidManifest.xml içinde `android:allowBackup` öğesini açıkça **false** olarak ayarlarsanız, uygulamanız hiçbir zaman Android tarafından yedeklenmek üzere sıraya alınmaz ve "kurumsal" veriler uygulama içinde kalır. Bu durumda, başka bir eylem gerekmez.

Ancak, `android:allowBackup` özniteliği, bildirim dosyasında `android:allowBackup` belirtilmemiş olsa bile varsayılan olarak true olarak ayarlanmıştır. Bu, tüm uygulama verilerinin otomatik olarak Google Drive hesabına yedeklendiği anlamına gelir ve bu da **veri sızıntısı riski** oluşturan bir varsayılan davranıştır. Bu nedenle SDK, veri korumasının uygulandığından emin olmak için aşağıda ana hatlarıyla verilen değişiklikleri gerektirir.  Uygulamanızın Android Marshmallow cihazlarında çalışmasını istiyorsanız, müşteri verilerini düzgün bir şekilde korumak için aşağıdaki yönergeleri izlemek önemlidir.  

Intune, XML’de özel kurallar tanımlama becerisi de dahil olmak üzere Android’in sunduğu tüm [Otomatik Yedekleme özelliklerinden](https://developer.android.com/guide/topics/data/autobackup.html) faydalanmanıza olanak tanır, ancak verilerinizin güvenliğini sağlamak için aşağıdaki adımları uygulamanız gerekir:

1. Uygulamanız kendi özel BackupAgent’ını **kullanmıyorsa**, Intune ilkesi uyumluluğu olan otomatik tam yedeklemelere olanak tanımak için varsayılan MAMBackupAgent’ı kullanın. Uygulama bildirimine aşağıdakileri yerleştirin:

    ```xml
    android:fullBackupOnly="true"
    android:backupAgent="com.microsoft.intune.mam.client.app.backup.MAMDefaultBackupAgent"
    ```
    
2. **[İsteğe bağlı]** İsteğe bağlı bir özel BackupAgent gerçekleştirdiyseniz, MAMBackupAgent veya MAMBackupAgentHelper kullandığınızdan emin olmalısınız. Aşağıdaki bölümlere bakın. Android M ve üzeri sürümlerde kolay yedekleme sağlayan Intune’un **MAMDefaultFullBackupAgent** aracısını (1. adımda açıklanmıştır) kullanmaya geçmeniz önerilir.

3. Uygulamanızın hangi tam yedekleme türünü (filtresiz, filtreli veya hiçbiri) almasını istediğinize karar verdiğinizde, `android:fullBackupContent` özniteliğini true, false veya uygulamanızda bir XML kaynağı olarak ayarlamanız gerekir.

4. Ardından, `android:fullBackupContent` içine yerleştirdiğiniz her şeyi bildirimde `com.microsoft.intune.mam.FullBackupContent` adlı meta veri etiketine kopyalamanız _**gerekir**_.

    **1. Örnek**: Uygulamanızın özel durumlar olmadan tam yedeklemeleri olmasını istiyorsanız, hem `android:fullBackupContent` özniteliğini hem de `com.microsoft.intune.mam.FullBackupContent` meta veri etiketini **true** olarak ayarlayın:

    ```xml
    android:fullBackupContent="true"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="true" />  
    ```

    **2. Örnek**: Uygulamanızın kendi özel BackupAgent’ını kullanmasını istiyor ve tam, Intune ilkesiyle uyumlu, otomatik yedeklemelerden vazgeçiyorsanız, özniteliği ve meta veri etiketini **false** olarak ayarlamalısınız:

    ```xml
    android:fullBackupContent="false"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="false" />  
    ```

    **3. Örnek**: Uygulamanızın XML dosyasında tanımlanan özel kurallarınıza uygun olarak tam yedeklemeleri olmasını istiyorsanız, öznitelikle meta veri etiketini aynı XML kaynağına ayarlayın:

    ```xml
    android:fullBackupContent="@xml/my_scheme"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:resource="@xml/my_scheme" />  
    ```


### <a name="keyvalue-backup"></a>Anahtar/Değer Yedeklemesi

[Anahtar/Değer Yedeklemesi](https://developer.android.com/guide/topics/data/keyvaluebackup.html) seçeneği tüm 8+ API’lerinde kullanılabilir ve uygulama verilerini [Android Yedekleme Hizmeti](https://developer.android.com/google/backup/index.html)’ne yükler. Uygulamanızın kullanıcı başına veri miktarı sınırı 5 MB’tır. Anahtar/Değer Yedeklemesi’ni kullanıyorsanız, bir **BackupAgentHelper** veya **BackupAgent** kullanmalısınız.

### <a name="backupagenthelper"></a>BackupAgentHelper

BackupAgentHelper’ın uygulanması, hem yerel Android işlevselliği hem de Intune MAM tümleştirmesi bakımından BackupAgent‘ın uygulanmasından daha kolaydır. BackupAgentHelper, geliştiricinin tüm dosyaları ve paylaşılan tercihleri sırasıyla bir **FileBackupHelper** ve **SharedPreferencesBackupHelper**’a kaydetmesine olanak tanır. Bunlar, oluşturma sonrasında BackupAgentHelper’a eklenir. Intune MAM ile BackupAgentHelper kullanmak için aşağıdaki adımları izleyin:

1. Çok kimlikli yedeklemeyi BackupAgentHelper ile kullanmak için, Android’in [BackupAgentHelper’ın Kapsamını Genişletme](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgentHelper) yönergelerini izleyin.

2. Sınıfınızı BackupAgentHelper, FileBackupHelper ve SharedPreferencesBackupHelper’ın MAM eşdeğerini içerecek şekilde genişletin.

|Android sınıfı | MAM eşdeğeri |
|--|--|
|BackupAgentHelper |MAMBackupAgentHelper |
|FileBackupHelper | MAMFileBackupHelper
|SharedPreferencesBackupHelper| MAMSharedPreferencesBackupHelper|

Bu yönergelerin ardından, başarılı bir çoklu kimlik yedekleme ve geri yükleme işlemi yapılır.

### <a name="backupagent"></a>BackupAgent

BackupAgent, hangi verilerin yedeklendiği konusunda çok daha net olmanızı sağlar. Uygulama sorumluluğunun büyük bölümü geliştiriciye ait olduğundan, Intune aracılığıyla uygun veri korumasını sağlamak için daha fazla adım gerekir. Intune tümleştirme işlerinin büyük bölümü geliştirici olarak size gönderildiğinden, Intune tümleştirmesi biraz daha karmaşıktır.

**MAM tümleştirmesi:**

1. BackupAgent uygulamanızın Android yönergelerine uyduğundan emin olmak için Android’in [Anahtar/Değer Yedeklemesi](https://developer.android.com/guide/topics/data/keyvaluebackup.html) kılavuzunu ve özellikle de [BackupAgent’ın Kapsamını Genişletme](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) konusunu dikkatle okuyun.

2. Sınıfınızın kapsamını `MAMBackupAgent` için genişletin.

**Çok Kimlikli Yedekleme:**

1. Yedekleme işleminize başlamadan önce, yedeklemeyi planladığınız dosyaların ve veri arabelleklerinin çok kimlikli senaryolarda **yedeklenmesine BT yöneticisi tarafından gerçekten izin verilip verilmediğini** denetleyin. Bunu saptamak için size `MAMFileProtectionManager` ve `MAMDataProtectionManager` içinde `isBackupAllowed` işlevini sağlıyoruz. Dosya veya veri arabelleğinin yedeklenmesine izin verilmiyorsa, bunu yedeklemenize eklemeye çalışmamanız gerekir.

2. Yedeklemenin belirli bir noktasında, 1. adımda denetlediğiniz dosyaların kimliklerini yedeklemek isterseniz, verileri ayıklamayı planladığınız dosyalarla birlikte `backupMAMFileIdentity(BackupDataOutput data, File … files)` çağrısı yapmanız gerekir. Bu, otomatik olarak yeni yedekleme varlıkları oluşturur ve bunları sizin için `BackupDataOutput` ’a yazar. Bu varlıklar geri yükleme sonrasında otomatik olarak kullanılır.

**Çok Kimlikli Geri Yükleme:**

Veri Yedekleme kılavuzu uygulamanızın verilerini geri yüklemeniz için genel bir algoritma belirler ve [BackupAgent’ı Genişletme](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) bölümünde bir kod örneği sağlar. Çok kimlikli geri yükleme işlemini başarmak için, bu kod örneğinde sağlanan genel yapıya uymalı ve aşağıdakilere özel olarak dikkat etmelisiniz:

1. Yedekleme varlıkları arasında ilerlemek için `while(data.readNextHeader())`* döngüsü kullanmalısınız.

2. `data.getKey()`* `onBackup` içinde yazdığınız anahtarla eşleşmezse, `data.skipEntityData()`* çağrısı yapmalısınız. Bu adımı gerçekleştirmeden geri yüklemeleriniz başarılı olamaz.

3. `while(data.readNextHeader())`* yapısında yedekleme varlıklarını kullanırken geri dönmekten kaçının, çünkü otomatik olarak yazılan varlıklar kaybedilir.

* Burada `data`, geri yüklemede uygulamanıza geçilen **MAMBackupDataInput** için yerel değişken adıdır.

## <a name="multi-identity-optional"></a>Çoklu kimlik (isteğe bağlı)

### <a name="overview"></a>Genel bakış
Intune Uygulama SDK’sı varsayılan olarak, ilkeyi uygulamaya bir bütün olarak uygular. Çoklu kimlik; ilkenin her kimlik düzeyinde uygulanmasına izin vermek üzere etkinleştirilebilen, isteğe bağlı bir Intune uygulama koruma özelliğidir. Bu, diğer uygulama koruma özelliklerine kıyasla önemli oranda daha fazla uygulama katılımı gerektirir.

> [!NOTE]
> Uygulamanın doğru yerlerde katılımda bulunmaması, veri sızıntısı veya diğer güvenlik sorunlarıyla sonuçlanabilir.

Kullanıcı cihaz veya uygulamayı kaydettikten sonra, SDK bu kimliği kaydeder ve bunu Intune tarafından yönetilen birincil kimlik olarak kabul eder. Uygulamadaki diğer kullanıcılar kısıtlanmamış ilke ayarlarıyla yönetilmeyen olarak kabul edilirler.

> [!NOTE]
> Şu anda cihaz başına yalnızca bir Intune tarafından yönetilen kimlik desteklenir.

Kimlikler, bir dize olarak tanımlanır. Kimlikler büyük/küçük harfe duyarlıdır ve bir kimlik için SDK 'ya yapılan istek, kimlik ayarlanırken başlangıçta kullanılan büyük/küçük harfleri döndürmeyebilir.

Uygulama, etkin kimliği değiştirmeyi amaçladığında bunu SDK’ya bildirmek *zorundadır*. Bazı durumlarda, bir kimlik değişikliği gerektiğinde SDK bunu uygulamaya bildirir. Ancak çoğu zaman MAM, hangi verilerin kullanıcı arabiriminde görüntülendiğini veya belirli bir anda bir iş parçacığında kullanıldığını bilemez, veri sızıntısını önlemek için doğru kimliğin uygulama tarafından ayarlanması gerekir. Aşağıdaki bölümlerde, uygulama eylemi gerektiren bazı senaryolar verilmiştir.

### <a name="enabling-multi-identity"></a>Çoklu Kimliği Etkinleştirme

Varsayılan olarak, tüm uygulamalar tek kimlikli uygulamalar olarak değerlendirilir. AndroidManifest.xml dosyasına aşağıdaki meta verileri yerleştirerek uygulamanın çok kimliği tanıdığını bildirebilirsiniz.

```xml
  <meta-data
    android:name="com.microsoft.intune.mam.MAMMultiIdentity"
    android:value="true" />
```

### <a name="setting-the-identity"></a>Kimliği Ayarlama

Geliştiriciler uygulama kullanıcısının kimliğini azalan öncelik sırasına göre aşağıdaki düzeylerde ayarlayabilir:

  1. İş parçacığı düzeyi
  2. `Context` (genellikle `Activity` ) düzeyde
  3. İşlem düzeyi

İş parçacığı düzeyinde ayarlanmış bir kimlik, `Context` düzeyinde ayarlanmış bir kimliğin; bağlam düzeyinde ayarlanmış bir kimlikse işlem düzeyinde ayarlanmış bir kimliğin yerini alır. İçindeki bir kimlik kümesi `Context` yalnızca ilgili ilişkili senaryolarda kullanılır. Örneğin, dosya GÇ işlemlerinin ilişkili bir dosyası yoktur `Context` . En yaygın olarak, uygulamalar `Context` bir üzerinde kimlik ayarlar `Activity` . Kimlik aynı kimliğe ayarlanmadığı takdirde, bir uygulamanın yönetilen kimliğin verilerini görüntülemesi *gerekir* `Activity` . Genel olarak işlem düzeyi kimliği yalnızca, uygulama belirli bir anda tüm iş parçacıklarında sadece tek bir kullanıcıyla çalışıyorsa kullanışlıdır. Pek çok uygulamanın bunu kullanmaya ihtiyacı yoktur.

Uygulamanız `Application` sistem hizmetlerini almak için bağlamını kullanıyorsa, iş parçacığı veya işlem kimliğinin ayarlandığından veya uygulamanızın bağlamında Kullanıcı arabirimi kimliğini ayarlamış olduğunuzdan emin olun `Application` .

Uygulamanız `Service` amaçları başlatmak için bir bağlam kullanıyorsa, içerik çözümleyicilerine veya diğer sistem hizmetlerinden yararlanarak bağlamdaki kimliği ayarladığınızdan emin olun `Service` .

Veya ile Kullanıcı arabirimi kimliğini güncelleştirirken özel durumları işlemek için `setUIPolicyIdentity` `switchMAMIdentity` her iki yöntemde de bir değer kümesi geçirilebilir `IdentitySwitchOption` .

* `IGNORE_INTENT`: Geçerli etkinlikle ilişkili amacı yoksayması gereken bir kimlik anahtarı istiyorsa kullanın.
  Örneğin:

  1. Uygulamanız yönetilen bir belge içeren yönetilen bir kimlikle bir amaç alır ve uygulamanız belgeyi görüntüler.
  2. Kullanıcı kendi kişisel kimlik özelliklerine geçiş yaptığında, uygulamanız bir kullanıcı arabirimi kimlik anahtarı ister. Kişisel kimlik ' te, uygulamanız artık belgeyi görüntülemediğinden, `IGNORE_INTENT` kimlik anahtarını istenirken kullanmanız gerekir.

  Ayarlanmamışsa, SDK en son amacın uygulamada hala kullanılmakta olduğunu varsayacaktır. Bu, yeni kimliğin alma ilkesinin, amacı gelen veri olarak ele alınmasına ve kimliğini kullanmasına neden olur.

>[!NOTE]
> , `CLIPBOARD_SERVICE` Kullanıcı arabirimi işlemleri için kullanıldığından, SDK, işlemler için ön plan etkinliğinin Kullanıcı arabirimi kimliğini kullanır `ClipboardManager` .

Aşağıdaki `MAMPolicyManager` yöntemleri kimlik ayarlamak ve önceden ayarlanan kimlik değerlerini almak için kullanılabilir.

```java
public static void setUIPolicyIdentity(final Context context, final String identity, final MAMSetUIIdentityCallback mamSetUIIdentityCallback,
final EnumSet<IdentitySwitchOption> options);

public static String getUIPolicyIdentity(final Context context);

public static MAMIdentitySwitchResult setProcessIdentity(final String identity);

public static String getProcessIdentity();

public static MAMIdentitySwitchResult setCurrentThreadIdentity(final String identity);

public static String getCurrentThreadIdentity();

/**
 * Get the current app policy. This does NOT take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use the overload below.
 */
public static AppPolicy getPolicy();

/**
 * Get the current app policy. This DOES take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use this function.
 */
public static AppPolicy getPolicy(final Context context);


public static AppPolicy getPolicyForIdentity(final String identity);

public static boolean getIsIdentityManaged(final String identity);
```

>[!NOTE]
> Bir uygulamanın kimliğini null olarak ayarlayarak temizleyebilirsiniz.
>
> Boş dize, hiçbir zaman uygulama koruma ilkesine sahip olmayacak bir kimlik olarak kullanılabilir.

#### <a name="results"></a>Sonuçlar
Kimlik ayarlamak için kullanılan tüm yöntemler, sonuç değerlerini `MAMIdentitySwitchResult` aracılığıyla geri rapor eder. Döndürülebilecek dört değer vardır:

| Döndürülen değer | Senaryo |
|--            |--        |
| `SUCCEEDED`    | Kimlik değişikliği başarılı oldu. |
| `NOT_ALLOWED`  | Kimlik değişikliğine izin verilmiyor. `Context`Geçerli iş parçacığında farklı bir kimlik AYARLANDıĞıNDA UI () kimliğini ayarlamak için bir girişimde bulunulduğunda bu durum oluşur. |
| `CANCELLED`    | Kullanıcı, kimlik değişikliğini iptal etmiştir. Bu genellikle PIN veya kimlik doğrulama istemi üzerindeki geri tuşuna basarak yapılır. |
| `FAILED`       | Kimlik değişikliği belirlenemeyen bir nedenden dolayı başarısız oldu.|

Uygulama, kurumsal verileri görüntülemeden veya kullanmadan önce bir kimlik anahtarının başarılı olduğundan emin olmalıdır. Şu anda birden çok kimlik etkin uygulamalarda, işlem ve iş parçacığı kimliklerinin geçişleri her zaman başarılı olmaktadır ancak hata koşulları ekleme hakkımızı saklı tutuyoruz. İş parçacığı kimliğiyle çakışırsa veya kullanıcı koşullu başlatma gereksinimlerini iptal ederse (örneğin PIN ekranında geri düğmesine basarsa) kullanıcı arabirimi kimlik geçişi, geçersiz bağımsız değişkenler için başarısız olabilir. Etkinlik üzerinde başarısız bir kullanıcı arabirimi kimlik anahtarı için varsayılan davranış etkinliğin tamamlanmasından ( `onSwitchMAMIdentityComplete` aşağıya bakın).

Aracılığıyla bir kimlik ayarlamak durumunda `Context` `setUIPolicyIdentity` sonuç zaman uyumsuz olarak bildirilir. `Context`Bir ise, `Activity` SDK, koşullu başlatma gerçekleştirilene kadar kimlik değişikliğinin başarılı olup olmadığını bilmez--kullanıcının bir PIN veya Şirket kimlik bilgileri girmesini gerektirebilir. Uygulama `MAMSetUIIdentityCallback` Bu sonucu almak için bir uygulayabilir veya geri çağırma nesnesi için null geçirebilir. Bir çağrının, `setUIPolicyIdentity` `setUIPolicyIdentity` *aynı bağlamdaki* önceki bir çağrının sonucu henüz teslim edilmediğini, yeni geri aramanın eskisini yerini alacağını ve özgün geri aramanın hiçbir şekilde sonuç almayacağını unutmayın.

```java
  public interface MAMSetUIIdentityCallback {
    void notifyIdentityResult(MAMIdentitySwitchResult identitySwitchResult);
  }
```

Ayrıca bir etkinliğin kimliğini, `MAMPolicyManager.setUIPolicyIdentity` çağrısı yapmak yerine doğrudan `MAMActivity` yöntemiyle de ayarlayabilirsiniz. Bunu yapmak için şu yöntemi kullanın:

```java
     public final void switchMAMIdentity(final String newIdentity, final EnumSet<IdentitySwitchOption> options);
```

Ayrıca, bu etkinliğin kimliğini değiştirme denemelerinin sonucu hakkında uygulamanın bildirim almasını istiyorsanız `MAMActivity` üzerinde bir yöntemi geçersiz kılabilirsiniz.

``` java
    public void onSwitchMAMIdentityComplete(final MAMIdentitySwitchResult result);
```

Geçersiz kıldıysanız `onSwitchMAMIdentityComplete` (veya `super` yöntemini çağırdığınızda), etkinlik üzerinde başarısız bir kimlik anahtarı etkinliğin tamamlanmasının oluşmasına neden olur. Yöntemini geçersiz kılarsınız, bir başarısız kimlik anahtarından sonra kurumsal verilerin görüntülenmediğinden emin olmanız gerekir.

>[!NOTE]
> Kimliği değiştirmek için etkinliğin yeniden oluşturulması gerekebilir. Bu durumda, `onSwitchMAMIdentityComplete` geri çağırma yeni etkinlik örneğine gönderilir.


### <a name="implicit-identity-changes"></a>Örtük Kimlik Değişiklikleri

Uygulamanın kimlik ayarlayabilme özelliğine ek olarak, bir iş parçacığı veya bir bağlamın kimliği; uygulama koruma ilkesi olan başka bir Intune yönetimli uygulamadan veri girişine göre değişebilir.

#### <a name="examples"></a>Örnekler
1. Bir etkinlik `Intent` başka BIR mam uygulamasından gönderilen bir uygulama tarafından başlatılmışsa, etkinliğin kimliği, gönderildiği noktada diğer uygulamadaki etkin kimliğe göre ayarlanır `Intent` .

2. Hizmetler için iş parçacığı kimliği bir `onStart` veya `onBind` çağrısının süresine benzer şekilde ayarlanır. `Binder` öğesinden döndürülen `onBind` içine yapılan çağrılar iş parçacığı kimliğini de geçici olarak ayarlar.

3. `ContentProvider` içine yapılan çağrılar da benzer şekilde iş parçacığı kimliğini süreleri boyunca ayarlar.


  Ayrıca, bir etkinlikle kullanıcı etkileşimi bir örtük kimlik anahtarına neden olabilir.

  **Örnek:**`Resume` sırasında bir kullanıcının bir yetkilendirme istemini iptal etmesi, boş bir kimliğe örtük anahtar ile sonuçlanır.

  Uygulamaya bu değişiklikler hakkında haber alma fırsatı verilir ve gerekirse uygulama bunları yasaklayabilir. `MAMService` ve `MAMContentProvider`, alt sınıfların geçersiz kılabileceği aşağıdaki yöntemi kullanıma sunar:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchResultCallback callback);
  ```

  `MAMActivity` sınıfında, yöntemde ek bir parametre bulunur:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchReason reason,
          final AppIdentitySwitchResultCallback callback);
  ```

  * `AppIdentitySwitchReason`, örtük anahtarın kaynağını yakalar ve `CREATE`, `RESUME_CANCELLED` ve `NEW_INTENT` değerlerini kabul edebilir.  Etkinliği sürdürmek PIN, kimlik doğrulama veya başka bir uyumluluk UI’sinin görüntülenmesine neden olduğunda ve kullanıcı bu UI’yi genellikle geri tuşuna basarak iptal etmeyi denediğinde `RESUME_CANCELLED` nedeni kullanılır.


    * `AppIdentitySwitchResultCallback` aşağıdaki şekildedir:

      ```java
      public interface AppIdentitySwitchResultCallback {
          /**
            * @param result
            *            whether the identity switch can proceed.
            */
          void reportIdentitySwitchResult(AppIdentitySwitchResult result);
        }
        ```

      Burada ```AppIdentitySwitchResult```; `SUCCESS` veya `FAILURE` olur.

`onMAMIdentitySwitchRequired` yöntemi, `MAMService.onMAMBind` öğesinden döndürülen bir Bağlayıcı aracılığıyla yapılanlar dışındaki tüm örtük kimlik değişiklikleri için çağrılır. Varsayılan `onMAMIdentitySwitchRequired` uygulamaları hemen şu çağrıyı yapar:

* `reportIdentitySwitchResult(FAILURE)` nedeni `RESUME_CANCELLED` .

* Diğer tüm durumlarda `reportIdentitySwitchResult(SUCCESS)`.

  Çoğu uygulamanın bir kimlik anahtarını farklı bir şekilde engellemesi veya geciktirmesi beklenmez, ancak bir uygulamanın böyle yapması gerekirse aşağıdaki noktaların göz önünde bulundurulması gerekir:

  * Bir kimlik değişimi engellenirse, sonuç `Receive` paylaşım ayarları veri girişini yasakladığında olan ile aynıdır.

  * Ana iş parçacığında bir hizmet çalışıyorsa, `reportIdentitySwitchResult` zaman uyumlu olarak çağrılmalıdır veya UI iş parçacığı yanıt vermeyi **durdurmalıdır** .

  * **`Activity`** Oluşturma için, daha `onMAMIdentitySwitchRequired` önce çağrılacaktır `onMAMCreate` . Uygulamanın kimlik anahtarına izin verip vermeyeceğinizi belirleyebilmek için Kullanıcı arabirimini göstermesi gerekiyorsa, bu UI *farklı* bir etkinlik kullanılarak gösterilmelidir.

  * Bir içinde **`Activity`** , bir nedenden dolayı boş kimliğe bir anahtar istendiğinde `RESUME_CANCELLED` , uygulamanın bu kimlik anahtarıyla tutarlı verileri görüntülemesi için devam eden etkinliği değiştirmesi gerekir.  Bu mümkün değilse, uygulama anahtarı reddeder ve kullanıcıdan bir kez daha sürdürülen kimlik ilkesine uyması istenir (örneğin uygulamanın PIN girişi ekranı gösterilerek).

    > [!NOTE]
    > Çok kimlikli bir uygulama, yönetilen ve yönetilmeyen uygulamalardan gelen verileri her zaman alır. Yönetilen kimliklerden alınan verileri yönetilen kabul etmek uygulamanın sorumluluğudur.

  İstenen kimlik yönetiliyorsa (bunu `MAMPolicyManager.getIsIdentityManaged` ile denetleyebilirsiniz) ancak uygulama bu hesabı kullanamıyorsa (örneğin e-posta hesapları gibi hesapların ilk olarak uygulamada ayarlanması gerektiği için) kimlik anahtarı reddedilir.

#### <a name="build-plugin--tool-considerations"></a>Derleme eklentisi / aracı ile ilgili değerlendirmeler
, Veya ' den açıkça kalıtımla almadıysanız `MAMActivity` `MAMService` `MAMContentProvider` (Bu değişikliği yapmak için derleme araçlarına izin verseniz), ancak yine de kimlik anahtarlarını işlemesi gerekiyorsa, bunun yerine `MAMActivityIdentityRequirementListener` (bir `Activity` ) veya `MAMIdentityRequirementListener` ( `Service` veya için) kullanabilirsiniz `ContentProviders` .
`MAMActivity.onMAMIdentitySwitchRequired` için varsayılan davranışa `MAMActivity.defaultOnMAMIdentitySwitchRequired(activity, identity,
reason, callback)` statik yöntemi çağrılarak erişilebilir.

Benzer şekilde `MAMActivity.onSwitchMAMIdentityComplete` yöntemini geçersiz kılmanız gerekiyorsa, `MAMActivityIdentitySwitchListener` sınıfını `MAMActivity` sınıfını açık olarak devralmadan uygulayabilirsiniz.

### <a name="preserving-identity-in-async-operations"></a>Zaman Uyumsuz İşlemlerde Kimliği Koruma
UI iş parçacığındaki işlemler için arka plan görevlerinin başka bir iş parçacığına gönderilmesi yaygın bir durumdur. Çok kimlikli bir uygulama, bu arka plan görevlerinin uygun kimlikle çalıştırıldığından emin olmak ister; bu kimlik çoğunlukla bunları gönderen etkinliğin kullandığı kimliktir. MAM SDK'sı, kimliği koruma konusunda yardımcı olmak için `MAMAsyncTask` ve `MAMIdentityExecutors` sağlar.
Bu, zaman uyumsuz işlem bir dosyaya şirket verileri yazabileceği veya diğer uygulamalarla iletişim kurabiliyorsa kullanılmalıdır.

#### <a name="mamasynctask"></a>MAMAsyncTask

Kullanmak için `MAMAsyncTask` , yalnızca öğesinden devralmalı ve `AsyncTask` ile geçersiz kılmaları ve `doInBackground` ile değiştirin `onPreExecute` `doInBackgroundMAM` `onPreExecuteMAM` . `MAMAsyncTask` oluşturucusu bir etkinlik bağlamı alır. Örneğin:

```java
AsyncTask<Object, Object, Object> task = new MAMAsyncTask<Object, Object, Object>(thisActivity) {

    @Override
    protected Object doInBackgroundMAM(final Object[] params) {
        // Do operations.
    }

    @Override
    protected void onPreExecuteMAM() {
        // Do setup.
    };
}
```

### <a name="mamidentityexecutors"></a>MAMIdentityExecutors
`MAMIdentityExecutors`, `Executor`/`ExecutorService` öğesini `wrapExecutor` ve `wrapExecutorService` yöntemleriyle koruyarak mevcut `Executor` veya `ExecutorService` örneğini bir kimlik olarak sarmalamanıza olanak tanır. Örneğin:

```java
Executor wrappedExecutor = MAMIdentityExecutors.wrapExecutor(originalExecutor, activity);
ExecutorService wrappedService = MAMIdentityExecutors.wrapExecutorService(originalExecutorService, activity);
```

### <a name="file-protection"></a>Dosya Koruması
Her dosyanın, oluşturulduğu sırada iş parçacığı ve işlem kimliğine dayalı olarak kendisiyle ilişkilendirilmiş bir kimliği vardır. Bu kimlik hem dosya şifreleme hem de seçici silme için kullanılır. Yalnızca kimliği yönetilen ve şifreleme gerektiren ilkesi bulunan dosyalar şifrelenir. SDK'nın varsayılan seçmeli silme işlevselliği, yalnızca silme işleminin istendiği yönetilen kimlikle ilişkilendirilmiş dosyaları siler. Uygulama, `MAMFileProtectionManager` sınıfını kullanarak bir dosyanın kimliğini sorgulayabilir veya değiştirebilir.

```java
public final class MAMFileProtectionManager {

   /**
    * Protect a file or directory. This will synchronously trigger whatever protection is required for the file, and will tag the
    * file for future protection changes. If an identity is set on a directory, it is set recursively on all files and
    * subdirectories. New files or directories will inherit their parent directory's identity. If MAM is operating in offline mode,
    * this method will silently do nothing.
    *
    * @param identity
    *        Identity to set.
    * @param file
    *        File to protect.
    *
    * @throws IOException
    *         If the file cannot be protected.
    */
   public static void protect(final File file, final String identity) throws IOException;

   /**
     * Protect a file obtained from a content provider. This is intended to be used for
     * sdcard (whether internal or removable) files accessed through the Storage Access Framework.
     * It may also be used with descriptors referring to private files owned by this app.
     * It is not intended to be used for files owned by other apps and such usage will fail. If
     * creating a new file via a content provider exposed by another MAM-integrated app, the new
     * file identity will automatically be set correctly if the ContentResolver in use was
     * obtained via a Context with an identity or if the thread identity is set.
     *
     * This will synchronously trigger whatever protection is required for the file, and will tag
     * the file for future protection changes. If an identity is set on a directory, it is set
     * recursively on all files and subdirectories. If MAM is operating in offline mode, this
     * method will silently do nothing.
     *
     * @param identity
     *            Identity to set.
     * @param file
     *            File to protect.
     *
     * @throws IOException
     *             If the file cannot be protected.
     */
    public static void protect(final ParcelFileDescriptor file, final String identity) throws IOException;

   /**
    * Get the protection info on a file. This method should only be used if the file is located in the calling application's
    * private storage or the device's shared storage. If opening a file with a content resolver, use the overload which
    * takes a ParcelFileDescriptor instead.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final File file) throws IOException;

   /**
    * Get the protection info on a file descriptor such as one opened through a content resolver.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final ParcelFileDescriptor file) throws IOException;

}

public interface MAMFileProtectionInfo {
    String getIdentity();
}
 ```

#### <a name="app-responsibility"></a>Uygulama Sorumluluğu
MAM, bir `Activity` öğesinde okunan dosyalar ve görüntülenen veriler arasında otomatik olarak bir ilişki çıkaramaz. Uygulamalar, şirket verilerini görüntülemeden önce kullanıcı arabirimi kimliğini uygun şekilde *ayarlamalıdır*. Bu, dosyalardan veri okumayı içerir. Bir dosya uygulamanın dışından geliyorsa (bir `ContentProvider` veya genel olarak yazılabilir bir konumdan), dosya, dosyadan okunan bilgileri görüntülemeden önce dosya kimliğini (veri kaynağı için doğru aşırı yüklemeyi kullanarak) belirlemeyi *denemelidir* `MAMFileProtectionManager.getProtectionInfo` . `getProtectionInfo` null veya boş olmayan bir kimlik rapor ederse kullanıcı arabirimi kimliği, bu kimlikle eşleşmek üzere (`MAMActivity.switchMAMIdentity` veya `MAMPolicyManager.setUIPolicyIdentity` kullanarak) *ayarlanmalıdır*. Kimlik geçişi başarısız olursa dosyadan okunan veriler *görüntülenmemelidir*.

Örnek bir akış aşağıdaki gibi olabilir:
  * Kullanıcı uygulamada açmak için bir belge seçer.
  * Açık akış sırasında, diskten veri okumadan önce, uygulama, içeriği göstermek için kullanılması gereken kimliği onaylar:

    ```java
    MAMFileProtectionInfo info = MAMFileProtectionManager.getProtectionInfo(docPath)
    if (info != null)
        MAMPolicyManager.setUIPolicyIdentity(activity, info.getIdentity(), callback, EnumSet.noneOf<IdentitySwitchOption.class>)
    ```

  * Uygulama, geri çağırmaya bir sonuç bildirilene kadar bekler.
  * Sonuç başarısız olarak rapor edilirse uygulama, belgeyi görüntülemez.
  * Uygulama açılır ve dosyayı işler.
  
Bir uygulama, `DownloadManager` dosyaları indirmek Için Android kullanıyorsa, mam SDK, bu dosyaları işlem kimliğini kullanarak otomatik olarak korumaya çalışacaktır. İndirilen dosyalar şirket verileri içeriyorsa, `protect` yükleme sonrasında dosyalar taşınsa veya yeniden oluşturulduğunda uygulamanın çağrı yaptığı sorumluluğudur.

#### <a name="single-identity-to-multi-identity-transition"></a>Tek kimlikle çoklu kimlik geçişi
Daha önce tek kimlik Intune tümleştirmesiyle yayınlanan bir uygulama, daha sonra çok kimliği tümleştirirse, daha önce yüklenen uygulamalar bir geçişe (kullanıcıya görünmez, ilişkili bir UX yoktur) sahip olur. Uygulamanın bu geçişi işlemek için açık bir şey *yapması gerekmez.* Geçişten önce oluşturulan tüm dosyalar yönetilmeye devam edecektir (Bu nedenle, şifreleme ilkesi açık ise şifreli kalacak). İsterseniz, yükseltmeyi algılayabilir ve `MAMFileProtectionManager.protect` belirli dosya veya dizinleri boş kimlikle etiketlemek için kullanabilirsiniz (şifrelendiklerinde şifrelemeyi kaldırır).

#### <a name="offline-scenarios"></a>Çevrimdışı Senaryolar
Dosya kimliği etiketlemesi çevrimdışı moda karşı hassastır. Aşağıdaki noktalar göz önünde bulundurulmalıdır:

* Şirket Portalı yüklü değilse, dosyalar kimlik etiketli olamaz.

* Şirket Portalı yüklüyse ancak uygulamada Intune MAM ilkesi yoksa, dosyalar güvenilir bir şekilde kimlikle etiketlenemez.

* Dosya kimliği etiketleme kullanılabilir olduğunda, uygulama kayıtlı kullanıcıya ait kabul edildiği durumda önceden tek kimlikli yönetilen uygulama olarak yüklenmediyse, önceden oluşturulan tüm dosyalar kişisel/yönetilmeyen olarak kabul edilir (boş dize kimliğine ait olarak).

### <a name="directory-protection"></a>Dizin Koruması

Dizinler, dosyaları korumak için kullanılan aynı `protect` yöntemiyle korunabilir. Dizin koruması; dizinin içindeki tüm dosyalara, alt dizinlere ve dizin içinde oluşturulan yeni dosyalara yinelemeli olarak uygulanır. Dizin koruması yinelemeli olarak uygulandığı için büyük dizinlerde `protect` çağrısı biraz zaman alabilir. Bu nedenle, çok fazla sayıda dosya içeren bir dizine koruma gerçekleştiren uygulamalar `protect` çağrısını bir arka plan iş parçacığında zaman uyumsuz olarak çalıştırmak isteyebilir.

### <a name="data-protection"></a>Veri Koruma

Çoklu kimliklere ait bir dosyayı etiketlemek mümkün değildir. Aynı dosyada farklı kullanıcılara ait verileri depolaması gereken uygulamalar bunu, `MAMDataProtectionManager` tarafından sağlanan özellikleri kullanarak yapabilir. Bu, uygulamanın veri şifrelemesine ve belirli bir kullanıcıya bağlamasına olanak tanır. Şifrelenmiş veriler, bir dosyadaki diske depolamak için uygundur. Kimlikle ilişkili verileri sorgulayabilir ve verilerin şifresini daha sonra kaldırabilirsiniz.

`MAMDataProtectionManager` kullanan uygulamalar, `MANAGEMENT_REMOVED` bildirimi için bir alıcı ayarlamalıdır. Bu bildirim tamamlandıktan sonra, arabellekler korunduğu sırada dosya şifrelemesi etkinleştirilmişse bu sınıf yoluyla korunan arabellekler artık okunabilir durumda olmaz. Bir uygulama, `MAMDataProtectionManager.unprotect` Bu bildirim sırasında tüm arabelleklere çağrı yaparak bu durumu düzeltebilir. Kimlik bilgilerinin korunması isteniyorsa bu bildirim sırasında koruma çağrısı yapmak da güvenlidir; çağrı sırasında şifrelemenin devre dışı bırakılacağı kesindir.


```java

public final class MAMDataProtectionManager {
    /**
     * Protect a stream. This will return a stream containing the protected
     * input.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect, read sequentially. This function
     *            will change the position of the stream but may not have
     *            read the entire stream by the time it returns. The
     *            returned stream will wrap this one. Calls to read on the
     *            returned stream may cause further reads on the original
     *            input stream. Callers should not expect to read directly
     *            from the input stream after passing it to this method.
     *            Calling close on the returned stream will close this one.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static InputStream protect(final InputStream input, final String identity);

    /**
     * Protect a byte array. This will return protected bytes.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static byte[] protect(final byte[] input, final String identity) throws IOException;

    /**
     * Unprotect a stream. This will return a stream containing the
     * unprotected input.
     *
     * @param input
     *            Input data to protect, read sequentially.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static InputStream unprotect(final InputStream input) throws IOException;

    /**
     * Unprotect a byte array. This will return unprotected bytes.
     *
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static byte[] unprotect(final byte[] input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input stream to get information on. Either this input
     *            stream must have been returned by a previous call to
     *            protect OR input.markSupported() must return true.
     *            Otherwise it will be impossible to get protection info
     *            without advancing the stream position. The stream must be
     *            positioned at the beginning of the protected data.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final InputStream input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input bytes to get information on. These must be bytes
     *            returned by a previous call to protect() or a copy of
     *            such bytes.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final byte[] input) throws IOException;
}
```


### <a name="content-providers"></a>İçerik Sağlayıcıları

Uygulama, ile arasında şirket verileri sağlıyorsa `ParcelFileDescriptor` `ContentProvider` , uygulamanın içindeki yöntemini çağırması `isProvideContentAllowed(String)` `MAMContentProvider` ve IÇERIK için sahip kimliğinin UPN 'sini (Kullanıcı asıl adı) geçirmelidir. Bu işlev false döndürürse, içerik çağrıyı yapana *döndürülmemelidir*. İçerik sağlayıcısı aracılığıyla döndürülen dosya tanımlayıcıları dosya kimliğine göre otomatik olarak işlenir.

`MAMContentProvider`Açıkça devralmayı ve bunun yerine bu değişikliği yapmak için derleme araçlarına izin vermeyi düşünüyorsanız, aynı yöntemin statik bir sürümünü çağırabilirsiniz: `MAMContentProvider.isProvideContentAllowed(provider,
contentIdentity)` .

### <a name="selective-wipe"></a>seçmeli silme

Çok kimlikli bir uygulama `WIPE_USER_DATA` bildirimine kaydolursa kullanıcı için bu kullanıcıya ait olarak kimlik ile etiketlenmiş tüm dosyalar dahil bütün verilerin kaldırılmasından uygulama sorumludur. Uygulama, kullanıcı verilerini bir dosyadan kaldırır ancak diğer verileri dosyada tutmayı isterse dosyanın kimliğini *değiştirmelidir* (`MAMFileProtectionManager.protect` ile bir kişisel kullanıcı veya boş kimliğe). Şifreleme ilkesi kullanımdaysa silinen kullanıcıya ait kalan dosyaların şifresi çözülmez ve silme işleminden sonra erişilemez hale gelir.

`WIPE_USER_DATA` için uygulama kaydı, SDK’nın varsayılan seçmeli silme davranışının avantajından yararlanamaz. Çoklu kimliği tanıyan uygulamalarda, MAM varsayılan seçmeli silme yalnızca silme işleminde kimliği hedeflenen dosyaları sileceğinden bu kayıp daha önemli olabilir. Çoklu kimliği tanıyan bir uygulama MAM varsayılan seçmeli silme işleminin yapılmasını _**ve**_ silme işleminde kendi eylemlerini gerçekleştirmek isterse, `WIPE_USER_AUXILIARY_DATA` bildirimlerine kayıtlı olması gerekir. Bu bildirim, SDK tarafından MAM varsayılan seçmeli silme gerçekleştirmeden hemen önce gönderilir. Bir uygulama asla ve için hiçbir şekilde kaydolmamalıdır `WIPE_USER_DATA` `WIPE_USER_AUXILIARY_DATA` .

Varsayılan seçmeli silme, uygulamayı düzgün bir şekilde kapatacak, etkinlikleri sonlandıracaktır ve uygulama işlemini sonlandıracaktır. Uygulamanız varsayılan seçmeli silme işlemlerini geçersiz kılıyorsa, silme gerçekleştikten sonra kullanıcının bellek içi verilere erişmesini engellemek için uygulamanızı el ile kapatmayı düşünebilirsiniz.


## <a name="enabling-mam-targeted-configuration-for-your-android-applications-optional"></a>Android uygulamalarınız için MAM hedefli yapılandırmayı etkinleştirme (isteğe bağlı)
Uygulamaya özgü anahtar-değer çiftleri, [mam-we](../apps/app-configuration-policies-managed-app.md) ve [Android Enterprise](../apps/app-configuration-policies-use-android.md)için Intune konsolunda yapılandırılabilir.
Bu anahtar-değer çiftleri, Intune tarafından değiştirilmeden uygulamaya geçirilir. Bu tip bir yapılandırma almak isteyen uygulamalar bunun için `MAMAppConfigManager` ve `MAMAppConfig` sınıflarını kullanabilir. Aynı uygulamaya birden çok ilke hedeflenmişse aynı anahtar için birden çok çakışan değer olabilir.

> [!NOTE] 
> MAM aracılığıyla teslim için yapılandırma kurulumu- `offline` (Şirket portalı yüklü olmadığında).  Bu durumda yalnızca Android Enterprise AppRestrictions boş bir kimlik ile gönderilir `MAMUserNotification` .

### <a name="get-the-app-config-for-a-user"></a>Bir Kullanıcı Için uygulama yapılandırmasını al
Uygulama yapılandırması aşağıdaki gibi alınmış olabilir:
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
```

MAM kayıtlı kullanıcı yoksa ancak uygulamanız hala Android kurumsal yapılandırmasını (belirli bir kullanıcıya hedeflenmeyecek) almak istiyorsanız, null veya boş bir dize geçirebilirsiniz.

### <a name="conflicts"></a>Çakışmalar
MAM App config içindeki bir değer, Android kurumsal yapılandırması 'nda aynı anahtarla ayarlanmış bir değeri geçersiz kılacaktır. 

Bir yönetici aynı anahtar için çakışan değerleri yapılandırırsa (örneğin, aynı kullanıcıyı içeren birden çok gruba sahip farklı uygulama yapılandırma kümelerini hedefleyerek), Intune bu çakışmayı otomatik olarak çözme yöntemine sahip değildir ve tüm değerleri uygulamanız için kullanılabilir hale getirir. 

Uygulamanız, bir nesneden belirli bir anahtar için tüm değerleri isteyebilir `MAMAppConfig` :
```java
List<Boolean> getAllBooleansForKey(String key)
List<Long> getAllIntegersForKey(final String key)
List<Double> getAllDoublesForKey(final String key)
List<String> getAllStringsForKey(final String key)
```

veya seçilecek bir değer iste:
```java
Boolean getBooleanForKey(String key, BooleanQueryType queryType)
Long getIntegerForKey(String key, NumberQueryType queryType)
Double getDoubleForKey(String key, NumberQueryType queryType)
String getStringForKey(String key, StringQueryType queryType)

enum BooleanQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns true if any of the values are true.
     */
    Or,
    /**
     * In case of conflict, returns false if any of the values are false.
     */
    And
}

enum NumberQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the minimum Integer.
     */
    Min,
    /**
     * In case of conflict, returns the maximum Integer.
     */
    Max
}

enum StringQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the first result ordered alphabetically.
     */
    Min,

    /**
     * In case of conflict, returns the last result ordered alphabetically.
     */
    Max
}
```

Uygulamanız ham verileri anahtar-değer çiftleri kümesinin bir listesi olarak da talep edebilir.

```java
List<Map<String, String>> getFullData()
```


### <a name="full-example"></a>Tam Örnek
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
String fooValue = null;
if (appConfig.hasConflict("foo")) {
    List<String> values = appConfig.getAllStringsForKey("foo");
    fooValue = chooseBestValue(values);
} else {
    valueToUse = appConfig.getStringForKey("foo", MAMAppConfig.StringQueryType.Any);
}
Long barValue = appConfig.getIntegerForKey("bar", MAMAppConfig.NumberQueryType.Min);
```

### <a name="notification"></a>Bildirim
Uygulama yapılandırma, yeni bir bildirim türü ekler:
* **REFRESH_APP_CONFIG**: Bu bildirim, bir `MAMUserNotification` ile gönderilir ve yeni uygulama yapılandırmasının kullanılabilir olduğu hakkında uygulamayı bilgilendirir.

### <a name="further-reading"></a>Daha Fazla Bilgi
Android’de MAM hedefli bir uygulama yapılandırma ilkesi oluşturma hakkında daha fazla bilgi için [Android için Microsoft Intune uygulama yapılandırma ilkeleri kullanma](../apps/app-configuration-policies-managed-app.md) konusunun MAM hedefli uygulama yapılandırması hakkındaki bölümüne bakın.

Uygulama yapılandırması, Graph API kullanılarak da yapılandırılabilir. Bilgi için, [mam hedeflenen yapılandırması için Graph API belgelerine](https://docs.microsoft.com/graph/api/resources/intune-mam-targetedmanagedappconfiguration)bakın.

## <a name="custom-themes-optional"></a>Özel Temalar (isteğe bağlı)
MAM SDK 'sine, tüm MAM ekranları ve iletişim kutularına uygulanacak özel bir tema sağlayabilirsiniz. Bir tema sağlanmazsa, varsayılan bir MAM teması kullanılacaktır.

### <a name="how-to-provide-a-theme"></a>Tema sağlama
Bir tema sağlamak için, aşağıdaki kod satırını yöntemine eklemeniz gerekir `Application.onCreate` :

```java
MAMThemeManager.setAppTheme(R.style.AppTheme);
```

Yukarıdaki örnekte, `R.style.AppTheme` SDK 'nın uygulanmasını istediğiniz stil teması ile değiştirmeniz gerekir.

## <a name="style-customization-deprecated"></a>Stil özelleştirmesi (kullanım dışı)

Bu artık kullanım dışıdır ve özel temalar (yukarıdaki), görünümleri özelleştirmenin tercih edilen yoludur.

MAM SDK tarafından oluşturulan görünümler, içine tümleştirildiği uygulamayla daha iyi eşleşmesi için görsel olarak özelleştirilebilir. Birincil ve ikincil renklerle arka plan renklerini ve uygulama logosunun boyutunu özelleştirebilirsiniz. Bu stil özelleştirmesi isteğe bağlıdır ve özel bir stil yapılandırılmazsa varsayılanlar kullanılır.


### <a name="how-to-customize"></a>Nasıl özelleştirilir?
Stil değişikliklerinin Intune MAM görünümlerine uygulanmasını sağlamak için, önce bir stil geçersiz kılma XML dosyası oluşturmalısınız. Bu dosya uygulamanızın “/res/xml” dizinine yerleştirilmelidir ve bu dosyayı istediğiniz gibi adlandırabilirsiniz. Aşağıda, bu dosyanın uyması gereken biçimin örneği gösterilmektedir.

```xml
<?xml version="1.0" encoding="utf-8"?>
<styleOverrides>
    <item
        name="foreground_color"
        resource="@color/red"/>
    <item
        name="accent_color"
        resource="@color/blue"/>
    <item
        name="background_color"
        resource="@color/green"/>
    <item
        name="logo_image"
        resource="@drawable/app_logo"/>
</styleOverrides>
```

Uygulamanızın içinde zaten mevcut olan kaynakları yeniden kullanmalısınız. Örneğin, yeşil rengini colors.xml dosyasında tanımlamalı ve bu renge burada başvuruda bulunmalısınız. Onaltılı “#0000ff" renk kodunu kullanamazsınız. Uygulama logosu için boyut üst sınırı 110 dip’tir (dp). Daha küçük bir logo resmi kullanabilirsiniz, ama en iyi görünen sonuçlar en yüksek boyutta elde edilir. 110 dip sınırını aşarsanız, resmin ölçeği küçültülür ve büyük olasılıkla bulanık bir görüntü elde edilir.

Aşağıda izin verilen stil özniteliklerinin, bunların denetledikleri UI öğelerinin, XML özniteliği öğe adlarının ve her biri için beklenen kaynak türünün tam listesi verilmiştir.

|Stil özniteliği | Etkilenen UI öğeleri | Öznitelik öğesi adı | Beklenen kaynak türü |
| -- | -- | -- | -- |
| Arka plan rengi | PIN ekranı arka plan rengi <Br>PIN kutusu dolgu rengi | background_color | Color |
| Ön plan rengi | Ön plan metin rengi <br> Varsayılan durumda PIN kutusu kenarlığı <br> Kullanıcı PIN girdiğinde PIN kutusundaki karakterler (gizlenmiş karakterler dahil)| foreground_color | Color|
| Vurgu rengi | Vurgulandığında PIN kutusu kenarlığı <br> Köprüler |accent_color | Color |
| Uygulama logosu | Intune uygulaması PIN ekranında gösterilen büyük simge | logo_image | Çizilebilir |

## <a name="default-enrollment-optional"></a>Varsayılan kayıt (isteğe bağlı)

Aşağıdakiler; otomatik bir APP-WE hizmet kaydı (buna bu bölümde **varsayılan kayıt** adı veriyoruz) için uygulama başlatırken kullanıcı istemi gerektirme, yalnızca Intune tarafından korunan kullanıcıların SDK ile tümleştirilmiş Android LOB uygulamanızı kullanmasına izin vermek için Intune uygulama koruma ilkelerini gerektirme hakkında bir kılavuzdur. Ayrıca SDK ile tümleştirilmiş Android LOB uygulamanız için SSO’yu nasıl etkinleştireceğinizi de açıklar. Bu, Intune yönetiminde olmayan kullanıcılar tarafından kullanılabilen mağaza uygulamalarında geçerli **değildir**.

> [!NOTE] 
> **Varsayılan kaydın** faydaları arasında, cihazdaki bir uygulama için APP-WE hizmetinden ilke almanın basitleştirilmiş bir yöntemi de bulunur.

> [!NOTE] 
> **Varsayılan kayıt** , bulut farkınındır.

Aşağıdaki adımlarla varsayılan kaydı etkinleştirin:

1. Uygulamanız ADAL 'yi tümleştirirse veya SSO 'yu etkinleştirmeniz gerekiyorsa, [ortak adal yapılandırma](#common-adal-configurations) #2 takıp eden [adal 'ı yapılandırın](#configure-azure-active-directory-authentication-library-adal) . Aksi takdirde, bu adımı atlayabilirsiniz.
   
2. Aşağıdaki değeri etiketi altında bulunan bildirime ekleyerek varsayılan kaydı etkinleştirin `<application>` :

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.DefaultMAMServiceEnrollment" android:value="true" />
   ```

   > [!NOTE] 
   > Bu, uygulamadaki tek MAM-WE tümleştirmesi olmalıdır. Başka MAMEnrollmentManager API'si çağırma denemeleri olursa, çakışmalar ortaya çıkar.

3. Aşağıdaki değeri etiketi altında bulunan bildirime ekleyerek gerekli MAM ilkesini etkinleştirin `<application>` :

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.MAMPolicyRequired" android:value="true" />
   ```

   > [!NOTE] 
   > Böylece kullanıcı, cihaza Şirket Portalı’nı indirmeye ve bunu kullanmadan önce varsayılan kayıt akışını tamamlamaya zorlanır.


## <a name="limitations"></a>Sınırlamalar

### <a name="policy-enforcement-limitations"></a>İlke zorlama sınırlamaları

* **İçerik Çözümleyicileri Kullanma**: “Aktarma veya alma” Intune ilkesi, başka bir uygulamadaki içerik sağlayıcısına erişmek için bir içerik çözümleyicisinin kullanılmasını tamamen veya kısmen engelleyebilir. Bu, `ContentResolver` yöntemlerin null döndürmesine veya bir hata değeri oluşturmasına neden olur (örneğin, `openOutputStream` `FileNotFoundException` engellenirse oluşturur). Uygulama, içerik çözümleyicisi ile veri yazma hatasının bir ilkeden kaynaklanıp kaynaklanmadığını (veya ilke tarafından kaynaklanabileceğini) şu çağrıyı yaparak belirleyebilir:

    ```java
    MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(contentURI);
    ```

    ya da ilişkili etkinlik yoksa:

    ```java
    MAMPolicyManager.getPolicy().getIsSaveToLocationAllowed(contentURI);
    ```

    İkinci durumda birden çok kimlikli uygulamalar, iş parçacığı kimliğini uygun şekilde ayarlamaya (veya `getPolicy` çağrısına bir açık kimlik geçirmeye) özen göstermelidir.

### <a name="exported-services"></a>Dışarı aktarılan hizmetler
Intune Uygulama SDK’sına dahil edilen AndroidManifest.xml dosyası, **MAMNotificationReceiverService** öğesini içerir. Bu öğenin, Şirket Portalı’nın yönetilen bir uygulamaya bildirim göndermesine izin vermek üzere dışarı aktarılan bir hizmet olması gerekir. Hizmet, yalnızca Şirket Portalı’nın bildirim göndermesine izin verildiğinden emin olmak için çağıranı denetler.

### <a name="reflection-limitations"></a>Yansıma sınırlamaları
MAM temel sınıflarından bazıları (örneğin, `MAMActivity` `MAMDocumentsProvider` ), yalnızca belirli API düzeylerinin üzerinde bulunan parametre veya dönüş türleri kullanan Yöntemler (orijinal Android taban sınıflarına göre) içerir. Bu nedenle, uygulama bileşenlerinin tüm yöntemlerini listelemek için yansıma kullanmak her zaman mümkün olmayabilir. Bu kısıtlama MAM ile sınırlı değildir; uygulamanın kendisi Android tabanlı sınıflardan bu yöntemleri uyguladığında da aynı kısıtlama geçerli olur.

### <a name="robolectric"></a>Robolectric
MAM SDK'sının Roboelectic altında test edilmesi desteklenmez. Gerçek cihazlarda veya öykünücülere doğru şekilde benzemez Robolectric altında bulunan davranışlar nedeniyle, Robolectric altında MAM SDK çalıştıran bilinen sorunlar vardır.

Uygulamanızı Robolectric altında test etmeniz gerekiyorsa, önerilen geçici çözüm, uygulama sınıfı mantığınızı bir yardımcıya taşımak ve birim testi APK 'nizi, Mamappler 'dan kalıtımla almayan bir uygulama sınıfıyla üretmeniz gerekir.

## <a name="expectations-of-the-sdk-consumer"></a>SDK tüketicisinin beklentileri

İlkeleri zorunlu kılma işlemi sonucunda hata koşulları daha sık tetiklenebilir, ancak Intune SDK’sı, Android API’si tarafından sağlanan sözleşmeyi korur. Aşağıda belirtilen Android’e yönelik en iyi uygulamalar, hata olasılığını azaltır:

* Null döndürme olasılığı bulunan Android SDK işlevlerinin şu anda da null olma olasılığı daha yüksektir.  Sorunları en aza indirmek için null denetimlerinin doğru yerlerde olduğundan emin olun.

* Denetlenebilir özellikler MAM değiştirme API'leri aracılığıyla denetlenmelidir.

* Türetilen tüm işlevler üst sınıf sürümlerine çağrılmalıdır.

* Herhangi bir API'yi belirsiz bir şekilde kullanmaktan kaçının. Örneğin, requestCode denetlenmeden `Activity.startActivityForResult` kullanmak garip davranışlara neden olur.

### <a name="services"></a>Hizmetler
İlke zorlama, hizmet etkileşimlerini etkileyebilir.
' De bağlı bir hizmet bağlantısı oluşturan Yöntemler, `Context.bindService` ' de temel alınan ilke zorlaması nedeniyle başarısız olabilir ve bu durum `Service.onBind` veya ile sonuçlanabilir `ServiceConnection.onNullBinding` `ServiceConnection.onServiceDisconnected` .
Kurulu bir bağlı hizmetle etkileşim kurmak, `SecurityException` ' de ilke zorlaması nedeniyle bir oluşturabilir `Binder.onTransact` .

## <a name="telemetry"></a>Telemetri

Android için Intune Uygulama SDK’sı, uygulamanızdan veri toplanmasını denetlemez. Şirket Portalı uygulama, varsayılan olarak sistem tarafından oluşturulan verileri günlüğe kaydeder. Bu veriler Microsoft Intune’a gönderilir. Microsoft Ilkesi gereğince, kişisel veri toplamayız.

> [!NOTE]
> Son kullanıcılar bu verileri göndermemeyi tercih ederse, Şirket Portalı uygulamasının Ayarlar bölümünde telemetriyi kapatmaları gerekir. Daha fazla bilgi için bkz. [Microsoft kullanım verilerini toplamayı devre dışı bırakma](../user-help/turn-off-microsoft-usage-data-collection-android.md). 

## <a name="recommended-android-best-practices"></a>Android için önerilen en iyi yöntemler

* Tüm kitaplık projeleri, mümkün olduğunda aynı `android:package` öğesini paylaşmalıdır. Bu durum düzensiz aralıklarla çalışma zamanında hataya neden olmaz; yalnızca derleme zamanıyla ilgili bir sorundur. Intune Uygulama SDK’sının daha yeni sürümleri, gecikmeyi kısmen ortadan kaldıracaktır.

* En yeni Android SDK’sı derleme araçlarını kullanın.

* Tüm gereksiz ve kullanılmayan kitaplıkları kaldırın (örneğin android.support.v4)

## <a name="testing"></a>Test Etme
Bkz. [Test Kılavuzu](app-sdk-android-testing-guide.md).
