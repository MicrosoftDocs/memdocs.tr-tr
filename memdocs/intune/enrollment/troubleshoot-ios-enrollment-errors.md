---
title: Microsoft Intune iOS/ıpados cihaz kaydı sorunlarını giderme
titleSuffix: Microsoft Intune
description: Intune 'A iOS/ıpados cihazlarını kaydettiğinizde en yaygın sorunlardan bazılarının sorunlarını gidermeye yönelik öneriler.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/16/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 97e837d99ee6f3558a408c443e32eb86fd803de6
ms.sourcegitcommit: 02635469d684d233fef795d2a15615658e62db10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84814874"
---
# <a name="troubleshoot-iosipados-device-enrollment-problems-in-microsoft-intune"></a>Microsoft Intune 'de iOS/ıpados cihaz kaydı sorunlarını giderme

Bu makalede, Intune 'da iOS/ıpados cihazlarını kaydetme sırasında Intune yöneticilerinin sorunları anlamasına ve sorunlarını gidermenize yardımcı olur.

## <a name="prerequisites"></a>Ön koşullar

Sorun gidermeye başlamadan önce bazı temel bilgilerin toplanması önemlidir. Bu bilgiler sorunu daha iyi anlamanıza ve çözüm bulma süresini azaltmanıza yardımcı olabilir.

Sorunla ilgili olarak aşağıdaki bilgileri toplayın:

- Hata iletisinde tam olarak ne yazıyor?
- Hata iletisini nerede görüyorsunuz?
- Sorun ne zaman başladı? Kayıt hiç çalıştı mı?
- Hangi platform (Android, iOS/ıpados, Windows) soruna sahip?
- Kaç Kullanıcı etkilendi? Tüm kullanıcılar mı etkilendi?
- Kaç cihaz etkilendi? Tüm cihazlar etkileniyor mu ya da yalnızca bir şey var mı?
- MDM yetkilisi nedir?
- Kayıt nasıl gerçekleştirilir? Kayıt profilleriyle "kendi cihazını getir" (BYOD) veya Apple otomatik cihaz kaydı (ADE) midir?

## <a name="error-messages"></a>Hata iletileri

### <a name="profile-installation-failed-a-network-error-has-occurred"></a>Profil yüklemesi başarısız oldu. Bir ağ hatası oluştu.

**Neden:** Cihazda iOS/ıpados ile ilgili belirtilmeyen bir sorun var.

#### <a name="resolution"></a>Çözüm

1. Aşağıdaki adımlarda veri kaybını engellemek için (iOS/ıpados geri yüklenirken cihazdaki tüm veriler silinir), verilerinizi yedeklediğinizden emin olun.
2. Cihazı kurtarma moduna alın ve geri yükleyin. Bunu yeni bir cihaz olarak ayarladığınızdan emin olun. İOS/ıpados cihazlarını geri yükleme hakkında daha fazla bilgi için bkz [https://support.apple.com/HT201263](https://support.apple.com/HT201263) ..
3. Cihazı yeniden kaydedin.

### <a name="profile-installation-failed-connection-to-the-server-could-not-be-established"></a>Profil yüklemesi başarısız oldu. Sunucuyla bağlantı kurulamadı.

**Neden:** Intune kiracınız yalnızca şirkete ait cihazlara izin verecek şekilde yapılandırılmıştır. 

#### <a name="resolution"></a>Çözüm
1. Azure Portal’da oturum açın.
2. **Diğer hizmetler**' i seçin, Intune ' u arayın ve ardından **Intune**' u seçin.
3. **Cihaz kaydı**  >  **Kayıt kısıtlamaları**' nı seçin.
4. **Cihaz türü kısıtlamaları**' nın altında, ayarlamak istediğiniz kısıtlamayı seçin > **Özellikler**  >  **platformları seçin** > **iOS**için **izin ver** ' i seçin ve ardından **Tamam**' a tıklayın.
5. **Platformları Yapılandır**' ı seçin, kişisel IOS/ıpados cihazlarına **izin ver** ' i seçin ve ardından **Tamam**' a tıklayın.
6. Cihazı yeniden kaydedin.

**Neden:** Daha önce farklı bir kullanıcı hesabıyla kaydedilmiş bir cihazı kaydeder ve önceki Kullanıcı Intune 'dan uygun şekilde kaldırılmadı.

#### <a name="resolution"></a>Çözüm
1. Geçerli profil yüklemesini iptal edin.
2. [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com)Safari 'de açın.
3. Cihazı yeniden kaydedin.

> [!NOTE]
> Kayıt hala başarısız olursa, Safari 'de tanımlama bilgilerini kaldırın (tanımlama bilgilerini engellemez) ve ardından cihazı yeniden kaydedin.

**Neden:** Cihaz zaten başka bir MDM sağlayıcısına kayıtlı.

#### <a name="resolution"></a>Çözüm
1. İOS/ıpados cihazında **ayarları** açın, **genel > cihaz yönetimi**' ne gidin.
2. Var olan tüm yönetim profillerini kaldırın.
3. Cihazı yeniden kaydedin.

**Neden:** Cihazı kaydetmeye çalışan kullanıcının Microsoft Intune lisansı yok.

#### <a name="resolution"></a>Çözüm
1. [Office 365 yönetim merkezine](https://admin.microsoft.com)gidin ve ardından **etkin kullanıcılar > kullanıcılar**' ı seçin.
2. Intune kullanıcı lisansı atamak istediğiniz kullanıcı hesabını seçin ve ardından **düzenle > ürün lisansları**' nı seçin.
3. Bu kullanıcıya atamak istediğiniz lisansın konumunu **Açık** konumuna geçirin ve ardından **Kaydet**' i seçin.
4. Cihazı yeniden kaydedin.

### <a name="this-service-is-not-supported-no-enrollment-policy"></a>Bu Hizmet desteklenmiyor. Kayıt Ilkesi yok.

**Neden**: Intune 'Da BIR Apple MDM anında iletme sertifikası yapılandırılmamış veya sertifika geçersiz. 

#### <a name="resolution"></a>Çözüm

- MDM anında iletme sertifikası yapılandırılmamışsa, [bir Apple MDM anında iletme sertifikası edinme](apple-mdm-push-certificate-get.md#steps-to-get-your-certificate)bölümündeki adımları izleyin.
- MDM anında iletme sertifikası geçersizse, [Apple MDM anında iletme sertifikasını yenileme](apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate)bölümündeki adımları izleyin.

### <a name="company-portal-temporarily-unavailable-the-company-portal-app-encountered-a-problem-if-the-problem-persists-contact-your-system-administrator"></a>Şirket Portalı geçici olarak kullanılamıyor. Şirket Portalı uygulama bir sorunla karşılaştı. Sorun devam ederse sistem yöneticinize başvurun.

**Neden:** Şirket Portalı uygulama güncel değil veya bozuk.

#### <a name="resolution"></a>Çözüm
1. Şirket Portalı uygulamayı cihazdan kaldırın.
2. **Microsoft Intune şirket portalı** uygulamasını **App Store**'dan indirin ve yükleyin.
3. Cihazı yeniden kaydedin.
 > [!NOTE]
    > Bu hata, Kullanıcı cihaz kaydı izin verilecek şekilde yapılandırıldığından daha fazla cihaz kaydetmeye çalışıyorsa de oluşabilir. Bu adımlar sorunu gidermezse, aşağıda **ulaşılan cihaz sınırına** yönelik çözüm adımlarını izleyin.

### <a name="device-cap-reached"></a>Cihaz Sınırına Ulaşıldı

**Neden:** Kullanıcı cihaz kayıt sınırından daha fazla cihaz kaydetmeye çalışır.

#### <a name="resolution"></a>Çözüm
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **tüm cihazlar**' ı seçin ve kullanıcının kaydolduğu cihaz sayısını denetleyin.
    > [!NOTE]
    > Ayrıca, etkilenen kullanıcının [Intune kullanıcı portalında](https://portal.manage.microsoft.com/) oturum açmasını ve kaydolmuş cihazları kontrol etmeniz gerekir. Intune [Kullanıcı portalında](https://portal.manage.microsoft.com/) görünen ancak [Intune yönetim portalında](https://portal.azure.com/?Microsoft_Intune=1&Microsoft_Intune_DeviceSettings=true&Microsoft_Intune_Enrollment=true&Microsoft_Intune_Apps=true&Microsoft_Intune_Devices=true#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview)yer alan cihazlar olabilir, bu da cihaz kayıt sınırına doğru sayılır.
2. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde cihaz kayıt kısıtlamaları ' **nı seçin**  >  **Enrollment restrictions** > cihaz kayıt sınırı ' nı işaretleyin. Varsayılan olarak, sınır 15 olarak ayarlanır. 
3. Kaydedilen cihazların sayısı sınıra ulaştıysa, gereksiz cihazları kaldırın veya cihaz kayıt sınırını artırın. Kayıtlı her cihaz bir Intune lisansı kullandığından, önce gereksiz cihazları her zaman kaldırmanız önerilir.
4. Cihazı yeniden kaydedin.

### <a name="workplace-join-failed"></a>Workplace Join başarısız oldu

**Neden:** Şirket Portalı uygulama güncel değil veya bozuk.  

#### <a name="resolution"></a>Çözüm
1. Şirket Portalı uygulamayı cihazdan kaldırın.
2. **Microsoft Intune şirket portalı** uygulamasını **App Store**'dan indirin ve yükleyin.
3. Cihazı yeniden kaydedin.

### <a name="user-license-type-invalid"></a>Kullanıcı Lisans türü geçersiz

**Neden:** Cihazı kaydetmeye çalışan kullanıcının geçerli bir Intune lisansı yok.

#### <a name="resolution"></a>Çözüm
1. [Microsoft 365 yönetim merkezine](https://admin.microsoft.com)gidin ve ardından **Kullanıcılar**  >  **etkin kullanıcılar**' ı seçin.
2. Etkilenen Kullanıcı hesabını > **ürün lisansları**  >  **Düzenle**' yi seçin.
3. Bu kullanıcıya geçerli bir Intune lisansının atandığını doğrulayın.
4. Cihazı yeniden kaydedin.

### <a name="user-name-not-recognized-this-user-account-is-not-authorized-to-use-microsoft-intune-contact-your-system-administrator-if-you-think-you-have-received-this-message-in-error"></a>Kullanıcı adı tanınmıyor. Bu Kullanıcı hesabının Microsoft Intune kullanma yetkisi yok. Bu iletiyi hata halinde aldığınızı düşünüyorsanız, sistem yöneticinize başvurun.

**Neden:** Cihazı kaydetmeye çalışan kullanıcının geçerli bir Intune lisansı yok.

1. [Microsoft 365 yönetim merkezine](https://admin.microsoft.com)gidin ve ardından **Kullanıcılar**  >  **etkin kullanıcılar**' ı seçin.
2. Etkilenen Kullanıcı hesabını seçin ve ardından **ürün lisansları**  >  **Düzenle**' yi seçin.
3. Bu kullanıcıya geçerli bir Intune lisansının atandığını doğrulayın.
4. Cihazı yeniden kaydedin.

### <a name="profile-installation-failed-the-new-mdm-payload-does-not-match-the-old-payload"></a>Profil yüklemesi başarısız oldu. Yeni MDM yükü eski yük ile eşleşmiyor.

**Neden:** Cihazda bir yönetim profili zaten yüklü.

#### <a name="resolution"></a>Çözüm

1. **Settings** **Genel**  >  **cihaz yönetimi**> iOS/ıpados cihazında ayarları açın.
2. Var olan yönetim profiline dokunun ve **yönetimi kaldır**' a dokunun.
3. Cihazı yeniden kaydedin.

### <a name="noenrollmentpolicy"></a>NoEnrollmentPolicy

**Neden:** Apple Anında İletilen Bildirim Servisi (APNs) sertifikası eksik, geçersiz veya zaman aşımına uğradı.

#### <a name="resolution"></a>Çözüm
Intune 'a geçerli bir APNs sertifikası eklendiğini doğrulayın. Daha fazla bilgi için bkz. [iOS/ıpados kaydını ayarlama](ios-enroll.md).

### <a name="accountnotonboarded"></a>AccountNotOnboarded

**Neden:** Intune 'da yapılandırılmış Apple Anında Iletilen bildirim hizmeti (APNs) sertifikasıyla ilgili bir sorun var.

#### <a name="resolution"></a>Çözüm
APNs sertifikasını yenileyin ve sonra cihazı yeniden kaydedin.

> [!IMPORTANT]
> APNs sertifikasını yenilediğinizden emin olun. APNs sertifikasını değiştirme. Sertifikayı değiştirirseniz, tüm iOS/ıpados cihazlarını Intune 'a yeniden kaydetmeniz gerekir. 

- Tek başına Intune 'da APNs sertifikasını yenilemek için bkz. [Apple MDM anında iletme sertifikasını yenileme](apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate).
- Office 365 ' de APNs sertifikasını yenilemek için bkz. [iOS/ıpados cihazları Için APNs sertifikası oluşturma](https://support.office.com/article/Create-an-APNs-Certificate-for-iOS-devices-522b43f4-a2ff-46f6-962a-dd4f47e546a7).

### <a name="xpc_type_error-connection-invalid"></a>XPC_TYPE_ERROR bağlantı geçersiz

Kayıt profili atanan bir ADE ile yönetilen Cihazı açtığınızda, kayıt başarısız olur ve aşağıdaki hata iletisini alırsınız:

```
asciidoc
mobileassetd[83] <Notice>: 0x1a49aebc0 Client connection: XPC_TYPE_ERROR Connection invalid <error: 0x1a49aebc0> { count = 1, transaction: 0, voucher = 0x0, contents = "XPCErrorDescription" => <string: 0x1a49aee18> { length = 18, contents = "Connection invalid" } }
iPhone mobileassetd[83] <Notice>: Client connection invalid (Connection invalid); terminating connection
iPhone com.apple.accessibility.AccessibilityUIServer(MobileAsset)[288] <Notice>: [MobileAssetError:29] Unable to copy asset information from https://mesu.apple.com/assets/ for asset type com.apple.MobileAsset.VoiceServices.CombinedVocalizerVoices
iPhone mobileassetd[83] <Notice>: 0x1a49aebc0 Client connection: XPC_TYPE_ERROR Connection invalid <error: 0x1a49aebc0> { count = 1, transaction: 0, voucher = 0x0, contents = "XPCErrorDescription" => <string: 0x1a49aee18> { length = 18, contents = "Connection invalid" }
```

**Neden:** Cihaz ve Apple ADE hizmeti arasında bir bağlantı sorunu var.

#### <a name="resolution"></a>Çözüm
Bağlantı sorununu giderip cihazı kaydetmek için farklı bir ağ bağlantısı kullanın. Sorun devam ederse Apple ile iletişim kurmanız da gerekebilir.


## <a name="other-issues"></a>Diğer sorunlar

### <a name="ade-enrollment-doesnt-start"></a>ADE kaydı başlamıyor
Kayıt profili atanan bir ADE tarafından yönetilen Cihazı açtığınızda, Intune kayıt işlemi başlatılmaz.

**Neden:** Kayıt profili, ADE belirteci Intune 'a yüklenmeden önce oluşturulur.

#### <a name="resolution"></a>Çözüm

1. Kayıt profilini düzenleyin. Profilde herhangi bir değişiklik yapabilirsiniz. Amaç, profilin değiştirilme saatini güncelleştirmedir.
2. Ade ile yönetilen cihazları eşitleme: [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) **cihazlar**  >  **iOS**  >  **iOS kaydı**  >  **kayıt programı belirteçleri** ' ni seçin > bir belirteç > **Şimdi Eşitle**' yi seçin. Apple'a bir eşitleme isteği gönderilir.

### <a name="ade-enrollment-stuck-at-user-login"></a>Kullanıcı oturum açmada ADE kaydı takıldı
Kayıt profili atanan bir ADE ile yönetilen bir cihazı açtığınızda, kimlik bilgilerini girdikten sonra ilk kurulum açılır.

**Neden:** Multi-Factor Authentication (MFA) etkin. Şu anda MFA, ADE cihazlarındaki kayıt sırasında çalışmaz.

#### <a name="resolution"></a>Çözüm
MFA 'yı devre dışı bırakın ve ardından cihazı yeniden kaydedin.


## <a name="next-steps"></a>Sonraki adımlar

- [Intune'da cihaz kaydıyla ilgili sorunları giderme](troubleshoot-device-enrollment-in-intune.md)
- [Intune forumundan soru sorun](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Microsoft Intune destek ekibi blogunu denetleyin](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Microsoft Enterprise Mobility ve Security blogunu denetleyin](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)
