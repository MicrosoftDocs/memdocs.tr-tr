---
title: Yönetilen Android Kurumsal cihazları için uygulama yapılandırma ilkeleri ekleme
titleSuffix: Microsoft Intune
description: Kullanıcılar yönetilen bir Google Play uygulamasını çalıştırdığınızda ayarları sağlamak için Microsoft Intune 'de uygulama yapılandırma ilkeleri kullanın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d0b6f3fe-2bd4-4518-a6fe-b9fd115ed5e0
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: da9c7b1f9a85f42b18dcba4d2349698cbb77daeb
ms.sourcegitcommit: 86c2c438fd2d87f775f23a7302794565f6800cdb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411006"
---
# <a name="add-app-configuration-policies-for-managed-android-enterprise-devices"></a>Yönetilen Android Kurumsal cihazları için uygulama yapılandırma ilkeleri ekleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Microsoft Intune içindeki uygulama yapılandırma ilkeleri, yönetilen Android kurumsal cihazlarda yönetilen Google Play uygulamalar için ayarları sağlar. Uygulama geliştiricisi, Android tarafından yönetilen uygulama yapılandırma ayarlarını gösterir. Intune, yöneticinin uygulama için özellikleri yapılandırmasına izin vermek için bu sunulan ayarı kullanır. Uygulama yapılandırma ilkesi Kullanıcı gruplarınıza atanır. İlke ayarları, uygulama tarafından, genellikle uygulama ilk kez çalıştırıldığında kullanılır.

> [!NOTE]  
> Tüm uygulamalar, uygulama yapılandırmasını desteklemez. Uygulamanın uygulama yapılandırma ilkelerini destekleyip desteklemediğini görmek için uygulama geliştiricisine danışın.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen cihazlar**Ekle ' yi seçin. **Yönetilen cihazlar** ve **yönetilen uygulamalar**arasından seçim yapabileceğiniz unutulmamalıdır. Daha fazla bilgi için bkz. [uygulama yapılandırmasını destekleyen uygulamalar](app-configuration-policies-overview.md#apps-that-support-app-configuration).
3. **Temel bilgiler** sayfasında, aşağıdaki ayrıntıları ayarlayın:
    - **Ad** - Azure portalında görünen profil adı.
    - **Açıklama** - Azure portalında görünen profil açıklaması.
    - **Cihaz kayıt türü** -Bu ayar, **yönetilen cihazlar**olarak ayarlanır.
4. **Platform**olarak **Android Enterprise** ' ı seçin.
5. **Hedeflenen uygulamanın**yanındaki **Uygulama Seç** ' e tıklayın. **İlişkili uygulama** bölmesi görüntülenir. 
6. **İlişkili uygulama** bölmesinde, yapılandırma ilkesiyle ilişkilendirilecek yönetilen uygulamayı seçin ve **Tamam**' a tıklayın.
7. **İleri** ' ye tıklayarak **Ayarlar** sayfasını görüntüleyin.
8. **Izin Ekle** bölmesini göstermek için **Ekle** ' ye tıklayın.
9. Geçersiz kılmak istediğiniz izinlere tıklayın. Verilen izinler, seçilen uygulamalar için "varsayılan uygulama izinleri" ilkesini geçersiz kılar.
10. Her izin için **izin durumunu** ayarlayın. **Komut istemi**, **Otomatik Izin ver**veya **Otomatik Reddet**seçeneklerinden birini belirleyebilirsiniz. İzinler hakkında daha fazla bilgi için bkz. [Intune kullanarak cihazları uyumlu veya uyumsuz olarak işaretlemek Için Android kurumsal ayarları](../protect/compliance-policy-create-android-for-work.md).
11. Yönetilen uygulama yapılandırma ayarlarını destekliyorsa, **yapılandırma ayarları biçim** açılan kutusu görünür. Yapılandırma bilgilerini eklemek için aşağıdaki yöntemlerden birini seçin:
    - **Yapılandırma tasarımcısını kullan**
    - **JSON verilerini girin**<br><br>
    Yapılandırma tasarımcısını kullanma hakkında ayrıntılar için bkz. [Yapılandırma tasarımcısını kullanma](#use-the-configuration-designer). XML verileri girme hakkında daha fazla bilgi için bkz. [JSON verisi](#enter-json-data)girme.
12. **Atamalar** sayfasını göstermek için **İleri** ' ye tıklayın.
13. **Ata**seçeneğinin yanındaki açılan kutuda, uygulama yapılandırma ilkesini atamak için **Seçili gruplar**, **tüm kullanıcılar**, **tüm cihazlar**veya **tüm kullanıcılar ve tüm sapları** seçin.

    ![İlke atamaları Ekle sekmesinin ekran görüntüsü](./media/app-configuration-policies-use-ios/app-config-policy01.png)

14. Açılan kutudaki **tüm kullanıcılar** ' ı seçin.

    ![İlke atamaları - Tüm Kullanıcılar açılan seçeneğinin ekran görüntüsü](./media/app-configuration-policies-use-ios/app-config-policy02.png)

15. İlgili bölmeyi görüntülemek için **Dışlanacak grupları seçin**’e tıklayın.

    ![Ilke atamalarının ekran görüntüsü-dışlanacak grupları seçin bölmesi](./media/app-configuration-policies-use-ios/app-config-policy03.png)

16. Dışlamak istediğiniz grupları seçin ve **Seç**’e tıklayın.

    >[!NOTE]
    >Bir grup eklerken, herhangi bir atama türü için başka bir grup önceden dahil edilmişse bu grup, diğer dahil etme atama türleri için önceden seçili ve değiştirilemez bir biçimde görüntülenir. Dolayısıyla bu grup zaten kullanılmıştır ve dışlanmış bir grup olarak kullanılamaz.

17. **İleri** ' ye tıklayarak **gözden geçir + oluştur** sayfasını görüntüleyin.
18. Uygulama yapılandırma ilkesini Intune 'a eklemek için **Oluştur** ' a tıklayın.

## <a name="use-the-configuration-designer"></a>Yapılandırma tasarımcısını kullanma

Uygulama yapılandırma ayarlarını destekleyecek şekilde tasarlandıysa, yönetilen Google Play uygulamalar için yapılandırma tasarımcısını kullanabilirsiniz. Yapılandırma, Intune 'a kayıtlı cihazlar için geçerlidir. Tasarımcı, uygulama tarafından sunulan ayarlar için belirli yapılandırma değerlerini yapılandırmanızı sağlar.

1. **Add (Ekle)** seçeneğini belirleyin. Uygulama için girmek istediğiniz yapılandırma ayarları listesini seçin.

    E-posta uygulamanız için GMail veya dokuz Iş kullanıyorsanız, bu ayarlarla ilgili daha fazla bilgi için [e-postayı yapılandırmak üzere Android kurumsal cihaz ayarları](../configuration/email-settings-android-enterprise.md) ' na bakın.

2. Yapılandırmadaki her bir anahtar ve değer için şunları ayarlayın:

    - **Değer türü**: yapılandırma değerinin veri türü. Dize değer türleri için isteğe bağlı olarak bir değişken veya sertifika profili seçebilirsiniz.
    - **Yapılandırma değeri**: yapılandırmanın değeri. **Değer türü**için değişken veya sertifika ' yı seçerseniz, bir değişken veya sertifika profili listesinden öğesini seçin. Bir sertifika seçerseniz, cihaza dağıtılan sertifikanın sertifika diğer adı çalışma zamanında doldurulur.

### <a name="supported-variables-for-configuration-values"></a>Yapılandırma değerleri için desteklenen değişkenler

Yapılandırma değeri olarak değişken seçerseniz şunlar arasından seçim yapabilirsiniz:

| Seçenek | Örnek |
|----|----|
| AAD cihaz KIMLIĞI | dc0dc142-11d8-4b12-bfea-cae2a8514c82 |
| Hesap Kimliği | fc0dc142-71d8-4b12-bbea-bae2a8514c81 |
| Intune Cihaz Kimliği | b9841cd9-9843-405f-be28-b2265c59ef97 |
| Etki alanı | contoso.com |
| Posta | john@contoso.com |
| Kısmi UPN | john |
| Kullanıcı Kimliği | 3ec2c00f-b125-4519-acf0-302ac3761822 |
| Kullanıcı adı | John Doe |
| Kullanıcı Asıl Adı | john@contoso.com |

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>Çok kimlikli uygulamalarda yalnızca yapılandırılmış kuruluş hesaplarına izin verme 

Microsoft Intune Yöneticisi olarak, yönetilen cihazlarda Microsoft uygulamalarına hangi iş veya okul hesaplarının ekleneceğini denetleyebilirsiniz. Erişimi yalnızca izin verilen kullanıcı hesaplarıyla sınırlayabilecek ve kayıtlı cihazlarda kişisel hesapları engelleyebilirsiniz. Android cihazlarda, yönetilen cihazlar uygulama yapılandırma ilkesinde aşağıdaki anahtar/değer çiftlerini kullanın:

| **Key** | com.microsoft.intune.mam.AllowedAccountUPNs |
|---|---|
| **Değerler** | <ul><li>Bir veya daha fazla <code>;</code> ile sınırlandırılmış UPN.</li><li>Yalnızca bu anahtar ile tanımlanan yönetilen kullanıcı hesaplarına izin verilir.</li><li> Intune'a kayıtlı cihazlar için <code>{{userprincipalname}}</code> belirteci kayıtlı kullanıcı hesabını temsil etmek için kullanılabilir.</li></ul> |

   > [!NOTE]
   > Aşağıdaki uygulamalar, yukarıdaki uygulama yapılandırmasını işler ve yalnızca kuruluş hesaplarına izin verir:
   > - Android için Edge (42.0.4.4048 ve üzeri)
   > - Office, Word, Excel, Android için PowerPoint (16.0.9327.1000 ve üzeri)
   > - Android için OneDrive (5,28 ve üzeri)
   > - Android için Outlook (2.2.222 ve üzeri)
   > - Android için takımlar (1416/1.0.0.2020061103 ve üzeri)

## <a name="enter-json-data"></a>JSON verilerini girin

Uygulamalarda bazı yapılandırma ayarları (örneğin, paket türlerine sahip uygulamalar) yapılandırma Tasarımcısı ile yapılandırılamaz. Bu değerler için JSON düzenleyicisini kullanın. Uygulama yüklendiğinde ayarlar uygulamalara otomatik olarak sağlanır.

1. **Yapılandırma ayarları biçimi** için **JSON düzenleyicisine gir**’i seçin.
2. Düzenleyicide, yapılandırma ayarları için JSON değerlerini tanımlayabilirsiniz. Örnek bir dosya indirip ardından yapılandırmak için **JSON şablonu indir**’i seçebilirsiniz.
3. **Tamam**’ı ve daha sonra **Ekle**’yi seçin.

İlke oluşturulur ve listede gösterilir.

Atanan uygulama bir cihazda çalıştırıldığında, uygulama yapılandırma ilkesinde yapılandırdığınız ayarlarla çalışır.

## <a name="preconfigure-the-permissions-grant-state-for-apps"></a>Uygulamalar için izin verme durumunu önceden yapılandırma

Ayrıca, Android cihaz özelliklerine erişmek için uygulama izinlerini önceden yapılandırabilirsiniz. Varsayılan olarak, konuma veya cihaz kamerasına erişim gibi cihaz izinleri gerektiren Android Uygulamaları, kullanıcılardan izinleri kabul etmesini veya reddetmesini ister.

Örneğin, bir uygulama cihazın mikrofonunu kullanır. Kullanıcıdan mikrofonu kullanmak için uygulamaya izin vermesi istenir.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >   **Add**  >  **yönetilen cihazlar**Ekle ' yi seçin.
2. Aşağıdaki özellikleri ekleyin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı, **tüm şirket Için Android kurumsal istem izinleri uygulama ilkesidir**.
    - **Açıklama**. Profil için açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Cihaz kayıt türü**: Bu ayar **yönetilen cihazlar**olarak ayarlanır.
    - **Platform**: **Android**' i seçin.

3. **Ilişkili uygulama**' yı seçin. Yapılandırma ilkesi tanımlamak istediğiniz uygulamayı seçin. Onaylanan ve Intune ile eşitlenen Android iş profili uygulamaları listesinden seçim yapın.
4. **İzin**  >  **Ekle**' yi seçin. Listeden, kullanılabilir uygulama izinlerini seçin > **Tamam**' ı seçin.
5. Bu ilkeyle verilecek her izin için bir seçenek belirleyin:
    - **İstem**. Kullanıcıdan kabul etmesini veya reddetmesini isteme.
    - **Otomatik olarak izin ver**. Kullanıcıya bildirmeden otomatik olarak onayla.
    - **Otomatik olarak reddet**. Kullanıcıya bildirmeden otomatik olarak reddet.
6. Uygulama yapılandırma ilkesini atamak için, uygulama yapılandırma ilkesi > **atama**  >  **grupları seçin**' i seçin. Atanacak Kullanıcı gruplarını seçin > **seçin**.
7. İlkeyi atamak için **Kaydet**’i seçin.

## <a name="additional-information"></a>Ek bilgiler

- [Android kurumsal cihazlara yönetilen Google Play uygulaması atama](apps-add-android-for-work.md#assigning-a-managed-google-play-app-to-android-enterprise-work-profile-devices)
- [İOS için Outlook 'U/ıpados ve Android uygulama yapılandırma ayarlarını dağıtma](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## <a name="next-steps"></a>Sonraki adımlar

Uygulamayı [atamaya](apps-deploy.md) ve [izlemeye](apps-monitor.md) devam edin.
