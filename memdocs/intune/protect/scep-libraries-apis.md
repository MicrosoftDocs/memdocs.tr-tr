---
title: 3. taraf sertifika yetkililerini eklemek için API 'Ler
titleSuffix: Microsoft Intune
description: Microsoft Intune’daki cihazlara SCEP sertifikaları vermek için üçüncü taraf sertifika yetkililerine (CA) yönelik SCEP GitHub çözümünü ekleyin veya tümleştirin. Bu çözüm sertifikaları doğrulayan, Intune’a başarı ve başarısızlık bildirimleri gönderen ve Intune’la iletişim kurarken SSL yuva fabrikasını kullanan Java ve C# API’leri içerir. Ayrıca, SCEP CA yapılandırmanızı test etme adımlarına genel bakış bilgilerini görüntüleyin.
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/06/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 16b212bde0f46861b8acb1470588b784c6f2a7fb
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565674"
---
# <a name="use-apis-to-add-third-party-cas-for-scep-to-intune"></a>API’leri kullanarak Intune’a SCEP için üçüncü taraf CA’ları ekleme

Microsoft Intune’da, üçüncü taraf sertifika yetkililerini (CA) ekleyebilir ve bu CA’ların Basit Sertifika Kayıt Protokolü’nü (SCEP) kullanarak sertifikaları vermesini ve doğrulamasını sağlayabilirsiniz. [Üçüncü taraf sertifika yetkilisi ekleme](certificate-authority-add-scep-overview.md) başlığı altında bu özelliğe genel bir bakış sağlanır ve Intune’daki Yönetici görevleri açıklanır.

Ayrıca, bazı geliştirici görevleri de Microsoft’un GitHub.com’da yayımladığı bir açık kaynak kitaplığını kullanır. Kitaplıkta aşağıdakileri gerçekleştiren bir API vardır:

- Intune tarafından dinamik olarak oluşturulan SCEP parolasını doğrular
- SCEP isteklerini gönderen cihazlarda oluşturulan sertifikaları Intune’a bildirir

Bu API’yi kullanarak, üçüncü taraf SCEP sunucunuz MDM cihazları için Intune SCEP yönetim çözümüyle tümleştirilir. Kitaplık kullanıcılardan kimlik doğrulama, hizmet korumu ve ODATA Intune Hizmet API’si gibi konuları soyutlar.

## <a name="scep-management-solution"></a>SCEP yönetim çözümü

![Üçüncü taraf sertifika yetkilisi SCEP Microsoft Intune ile nasıl tümleştirilir?](./media/scep-libraries-apis/scep-certificate-vendor-integration.png)

Yöneticiler Intune kullanarak SCEP profilleri oluşturur ve sonra bu profilleri MDM cihazlarına atar. SCEP profilleri şöyle parametreler içerir:

- SCEP sunucusunun URL’si
- Sertifika Yetkilisinin Güvenilen Kök Sertifikası
- Sertifika öznitelikleri ve daha fazlası

Intune’a iade edilen cihazlar SCEP profiline atanır ve bu parametrelerle yapılandırılır. Dinamik olarak üretilen değişken SCEP parolası Intune tarafından oluşturulur ve sonra cihaza atanır.

Bu sınama şunları içerir:

- Dinamik olarak oluşturulan değişken parola
- Cihazın SCEP sunucusuna gönderdiği sertifika imzalama isteğinde beklenen parametreler hakkındaki ayrıntılar
- Sınama sona erme zamanı

Intune bu bilgileri şifreler, şifrelenmiş blobu imzalar ve ardından bu ayrıntıları değişken SCEP parolasında paketler.

Sertifika istemek için SCEP sunucusuyla iletişim kuran cihazlar da bu değişken SCEP parolasını verir. SCEP sunucusu SCR’yi ve şifreli değişken SCEP parolasını doğrulama için Intune’a gönderir.  Cihaza sertifika verilmesi için bu değişken parola ve CSR, SCEP sunucusunun doğrulamasından geçmelidir. SCEP değişken parolası doğrulandığında aşağıdaki denetimler yapılır:


- Şifrelenmiş blobun imzası doğrulanır
- Sınamanın süresinin dolmadığı doğrulanır
- Profilin hala cihazı hedeflediği doğrulanır
- CSR’de cihaz tarafından istenen sertifika özelliklerinin beklenen değerlerle eşleştiği doğrulanır

SCEP yönetim çözümüne raporlama da dahildir. Yönetici, SCEP profilinin dağıtım durumuyla ve cihazlara verilen sertifikalarla ilgili bilgileri alabilir.

## <a name="integrate-with-intune"></a>Azure ile tümleştirme

Kitaplığı Intune SCEP ile tümleştirme kodu [Microsoft/Intune-Resource-Access GitHub deposundan](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation) indirilebilir.

Kitaplığı ürünlerinizle tümleştirme işlemi aşağıdaki adımlardan oluşur. Bu adımlar için GitHub depolarıyla çalışma ve Visual Studio’da çözümlerle projeler oluşturma konusunda bilgi sahibi olmak gerekir.

1. Depodan bildirimleri almak için kaydolma
2. Depoyu kopyalama ve indirme
3. `\src\CsrValidation` klasörünün (https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation) altında ihtiyacınız olan kitaplık uygulamasına gitme
4. README dosyasındaki yönergeleri kullanarak kitaplığı oluşturma
5. Kitaplığı, SCEP sunucunuzu oluşturan projeye ekleme
6. SCEP Sunucusunda aşağıdaki görevleri tamamlama:

   - Yöneticinin kitaplık tarafından kimlik doğrulaması için kullanılan [Azure Uygulama Tanımlayıcısı, Azure Uygulama Anahtarı ve Kiracı Kimliği](#onboard-scep-server-in-azure)’ni yapılandırmasına izin verme (bu makalede). Yöneticilerin Azure Uygulama Anahtarını güncelleştirmesine izin verilmelidir.
   - Intune tarafından üretilen SCEP parolasını içeren SCEP isteklerini tanımlama
   - **İstek Doğrulama API'si** kitaplığını kullanarak Intune tarafından üretilen SCEP parolalarını doğrulama
   - Intune tarafından üretilen SCEP parolalarının bulunduğu SCEP isteklerine verilen sertifikaları Intune'a bildirmek için kitaplı bildirim API'lerini kullanma. Ayrıca, bu SCEP istekleri işlenirken oluşabilecek hataları da Intune'a bildirin.
   - Yöneticinin sorun gidermesine yardımcı olmak için sunucunun yeterli bilgiyi günlüğe kaydettiğini onaylama

7. [Tümleştirme testlerini ](#integration-testing) tamamlama (bu makalede) ve tüm sorunlarla ilgilenme
8. Müşteriye aşağıdakileri açıklayan yazılı yönergeler verme:

   - SCEP Sunucusunun Azure portalına nasıl eklenmesi gerektiği
   - Kitaplığı yapılandırmak için Azure Uygulama Tanımlayıcısı ile Azure Anahtar Kimliğinin nasıl alındığı

### <a name="onboard-scep-server-in-azure"></a>Azure'a SCEP sunucusunu ekleme

Intune'da kimliğini doğrulamak için, SCEP sunucusuna Azure Uygulama Kimliği, Azure Uygulama Anahtarı ve Kiracı Kimliği gerekir. Ayrıca SCEP Sunucusu Intune API'sine erişmek için yetkilendirilmelidir.

Bu verileri almak için, SCEP sunucu yöneticisi Azure portalında oturum açar, uygulamayı kaydeder, uygulamaya **Microsoft Intune API\SCEP sınama doğrulaması** izni verir, uygulama için bir anahtar oluşturur ve sonra da uygulama kimliğini, onun anahtarını ve kiracı kimliğini indirir.

Uygulamayı kaydetme ve kimliklerle anahtarları alma yönergeleri için bkz. [Portalı kullanarak kaynaklara erişmek için AAD uygulaması ve hizmet sorumlusu oluşturma](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).

### <a name="java-library-api"></a>Java Kitaplığı API'si

Java kitaplığı, oluşturulurken bağımlılıklarını içeri çeken bir Maven projesi olarak uygulanır. API, `IntuneScepServiceClient` sınıfı tarafından `com.microsoft.intune.scepvalidation` ad alanı altında uygulanır.

#### <a name="intunescepserviceclient-class"></a>IntuneScepServiceClient sınıfı

`IntuneScepServiceClient` sınıfı, SCEP parolalarını doğrulamak, oluşturulan sertifikaları Intune'a bildirmek ve hataları listelemek için kullanılan yöntemleri içerir.

##### <a name="intunescepserviceclient-constructor"></a>IntuneScepServiceClient oluşturucusu

**İmza**:

```java
IntuneScepServiceClient(
    Properties configProperties)
```

**Açıklama**:

`IntuneScepServiceClient` nesnesinin örneğini oluşturur ve bu nesneyi yapılandırır.

**Parametreler**:

- **ConfigProperties** -istemci yapılandırma bilgilerini içeren özellikler nesnesi

Yapılandırma aşağıdaki özellikleri içerir:

- AAD_APP_ID="Ekleme işlemi sırasında alınan Azure Uygulama Kimliği"
- AAD_APP_KEY="Ekleme işlemi sırasında alınan Azure Uygulama Anahtarı"
- TENANT="Ekleme işlemi sırasında alınan Kiracı Kimliği"
- PROVIDER_NAME_AND_VERSION="Ürününüzü ve sürümünü tanımlamak için kullanılan bilgiler"

Çözümünüz kimlik doğrulaması olan veya olmayan bir proxy gerektiriyorsa, aşağıdaki özellikleri ekleyebilirsiniz:

- PROXY_HOST="Proxy'nin üzerinde barındırıldığı konak."
- PROXY_PORT="Proxy'nin dinlediği bağlantı noktası."
- PROXY_USER="Proxy temel kimlik doğrulaması kullanıyorsa, girilecek kullanıcı adı."
- PROXY_PASS="Proxy temel kimlik doğrulaması kullanıyorsa, girilecek parola."

Şunu **oluşturur**:

- **Düzeneği** , uygun bir özellik nesnesi olmadan yürütülürse,

> [!IMPORTANT]
> En iyi yöntem bu sınıfın bir örneğini oluşturmak ve birden çok SCEP isteğini işlemek için bu örneği kullanmaktır. Bunun yapılması, kimlik doğrulama belirteçlerini ve hizmet konumu bilgilerini önbelleğe aldığından ek yükü azaltır.

**Güvenlik notları**  
SCEP sunucu uygulayıcısı, depolamada kalıcı olan yapılandırma özelliklerine girilen verileri, üzerinde oynanmaya ve açıklanmaya karşı korumalıdır. Bilgilerin güvenliğini sağlamak için düzgün ACL'ler ve şifreleme kullanılması önerilir.

##### <a name="validaterequest-method"></a>ValidateRequest yöntemi

**İmza**:

```java
void ValidateRequest(
    String transactionId,
    String certificateRequest)
```

**Açıklama**:

SCEP sertifika isteğini doğrular.

**Parametreler**:

- **Işlem kimliği** -SCEP işlem kimliği
- **certificateRequest** -der-encoded PKCS #10 sertifika isteği Base64 olarak kodlanmış bir dize

Şunu **oluşturur**:

- Çağıran **Galargumentexception** -geçerli olmayan bir parametre ile çağrılırsa oluşturuldu
- **Intunescepserviceexception** -sertifika isteğinin geçerli olmadığı bulunursa oluşturulur
- **Özel durum** -beklenmeyen bir hatayla karşılaşılırsa oluşturuldu

> [!IMPORTANT]
> Bu yöntem tarafından oluşturulan özel durumlar sunucu tarafından günlüğe kaydedilir. `IntuneScepServiceException` özelliklerinde sertifika isteği doğrulamasının neden başarısız olduğuna ilişkin ayrıntılı bilgiler bulunduğuna dikkat edin.

**Güvenlik notları**:

- Bu yöntemde özel durum oluşturulursa, SCEP sunucusunun istemciye sertifika **vermemesi gerekir**.
- SCEP sertifika isteği doğrulaması hataları Intune altyapısında bir sorun olduğunu gösteriyor olabilir. Öte yandan bunlar bir saldırganın sertifika almaya çalıştığını gösteriyor da olabilir.

##### <a name="sendsuccessnotification-method"></a>SendSuccessNotification yöntemi

**İmza**:

```java
void SendSuccessNotification(
    String transactionId,
    String certificateRequest,
    String certThumbprint,
    String certSerialNumber,
    String certExpirationDate,
    String certIssuingAuthority)
```

**Açıklama**:

Intune'a sertifikanın bir SCEP isteğini işleme kapsamında oluşturulduğunu bildirir.

**Parametreler**:

- **Işlem kimliği** -SCEP işlem kimliği
- **certificateRequest** -der-encoded PKCS #10 sertifika isteği Base64 olarak kodlanmış bir dize
- **Certthtrrint** -sağlanan sertifikanın parmak izinin SHA1 karması
- **Certserialnumber** -sağlanan sertifikanın seri numarası
- **certExpirationDate** -sağlanan sertifikanın sona erme tarihi. Tarih saat dizesi web UTC saati (YYYY-AA-DDThh:mm:ss.sssTZD) ISO 8601 olarak biçimlendirilmelidir.
- **Certısingauthority** -sertifikayı veren yetkilinin adı

Şunu **oluşturur**:

- Çağıran **Galargumentexception** -geçerli olmayan bir parametre ile çağrılırsa oluşturuldu
- **Intunescepserviceexception** -sertifika isteğinin geçerli olmadığı bulunursa oluşturulur
- **Özel durum** -beklenmeyen bir hatayla karşılaşılırsa oluşturuldu

> [!IMPORTANT]
> Bu yöntem tarafından oluşturulan özel durumlar sunucu tarafından günlüğe kaydedilir. `IntuneScepServiceException` özelliklerinde sertifika isteği doğrulamasının neden başarısız olduğuna ilişkin ayrıntılı bilgiler bulunduğuna dikkat edin.

**Güvenlik notları**:

- Bu yöntemde özel durum oluşturulursa, SCEP sunucusunun istemciye sertifika **vermemesi gerekir**.
- SCEP sertifika isteği doğrulaması hataları Intune altyapısında bir sorun olduğunu gösteriyor olabilir. Öte yandan bunlar bir saldırganın sertifika almaya çalıştığını gösteriyor da olabilir.

##### <a name="sendfailurenotification-method"></a>SendFailureNotification yöntemi

**İmza**:

```java
void SendFailureNotification(
    String transactionId,
    String certificateRequest,
    long  hResult,
    String errorDescription)
```

**Açıklama**:

Intune'a SCEP isteği işlenirken hata oluştuğunu bildirir. Bu yöntem, bu sınıfın yöntemleri tarafından oluşturulan özel durumlar için çağrılmamalıdır.

**Parametreler**:

- **Işlem kimliği** -SCEP işlem kimliği
- **certificateRequest** -der-encoded PKCS #10 sertifika isteği Base64 olarak kodlanmış bir dize
- **hResult** -karşılaşılan hatayı en iyi şekilde açıklayan Win32 hata kodu. Bkz. [Win32 Hata Kodları](https://msdn.microsoft.com/library/cc231199.aspx)
- **ErrorDescription** -karşılaşılan hatanın açıklaması

Şunu **oluşturur**:

- Çağıran **Galargumentexception** -geçerli olmayan bir parametre ile çağrılırsa oluşturuldu
- **Intunescepserviceexception** -sertifika isteğinin geçerli olmadığı bulunursa oluşturulur
- **Özel durum** -beklenmeyen bir hatayla karşılaşılırsa oluşturuldu

> [!IMPORTANT]
> Bu yöntem tarafından oluşturulan özel durumlar sunucu tarafından günlüğe kaydedilir. `IntuneScepServiceException` özelliklerinde sertifika isteği doğrulamasının neden başarısız olduğuna ilişkin ayrıntılı bilgiler bulunduğuna dikkat edin.

**Güvenlik notları**:

- Bu yöntemde özel durum oluşturulursa, SCEP sunucusunun istemciye sertifika **vermemesi gerekir**.
- SCEP sertifika isteği doğrulaması hataları Intune altyapısında bir sorun olduğunu gösteriyor olabilir. Öte yandan bunlar bir saldırganın sertifika almaya çalıştığını gösteriyor da olabilir.

##### <a name="setsslsocketfactory-method"></a>SetSslSocketFactory yöntemi

**İmza**:

```java
void SetSslSocketFactory(
    SSLSocketFactory factory)
```

**Açıklama**:

İstemciye Intune'la iletişim kurarken belirtilen SSL yuva fabrikasını kullanması gerektiğini (varsayılan değer yerine) bildirmek için bu yöntemi kullanın.

**Parametreler**:

- **Factory** -istemcinin https istekleri için kullanması gereken SSL yuva fabrikası

Şunu **oluşturur**:

- Çağıran **Galargumentexception** -geçerli olmayan bir parametre ile çağrılırsa oluşturuldu

> [!NOTE]
> Bu sınıftaki diğer yöntemler yürütülmeden önce gerekiyorsa SSL Yuva fabrikası ayarlanmalıdır.

## <a name="integration-testing"></a>Tümleştirme testleri

Çözümünüzün Intune'la düzgün bir şekilde tümleştirildiğini doğrulamak ve test etmek bir zorunluluktur. Aşağıdaki listede adımlara genel bir bakış sağlanır:

1. [Intune deneme hesabı](../fundamentals/account-sign-up.md) ayarlayın.
2. [Azure portalına SCEP Sunucusunu](#onboard-scep-server-in-azure) ekleyin (bu makalede).
3. SCEP sunucunuzu eklerken oluşturulan kimlikler ve anahtarla [SCEP Sunucusunu yapılandırın](certificates-scep-configure.md).
4. [Senaryo test matrisindeki](https://github.com/Microsoft/Intune-Resource-Access/blob/develop/src/CsrValidation/doc/TestMatrix.csv) senaryoları test etmek için [cihazları kaydedin](../enrollment/device-enrollment.md).
5. Test Sertifika Yetkiliniz için [bir Güvenilen Kök Sertifika profili oluşturun](certificates-scep-configure.md).
6. [Senaryo test matrisinde](https://github.com/Microsoft/Intune-Resource-Access/blob/develop/src/CsrValidation/doc/TestMatrix.csv) listelenen senaryoları test etmek için SCEP profilleri oluşturun.
7. Cihazlarını kaydeden kullanıcılara [profilleri atayın](../configuration/device-profile-assign.md).
8. Cihazların Intune'la eşitlenmesi için bekleyin. İsterseniz, [cihazları el ile de eşitleyebilirsiniz](../remote-actions/device-sync.md).
9. Güvenilen Kök Sertifikanın ve SCEP [profillerinin cihazlara dağıtıldığını](../configuration/device-profile-monitor.md) onaylayın.
10. Güvenilen Kök Sertifikanın tüm cihazlara yüklendiğini onaylayın.
11. Atanan profiller için SCEP Sertifikalarının tüm cihazlara yüklendiğini onaylayın.
12. Yüklenen sertifikaların özelliklerinin SCEP profilinde ayarlanan özelliklerle eşleştiğini onaylayın.
13. Verilen sertifikaların Intune konsolunda düzgün bir şekilde listelendiğini onaylayın

## <a name="see-also"></a>Ayrıca bkz.

- [Üçüncü taraf CA eklemeye genel bakış](certificate-authority-add-scep-overview.md)
- [Intune Kurulumu](../fundamentals/setup-steps.md)
- [Cihaz kaydı](../enrollment/device-enrollment.md)
- [SCEP sertifika profillerini yapılandırma](certificates-profile-scep.md) (Microsoft NDES Sunucusu\Bağlayıcısı kurulumu bu senaryoda kullanılmaz)
