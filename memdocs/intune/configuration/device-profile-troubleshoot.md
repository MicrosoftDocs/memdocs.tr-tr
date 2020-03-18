---
title: Microsoft Intune - Azure’da cihaz profillerinde sorun giderme | Microsoft Docs
description: Cihaz ilkeleri ve profillerle ilgili yaygın sorular ve yanıtlar, Kullanıcı veya cihazlara uygulanmadı, yeni ilkelerin cihazlara itilmesi ne kadar sürer, birden çok ilke olduğunda hangi ayarlar uygulanır, bir profil silinir veya kaldırılır ve Microsoft Intune daha fazla.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67d0d271b5befc65ad286a8da6e00f647973d73d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333134"
---
# <a name="common-questions-issues-and-resolutions-with-device-policies-and-profiles-in-microsoft-intune"></a>Microsoft Intune 'deki cihaz ilkeleri ve profillerle ilgili yaygın sorular, sorunlar ve çözümler

Intune 'da cihaz profilleri ve ilkeleriyle çalışırken sık sorulan soruların yanıtlarını alın. Bu makalede ayrıca iade zaman aralıkları listelenmekte, çakışmalar üzerinde daha fazla detaın ve daha fazlası verilmektedir.

## <a name="why-doesnt-a-user-get-a-new-profile-when-changing-a-password-or-passphrase-on-an-existing-wi-fi-profile"></a>Bir kullanıcı, mevcut bir Wi-Fi profilinde parola değiştirirken neden yeni bir profil almıyor?

Şirket Wi-Fi profili oluşturur, profili bir gruba dağıtır, parolayı değiştirir ve profili kaydedersiniz. Profil değiştiğinde, bazı kullanıcılar yeni profili alamayabilir.

Bu sorunu azaltmak için konuk Wi-Fi kurulumu yapın. Şirket Wi-Fi başarısız olursa, kullanıcılar konuk Wi-Fi ile bağlanabilir. Otomatik bağlanma ayarlarının tümünü etkinleştirdiğinizden emin olun. Konuk Wi-Fi profilini tüm kullanıcılara dağıtın.

Bazı ek öneriler:  

- Bağlanmakta olduğunuz Wi-Fi ağı bir parola veya parola kullanıyorsa, Wi-Fi yönlendiricisine doğrudan bağlanabildiğinizden emin olun. İOS/ıpados cihazından test edebilirsiniz.
- Bir Wi-Fi uç noktasına (Wi-Fi yönlendiricisi) başarıyla bağlandıktan sonra SSID’yi ve kullanılan kimlik bilgilerini (bu değer erişim kodu veya paroladır) not edin.
- SSID ve kimlik bilgilerini (parola) Önceden Paylaşılan Anahtar alanına girin. 
- Profili, tercihen yalnızca BT ekibinden oluşan, sınırlı sayıda kullanıcıları olan bir test grubuna dağıtın. 
- İOS/ıpados cihazınızı Intune 'a eşitleyin. Daha önce kaydolmadıysanız kaydolun. 
- Aynı Wi-Fi uç noktasına bağlantıyı (ilk adımda bahsedildiği gibi) tekrar test edin.
- Daha büyük gruplara veya sonuçta kuruluşunuzdaki tüm beklenen kullanıcılara dağıtın. 

## <a name="how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned"></a>Cihazların, atandıktan sonra bir ilke, profil veya uygulamayı alması ne kadar sürer?

Intune, cihaza Intune hizmetini iade etme konusunda bilgilendirir. Bildirim süreleri, en fazla birkaç saate kadar değişir. Bu bildirim süreleri de platformlar arasında farklılık gösterir.

Bir cihaz, ilk bildirimden sonra ilkeyi veya profili almak için iade vermezse, Intune üç denemeden daha fazlasını yapar. Kapalı veya bir ağa bağlı olmayan gibi çevrimdışı bir cihaz bildirimleri alamayabilir. Bu durumda cihaz, ilkeyi veya profili Intune hizmeti ile bir sonraki zamanlanmış iadede alır. Aynı şekilde, uyumlu olmayan bir duruma geçiş yapan cihazlar dahil, uyumsuzluğun denetimi için de geçerlidir.

**Tahmini** Sıklık:

| Platfveyam | Döngü süresi|
| --- | --- |
| iOS/iPadOS | Her 8 saatte bir |
| Mac OS | Her 8 saatte bir |
| Android | Her 8 saatte bir |
| Cihaz olarak kaydedilen Windows 10 bilgisayarlar | Her 8 saatte bir |
| Windows Phone | Her 8 saatte bir |
| Windows 8.1 | Her 8 saatte bir |

Cihaz son zamanlarda kaydedildiyse, uyumluluk, uyumsuzluk ve yapılandırma iadede daha sık çalışır ve bu da **tahmin** edilir:

| Platfveyam | Sıklık |
| --- | --- |
| iOS/iPadOS | 1 saat boyunca 15 dakikada bir ve daha sonra 8 saatte bir |  
| Mac OS | 1 saat boyunca 15 dakikada bir ve daha sonra 8 saatte bir | 
| Android | 15 dakika boyunca 3 dakikada bir, sonra 2 saat boyunca 15 dakikada bir ve daha sonra 8 saatte bir | 
| Cihaz olarak kaydedilen Windows 10 bilgisayarlar | 15 dakika boyunca 3 dakikada bir, sonra 2 saat boyunca 15 dakikada bir ve daha sonra 8 saatte bir | 
| Windows Phone | 15 dakika boyunca 5 dakikada bir, sonra 2 saat boyunca 15 dakikada bir ve daha sonra 8 saatte bir | 
| Windows 8.1 | 15 dakika boyunca 5 dakikada bir, sonra 2 saat boyunca 15 dakikada bir ve daha sonra 8 saatte bir | 

Herhangi bir zamanda kullanıcılar, ilke veya profil güncelleştirmelerini anında denetlemek için Şirket Portalı uygulaması, **ayarlar** > **eşitleme** ' yi açabilir.

## <a name="what-actions-cause-intune-to-immediately-send-a-notification-to-a-device"></a>Hangi eylemler cihaza Intune tarafından anında bildirim gönderilmesine neden olur?

Bir ilke, profil veya uygulamanın atanma (veya atanmamış), güncelleştirildiği, silindiği vb. gibi bir bildirimi tetikleyen farklı eylemler vardır. Bu eylem süreleri platformlar arasında farklılık gösterir.

Cihazlar, iade etme ya da zamanlanan iade sırasında bir bildirim aldıklarında Intune 'a giriş yapılır. Bir cihazı veya kullanıcıyı kilit, geçiş kodu sıfırlama, uygulama, profil veya ilke atama gibi bir eylemle hedeflediğinizde, Intune bu güncelleştirmeleri hemen almak için cihazı iade etmek üzere bilgilendirir.

Şirket Portalı uygulamasındaki iletişim bilgilerinin düzeltilmesi gibi diğer değişiklikler, cihazlara anında bildirim gönderilmesine neden olmaz.

İlke veya profildeki ayarlar her iadede uygulanır. [Windows 10 MDM ilke yenileme blog gönderisi](https://www.petervanderwoude.nl/post/windows-10-mdm-policy-refresh/) iyi bir kaynak olabilir.

## <a name="if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied"></a>Aynı kullanıcı veya cihaza birden çok ilke atanıyorsa hangi ayarların uygulanacağını nasıl bilebilirim?

Aynı kullanıcı veya cihaza iki veya daha fazla ilke atandığında, uygulanan ayar ayrı ayar düzeyinde gerçekleşir:

- Uyumluluk ilkesi ayarları her zaman yapılandırma profili ayarlarından önceliklidir.

- Bir uyumluluk ilkesi başka bir uyumluluk ilkesindeki aynı ayarla değerlendirilirse, en kısıtlayıcı uyumluluk ilkesi ayarı uygulanır.

- Bir yapılandırma ilkesi ayarı başka bir yapılandırma ilkesindeki bir ayarla çakışırsa, bu çakışma Intune 'da gösterilir. Bu çakışmaları el ile çözün.

## <a name="what-happens-when-app-protection-policies-conflict-with-each-other-which-one-is-applied-to-the-app"></a>Uygulama koruma ilkeleri birbiriyle çakışırsa ne olur? Uygulamaya hangisi uygulanır?

Çakışma değerleri, sıfırlamadan önce PIN denemeleri gibi sayı girişi alanları *hariç* olmak üzere, bir uygulama koruma ilkesinde bulunan en kısıtlayıcı ayarlardır. Sayı girişi alanları, önerilen ayarlar seçeneğini kullanarak bir MAM ilkesi oluşturmuşu gibi değerlerle aynı şekilde ayarlanır.

İki profil ayarı aynı olduğunda çakışmalar meydana gelir. Örneğin, kopyala/yapıştır ayarı dışında birbirinin aynı olan iki MAM ilkesi yapılandırdığınızı düşünün. Bu senaryoda, kopyala/yapıştır ayarı en kısıtlayıcı değer olarak ayarlanır, ancak ayarların geri kalanı yapılandırıldığı gibi uygulanır.

Bir ilke uygulamaya dağıtılır ve devreye girer. İkinci bir ilke dağıtılır. Bu senaryoda, ilk ilke öncelik kazanır ve uygulanır. İkinci ilke bir çakışma gösterir. Her ikisi de aynı anda uygulanırsa, önceki ilke olmadığında, her ikisi de çakışmadır. Çakışmadaki ayarlarda, en kısıtlayıcı olan değerler kullanılır.

## <a name="what-happens-when-iosipados-custom-policies-conflict"></a>İOS/ıpados özel ilkeleri çakıştığında ne olur?

Intune, Apple yapılandırma dosyalarının veya özel bir Open Mobile Alliance Tekdüzen Kaynak Tanımlayıcısı (OMA-URI) ilkesinin yükünü değerlendirmez. Yalnızca bir teslim mekanizması olarak görev yapar.

Özel bir ilke atadığınızda, yapılandırılan ayarların uyumluluk, yapılandırma veya diğer özel ilkelerle çakışmadığından emin olun. Özel bir ilke ve ayarları çakışıyorsa, ayarlar rastgele uygulanır.

## <a name="what-happens-when-a-profile-is-deleted-or-no-longer-applicable"></a>Bir profil silindiğinde veya artık geçerli olmadığında ne olur?

Bir profili sildiğinizde veya bir cihazı profilin bulunduğu bir gruptan kaldırdığınızda, profil ve Ayarlar cihazdan şu şekilde kaldırılır:

- Wi-Fi, VPN, sertifika ve e-posta profilleri: Bu profiller tüm desteklenen kayıtlı cihazlardan kaldırılır.
- Diğer tüm profil türleri:  

  - **Windows ve Android cihazları**: Ayarlar cihazdan kaldırılmaz
  - **Windows Phone 8.1 cihazları**: Aşağıdaki ayarlar kaldırılır:  
  
    - Mobil cihazların kilidini açmak için bir parola gerektir
    - Basit parolalara izin ver
    - Parola uzunluğu alt sınırı
    - Gerekli parola türü
    - Parola geçerlilik süresi (gün)
    - Parola geçmişini anımsa
    - Cihaz temizlenmeden önce izin verilen yinelenen oturum açma hatası sayısı
    - Parola istenmeden önce geçen işlem yapılmayan dakika sayısı
    - Gerekli parola türü – minimum karakter kümesi sayısı
    - Kameraya izin ver
    - Cihazda şifrelemeyi gerektir
    - Çıkarılabilir depolama birimine izin ver
    - Web tarayıcısına izin ver
    - Uygulama mağazasına izin ver
    - Ekran yakalamaya izin ver
    - Coğrafi konuma izin ver
    - Microsoft Hesabına izin ver
    - Kopyalama ve yapıştırmaya izin ver
    - Wi-Fi İnternet paylaşımına izin ver
    - Ücretsiz Wi-Fi etkin noktalarına otomatik olarak bağlanmaya izin ver
    - Wi-Fi etkin noktası bildirimine izin ver
    - Silmeye izin ver
    - Bluetooth'a izin ver
    - NFC'ye izin ver
    - Wi-Fi'a izin ver

  - **iOS/ıpados**: aşağıdakiler dışında tüm ayarlar kaldırılır:
  
    - Sesli dolaşıma izin ver
    - Veri dolaşımına izin ver
    - Dolaşım sırasında otomatik eşitlemeye izin ver

## <a name="i-changed-a-device-restriction-profile-but-the-changes-havent-taken-effect"></a>Cihaz kısıtlama profilini değiştirdim ama değişiklikler uygulanmadı

Windows Phone cihazlar bir kez ayarlandıktan sonra MDM veya EAS kullanılarak ayarlanan güvenlik ilkelerine güvenlik altına düşmesini sağlar. Örneğin, **en az sayıda karakter parolası** 8 olarak ayarlanır. Bunu 4 ' e azaltmayı deneyin. Cihaza daha kısıtlayıcı olan profil zaten uygulandı.

Profili daha az güvenli bir değerle değiştirmek için güvenlik ilkelerini sıfırlayın. Örneğin, Windows 8.1 Masaüstünde, sağ tarafta içeri doğru kaydırın > **ayarlar** > **Denetim Masası**' nı seçin. **Kullanıcı Hesapları** uygulamasını seçin. Sol taraftaki gezinti menüsünde **güvenlik Ilkelerini Sıfırla** bağlantısı vardır (en alta doğru). Bunu seçin ve ardından **İlkeleri Sıfırla**’yı seçin.

Android, Windows Phone 8,1 ve üzeri, iOS/ıpados ve Windows 10 gibi diğer MDM cihazlarının devre dışı bırakılması ve daha az kısıtlayıcı bir profil uygulamak için Intune 'a yeniden kaydedilmesi gerekebilir.

## <a name="some-settings-in-a-windows-10-profile-return-not-applicable"></a>Windows 10 profilindeki bazı ayarlar "uygulanamaz" olarak döndürülür

Windows 10 cihazlarında bazı ayarlar "uygulanamaz" olarak gösterilebilir. Bu durumda, bu belirli ayar cihazda çalışan Windows sürümü veya sürümünde desteklenmez. Bu ileti aşağıdaki nedenlerden kaynaklanabilir:

- Ayar, cihazdaki geçerli işletim sistemi (OS) sürümü değil, yalnızca Windows 'un daha yeni sürümlerinde kullanılabilir.
- Bu ayar yalnızca belirli Windows sürümleri veya giriş, profesyonel, kurumsal ve eğitim gibi belirli SKU 'Lar için kullanılabilir.

Farklı ayarların sürümü ve SKU gereksinimleri hakkında daha fazla bilgi edinmek için bkz. [yapılandırma hizmeti sağlayıcısı (CSP) başvurusu](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).

## <a name="next-steps"></a>Sonraki adımlar

Ek yardım mı gerekiyor? Bkz. [Microsoft Intune için destek alma](../fundamentals/get-support.md).
