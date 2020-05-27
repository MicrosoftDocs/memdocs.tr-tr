---
title: Microsoft Intune’da kayıt kısıtlamalarını ayarlama
titleSuffix: ''
description: Intune’da platforma göre kaydı kısıtlama ve cihaz kayıt sınırı ayarlama.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/17/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1bbcfc953945f7e8525cb7dc7edf3b1dd8a2f5c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989069"
---
# <a name="set-enrollment-restrictions"></a>Kayıt kısıtlamalarını ayarlama

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Bir Intune Yöneticisi olarak, cihazları aşağıdakiler dahil olmak üzere hangi cihazların Intune ile yönetime kaydolabileceğini tanımlayan kayıt kısıtlamaları oluşturabilir ve bunları yönetebilirsiniz:
- Cihaz sayısı.
- İşletim sistemleri ve sürümleri.

Birden çok kısıtlama oluşturabilir ve bunları farklı kullanıcı gruplarına uygulayabilirsiniz. Farklı kısıtlamalarınız için [öncelik sırasını](#change-enrollment-restriction-priority) ayarlayabilirsiniz.

>[!NOTE]
>Kayıt kısıtlamaları güvenlik özellikleri değildir. Güvenliği aşılan cihazlar karakterlerini yanlış gösterebilir. Bu kısıtlamalar, kötü amaçlı olmayan kullanıcılara yönelik olabilecek en iyi engeldir.

Özel olarak şu kayıt kısıtlamalarını oluşturabilirsiniz:

- Kayıtlı cihaz sayısı üst sınırı.
- Kaydedilebilecek cihaz platformları:
  - Android cihaz yöneticisi
  - Android kurumsal iş profili
  - iOS/iPadOS
  - macOS
  - Windows
  - Windows Mobile
- İOS/ıpados, Android Cihaz Yöneticisi, Android kurumsal iş profili, Windows ve Windows Mobile için Platform işletim sistemi sürümü. (Yalnızca Windows 10 sürümleri kullanılabilir. Windows 8.1'e izin veriliyorsa bunu boş bırakın.)
  - En düşük sürüm.
  - En yüksek sürüm.
- [Kişisel cihazları](device-enrollment.md#bring-your-own-device) kısıtlama (IOS, Android Cihaz Yöneticisi, Android kurumsal iş profili, MacOS, Windows ve Windows Mobile).

## <a name="default-restrictions"></a>Varsayılan kısıtlamalar

Hem cihaz türü hem de cihaz sınırı kayıt kısıtlamaları için varsayılan kısıtlamalar otomatik olarak sağlanır. Varsayılanların seçeneklerini değiştirebilirsiniz. Varsayılan kısıtlamalar tüm kullanıcı kayıtlarıyla kullanıcısız kayıtlar için geçerlidir. Daha yüksek önceliklere sahip yeni kısıtlamalar oluşturarak, bu varsayılan kısıtlamaları geçersiz kılabilirsiniz.

## <a name="create-a-device-type-restriction"></a>Cihaz türü kısıtlaması oluşturma

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)cihazlar kayıt kısıtlamaları ' nda oturum açın,  >  **Devices**  >  **Enrollment restrictions**  >  **kısıtlama**  >  **cihaz türü kısıtlaması**oluşturun.
2. **Temel bilgiler** sayfasında, kısıtlamaya bir **ad** ve isteğe bağlı bir **Açıklama**sağlayın.
3. **İleri ' yi** seçerek **Platform ayarları** sayfasına gidin.
4. **Platform**altında, bu kısıtlamanın izin vermek istediğiniz platformlar Için **izin ver** ' i seçin.
    ![Platform ayarlarını seçmek için ekran ucu](./media/enrollment-restrictions-set/choose-platform-settings.png)
5. **Sürümler**altında, izin verilen platformların desteklemesini istediğiniz en düşük ve en yüksek sürümleri seçin. Sürüm kısıtlamaları yalnızca Şirket Portalı kaydedilmiş cihazlara uygulanır.
     Desteklenen sürüm biçimleri:
    - Android Cihaz Yöneticisi ve Android kurumsal iş profili, ana. ikincil. Rev. Build 'yi destekler.
    - iOS/ıpados, ana. Minor. Rev 'ı destekler. İşletim sistemi sürümleri Aygıt Kayıt Programı, Apple Okul Yöneticisi veya Apple Configurator uygulaması ile kaydolmasını sağlayan Apple cihazlarına uygulanmaz.
    - Windows yalnızca Windows 10 için ana. Minor. Build. Rev 'ı destekler.
    
    > [!IMPORTANT]
    > Android Enterprise (iş profili) ve Android Cihaz Yöneticisi platformları aşağıdaki davranışa sahiptir:
    > - Aynı grup için her iki platformda de izin veriliyorsa kullanıcılar, cihazları destekliyorsa bir iş profiliyle kaydedilir, aksi takdirde DA olarak kaydedilir. 
    > - Grup için her iki platforma de izin veriliyorsa ve bu ve çakışmayan olmayan sürümler için, kullanıcılar işletim sistemi sürümleri için tanımlanan kayıt akışını alır. 
    > - Her iki platforma de izin veriliyorsa, ancak aynı sürümler için engelleniyorsa, engellenen sürümlere sahip cihazlardaki kullanıcılar Android Cihaz Yöneticisi kayıt akışını aşağı götürülecektir ve sonra kayıt işleminden sonra oturum kapatması istenir. 
    >
    > Android kaydında uygun dilekleri tamamlanana kadar iş profili veya cihaz yöneticisi kaydının çalışmayacak şekilde dikkat edin. 
    
   > [!Note]
   > Windows 10 kayıt sırasında Rev numarası sağlamaz, örneğin, 10.0.17134.100 içine girdiğinizde ve cihaz 10.0.17134.174 ise kayıt sırasında engellenir.

6. **Kişisel**olarak sahip olunan cihazlara izin vermek istediğiniz platformlar Için **izin ver** ' i seçin.
7. **Cihaz üreticisi**altında, engellemek istediğiniz üreticilerin virgülle ayrılmış bir listesini girin.
8. **Kapsam etiketleri** sayfasına gitmek için **İleri ' yi** seçin.
9. **Kapsam etiketleri** sayfasında isteğe bağlı olarak, bu kısıtlamaya uygulamak istediğiniz kapsam etiketlerini ekleyin. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md). Kapsam etiketleri kayıt kısıtlamalarıyla kullanılırken, kullanıcılar yalnızca kapsamlarına sahip oldukları ilkeleri yeniden sıraya alabilir. Ayrıca, yalnızca kapsamlarına sahip oldukları ilke konumlarına yönelik yeniden sıralama yapılabilir. Kullanıcılar her ilkede doğru ilke öncelik numarasını görür. Kapsamlı bir Kullanıcı, diğer tüm ilkeleri görmese de, ilkelerinin göreli önceliğini söyleyebilir.
10. **Atamalar** sayfasına gitmek için **İleri ' yi** seçin.
11. **Dahil edilecek grupları seç** ' i seçin ve ardından bu kısıtlamaya dahil etmek istediğiniz grupları bulmak için arama kutusunu kullanın. Kısıtlama yalnızca atandığı gruplara uygulanır. Kısıtlamayı en az bir gruba atamazsanız, hiçbir etkisi olmaz. Ardından **Seç** seçeneğini belirleyin. 
    ![Platform ayarlarını seçmek için ekran ucu](./media/enrollment-restrictions-set/select-groups.png)
12. **İleri ' yi** seçerek **gözden geçir + oluştur** sayfasına gidin.
13. Kısıtlamayı oluşturmak için **Oluştur** ' u seçin.
14. Yeni kısıtlama, varsayılan öncelik düzeyinin hemen üstündeki öncelik düzeyiyle oluşturulur. [Önceliği değiştirebilirsiniz](#change-enrollment-restriction-priority).


## <a name="create-a-device-limit-restriction"></a>Cihaz sınırı kısıtlaması oluşturma

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **Kayıt kısıtlamaları**  >  **kısıtlama**  >  **cihaz sınırı kısıtlaması**' nda oturum açın.
2. **Temel bilgiler** sayfasında, kısıtlamaya bir **ad** ve isteğe bağlı bir **Açıklama**sağlayın.
3. **Cihaz sınırı** sayfasına gitmek için **İleri ' yi** seçin.
4. **Cihaz sınırı**için, bir kullanıcının kaydedebileceği en fazla cihaz sayısını seçin.
    ![Cihaz sınırı seçmek için ekran ucu](./media/enrollment-restrictions-set/choose-device-limit.png)
5. **Kapsam etiketleri** sayfasına gitmek için **İleri ' yi** seçin.
6. **Kapsam etiketleri** sayfasında isteğe bağlı olarak, bu kısıtlamaya uygulamak istediğiniz kapsam etiketlerini ekleyin. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md). Kapsam etiketleri kayıt kısıtlamalarıyla kullanılırken, kullanıcılar yalnızca kapsamlarına sahip oldukları ilkeleri yeniden sıraya alabilir. Ayrıca, yalnızca kapsamlarına sahip oldukları ilke konumlarına yönelik yeniden sıralama yapılabilir. Kullanıcılar her ilkede doğru ilke öncelik numarasını görür. Kapsamlı bir Kullanıcı, diğer tüm ilkeleri görmese de, ilkelerinin göreli önceliğini söyleyebilir.
7. **Atamalar** sayfasına gitmek için **İleri ' yi** seçin.
8. **Dahil edilecek grupları seç** ' i seçin ve ardından bu kısıtlamaya dahil etmek istediğiniz grupları bulmak için arama kutusunu kullanın. Kısıtlama yalnızca atandığı gruplara uygulanır. Kısıtlamayı en az bir gruba atamazsanız, hiçbir etkisi olmaz. Ardından **Seç** seçeneğini belirleyin. 
    ![Grupları seçmek için ekran ucu](./media/enrollment-restrictions-set/select-groups-device-limit.png)
9. **İleri ' yi** seçerek **gözden geçir + oluştur** sayfasına gidin.
10. Kısıtlamayı oluşturmak için **Oluştur** ' u seçin.
11. Yeni kısıtlama, varsayılan öncelik düzeyinin hemen üstündeki öncelik düzeyiyle oluşturulur. [Önceliği değiştirebilirsiniz](#change-enrollment-restriction-priority).

KCG kayıtları sırasında kullanıcılar, kayıtlı cihaz sınırına ulaştığında bunu belirten bir bildirim görür. Örneğin iOS üzerinde:

![iOS cihazı sınır bildirimi](./media/enrollment-restrictions-set/enrollment-restrictions-ios-set-limit-notification.png)

> [!IMPORTANT]
> Cihaz sınırı kısıtlamaları, aşağıdaki Windows kayıt türleri için geçerli değildir:
> - Ortak yönetilen kayıtlar
> - GPO kayıtları
> - Azure Active Directory katılımlı kayıtlar
> - Toplu Azure Active Directory katılımlı kayıtlar
> - Autopilot kayıtları
> - Cihaz kayıt yöneticisi kayıtları
>
> Cihaz sınırı kısıtlamaları, paylaşılan cihaz senaryolarında kabul edildiği için bu kayıt türleri için zorlanmaz.
> [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)'de bu kayıt türleri için sabit sınır belirleyebilirsiniz.


## <a name="change-enrollment-restrictions"></a>Kayıt kısıtlamalarını değiştirme

Aşağıdaki adımları izleyerek, bir kayıt kısıtlamasının ayarlarını değiştirebilirsiniz. Bu kısıtlamalar, zaten kaydedilmiş olan cihazları etkilemez. Bu özellikle [Intune PC aracısı](../fundamentals/manage-windows-pcs-with-microsoft-intune.md) ile kaydedilen cihazlar engellenemez.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **kayıt kısıtlamalarında** oturum açın > > **özelliklerini**değiştirmek istediğiniz kısıtlamayı seçin.
2. Değiştirmek istediğiniz ayarların yanındaki **Düzenle** ' yi seçin.
3. **Düzenle** sayfasında, istediğiniz değişiklikleri yapın ve **gözden geçir + kaydet** sayfasına ilerleyin ve ardından **Kaydet**' i seçin.


## <a name="blocking-personal-android-devices"></a>Kişisel Android cihazlarını engelleme
- Kişisel Android Cihaz Yöneticisi cihazlarını kayıttan engellerseniz, kişisel Android kurumsal iş profili cihazları yine de kayıt yapabilir.
- Varsayılan olarak, Android kurumsal iş profili cihazlarınızın ayarları, Android Cihaz Yöneticisi cihazlarınızla ilgili ayarlarınızla aynıdır. Android kurumsal iş profilinizi veya Android Cihaz Yöneticisi ayarlarınızı değiştirdikten sonra bu durum artık böyle değildir.
- Kişisel Android kurumsal iş profili kaydını engellerseniz, yalnızca şirkete ait Android cihazları Android kurumsal iş profillerine kaydedebilir.

## <a name="blocking-personal-windows-devices"></a>Kişisel Windows cihazlarını engelleme
Kişisel Windows cihazlarının kayıt yapmasını engellerseniz, Intune, kurumsal bir kayıt olarak yetkilendirildiğinden emin olmak için her yeni Windows kayıt isteğini denetler. Yetkilendirilmemiş kayıtlar engellenir.

Windows şirket kaydı olarak yetkilendirme için aşağıdaki yöntemler uygundur:
- Kaydeden kullanıcı [cihaz kayıt yöneticisi hesabı]( device-enrollment-manager-enroll.md) kullanıyor.
- Cihaz [Windows Autopilot](enrollment-autopilot.md) yoluyla kaydediliyor.
- Cihaz Windows Autopilot ile kaydediliyor ancak Windows Ayarları'ndan bir yalnızca MDM kaydı seçeneği değil.
- Cihazın IMEI numarası **cihaz kaydı**  >  **[Kurumsal cihaz tanımlayıcılarında](corporate-identifiers-add.md)** listelenir. (Windows Phone 8.1 için desteklenmez.)
- Cihaz bir [toplu sağlama paketi](windows-bulk-enroll.md) ile kaydediliyor.
- Cihaz, GPO 'dan kaydolur veya [ortak yönetim için Configuration Manager otomatik kayıt](https://docs.microsoft.com/configmgr/comanage/quickstart-paths#bkmk_path1)yapar.
 
Aşağıdaki kayıtlar Intune tarafından kurumsal olarak işaretlenir. Ancak Intune yöneticisi cihaz başına denetim sağlamadığı için engellenir:
- [Windows kurulumu sırasında Azure Active Directory'ye katılma](https://docs.microsoft.com/azure/active-directory/device-management-azuread-joined-devices-frx)\* ile [otomatik MDM kaydı](windows-enroll.md#enable-windows-10-automatic-enrollment).
- [Windows Ayarları'ndan Azure Active Directory'ye katılma](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network)*ile [otomatik MDM kaydı](windows-enroll.md#enable-windows-10-automatic-enrollment).
 
Aşağıdaki kişisel kayıt yöntemleri de engellenir:
- [Windows Ayarları'ndan İş Hesabı ekleme](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network)\* ile [otomatik MDM kaydı](windows-enroll.md#enable-windows-10-automatic-enrollment).
- Windows Ayarları’ndan [Yalnızca MDM kaydı]( https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) seçeneği.

\* Bunlar, Autopilot ile kaydedilirse engellenmez.


## <a name="blocking-personal-iosipados-devices"></a>Kişisel iOS/ıpados cihazlarını engelleme
Varsayılan olarak, Intune iOS/ıpados cihazlarını kişisel olarak sınıflandırır. Şirkete ait olarak sınıflandırılacak bir iOS/ıpados cihazı aşağıdaki koşullardan birini yerine getirmelidir:
- Seri numarası veya ıMEı ile kaydedilir.
- Otomatik cihaz kaydı (eski adıyla Aygıt Kayıt Programı) kullanılarak kaydedildi


## <a name="change-enrollment-restriction-priority"></a>Kayıt kısıtlama önceliğini değiştirme

Kullanıcı kısıtlamalar atanmış birden çok grupta yer alıyorsa, öncelik kullanılır. Kullanıcılar, yalnızca içinde bulundukları gruba atanmış olan en yüksek öncelik kısıtlamasına uymak zorundadır. Örneğin, Ali hem öncelik düzeyi 5 olan kısıtlamaların atandığı A grubunda hem de öncelik düzeyi 2 olan kısıtlamaların atandığı B grubunda yer alıyordur. Ali yanızca öncelik düzeyi 2 olan kısıtlamalara uymak zorundadır.

Kısıtlama oluşturduğunuzda, bu kısıtlama listede varsayılanın hemen üstüne eklenir.

Cihaz kaydı, hem cihaz türü hem de cihaz sınırı kısıtlamaları için varsayılan kısıtlamalar içerir. Daha yüksek öncelikli kısıtlamalarla geçersiz kılınmadığı sürece, bu iki kısıtlama tüm kullanıcılara uygulanır.

Varsayılan kısıtlamalar dışındaki tüm kısıtlamaların önceliğini değiştirebilirsiniz.

1. Azure Portal’da oturum açın.
2. **Diğer Hizmetler**'i seçin, **Intune** için arama yapın ve ardından **Intune**'u seçin.
3. **Cihaz kaydı**  >  **Kayıt kısıtlamaları**' nı seçin.
4. Öncelik listesinde kısıtlamanın üzerine gelin.
5. Üç dikey noktayı kullanarak, önceliği listede dilediğiniz konuma sürükleyin.
