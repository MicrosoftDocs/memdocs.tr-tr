---
title: Microsoft Intune - Azure’da cihaz uyumluluk ilkeleri | Microsoft Docs
description: Cihaz uyumluluk ilkelerini kullanma, durum ve önem düzeylerine genel bakış, Yetkisizkullanımsüresinde durumunu kullanma, koşullu erişimle çalışma ve cihazları atanan bir ilke olmadan işleme ile çalışmaya başlayın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c2af5957d22b5b512b28f574f2a0996801e19018
ms.sourcegitcommit: 5dc3545d7f76ce81598f6b1c9734b0ac0a3e9722
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83690518"
---
# <a name="set-rules-on-devices-to-allow-access-to-resources-in-your-organization-using-intune"></a>Intune'u kullanarak kuruluşunuzdaki kaynaklara erişim izni verme amacıyla cihazlarda kural oluşturun

Çoğu mobil cihaz yönetimi (MDM) çözümü, kullanıcıların ve cihazların bazı gereksinimleri karşılamasını şart koşarak kuruluş verilerin korunmasına yardımcı olmaktadır. Intune'da bu özellik "uyumluluk ilkeleri" olarak adlandırılır. Uyumluluk ilkeleri, kullanıcıların ve cihazların uyumlu olmak için karşılaması gereken kuralları ve ayarları tanımlar. Yönetici, koşullu erişim ile birleştirildiğinde, kuralları karşılamayan kullanıcıları ve cihazları engelleyebilirler.

Örneğin bir Intune yöneticisi şunları gerekli kılabilir:

- Son kullanıcıların mobil cihazlarındaki kuruluş verilerine erişebilmesi için parola kullanması
- Cihazda jailbreak uygulanmamış veya kök erişim izni verilmemiş olması
- Cihazdaki işletim sistemi sürümü için alt veya üst sınır
- Cihazın belirli bir tehdit düzeyinde veya altında olması

Bu özelliği, kuruluşunuzdaki cihazların uyumluluk durumunu izlemek için de kullanabilirsiniz.

> [!IMPORTANT]
> Intune, cihazdaki tüm uyumluluk değerlendirmeleri için cihaz iade zamanlamasını kullanır. [İlke ve profil yenileme döngüleri](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) tahmini yenileme zamanlarını listeler.

<!---### Actions for noncompliance

You can specify what needs to happen when a device is determined as noncompliant. This can be a sequence of actions during a specific time.
When you specify these actions, Intune will automatically initiate them in the sequence you specify. See the following example of a sequence of
actions for a device that continues to be in the noncompliant status for
a week:

- When the device is first determined to be noncompliant, an email with noncompliant notification is sent to the user.

- 3 days after initial noncompliance state, a follow up reminder is sent to the user.

- 5 days after initial noncompliance state, a final reminder with a notification that access to company resources will be blocked on the device in 2 days if the compliance issues are not remediated is sent to the user.

- 7 days after initial noncompliance state, access to company resources is blocked. This requires that you have Conditional Access policy that specifies that access from noncompliant devices should    be blocked for services such as Exchange and SharePoint.

### Grace Period

This is the time between when a device is first determined as
noncompliant to when access to company resources on that device is blocked. This time allows for time that the user has to resolve
compliance issues on the device. You can also use this time to create your action sequences to send notifications to the user before their access is blocked.

Remember that you need to implement Conditional Access policies in addition to compliance policies in order for access to company resources to be blocked.--->

## <a name="device-compliance-policies-work-with-azure-ad"></a>Cihaz uyumluluk ilkeleri Azure AD ile birlikte çalışır

Intune, uyumluluk uygulanmasını sağlamak için Azure Active Directory (AD) [koşullu erişim](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) (başka bir docs Web sitesi açar) kullanır. Bir cihaz Intune'a kaydedildiğinde Azure AD kayıt işlemi başlar ve Azure AD'deki cihaz bilgileri güncelleştirilir. En önemli bilgilerden biri, cihaz uyumluluk durumudur. Bu uyumluluk durumu, e-posta ve diğer kuruluş kaynaklarına erişimi engellemek veya erişime izin vermek için koşullu erişim ilkeleri tarafından kullanılır.

- [Azure Active Directory'de cihaz yönetimi nedir?](https://docs.microsoft.com/azure/active-directory/device-management-introduction) sayfasında cihazların Azure AD'ye kayıt nedeni ve yöntemi hakkında ayrıntılı bilgiler verilmektedir.

- [Koşullu erişim](conditional-access.md) ve [koşullu erişim kullanmanın yaygın yolları](conditional-access-intune-common-ways-use.md) , Intune ile ilgili olarak bu özelliği tanımlar.

## <a name="ways-to-use-device-compliance-policies"></a>Cihaz uyumluluk ilkelerini kullanma yolları

### <a name="with-conditional-access"></a>Koşullu erişimle

İlke kurallarıyla uyumlu olan cihazlar için, bu cihazlara e-posta ve diğer kuruluş kaynaklarına erişim izni verebilirsiniz. Cihazlar ilke kurallarıyla uyumlu değilse, kuruluş kaynaklarına erişemez. Bu koşullu erişimdir.

### <a name="without-conditional-access"></a>Koşullu erişim olmadan

Cihaz uyumluluk ilkelerini koşullu erişim olmadan da kullanabilirsiniz. Uyumluluk ilkelerini bağımsız olarak kullandığınızda, hedeflenen cihazlar değerlendirilir ve uyumluluk durumları raporlanır. Örneğin, kaç cihazın şifrelenmediği ya da hangi cihazlarda işletim sistemi engellemelerinin kaldırıldığı veya kök erişim izni verildiği konusunda bir rapor alabilirsiniz. Uyumluluk ilkelerini koşullu erişim olmadan kullandığınızda, kuruluş kaynaklarına hiçbir erişim kısıtlaması yoktur.

## <a name="ways-to-deploy-device-compliance-policies"></a>Cihaz uyumluluk ilkelerini dağıtma yolları

Kullanıcı gruplarındaki kullanıcılara veya cihaz gruplarındaki cihazlara uyumluluk ilkesi dağıtabilirsiniz. Bir uyumluluk ilkesi kullanıcıya dağıtıldığında, kullanıcının tüm cihazlarında uyumluluk denetimi yapılır. Bu senaryoda cihaz gruplarını kullanmak, uyumluluk raporlamasına yardımcı olur.

Intune ayrıca bir dizi yerleşik uyumluluk ilkesi ayarına da sahiptir. Aşağıdaki yerleşik ilkeler, Intune'a kaydedilen tüm cihazlarda değerlendirilir:

- **Cihazları uyumluluk ilkesi atanmamış olarak işaretle**: Bu, uyumsuzluk için varsayılan bir eylemdir. Bu özelliğin iki değeri vardır:

  - **Uyumlu** (*varsayılan*): güvenlik özelliği kapalı
  - **Uyumlu değil**: güvenlik özelliği açık

  Bir cihaza bir uyumluluk ilkesi atanmamışsa, bu cihaz varsayılan olarak uyumlu olarak değerlendirilir. Uyumluluk ilkeleriyle koşullu erişim kullanıyorsanız, varsayılan ayarı **uyumlu değil**olarak değiştirmeniz önerilir. Bir ilke atanmadığı için son kullanıcı uyumsuzsa, [Şirket Portalı](../apps/company-portal-app.md)`No compliance policies have been assigned` ifadesine yer verir.

- **Gelişmiş jailbreak algılama** (*IOS/ıpados için geçerlidir*): etkinleştirildiğinde, bu ayar jailbreak uygulanmış cihaz durumunun iOS/ıpados cihazlarında daha sık oluşmasına neden olur. Bu ayar yalnızca jailbreak uygulanmış cihazlarını engelleyen bir uyumluluk ilkesiyle hedeflenen cihazları etkiler. Bu özelliği etkinleştirmek, cihazın konum hizmetlerini kullanır ve pil kullanımını etkileyebilir. Kullanıcı konumu verileri Intune tarafından depolanmaz ve yalnızca arka planda jailbreak algılamayı daha sık tetiklemek için kullanılır. 

  Bu ayarın etkinleştirilmesi, cihazlarda şunları gerektirir:
  - Konum hizmetlerinin işletim sistemi düzeyinde etkinleştirilmesi.
  - Şirket Portalı konum hizmetlerini kullanmasına her zaman izin verin.

  Gelişmiş algılama, konum hizmetleri aracılığıyla çalışmaktadır. Değerlendirme, Şirket Portalı uygulaması açılarak veya cihazı fiziksel olarak yaklaşık 500 ölçüm veya daha fazla mesafede hareket ettirilerek tetiklenir. İOS 13 ve üzerinde, bu özellik, cihazın arka planda konumunu kullanmasına izin Şirket Portalı vermeye devam etmek için kullanıcıların her zaman Izin vermeyi seçmesini gerektirir. Kullanıcılar her zaman konum erişimine izin vermediğinde ve bu ayarı yapılandırılmış bir ilkeye sahip değilse, cihazları uyumsuz olarak işaretlenir. Intune 'un, her önemli konum değişikliğinin, bir cihazın ağ bağlantısına bağlı olarak bir jailbreak algılama denetimini güvence altına aldığından emin olamayacağını unutmayın.

- **Uyumluluk durumu geçerlilik süresi (gün)**: Alınan tüm uyumluluk ilkeleri için cihazların durum rapor etme süresini girin. Bu süre içinde durum döndürmeyen cihazlar uyumsuz olarak kabul edilir. Varsayılan değer 30 gündür. Maksimum değer 120 gündür. En küçük değer 1 gündür.

  Bu ayar, **etkin** varsayılan uyumluluk ilkesi (**cihazlar**  >  **izleyici**  >  **ayarı uyumluluğu**) olarak gösterilir. Bu ilke için arka plan görevi günde bir kez çalışır.

Bu ayarları izlemek için bu yerleşik ilkeleri kullanabilirsiniz. Intune ayrıca cihaz platformuna göre belirlenen farklı aralıklarla [yenileme yapar veya güncelleştirmeleri denetler](create-compliance-policy.md#refresh-cycle-times). [Microsoft Intune'daki cihaz ilkeleri ve profiller hakkında yaygın sorular, sorunlar ve çözümler](../configuration/device-profile-troubleshoot.md) sayfası iyi bir kaynaktır.

Uyumluluk raporları, cihazların durumunu denetlemek için harika bir yoldur. [Uyumluluk ilkelerini izleme](compliance-policy-monitor.md) sayfasında da yardımcı bilgiler bulunur.

## <a name="non-compliance-and-conditional-access-on-the-different-platforms"></a>Farklı platformlarda uyumsuzluk ve koşullu erişim

Aşağıdaki tabloda, bir uyumluluk ilkesi koşullu erişim ilkesi ile kullanıldığında uyumlu olmayan ayarların nasıl yönetildiği açıklanır.

---------------------------

|**İlke ayarı**| **Platform** |
| --- | ----|
| **PIN veya parola yapılandırması** | - **Android 4,0 ve üzeri**: karantinaya alındı<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı<br>- **Android Enterprise**: karantinaya alındı  <br>  <br>- **iOS 8,0 ve üzeri**: düzeltildi<br>- **MacOS 10,11 ve üzeri**: düzeltildi  <br>  <br>- **Windows 8.1 ve üzeri**: düzeltildi<br>- **Windows Phone 8,1 ve üzeri**: düzeltildi|
| **Cihaz şifrelemesi** | - **Android 4,0 ve üzeri**: karantinaya alındı<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı<br>- **Android Enterprise**: karantinaya alındı<br><br>- **iOS 8,0 ve üzeri**: DÜZELTILEN (PIN ayarlanarak)<br>- **MacOS 10,11 ve üzeri**: DÜZELTILEN (PIN ayarlanarak)<br><br>- **Windows 8.1 ve üzeri**: geçerli değil<br>- **Windows Phone 8,1 ve üzeri**: düzeltildi |
| **Güvenliği kırılmış veya kökü belirtilen cihaz** | - **Android 4,0 ve üzeri**: karantinaya alındı (ayar değil)<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı (ayar değil)<br>- **Android Enterprise**: karantinaya alındı (ayar değil)<br><br>- **iOS 8,0 ve üzeri**: karantinaya alındı (ayar değil)<br>- **MacOS 10,11 ve üzeri**: geçerli değil<br><br>- **Windows 8.1 ve üzeri**: geçerli değil<br>- **Windows Phone 8,1 ve üzeri**: geçerli değil |
| **E-posta profili** | - **Android 4,0 ve üzeri**: uygulanamaz<br>- **Samsung KNOX Standard 4,0 ve üzeri**: uygulanamaz<br>- **Android Enterprise**: uygulanamaz<br><br>- **iOS 8,0 ve üzeri**: karantinaya alındı<br>- **MacOS 10,11 ve üzeri**: karantinaya alındı<br><br>- **Windows 8.1 ve üzeri**: geçerli değil<br>- **Windows Phone 8,1 ve üzeri**: geçerli değil |
| **En düşük işletim sistemi sürümü** | - **Android 4,0 ve üzeri**: karantinaya alındı<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı<br>- **Android Enterprise**: karantinaya alındı<br><br>- **iOS 8,0 ve üzeri**: karantinaya alındı<br>- **MacOS 10,11 ve üzeri**: karantinaya alındı<br><br>- **Windows 8.1 ve üzeri**: karantinaya alındı<br>- **Windows Phone 8,1 ve üzeri**: karantinaya alındı |
| **En yüksek işletim sistemi sürümü** | - **Android 4,0 ve üzeri**: karantinaya alındı<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı<br>- **Android Enterprise**: karantinaya alındı<br><br>- **iOS 8,0 ve üzeri**: karantinaya alındı<br>- **MacOS 10,11 ve üzeri**: karantinaya alındı<br><br>- **Windows 8.1 ve üzeri**: karantinaya alındı<br>- **Windows Phone 8,1 ve üzeri**: karantinaya alındı |
| **Windows durum kanıtlama** | - **Android 4,0 ve üzeri**: uygulanamaz<br>- **Samsung KNOX Standard 4,0 ve üzeri**: uygulanamaz<br>- **Android Enterprise**: uygulanamaz<br><br>- **iOS 8,0 ve üzeri**: uygulanamaz<br>- **MacOS 10,11 ve üzeri**: geçerli değil<br><br>- **Windows 10 ve Windows 10 Mobile**: karantinaya alındı<br>- **Windows 8.1 ve üzeri**: karantinaya alındı<br>- **Windows Phone 8,1 ve üzeri**: geçerli değil |

---------------------------

**Düzeltildi**: cihaz işletim sistemi uyumluluğu zorluyor. Örneğin, kullanıcı bir PIN ayarlamaya zorlanır.

**Karantinaya alındı**: cihaz işletim sistemi uyumluluğu zorlamaz. Örneğin Android ve Android Kurumsal cihazlar kullanıcıyı cihazı şifrelemeye zorlamaz. Cihaz uyumsuz olduğunda aşağıdaki işlemler yapılır:

- Kullanıcı için bir koşullu erişim ilkesi geçerliyse cihaz engellenir.
- Şirket Portalı uygulaması, tüm uyumluluk sorunları hakkında kullanıcıya bildirim gönderir.

## <a name="next-steps"></a>Sonraki adımlar

- [İlke oluşturun](create-compliance-policy.md) ve önkoşulları görüntüleyin.
- Farklı cihaz platformlarına özgü uyumluluk ayarlarını görüntüleyin:

  - [Android](compliance-policy-create-android.md)
  - [Android Kurumsal](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows 10 Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 ve üzeri](compliance-policy-create-windows-8-1.md)
  - [Windows 10 ve üzeri](compliance-policy-create-windows.md)

- [İlke varlıkları için başvuru](../developer/reports-ref-policy.md) sayfasında Intune Veri Ambarı ilke varlıkları hakkında bilgiler yer almaktadır.
