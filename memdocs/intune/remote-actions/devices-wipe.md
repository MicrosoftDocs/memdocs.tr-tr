---
title: Microsoft Intune - Azure kullanarak cihazları kullanımdan kaldırma veya silme | Microsoft Docs
description: Microsoft Intune kullanarak bir Android, Android iş profili, iOS/ıpados, macOS veya Windows cihazında bir cihazı devre dışı bırakma veya silme. Ayrıca cihazı Azure Active Directory'den de silin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 2/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4fdb787e-084f-4507-9c63-c96b13bfcdf9
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cbcd54a56304df36c536e5a623f4e9da5ba3f15b
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254699"
---
# <a name="remove-devices-by-using-wipe-retire-or-manually-unenrolling-the-device"></a>Silme, kullanımdan kaldırma veya el ile kaydını kaldırma yoluyla cihaz kaldırma

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**Kullanımdan kaldırma** veya **Silme** eylemlerini kullanarak artık ihtiyaç duyulmayan, başka amaçla kullanılacak olan veya kaybolan cihazları Intune’dan kaldırabilirsiniz. Kullanıcılar Intune'a kayıtlı cihazlara Intune Şirket Portalı’ndan uzaktan komut da verebilir.

> [!NOTE]
> Bir kullanıcıyı Azure Active Directory’den (Azure AD) kaldırmadan önce, bu kullanıcıyla ilişkili tüm cihazlar için **Silme** veya **Kullanımdan kaldırma** eylemlerini kullanın. Yönetilen cihazları olan kullanıcıları Azure AD’den kaldırırsanız Intune artık bu cihazları artık silemez veya kullanımdan kaldıramaz.

## <a name="wipe"></a>Silme

**Silme** eylemi, cihazı fabrika varsayılan ayarlarına geri yükler. **Kayıt durumu ve kullanıcı hesabını koru** onay kutusunu seçerseniz kullanıcı verileri saklanır. Aksi takdirde, tüm veriler, uygulamalar ve ayarlar kaldırılır.

|Silme eylemi|**Kayıt durumu ve kullanıcı hesabını koru**|Intune yönetiminden kaldırıldı|Açıklama|
|:-------------:|:------------:|:------------:|------------|
|**Silme**| İşaretli değil | Yes | Tüm kullanıcı hesapları, verileri, MDM ilkeleri ve ayarlarını siler. İşletim sistemini varsayılan durum ve ayarlarına sıfırlar.|
|**Silme**| İşaretli | No | Tüm MDM ilkelerini temizler. Kullanıcı hesapları ve verilerini saklar. Kullanıcı ayarlarını varsayılana sıfırlar. İşletim sistemini varsayılan durum ve ayarlarına sıfırlar.|


> [!NOTE]
> Silme eylemi, Kullanıcı kaydıyla kaydedilen iOS/ıpados cihazları için kullanılamaz.

**Kayıt durumu ve kullanıcı hesabını koru** seçeneği yalnızca Windows 10 sürüm 1709 veya sonraki sürümlerde kullanılabilir.

MDM ilkeleri, cihazın Intune’a bir sonraki bağlanışında yeniden uygulanır.

Silme, cihazı yeni bir kullanıcıya vermeden önce veya cihaz kaybolduğunda/çalındığında kullanışlıdır. **Silme** eylemini seçerken dikkatli olun. Cihazdaki veriler kurtarılamaz.

### <a name="wiping-a-device"></a>Bir cihazı silme

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Cihazlar** > **tüm cihazlar**' ı seçin.
4. Silme eylemini uygulamak istediğiniz cihazın adını seçin.
5. Cihaz adının gösterildiği bölmede **Sil**’i seçin.
6. Windows 10 sürüm 1709 veya üzeri için, ayrıca **silme cihazına sahip olursunuz, ancak kayıt durumunu ve ilişkili kullanıcı hesabı seçeneğini saklayın** . 
    
    |Silme sırasında tutuldu |Tutulmadı|
    | -------------|------------|
    |Cihazla ilişkilendirilen kullanıcı hesapları|Kullanıcı dosyaları|
    |Makine durumu \(etki alanına katılmış, Azure AD'ye katılmış)| Kullanıcı tarafından yüklenen uygulamalar \(mağaza ve Win32 uygulamaları)|
    |Mobil cihaz yönetimi (MDM) kaydı|Varsayılan olmayan cihaz ayarları|
    |OEM tarafından yüklenen uygulamalar \(mağaza ve Win32 uygulamaları)||
    |Kullanıcı profili||
    |Kullanıcı profili dışındaki kullanıcı verileri||
    |Kullanıcı otomatik oturum açma|| 
    
7. Cihazı **silme ve cihaz güç kaybediyor olsa bile temizlemeye devam et.** seçenek, cihazı kapatarak silme eyleminin atlalanmasına neden olur. Bu seçenek, başarılı olana kadar cihazı sıfırlamaya çalışmaya devam edecektir. Bazı yapılandırmalarda bu eylem cihazın [yeniden başlatılamamasından](troubleshoot-device-actions.md#wipe-action)çıkamayabilir.        
8. Silmeyi onaylamak için **Evet**’i seçin.

Cihaz açık ve bağlı olduğu sürece, **Silme** eylemi 15 dakikadan kısa süre içinde tüm cihaz türlerine yayılır.

## <a name="retire"></a>Devre Dışı Bırakma

**Kullanımdan kaldırma** eylemi; yönetilen uygulama verilerini (varsa), ayarlarını ve Intune kullanarak atanmış e-posta profillerini kaldırır. Cihaz Intune yönetiminden kaldırılır. Bu durum cihaz iade etme işlemi gerçekleştirdiğinde ve **Kullanımdan kaldırma** uzak eylemini aldığında ortaya çıkar. Cihaz, cihaz iade edilene kadar Intune 'da görünmeye devam eder. Eski cihazları hemen kaldırmak istiyorsanız, bunun yerine [silme eylemini](devices-wipe.md#delete-devices-from-the-intune-portal) kullanın.

**Kullanımdan kaldırma**, kullanıcının kişisel verilerini cihazda bırakır.  

Aşağıdaki tablolarda, hangi verilerin kaldırıldığı ve şirket verileri kaldırıldıktan sonra **Kullanımdan kaldırma** eyleminin cihazda kalan veriler üzerindeki etkisi açıklanır.

### <a name="ios"></a>iOS

|Veri türü|iOS|
|-------------|-------|
|Intune tarafından yüklenen şirket uygulamaları ve ilişkili veriler|**Şirket Portalı kullanılarak yüklenen uygulamalar:** Yönetim profiline sabitlenmiş uygulamalar için tüm uygulama verileri ve uygulamalar kaldırılır. Bu uygulamalar, başlangıçta App Store 'dan yüklenen ve daha sonra şirket uygulamaları olarak yönetilen uygulamaların yanı sıra uygulama cihaz kaldırma işleminden kaldırılmadığı sürece bu uygulamalara dahildir. <br /><br /> **Mobil uygulama yönetimini kullanan ve App Store 'dan yüklenen Microsoft uygulamaları:** Şirket Portalı tarafından yönetilmeyen uygulamalarda, uygulama yerel depolama alanındaki mobil uygulama yönetimi (MAM) şifrelemesi tarafından korunan şirket uygulama verileri kaldırılır. Uygulama dışında MAM şifrelemesi ile korunan veriler şifrelenmiş ve kullanılamaz durumda kalır ama kaldırılmaz. Kişisel uygulamalar ve bunların verileri kaldırılmaz.|
|Ayarlar|Intune ilkesi tarafından ayarlanan yapılandırmalar artık zorunlu tutulmaz. Kullanıcılar ayarları değiştirebilir.|
|Wi-Fi ve VPN profili ayarları|Kaldırıldı.|
|Sertifika profili ayarları|Sertifikalar kaldırılır ve iptal edilir.|
|Yönetim aracısı|Yönetim profili kaldırılır.|
|E-posta|Intune üzerinden sağlanan e-posta profilleri kaldırılır. Cihazın önbelleğindeki e-postalar silinir.|
|Azure AD'den ayrılma|Azure AD kaydı kaldırılır.|

### <a name="android-device-administrator"></a>Android cihaz yöneticisi

|Veri türü|Android|Android Samsung Knox Standard|
|-------------|-----------|------------------------|
|Web bağlantıları|Kaldırıldı.|Kaldırıldı.|
|Yönetilmeyen Google Play uygulamaları|Uygulamalar ve veriler yüklü kalır. <br /> <br />Yerel depolama alanında Mobil Uygulama Yönetimi (MAM) şifrelemesi ile korunan şirket uygulaması verileri kaldırılır. Uygulama dışında MAM şifrelemesi ile korunan veriler şifrelenmiş ve kullanılamaz durumda kalır ama kaldırılmaz. |Uygulamalar ve veriler yüklü kalır. <br /> <br />Yerel depolama alanında Mobil Uygulama Yönetimi (MAM) şifrelemesi ile korunan şirket uygulaması verileri kaldırılır. Uygulama dışında MAM şifrelemesi ile korunan veriler şifrelenmiş ve kullanılamaz durumda kalır ama kaldırılmaz.|
|Yönetilmeyen iş kolu uygulamaları|Uygulamalar ve veriler yüklü kalır.|Uygulamalar kaldırılır ve uygulamada yerel olarak bulunan veriler kaldırılır. Uygulama dışındaki (örneğin, SD kartındaki) hiçbir veri kaldırılmaz.|
|Yönetilen Google Play uygulamaları|Uygulama verileri kaldırılır. Uygulama kaldırılmaz. Uygulama dışında (örneğin, SD kartında) Mobil Uygulama Yönetimi (MAM) şifrelemesi ile korunan veriler şifrelenmiş ve kullanılamaz durumda kalır ama kaldırılmaz.|Uygulama verileri kaldırılır. Uygulama kaldırılmaz. Uygulama dışında (örneğin, SD kartında) MAM şifrelemesi ile korunan veriler şifrelenmiş durumda kalır ama kaldırılmaz.|
|Yönetilen iş kolu uygulamaları|Uygulama verileri kaldırılır. Uygulama kaldırılmaz. Uygulama dışında (örneğin, SD kartında) MAM şifrelemesi ile korunan veriler şifrelenmiş ve kullanılamaz durumda kalır ama kaldırılmaz.|Uygulama verileri kaldırılır. Uygulama kaldırılmaz. Uygulama dışında (örneğin, SD kartında) MAM şifrelemesi ile korunan veriler şifrelenmiş ve kullanılamaz durumda kalır ama kaldırılmaz.|
|Ayarlar|Intune ilkesi tarafından ayarlanan yapılandırmalar artık zorunlu tutulmaz. Kullanıcılar ayarları değiştirebilir.|Intune ilkesi tarafından ayarlanan yapılandırmalar artık zorunlu tutulmaz. Kullanıcılar ayarları değiştirebilir.|
|Wi-Fi ve VPN profili ayarları|Kaldırıldı.|Kaldırıldı.|
|Sertifika profili ayarları|Sertifikaları iptal edilir ama kaldırılmaz.|Sertifikalar kaldırılır ve iptal edilir.|
|Yönetim aracısı|Cihaz Yöneticisi ayrıcalığı iptal edilir.|Cihaz Yöneticisi ayrıcalığı iptal edilir.|
|E-posta|Yok (E-posta profilleri Android cihazları tarafından desteklenmez)|Intune üzerinden sağlanan e-posta profilleri kaldırılır. Cihazın önbelleğindeki e-postalar silinir.|
|Azure AD'den ayrılma|Azure AD kaydı kaldırılır.|Azure AD kaydı kaldırılır.|

### <a name="android-enterprise-devices-with-a-work-profile"></a>İş profiline sahip Android Kurumsal cihazları

Bir Android iş profili cihazdan şirket verilerinin kaldırılması, cihazdaki iş profilinde bulunan tüm verileri, uygulamaları ve ayarları kaldırır. Cihaz Intune yönetiminde devre dışı bırakıldı. Silme, Android iş profillerinde desteklenmez.

### <a name="android-enterprise-dedicated-devices"></a>Android kurumsal adanmış cihazlar

Yalnızca bilgi noktası cihazlarını silebilirsiniz. Android bilgi noktası cihazlarını kullanımdan kaldıramazsınız.


### <a name="macos"></a>Mac OS

|Veri türü|Mac OS|
|-------------|-------|
|Ayarlar|Intune ilkesi tarafından ayarlanan yapılandırmalar artık zorunlu tutulmaz. Kullanıcılar ayarları değiştirebilir.|
|Wi-Fi ve VPN profili ayarları|Kaldırıldı.|
|Sertifika profili ayarları|MDM üzerinden dağıtılan sertifikalar kaldırılır ve iptal edilir.|
|Yönetim aracısı|Yönetim profili kaldırılır.|
|Outlook|Koşullu erişim etkinse, cihaz yeni e-posta almaz.|
|Azure AD'den ayrılma|Azure AD kaydı kaldırılır.|

### <a name="windows"></a>Windows

|Veri türü|Windows 8.1 (MDM) ve Windows RT 8.1|Windows RT|Windows Phone 8.1 ve Windows Phone 8|Windows 10|
|-------------|----------------------------------------------------------------|--------------|-----------------------------------------|--------|
|Intune tarafından yüklenen şirket uygulamaları ve ilişkili veriler|EFS tarafından korunan dosyalar için anahtarlar iptal edilir. Kullanıcı dosyaları açamaz.|Şirket uygulamaları kaldırılmaz.|Başlangıçta Şirket Portalı üzerinden yüklenen uygulamalar kaldırılır. Şirket uygulama verileri kaldırılır.|Uygulamalar kaldırılır. Dışarıdan yükleme anahtarları kaldırılır.<br>Windows 10 sürüm 1709 (Creators Update) ve üzeri için Microsoft 365 uygulamalar kaldırılmaz. Kaydı kaldırılan cihazlardaki Intune yönetim uzantısıyla yüklenmiş olan Win32 uygulamaları kaldırılmaz. Yöneticiler, KCG cihazlarına Win32 uygulamalarını sunmamak amacıyla bunları atamadan hariç tutma seçeneğini değerlendirebilir.|
|Ayarlar|Intune ilkesi tarafından ayarlanan yapılandırmalar artık zorunlu tutulmaz. Kullanıcılar ayarları değiştirebilir.|Intune ilkesi tarafından ayarlanan yapılandırmalar artık zorunlu tutulmaz. Kullanıcılar ayarları değiştirebilir.|Intune ilkesi tarafından ayarlanan yapılandırmalar artık zorunlu tutulmaz. Kullanıcılar ayarları değiştirebilir.|Intune ilkesi tarafından ayarlanan yapılandırmalar artık zorunlu tutulmaz. Kullanıcılar ayarları değiştirebilir.|
|Wi-Fi ve VPN profili ayarları|Kaldırıldı.|Kaldırıldı.|Desteklenmiyor.|Kaldırıldı.|
|Sertifika profili ayarları|Sertifikalar kaldırılır ve iptal edilir.|Sertifikalar kaldırılır ve iptal edilir.|Desteklenmiyor.|Sertifikalar kaldırılır ve iptal edilir.|
|E-posta|EFS'nin etkinleştirildiği e-postalar kaldırılır. Bunlar, Windows için Posta uygulamasındaki e-postalar ve eklerdir.|Desteklenmiyor.|Intune üzerinden sağlanan e-posta profilleri kaldırılır. Cihazın önbelleğindeki e-postalar silinir.|EFS'nin etkinleştirildiği e-postalar kaldırılır. Bunlar, Windows için Posta uygulamasındaki e-postalar ve eklerdir. Intune tarafından sağlanan posta hesaplarını kaldırır.|
|Azure AD'den ayrılma|Hayır.|Hayır.|Azure AD kaydı kaldırılır.|Azure AD kaydı kaldırılır.|

> [!NOTE]
> İlk kurulum (OOBE) sırasında Azure AD 'ye eklenen Windows 10 cihazlarında, devre dışı bırakma komutu cihazdan tüm Azure AD hesaplarını kaldırır. Yerel yönetici olarak oturum açmak ve kullanıcının yerel verilerine yeniden erişim kazanmak için [Bilgisayarınızı güvenli modda başlatma bölümündeki](https://support.microsoft.com/en-us/help/12376/windows-10-start-your-pc-in-safe-mode) adımları izleyin. 

### <a name="retire"></a>Devre Dışı Bırakma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihazlar** bölmesinde **Tüm cihazlar**'ı seçin.
3. Kullanımdan kaldırma eylemini uygulamak istediğiniz cihazın adını seçin.
4. Cihaz adının gösterildiği bölmede **Kullanımdan kaldır**’ı seçin. Onaylamak için **Evet**'i seçin.

Cihaz açık ve bağlı olduğu sürece, **Kullanımdan kaldırma** eylemi 15 dakikadan kısa süre içinde tüm cihaz türlerine yayılır.

## <a name="delete-devices-from-the-intune-portal"></a>Cihazları Intune portalından silme

Cihazları Intune portalından kaldırmak istiyorsanız, bunları belirli bir cihaz bölmesinden silebilirsiniz. Cihazın bir sonraki iade edilişinde, üzerindeki tüm şirket verileri kaldırılır.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihazlar** > **tüm cihazlar** ' ı seçin > silmek istediğiniz cihazları seçin > **silin**.

### <a name="automatically-delete-devices-with-cleanup-rules"></a>Temizleme kuralları ile cihazları otomatik olarak silme
Intune’u etkin olmayan, eski veya yanıt vermeyen cihazları otomatik olarak silmek üzere yapılandırabilirsiniz. Bu temizleme kuralları, cihaz kayıtlarınızın güncel kalması için cihazınızı kesintisiz bir şekilde izler. Bu şekilde silinen cihazlar, Intune yönetiminden kaldırılır.
1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihazlar** > **cihaz temizleme kuralları** > **Evet**' i seçin.
3. **Bu çok gün için iade edilmemiş cihazlarda silme** kutusuna 30 ile 270 arasında bir sayı girin.
4. **Kaydet**'i seçin.



## <a name="delete-devices-from-the-azure-active-directory-portal"></a>Azure Active Directory portalından cihazları silme

İletişim sorunları veya eksik cihazlar nedeniyle, cihazları Azure AD'den silmeniz gerekebilir. Ulaşılamaz olduğunu ve Azure ile yeniden iletişim kurmasının pek olası olmadığını bildiğiniz cihazlarda, cihaz kayıtlarını Azure portalından kaldırmak için **Sil** eylemini kullanabilirsiniz. **Sil** eylemi, cihazı yönetimden kaldırmaz.

1. Yönetici kimlik bilgilerinizi kullanarak [Azure portalında Azure Active Directory](https://aka.ms/accessaad)’de oturum açın. Ayrıca [Microsoft 365 yönetim merkezinde](https://admin.microsoft.com) de oturum açabilirsiniz. Menüden **Yönetim Merkezleri** > **Azure AD**' yi seçin.
2. Hesabınız yoksa bir Azure aboneliği oluşturun. Ücretli bir hesabınız varsa, bu işlem için kredi kartı veya ödeme gerekmez ( **Ücretsiz Azure Active Directory kaydınız** abonelik bağlantısını seçin).
3. **Azure Active Directory**’yi ve sonra da kuruluşunuzu seçin.
4. **Users (Kullanıcılar)** sekmesini seçin.
5. Silmek istediğiniz cihazla ilişkilendirilmiş olan kullanıcıyı seçin.
6. **Cihazlar**’ı seçin.
7. Gereken cihazları kaldırın. Örneğin, artık kullanımda olmayan veya tanımları yanlış olan cihazları kaldırabilirsiniz.

## <a name="retire-an-apple-dep-device-from-intune"></a>Intune’daki Apple DEP cihazını devre dışı bırakma

Apple DEP cihazını Intune yönetiminden tamamen kaldırmak istiyorsanız bu adımları izleyin:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihazlar** > **tüm cihazlar** ' ı seçin > **devre dışı**> cihaz seçin.
![Kullanımdan kaldırma ekran görüntüsü](./media/devices-wipe/retire.png)
3. [Business.Apple.com](http://business.apple.com) adresini ziyaret edin ve cihazın seri numarasına göre arama yapın.
4. **Atanan** menüsünde **Atanmış**’ı seçin.

5. **Yeniden Ata**’yı seçin.

    ![Apple yeniden atama ekran görüntüsü](./media/devices-wipe/apple-reassign.png)

## <a name="device-states"></a>Cihaz durumları
Cihaz durumlarının açıklaması için, bkz. [Managementstates koleksiyonu](../developer/intune-data-warehouse-collections.md#managementstates).

## <a name="fresh-start"></a>Yeni Başlangıç

Windows 10 cihazlarda kullanılabilir. [Yeni Başlangıç](device-fresh-start.md) hakkında daha fazla bilgi edinin.

## <a name="next-steps"></a>Sonraki adımlar

Silinen cihazı yeniden kaydetmek istiyorsanız bkz. [Kayıt seçenekleri](../enrollment/enrollment-options.md).

