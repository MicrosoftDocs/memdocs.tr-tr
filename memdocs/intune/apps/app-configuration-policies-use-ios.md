---
title: Yönetilen iOS/ıpados cihazları için uygulama yapılandırma ilkeleri ekleme
titleSuffix: Microsoft Intune
description: Uygulama yapılandırma ilkelerini, çalıştırıldığında bir iOS/ıpados uygulamasına yapılandırma verileri sağlamak üzere nasıl kullanacağınızı öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c9163693-d748-46e0-842a-d9ba113ae5a8
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28ce4e7d80e79f752bded8f0cdf03494aa629e1b
ms.sourcegitcommit: 670c90a2e2d3106048f53580af76cabf40fd9197
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233459"
---
# <a name="add-app-configuration-policies-for-managed-iosipados-devices"></a>Yönetilen iOS/ıpados cihazları için uygulama yapılandırma ilkeleri ekleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

İOS/ıpados uygulaması için özel yapılandırma ayarları sağlamak üzere Microsoft Intune içindeki uygulama yapılandırma ilkelerini kullanın. Bu yapılandırma ayarları, uygulamanın uygulama tedarikçileri yönüne göre özelleştirilbilmesine izin verir. Bu yapılandırma ayarlarını (anahtarlar ve değerleri) uygulama sağlayıcısından almanız gerekir. Uygulamayı yapılandırmak için ayarları, anahtarlar ve değerler olarak veya anahtarlar ve değerler içeren bir XML olarak belirtin.

Microsoft Intune yöneticisi olarak yönetilen cihazlarda hangi kullanıcı hesaplarının Microsoft Office uygulamalarına eklendiğini denetleyebilirsiniz. Erişimi yalnızca izin verilen kullanıcı hesaplarıyla sınırlayabilecek ve kayıtlı cihazlarda kişisel hesapları engelleyebilirsiniz. Destekleyen uygulamalar, uygulama yapılandırmasını işler ve onaylanmamış hesapları kaldırıp engeller. Yapılandırma ilkesi ayarları, uygulama tarafından denetim gerçekleştirildiğinde, genellikle de uygulama ilk defa çalıştırıldığında kullanılır.

Bir uygulama yapılandırma ilkesini ekledikten sonra bu uygulama yapılandırma ilkesi için atamaları ayarlayabilirsiniz. İlke için atamaları ayarladıktan sonra ilkenin uygulandığı kullanıcı gruplarını dahil etmeyi veya dışlamayı seçebilirsiniz. Bir veya daha fazla grubu dahil etmeyi seçtiğinizde, belirli grupları dahil etmeyi veya yerleşik grupları kullanmayı seçebilirsiniz. Yerleşik gruplar **Tüm Kullanıcılar**, **Tüm Cihazlar** ve **Tüm Kullanıcılar + Tüm Cihazlar** şeklindedir. 

> [!NOTE]
> Intune size kolaylık sağlamak adına konsolda önceden oluşturulmuş ve yerleşik iyileştirmeleri bulunan **Tüm Kullanıcılar** ve **Tüm Cihazlar** gruplarını sağlar. Kendi oluşturduğunuz ' tüm kullanıcılar ' veya ' tüm cihazlar ' grupları yerine tüm kullanıcıları ve tüm cihazları hedeflemek için bu grupları kullanmanız önemle tavsiye edilir.

Uygulama yapılandırma ilkenize dahil edilen grupları seçtikten sonra, dışlamak üzere de belirli grupları seçebilirsiniz. Daha fazla bilgi için bkz. [Microsoft Intune’da uygulama atamalarını dahil etme ve dışlama](apps-inc-exl-assignments.md).

> [!TIP]
> Bu ilke türü şu anda yalnızca iOS/ıpados 8,0 ve üstünü çalıştıran cihazlar için kullanılabilir. Aşağıdaki uygulama yükleme türlerini destekler:
>
> - **App Store 'dan yönetilen iOS/ıpados uygulaması**
> - **iOS için uygulama paketi**
>
> Uygulama yükleme türleri hakkında daha fazla bilgi için bkz. [Microsoft Intune’a uygulama ekleme](apps-add.md). Uygulama yapılandırmasını yönetilen cihazlar için. ipa uygulama paketinize ekleme hakkında daha fazla bilgi için bkz. [iOS Geliştirici belgelerindeki](https://developer.apple.com/library/archive/samplecode/sc2279/Introduction/Intro.html)yönetilen uygulama yapılandırması.

## <a name="create-an-app-configuration-policy"></a>Uygulama yapılandırma ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar** > **uygulama yapılandırma Ilkeleri** >  > **yönetilen cihaz** **Ekle** ' yi seçin. **Yönetilen cihazlar** ve **yönetilen uygulamalar**arasından seçim yapabileceğiniz unutulmamalıdır. Daha fazla bilgi için bkz. [uygulama yapılandırmasını destekleyen uygulamalar](app-configuration-policies-overview.md#apps-that-support-app-configuration).
3. **Temel bilgiler** sayfasında, aşağıdaki ayrıntıları ayarlayın:
    - **Ad** - Azure portalında görünen profil adı.
    - **Açıklama** - Azure portalında görünen profil açıklaması.
    - **Cihaz kayıt türü** -Bu ayar, **yönetilen cihazlar**olarak ayarlanır.
4. **Platform**olarak **IOS/ıpados** ' ı seçin.
5. **Hedeflenen uygulamanın**yanındaki **Uygulama Seç** ' e tıklayın. **İlişkili uygulama** bölmesi görüntülenir. 
6. **Hedeflenen uygulama** bölmesinde, yapılandırma ilkesiyle ilişkilendirilecek yönetilen uygulamayı seçin ve **Tamam**' a tıklayın.
7. **İleri** ' ye tıklayarak **Ayarlar** sayfasını görüntüleyin.
8. Açılan kutuda **yapılandırma ayarları biçimini**seçin. Yapılandırma bilgilerini eklemek için aşağıdaki yöntemlerden birini seçin:
    - **Yapılandırma tasarımcısını kullanma**
    - **XML verileri girme**<br><br>
    Yapılandırma tasarımcısını kullanma hakkında ayrıntılar için bkz. [Yapılandırma tasarımcısını kullanma](#use-configuration-designer). XML verileri girme hakkında ayrıntılar için bkz. [XML verileri girme](#enter-xml-data). 
9. **Atamalar** sayfasını göstermek için **İleri** ' ye tıklayın.
10. **Ata**seçeneğinin yanındaki açılan kutuda, uygulama yapılandırma ilkesini atamak için **Seçili gruplar**, **tüm kullanıcılar**, **tüm cihazlar**veya **tüm kullanıcılar ve tüm sapları** seçin.

    ![İlke atamaları Ekle sekmesinin ekran görüntüsü](./media/app-configuration-policies-use-ios/app-config-policy01.png)

11. Açılan kutudaki **tüm kullanıcılar** ' ı seçin.

    ![İlke atamaları - Tüm Kullanıcılar açılan seçeneğinin ekran görüntüsü](./media/app-configuration-policies-use-ios/app-config-policy02.png)

12. İlgili bölmeyi görüntülemek için **Dışlanacak grupları seçin**’e tıklayın.

    ![Ilke atamalarının ekran görüntüsü-dışlanacak grupları seçin bölmesi](./media/app-configuration-policies-use-ios/app-config-policy03.png)

13. Dışlamak istediğiniz grupları seçin ve **Seç**’e tıklayın.

    >[!NOTE]
    >Bir grup eklerken, herhangi bir atama türü için başka bir grup önceden dahil edilmişse bu grup, diğer dahil etme atama türleri için önceden seçili ve değiştirilemez bir biçimde görüntülenir. Dolayısıyla bu grup zaten kullanılmıştır ve dışlanmış bir grup olarak kullanılamaz.

14. **İleri** ' ye tıklayarak **gözden geçir + oluştur** sayfasını görüntüleyin.
15. Uygulama yapılandırma ilkesini Intune 'a eklemek için **Oluştur** ' a tıklayın.

## <a name="use-configuration-designer"></a>Yapılandırma tasarımcısı kullanma

Microsoft Intune, bir uygulamaya özgü yapılandırma ayarları sağlar. Microsoft Intune’a kaydedilen veya kaydedilmeyen cihazlardaki uygulamalar için yapılandırma tasarımcısını kullanabilirsiniz. Tasarımcı, temel alınan XML dilini oluşturmanıza yardımcı olan belirli yapılandırma anahtarları ve değerlerini yapılandırmanıza imkan tanır. Ayrıca her bir değer için veri türünü belirtmeniz gerekir. Uygulamalar yüklendiğinde bu ayarlar uygulamalara otomatik olarak sağlanır.

### <a name="add-a-setting"></a>Ayar ekle

1. Yapılandırmadaki her bir anahtar ve değer için şunları ayarlayın:
   - **Yapılandırma anahtarı** - Belirli ayar yapılandırmalarını benzersiz olarak tanımlayan anahtar.
   - **Veri türü** - Yapılandırma değerinin veri türü. Türler Tamsayı, Gerçek, Dize ve Boole değerlerini içerir.
   - **Yapılandırma değeri** - Yapılandırmanın değeri.
2. Yapılandırma ayarlarınızı yapmak için **Tamam**’a tıklayın.

### <a name="delete-a-setting"></a>Bir ayarı silme

1. Ayarların yanındaki üç nokta simgesini ( **...** ) seçin.
2. **Sil**’i seçin.

\{\{ ve \}\} karakterleri yalnızca belirteç türleri tarafından kullanılır ve başka bir amaçla kullanılmamalıdır.

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>Çok kimlikli uygulamalarda yalnızca yapılandırılmış kuruluş hesaplarına izin verme 

Microsoft Intune Yöneticisi olarak, yönetilen cihazlarda hangi kullanıcı hesaplarının Microsoft uygulamalarına ekleneceğini denetleyebilirsiniz. Erişimi yalnızca izin verilen kullanıcı hesaplarıyla sınırlayabilecek ve kayıtlı cihazlarda kişisel hesapları engelleyebilirsiniz. İOS/ıpados cihazları için aşağıdaki anahtar/değer çiftlerini kullanın:

| **Anahtar** | **Değerler** |
|----|----|
| IntuneMAMAllowedAccountsOnly | <ul><li>**Enabled**: İzin verilen tek hesap, [IntuneMAMUPN](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm) anahtarıyla tanımlanan yönetilen kullanıcı hesabıdır.</li><li>**Disabled** (veya **Enabled** ile eşleşmeyen bir değer): Tüm hesaplara izin verilir.</li></ul> |
| IntuneMAMUPN | <ul><li>Uygulamada oturum açmaya izin verilen hesabın UPN 'si.</li><li> Intune'a kayıtlı cihazlar için <code>{{userprincipalname}}</code> belirteci kayıtlı kullanıcı hesabını temsil etmek için kullanılabilir.</li></ul>  |

   > [!NOTE]
   > Aşağıdaki uygulamalar, yukarıdaki uygulama yapılandırmasını işler ve yalnızca kuruluş hesaplarına izin verir:
   > - İOS için Edge (44.8.7 ve üzeri)
   > - İOS için OneDrive (10,34 ve üzeri)
   > - İçin Outlook (iOS 2.99.0 veya üzeri)

## <a name="enter-xml-data"></a>XML verilerini girme

Intune’a kaydedilmiş cihazlar için uygulama yapılandırma ayarlarını içeren bir XML özellik listesi girebilir veya yapıştırabilirsiniz. XML özellik listesinin biçimi, yapılandırdığınız uygulamaya bağlı olarak değişir. Kullanılacak tam biçim hakkında ayrıntılı bilgi için uygulamanın sağlayıcısına başvurun.

Intune XML biçimini doğrular. Ancak Intune, XML özellik listesinin (PList) hedef uygulama ile çalışıp çalışmayacağını denetlemez.

XML özellik listeleri hakkında daha fazla bilgi edinmek için:

- iOS Geliştirici Kitaplığı’nda [XML Özellik Listelerini anlama](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) konusuna bakın.

### <a name="example-format-for-an-app-configuration-xml-file"></a>Uygulama yapılandırma XML dosyası için örnek biçim

Uygulama yapılandırma dosyasını oluşturduğunuzda, bu biçimi kullanarak aşağıdaki değerlerden birini veya daha fazlasını belirtebilirsiniz:

```xml
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
  <key>aaddeviceid</key>
  <string>{{aaddeviceid}}</string>
</dict>
```

### <a name="supported-xml-plist-data-types"></a>Desteklenen XML PList veri türleri

Intune, bir özellik listesinde aşağıdaki veri türlerini destekler:

- &lt;tamsayı&gt;
- &lt;gerçek&gt;
- &lt;dize&gt;
- &lt;dizi&gt;
- &lt;sözlük&gt;
- &lt;true /&gt; veya &lt;false /&gt;

### <a name="tokens-used-in-the-property-list"></a>Özellik listesinde kullanılan belirteçler

Ayrıca, Intune özellik listesinde aşağıdaki belirteç türlerini destekler:
- \{\{userPrincipalName\}\}— örneğin **John\@contoso.com**
- \{\{posta\}\}— örneğin **John\@contoso.com**
- \{\{partialupn\}\}—örneğin, **John**
- \{\{accountid\}\}—örneğin, **fc0dc142-71d8-4b12-bbea-bae2a8514c81**
- \{\{deviceid\}\}—örneğin, **b9841cd9-9843-405f-be28-b2265c59ef97**
- \{\{userid\}\}—örneğin, **3ec2c00f-b125-4519-acf0-302ac3761822**
- \{\{username\}\}—örneğin, **John Doe**
- \{\{SerialNumber\}\}— Örneğin, **F4KN99ZUG5V2** (IOS/ıpados cihazları için)
- \{\{serialnumberlast4digits\}\}— Örneğin, **G5V2** (IOS/ıpados cihazları için)
- \{\{aaddeviceid\}\}—örneğin **ab0dc123-45d6-7e89-aabb-cde0a1234b56**

## <a name="configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices"></a>Şirket Portalı uygulamasını iOS ve ıpados DEP cihazlarını destekleyecek şekilde yapılandırma

DEP (Apple Aygıt Kayıt Programı) kayıtları, Şirket Portalı uygulamasının App Store sürümü ile uyumlu değildir. Ancak, aşağıdaki adımları kullanarak Şirket Portalı uygulamasını iOS/ıpados DEP cihazlarını destekleyecek şekilde yapılandırabilirsiniz.

1. Intune 'da, gerekirse Intune Şirket Portalı uygulamasını **ıntune** > **uygulamalar** > **tüm uygulamalar** > **Ekle**' ye giderek ekleyin.
2. Şirket Portalı uygulamasına yönelik bir uygulama yapılandırma ilkesi oluşturmak için **uygulamalar** > **uygulama yapılandırma ilkeleri**' ne gidin.
3. Aşağıda XML ile bir uygulama yapılandırma ilkesi oluşturun. Uygulama yapılandırma ilkesi oluşturma hakkında daha fazla bilgi ve XML verilerinin girilmesi, [yönetilen iOS/ıpados cihazları için uygulama yapılandırma Ilkeleri ekleme](app-configuration-policies-use-ios.md)konusunda daha fazla bilgi bulunabilir.

    ``` xml
    <dict>
        <key>IntuneCompanyPortalEnrollmentAfterUDA</key>
        <dict>
            <key>IntuneDeviceId</key>
            <string>{{deviceid}}</string>
            <key>UserId</key>
            <string>{{userid}}</string>
        </dict>
    </dict>
    ```

3. Şirket Portalı, istenen gruplara hedeflenmiş uygulama yapılandırma ilkesiyle cihazlara dağıtın. İlkeyi yalnızca DEP kaydı yapılmış olan cihazların gruplarına dağıttığınızdan emin olun.
4. Son kullanıcılara otomatik olarak yüklendiğinde Şirket Portalı uygulamasında oturum açmasını söyleyin.

## <a name="monitor-iosipados--app-configuration-status-per-device"></a>Cihaz başına iOS/ıpados uygulama yapılandırma durumunu izle 
Bir yapılandırma ilkesi atandıktan sonra, yönetilen her cihaz için iOS/ıpados uygulama yapılandırma durumunu izleyebilirsiniz. Azure portalında **Microsoft Intune**'dan **Cihazlar** > **Tüm cihazlar**'ı seçin. Yönetilen cihazlar listesinden cihaz için bir bölme göstermek üzere belirli bir cihaz seçin. Cihaz bölmesinde **uygulama yapılandırması**' nı seçin.  

## <a name="additional-information"></a>Ek bilgiler

- [İOS için Outlook 'U/ıpados ve Android uygulama yapılandırma ayarlarını dağıtma](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## <a name="next-steps"></a>Sonraki adımlar

Uygulamayı [atamaya](apps-deploy.md) ve [izlemeye](apps-monitor.md) devam edin.
