---
title: Cihaz kaydıyla ilgili sorunları giderme
titleSuffix: Microsoft Intune
description: Microsoft Intune 'de cihaz kaydı sorunlarını gidermeye yönelik öneriler.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/09/2018
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6982ba0e-90ff-4fc4-9594-55797e504b62
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic;seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5c0aadb15587822ca2500ec477b6264ce4e96ed2
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993531"
---
# <a name="troubleshoot-device-enrollment-in-microsoft-intune"></a>Microsoft Intune cihaz kaydı sorunlarını giderme

Bu makalede [cihaz kayıt](device-enrollment.md) sorunlarını gidermeye yönelik öneriler sunulmaktadır. Bu bilgiler sorununuzu çözmezse, yardım almanın diğer yollarını öğrenmek için bkz. [Microsoft Intune için destek alma](../fundamentals/get-support.md).

## <a name="initial-troubleshooting-steps"></a>İlk sorun giderme adımları

Sorun gidermeye başlamadan önce, Intune’u kayıt sağlamak üzere doğru şekilde yapılandırdığınızdan emin olmak için kontrol edin. Bu yapılandırma gereksinimleri hakkında daha fazla bilgi edinebilirsiniz:

- [Microsoft Intune’da cihazları kaydetmeye hazırlanma](../fundamentals/setup-steps.md)
- [İOS/ıpados ve Mac cihaz yönetimini ayarlama](ios-enroll.md)
- [Windows cihaz yönetimini ayarlama](windows-enroll.md)
- [Android cihaz yönetimini ayarlama](android-enroll.md) - Ek adım gerekmez

Ayrıca kullanıcının cihazında saatin ve tarihin doğru ayarlandığından emin olabilirsiniz:

1. Cihazı yeniden başlatın.
2. Saatin ve tarihin, son kullanıcının saat dilimine göre GMT standartlarına yakın (+ veya - 12 saat) olarak ayarlandığından emin olun.
3. Intune şirket portalını kaldırın ve yeniden yükleyin (varsa).

Yönetilen cihaz kullanıcılarınız, gözden geçirmeniz için kayıt ve tanılama günlüklerini toplayabilir. Kullanıcılar için günlükleri toplama yönergeleri, şu konu başlıkları altında sağlanır:

- [Android kayıt hatalarını BT yöneticinize gönderme](../user-help/send-logs-to-your-it-admin-using-cable-android.md)
- [BT yöneticinize iOS/ıpados hataları gönderme](../user-help/send-errors-to-your-it-admin-ios.md)


## <a name="general-enrollment-issues"></a>Genel kayıt sorunları
Bu sorunlar, tüm cihaz platformlarında oluşabilir.

### <a name="device-cap-reached"></a>Cihaz sınırına ulaşıldı
**Sorun:** Kullanıcı kayıt sırasında bir hata alıyor ( **Şirket portalı geçici olarak kullanılamıyor**).

**Çözünürlüğüne**

#### <a name="check-number-of-devices-enrolled-and-allowed"></a>Kaydedilen ve izin verilen cihazların sayısını denetleme

Aşağıdaki adımları izleyerek kullanıcıya cihaz sayısı üst sınırını aşan sayıda cihaz atanıp atanmadığını denetleyin:

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **cihazlar**  >  **Kayıt kısıtlamaları**  >  **cihaz sınırı kısıtlamaları**' nı seçin. **Cihaz sınırı** sütunundaki değeri not alın.

2. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **Kullanıcılar**  >  **tüm kullanıcılar** ' ı seçin > Kullanıcı > **cihazları**seçin. Cihaz sayısını not alın.

3. Kullanıcının kayıtlı cihaz sayısı zaten cihaz sınır kısıtlamasına eşitse, şu ana kadar kaydolamazlar:
    - [Mevcut cihazlar kaldırılır](../remote-actions/devices-wipe.md) veya
    - [Cihaz kısıtlamalarını ayarlayarak](enrollment-restrictions-set.md) cihaz sınırını artırırsınız.

Cihaz sınırlarına ulaşmaktan kaçınmak için, eski cihaz kayıtlarını kaldırmaya dikkat edin.

> [!NOTE]
> 
> Cihaz kaydı için üst sınır uygulanmasını istemiyorsanız [Şirkete ait cihazları Microsoft Intune’da Cihaz Kayıt Yöneticisi’ne kaydetme](device-enrollment-manager-enroll.md) bölümünde açıklandığı gibi Cihaz Kayıt Yöneticisi hesabı kullanabilirsiniz.
> 
> Bir kullanıcı oturumu için Koşullu Erişim ilkesi zorunlu tutulduysa, söz konusu kullanıcı hesabı, Cihaz Kayıt Yöneticileri hesabına eklendiğinde kaydı tamamlayamaz.

### <a name="company-portal-temporarily-unavailable"></a>Şirket Portalı Geçici Olarak Devre Dışı
**Sorun:** Kullanıcılar, cihazlarında **Şirket Portalı Geçici Olarak Devre Dışı** hatası alıyor.

**Çözünürlüğüne**

1. Intune Şirket Portalı uygulamasını cihazınızdan kaldırın.

2. Cihazda, tarayıcıyı açın, [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com) bir Kullanıcı oturumu açmayı deneyin ve oturum açın.

3. Kullanıcı oturum açamazsa, başka bir ağ denemelidir.

4. Başarısız olursa, kullanıcının kimlik bilgilerinin Azure Active Directory doğru şekilde eşitlendiğini doğrulayın.

5. Kullanıcı başarıyla oturum açarsa, bir iOS/ıpados cihazı Intune Şirket Portalı uygulamasını yüklemenizi ve kaydolmasını ister. Bir Android cihazında kaydetmeyi yeniden denemeden önce Intune Şirket Portalı uygulamasını el ile yüklemeniz gerekir.

### <a name="mdm-authority-not-defined"></a>MDM yetkilisi tanımlı değil
**Sorun:** Bir kullanıcı, **MDM yetkilisi tanımlı değil** hatası alıyor.

**Çözünürlüğüne**

1. MDM Yetkilisinin [uygun şekilde ayarlandığını](../fundamentals/mdm-authority-set.md) doğrulayın.
    
2. Kullanıcının kimlik bilgilerinin Azure Active Directory doğru şekilde eşitlendiğinden emin olun. Kullanıcı UPN 'nin, Microsoft 365 yönetim merkezindeki Active Directory bilgileriyle eşleştiğini doğrulayabilirsiniz.
    UPN Active Directory bilgileriyle eşleşmiyorsa:

    1. Yerel sunucuda DirSync’i kapatın.

    2. Eşleşmeyen kullanıcıyı **Intune Hesap Portalı** kullanıcı listesinden silin.

    3. Azure hizmetinin yanlış verileri kaldırması için bir saat kadar bekleyin.

    4. DirSync’i yeniden açın ve şimdi kullanıcının doğru eşitlenip eşitlenmediğini denetleyin.

### <a name="unable-to-create-policy-or-enroll-devices-if-the-company-name-contains-special-characters"></a>Şirket adı özel karakterler içeriyorsa ilke oluşturulamaz veya cihazlar kaydedilemez
**Sorun:** İlke oluşturamıyor veya cihazları kaydedemiyorsunuz.

**Çözüm:** [Microsoft 365 Yönetim merkezinde](https://admin.microsoft.com/), şirket adından özel karakterleri kaldırın ve şirket bilgilerini kaydedin.

### <a name="unable-to-sign-in-or-enroll-devices-when-you-have-multiple-verified-domains"></a>Birden çok doğrulanmış etki alanınız olduğunda oturum açılamaz veya cihazlar kaydedilemez
**Sorun:** Bu sorun, ADFS'nize ikinci bir doğrulanmış etki alanı eklediğinizde oluşabilir. İkinci etki alanının kullanıcı asıl adı (UPN) sonekini taşıyan kullanıcılar portallarda oturum açamayabilir veya cihaz kaydedemeyebilir.


<strong>Çözüm:</strong> Microsoft 365 müşteriler, her sonek için AD FS 2,0 Federasyon Hizmeti ayrı bir örneğini dağıtmaları gerekir:
- AD FS 2.0 aracılığıyla çoklu oturum açma (SSO) kullanma
- kuruluşlarında kullanıcı UPN sonekleri için birden çok en üst düzey etki alanına sahip olma (örneğin @contoso.com veya @fabrikam.com).


AD FS sunucusunun bu senaryoyu ek AD FS 2.0 sunucularına gerek kalmadan destekleyebilmesi için, bir [AD FS 2.0 dağıtımı](https://support.microsoft.com/kb/2607496)<strong>SupportMultipleDomain</strong> anahtarıyla birlikte çalışır. Daha fazla bilgi için [Bu bloga](/archive/blogs/abizerh/supportmultipledomain-switch-when-managing-sso-to-office-365)bakın.


## <a name="android-issues"></a>Android sorunları

### <a name="android-enrollment-errors"></a>Android kayıt hataları

Son kullanıcıların Android cihazları Intune’a kaydederken karşılaşabileceği hatalar aşağıdaki tabloda listelenmiştir.

|Hata iletisi|Sorun|Çözüm|
|---|---|---|
|**Erişim için BT yöneticisinin lisans ataması gerekiyor**<br>BT yöneticiniz bu uygulamayı kullanmanız için size erişim vermemiş. BT yöneticinizden yardım isteyin veya daha sonra tekrar deneyin.|Cihaz kaydedilemiyor çünkü bu kullanıcının hesabında gerekli lisans yok.|Cihazlar kaydedilmeden önce kullanıcılara gerekli lisans atanmış olmalıdır. Bu ileti kullanıcının mobil cihaz yönetimi yetkilisi için yanlış lisans türüne sahip olduğu anlamına gelir. Örneğin aşağıdakilerin her ikisi de doğruysa kullanıcı bu hatayı görür:<ol><li>Intune mobil cihaz yönetim yetkilisi olarak ayarlanmıştır</li><li>Kullanıcı System Center 2012 R2 Configuration Manager lisansı kullanmaktadır.</li></ol>Daha fazla bilgi için bkz. [Kullanıcı hesaplarınıza Intune lisansları atama](/intune/licenses-assign).|
|**BT yöneticisinin MDM yetkilisini ayarlaması gerekiyor**<br>Görünüşe göre BT yöneticiniz MDM yetkilisi ayarlamamış. BT yöneticinizden yardım isteyin veya daha sonra tekrar deneyin.|Mobil cihaz yönetim yetkilisi tanımlanmamış.|Mobil cihaz yönetim yetkilisi Intune'da ayarlanmamış. [Mobil cihaz yönetimi yetkilisini ayarlama](/intune/mdm-authority-set) hakkında bilgi edinin.|


### <a name="devices-fail-to-check-in-with-the-intune-service-and-display-as-unhealthy-in-the-intune-admin-console"></a>Cihazlar Intune hizmetini denetlemiyor ve Intune yönetici konsolunda "Uygun olmayan durumda" olarak görüntüleniyor
**Sorun:** Android sürüm 4.4.x ve 5.x çalıştıran bazı Samsung cihazlar, Intune hizmetini denetlemeyi durdurabiliyor. Hizmeti denetlemeyen cihazlar:

- Intune hizmetinden ilke, uygulama ve uzak komutları alamaz.
- Yönetici konsolunda Yönetim Durumu olarak **Uygun olmayan durumda** görüntülenir.
- Koşullu erişim ilkeleriyle korunan kullanıcılar şirket kaynaklarına erişimi kaybedebilir.

Belirli Samsung cihazlara yüklü gelen Samsung Smart Manager yazılımı, Şirket Portalı uygulamasını ve bileşenlerini devre dışı bırakabilmektedir. Şirket Portalı devre dışı bırakıldığında arka planda çalışamaz ve Intune hizmetine bağlanamaz.

**Çözüm #1:**

Kullanıcılarınız Şirket Portalı uygulamasını el ile başlatmalarını söyleyin. Uygulama yeniden başlatıldığında Intune hizmeti ile bağlantıya geçer.

> [!IMPORTANT]
> Samsung Smart Manager, Şirket Portalı uygulamasını yeniden devre dışı bırakabileceği için Şirket Portalı uygulamasını el ile açmak geçici bir çözümdür.

**Çözüm #2:**

Kullanıcılarınıza cihazlarını Android 6.0 sürümüne yükseltmeyi denemelerini söyleyin. Devre dışı bırakma sorunu Android 6.0 cihazlarda yoktur. Bir güncelleştirmenin kullanılabilir olup olmadığını denetlemek için **Ayarlar**  >  **cihaz**  >  **indirme güncelleştirmeleri el ile** ' ye gidin > istemleri izleyin.

**Çözüm #3:**

Çözüm #2 işe yaramazsa, kullanıcılarınızın aşağıdaki adımları uygulayarak Şirket Portalı uygulamasını Smart Manager'da hariç tutmasını sağlayın:

1. Cihazda Smart Manager uygulamasını başlatın.

   ![Cihazda Smart Manager simgesini seçin](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-icon.png)

2. **Pil** kutucuğunu seçin.

   ![Pil kutucuğunu seçin](./media/troubleshoot-device-enrollment-in-intune/smart-manager-battery-tile.png)

3. **Uygulama güç tasarrufu** veya **Uygulama optimizasyonu** bölümünde **Ayrıntı**'yı seçin.

   ![Uygulama güç tasarrufu veya Uygulama optimizasyonu bölümünde Ayrıntı'yı seçin](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-power-saving-detail.png)

4. Uygulama listesinden **Şirket Portalı**'nı seçin.

   ![Uygulama listesinden Şirket Portalı'nı seçin](./media/troubleshoot-device-enrollment-in-intune/smart-manager-company-portal.png)

5. **Kapalı**'yı seçin.

   ![Uygulama optimizasyon iletişim kutusundan Kapalı'yı seçin](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-optimization-turned-off.png)

6. **Uygulama güç tasarrufu** veya **Uygulama optimizasyonu** altında Şirket Portalı'nın kapalı olduğunu onaylayın.

   ![Şirket Portalı'nın kapalı olduğunu doğrulayın](./media/troubleshoot-device-enrollment-in-intune/smart-manager-verify-comp-portal-turned-off.png)


### <a name="profile-installation-failed"></a>Profil yüklemesi başarısız oldu
**Sorun:** Bir kullanıcı, bir Android cihazında **Profil yüklemesi başarısız oldu** hatasını alıyor.

**Çözünürlüğüne**

1. Kullanıcıya Intune hizmetinin kullandığınız sürümü için uygun bir lisans atandığını doğrulayın.

2. Cihazın zaten başka bir MDM sağlayıcısına kaydedilmediğini doğrulayın.

3. Cihazın zaten yüklü bir yönetim profili olmadığını doğrulayın.

4. Android için Chrome’un varsayılan tarayıcı olduğunu ve tanımlama bilgilerinin etkinleştirildiğini doğrulayın.

### <a name="android-certificate-issues"></a>Android sertifika sorunları

**Sorun**: Kullanıcılar cihazda şu iletiyi alıyor: *Cihazınızda gerekli bir sertifika eksik olduğundan oturum açamazsınız.*

**Çözüm 1**:

Kullanıcı, [Cihazınızda gerekli bir sertifika eksik](../user-help/your-device-is-missing-an-IT-required-certificate-android.md) başlığı altında verilen yönergeleri izleyerek eksik sertifikayı alabilmelidir. Sorun devam ederse, 2. Çözümü deneyin.

**Çözüm 2**:

Kullanıcılar, şirket kimlik bilgilerini girdikten ve federe oturum açmaya yönlendirildikten sonra eksik sertifika hatasını hala görebilir. Bu durumda hata, Active Directory Federasyon Hizmetleri (AD FS) sunucunuzda bir ara sertifikanın eksik olduğu anlamına gelebilir

Sertifika hatasının nedeni, Android cihazlarında [SSL Sunucu selamlamasına](/previous-versions/windows/it-pro/windows-server-2003/cc783349(v=ws.10)) sertifikaların hemen eklenmesinin gerekli olmasıdır. Şu anda, varsayılan AD FS sunucusu veya WAP - AD FS Proxy sunucusu yüklemesi SSL İstemci selamlamasına yanıt olarak SSL sunucu selamlamasında yalnızca AD FS hizmeti SSL sertifikasını gönderir.

Sorunu düzeltmek için AD FS sunucusunda veya proxy’lerdeki Bilgisayar Kişisel Sertifikaları’na sertifikaları aşağıdaki gibi içeri aktarın:

1. ADFS ve proxy sunucularında, **Start**  >  **Run**  >  yerel makine sertifika yönetimi konsolunu başlatmak için**Certlm. msc** Çalıştır ' a sağ tıklayın.
2. **Kişisel**’i genişletip **Sertifikalar**’ı seçin.
3. AD FS hizmeti iletişiminizin sertifikasını (ortak olarak imzalanmış bir sertifika) bulun ve özelliklerini görüntülemek için çift tıklayın.
4. Sertifikanın üst sertifikası/s ' nı görmek için **sertifika yolu** sekmesini seçin.
5. Her üst sertifikada, **Sertifikayı Görüntüle**’yi seçin.
6. **Ayrıntıları**  >  **Dosyaya Kopyala...** seçeneğini belirleyin.
7. Ana sertifikanın ortak anahtarını, seçtiğiniz dosya konumuna dışarı veya dışarı aktarmak için sihirbaz istemlerini izleyin.
8. **Sertifikalar**  >  **Tüm görevler**  >  **içeri aktar**' a sağ tıklayın.
9. Üst sertifikaları **Yerel Bilgisayar\Kişisel\Sertifikalar** konumuna içeri aktarmak için sihirbazdaki istemleri izleyin.
10. AD FS sunucularını yeniden başlatın.
11. Tüm AD FS ve proxy sunucularınızda yukarıdaki adımları yineleyin.

Uygun bir sertifika yüklemesini doğrulamak için, ' de bulunan Tanılama aracını kullanabilirsiniz [https://www.digicert.com/help/](https://www.digicert.com/help/) . **Sunucu adresi** kutusuna ADFS sunucunuzun FQDN 'SINI (ıe: STS.contso.com) girin ve **sunucuyu denetle**' ye tıklayın.

**Sertifikanın düzgün yüklendiğini doğrulamak için**:

Aşağıdaki adımlar sertifikanın doğru yüklendiğini doğrulamak için kullanabileceğiniz birçok yöntem ve araçtan sadece birini açıklar.

1. [Ücretsiz Digicert aracı](https://www.digicert.com/help/)’na gidin.
2. AD FS sunucunuzun tam etki alanı adını girin (örneğin, sts.contoso.com) ve **sunucuyu denetle**' yi seçin.

Sunucu sertifikası düzgün yüklendiyse, sonuçlarda tüm onay işaretlerini görürsünüz. Yukarıdaki sorun varsa, raporun "sertifika adı eşleşmeleri" ve "SSL sertifikası düzgün yüklendi" bölümlerine kırmızı bir X işareti görürsünüz.


## <a name="iosipados-issues"></a>iOS/ıpados sorunları

### <a name="iosipados-enrollment-errors"></a>iOS/ıpados kayıt hataları
Aşağıdaki tabloda, Intune 'da iOS/ıpados cihazlarını kaydederken son kullanıcıların görebileceği hatalar listelenmektedir.

|Hata iletisi|Sorun|Çözüm|
|-------------|-----|----------|
|NoEnrollmentPolicy|Kayıt ilkesi bulunamadı|Apple Anında İletilen Bildirim Servisi (APNs) sertifikası gibi tüm kayıt önkoşullarının ayarlanmış olduğunu ve "iOS/ıpados as platform" özelliğinin etkinleştirildiğini denetleyin. Yönergeler için bkz. [iOS/ıpados ve Mac cihaz yönetimini ayarlama](ios-enroll.md).|
|DeviceCapReached|Zaten çok fazla mobil cihaz kaydedilmiş durumda.|Kullanıcı başka bir cihaz kaydetmeden önce o anda Şirket Portalı’na kayıtlı mobil cihazlarından birini kaldırmalıdır. Kullanmakta olduğunuz cihaz türüne ilişkin yönergelere bakın: [Android](../user-help/unenroll-your-device-from-intune-android.md), [IOS/ıpados](../user-help/unenroll-your-device-from-intune-ios.md), [Windows](../user-help/unenroll-your-device-from-intune-windows.md).|
|APNSCertificateNotValid|Mobil cihazın şirketinizin ağıyla iletişim kurmasına imkan tanıyan sertifika ile ilgili bir sorun var.<br /><br />|Apple Anında İletilen Bildirim Servisi (APNs), kayıtlı iOS/ıpados cihazlarıyla iletişim kurmak için bir kanal sağlar. Aşağıdakiler koşullarda kayıt başarısız olur ve bu ileti görüntülenir:<ul><li>APNs sertifikası alma adımları tamamlanmamıştır veya</li><li>APNs sertifikanın süresi bitmiştir.</li></ul>[Active Directory’yi eşitleme ve Intune’a kullanıcıları ekleme](../fundamentals/users-add.md) ve [Kullanıcıları ve cihazları düzenleme](../fundamentals/groups-add.md) konu başlıkları altında kullanıcıları ayarlamayla ilgili bilgileri gözden geçirin.|
|AccountNotOnboarded|Mobil cihazın şirketinizin ağıyla iletişim kurmasına imkan tanıyan sertifika ile ilgili bir sorun var.<br /><br />|Apple Anında İletilen Bildirim Servisi (APNs), kayıtlı iOS/ıpados cihazlarıyla iletişim kurmak için bir kanal sağlar. Aşağıdakiler koşullarda kayıt başarısız olur ve bu ileti görüntülenir:<ul><li>APNs sertifikası alma adımları tamamlanmamıştır veya</li><li>APNs sertifikanın süresi bitmiştir.</li></ul>Daha fazla bilgi için, [Microsoft Intune Ile iOS/ıpados ve Mac yönetimini ayarlama](ios-enroll.md)konusunu gözden geçirin.|
|DeviceTypeNotSupported|Kullanıcınız iOS olmayan bir cihaz kullanarak kaydolmayı denemiş olabilir. Kaydetmeye çalıştığınız mobil cihaz türü desteklenmemektedir.<br /><br />Cihazın iOS/ıpados sürüm 8,0 veya üzerini çalıştırdığından emin olun.<br /><br />|Kullanıcı cihazının iOS/ıpados sürüm 8,0 veya üzerini çalıştırdığından emin olun.|
|UserLicenseTypeInvalid|Kullanıcının hesabı henüz gerekli bir kullanıcı grubuna üye olmadığı için cihaz kaydedilemiyor.<br /><br />|Kullanıcıların cihazlarını kaydedebilmesi için doğru kullanıcı grubunun üyesi olmaları gerekir. Bu ileti kullanıcının mobil cihaz yönetimi yetkilisi için yanlış lisans türüne sahip olduğu anlamına gelir. Örneğin aşağıdakilerin her ikisi de doğruysa kullanıcı bu hatayı görür:<ol><li>Intune mobil cihaz yönetim yetkilisi olarak ayarlanmıştır</li><li>System Center 2012 R2 Configuration Manager lisansı kullanılıyordur.</li></ol>Daha fazla bilgi için aşağıdaki makaleleri inceleyin:<br /><br />[Microsoft Intune Ile iOS/ıpados ve Mac yönetimini ayarlama](ios-enroll.md) konusunu gözden geçirin ve kullanıcılara [eşitleme Active Directory ayarlama ve Intune 'a Kullanıcı ekleme](../fundamentals/users-add.md) ve kullanıcıları [ve cihazları düzenleme](../fundamentals/groups-add.md)hakkında bilgi edinmek için.|
|MdmAuthorityNotDefined|Mobil cihaz yönetim yetkilisi tanımlanmamış.<br /><br />|Mobil cihaz yönetim yetkilisi Intune'da ayarlanmamış.<br /><br />[30 günlük Microsoft Intune denemesini başlatın](../fundamentals/free-trial-sign-up.md) bölümündeki “6. Adım: Mobil cihazları kaydetme ve uygulama yükleme” kısmında madde 1’i gözden geçirin.|

### <a name="devices-are-inactive-or-the-admin-console-cant-communicate-with-them"></a>Cihazlar etkin değil veya yönetici konsolu cihazlarla iletişim kuramıyor
**Sorun:** IOS/ıpados cihazları Intune hizmetini iade etmemektedir. Korumalı şirket kaynaklarına erişimin sürdürülmesi için cihazların hizmete düzenli olarak giriş yapması gerekir. Hizmeti denetlemeyen cihazlar:

- Intune hizmetinden ilke, uygulama ve uzak komutları alamaz.
- Yönetici konsolunda Yönetim Durumu olarak **Uygun olmayan durumda** görüntülenir.
- Koşullu erişim ilkeleriyle korunan kullanıcılar şirket kaynaklarına erişimi kaybedebilir.

**Çözüm:** Şirket kaynaklarına erişimi yeniden sağlamaları için son kullanıcılarla aşağıdaki çözümleri paylaşın.

Kullanıcılar iOS/ıpados Şirket Portalı uygulamasını başladıkları zaman, cihazındaki Intune ile ilgili iletişime kayıp olup olmadığını söyleyebilir. İletişim olmadığını algılarsa, yeniden bağlanmak için Intune ile eşitlemeyi otomatik olarak dener (kullanıcılar **Eşitlemeye çalışılıyor...** iletisini görür).

  ![Eşitlemeye çalışılıyor bildirimi](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_trying_to_sync_notification.png)

Eşitleme başarılı olursa, iOS/ıpados Şirket Portalı uygulamasında, cihazınızın sağlıklı bir durumda olduğunu belirten başarılı bir çevrimiçi **eşitleme** bildirimi görürsünüz.

  ![Eşitleme başarılı bildirimi](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_sync_successful_notification.png)

Eşitleme başarısız olursa, kullanıcılar iOS/ıpados Şirket Portalı uygulamasında bir satır içi bildirim **ile eşitleme yapamıyor** .

  ![Eşitleme yapılamıyor bildirimi](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_unable_to_sync_notification.png)

Sorunu düzeltmek için kullanıcıların **Eşitleme yapılamıyor** bildiriminin sağındaki **Ayarla** düğmesini seçmesi gerekir. Ayarla düğmesi, kullanıcıları cihazlarını kaydetmek için istemleri takip edebilecekleri Şirket Erişim Kurulumu akış ekranına götürür.

  ![Şirket Erişimi Kurulum ekranı](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_company_access_setup.png)

Kaydedildikten sonra cihazlar, iyi duruma geri döner ve şirket kaynaklarına yeniden erişim kazanır.

### <a name="verify-ws-trust-13-is-enabled"></a>WS-Trust 1.3’ün etkinleştirildiğini doğrulama
**Sorun** Otomatik cihaz kaydı (ADE) iOS/ıpados cihazları kaydedilemiyor

Kullanıcı benzeşimi ile ADE cihazlarını kaydetme, Kullanıcı belirteçleri istemek için WS-Trust 1,3 Kullanıcı adı/karma uç noktasının etkinleştirilmesini gerektirir. Active Directory bu uç noktayı varsayılan olarak etkinleştirir. Etkinleştirilmiş uç noktaların bir listesini almak için Get-AdfsEndpoint PowerShell cmdlet'ini kullanın ve trust/13/UsernameMixed uç noktasını arayın. Örneğin:

```powershell
Get-AdfsEndpoint -AddressPath "/adfs/services/trust/13/UsernameMixed"
```

Daha fazla bilgi için [Get-AdfsEndpoint belgelerine](/powershell/module/adfs/get-adfsendpoint?view=win10-ps) bakın.

Daha fazla bilgi için bkz. [Active Directory Federasyon Hizmetleri’nin güvenliğini sağlamak için en iyi yöntemler](/windows-server/identity/ad-fs/deployment/Best-Practices-Securing-AD-FS). WS-Trust 1.3 Kullanıcı adı/Karma'nın kimlik federasyon sağlayıcınızda etkin olup olmadığının belirlenmesine yardımcı olması için:
- ADFS kullanıyorsanız Microsoft Desteği'ne başvurun
- üçüncü taraf kimlik satıcınıza başvurun.


### <a name="profile-installation-failed"></a>Profil yüklemesi başarısız oldu
**Sorun:** Bir Kullanıcı bir iOS/ıpados cihazında **profil yüklemesi başarısız oldu** hatasını alıyor.

### <a name="troubleshooting-steps-for-failed-profile-installation"></a>Başarısız olan profil yüklemesi sorunlarını giderme adımları

1. Kullanıcıya Intune hizmetinin kullandığınız sürümü için uygun bir lisans atandığını doğrulayın.

2. Cihazın zaten başka bir MDM sağlayıcısına kaydedilmediğini doğrulayın.

3. Cihazın zaten yüklü bir yönetim profili olmadığını doğrulayın.

4. ' A gidin [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com) ve istendiğinde profili yüklemeyi deneyin.

5. İOS/ıpados için Safari 'nin varsayılan tarayıcı olduğunu ve tanımlama bilgilerinin etkinleştirildiğini doğrulayın.

### <a name="users-iosipados-device-is-stuck-on-an-enrollment-screen-for-more-than-10-minutes"></a>Kullanıcının iOS/ıpados cihazı 10 dakikadan uzun bir bir kayıt ekranında takılı

**Sorun**: Kaydolmakta olan bir cihaz iki ekrandan birinde takılabilir:
- "Microsoft" kaynağından son yapılandırma bekleniyor
- Kılavuzlu Erişim uygulaması kullanılamadığında. Lütfen yöneticinize başvurun.

Bu sorun şu koşullarda oluşabilir:
- Apple hizmetlerinde geçici bir kesinti varsa veya
- iOS/ıpados kaydı, tabloda gösterildiği gibi VPP belirteçlerini kullanacak şekilde ayarlanmıştır, ancak VPP belirtecinde bir sorun var.

| Kayıt ayarları | Değer |
| ---- | ---- |
| Platform | iOS/iPadOS |
| Kullanıcı Benzeşimi | Kullanıcı Benzeşimi ile kaydolma |
|Apple Kurulum Yardımcısı yerine Şirket Portalı ile kimlik doğrulama | Evet |
| VPP ile Şirket Portalı'nı yükleme | Belirteç kullanma: belirteç adresi |
| Kimlik doğrulanana kadar Şirket Portalı'nı Tek Uygulama modunda çalıştırma | Evet |

**Çözüm**: Sorunu gidermek için şunları yapmanız gerekir:
1. VPP belirtecinde bir sorun olup olmadığını belirleyin ve varsa sorunu giderin.
2. Hangi cihazların engellendiğini belirleyin.
3. Etkilenen cihazları temizleyin.
4. Kullanıcıya kayıt işlemini yeniden başlatmasını söyleyin.

#### <a name="determine-if-theres-something-wrong-with-the-vpp-token"></a>VPP belirtecinde bir şeyin yanlış gidip gitmediğini belirleyin
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS/ıpados**  >  **iOS kayıt**  >  **kayıt programı belirteçleri** > belirteç adı > **profiller** > profil adı > **yönetme**  >  **özellikleri**.
2. Aşağıdaki gibi bir hata olup olmadığını görmek özellikleri gözden geçirin:
    - Bu belirtecin süresi sona erdi.
    - Bu belirtecin Şirket Portalı lisansları bitti.
    - Bu belirteç başka bir hizmet tarafından kullanılıyor.
    - Bu belirteç başka bir kiracı tarafından kullanılıyor.
    - Bu belirteç silindi.
3. Belirtecin sorunlarını giderin.

#### <a name="identify-which-devices-are-blocked-by-the-vpp-token"></a>VPP belirteci tarafından engellenen cihazları belirleme
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS/ıpados**k > **iOS kayıt**  >  **kayıt programı belirteçleri** > belirteç adı > **cihazları**' nı seçin.
2. **Profil durumu** sütununu **Engellendi**'ye göre filtreleyin.
3. **Engellenen** tüm cihazların seri numaralarını not edin.

#### <a name="remotely-wipe-the-blocked-devices"></a>Engellenen cihazları uzaktan silme
VPP belirteciyle ilgili sorunları düzelttikten sonra, engellenen cihazları silmelisiniz.
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **tüm cihazlar**  >  **sütunları**  >  **seri numarası**  >  **Uygula**' yı seçin. 
2. Engellenen her cihazı **Tüm cihazlar** listesinde seçin, ardından **Sil** > **Evet**'i seçin.

#### <a name="tell-the-users-to-restart-the-enrollment-process"></a>Kullanıcılara kayıt işlemini yeniden başlatmalarını söyleyin
Engellenen cihazları sildikten sonra kullanıcılara kayıt işlemini yeniden başlatmalarını söyleyebilirsiniz.

## <a name="macos-issues"></a>macOS sorunları

### <a name="macos-enrollment-errors"></a>macOS kayıt hataları
**Hata iletisi 1:** *bir sanal makine kullandığınızı anlaşılıyor. Sanal makinenizi seri numarası ve donanım modeli de dahil olmak üzere tam olarak yapılandırdığınızdan emin olun. Bu bir sanal makine değilse, lütfen desteğe başvurun.*  

**Hata iletisi 2:** *cihazınızı yönetilene yönelik bir sorunla karşılaşıyoruz. Bu sorun, bir sanal makine kullanıyorsanız, sınırlı bir seri numarası varsa veya bu cihaz başka birine zaten atanmışsa oluşabilir. Bu sorunları çözmeyi öğrenin veya şirketinizin destek birimine başvurun.*

**Sorun:** Bu ileti, aşağıdaki sebeplerden birinin sonucu olabilir:  
- Bir macOS sanal makine (VM) doğru yapılandırılmadı  
- Cihazın şirkete ait olmasını veya Intune’da kayıtlı cihaz seri numarası olmasını gerektiren bazı cihaz kısıtlamaları etkinleştirdiniz  
- Cihaz zaten kayıtlı ve Intune’da başka bir kişiye atanmış  

**Çözüm:** İlk olarak cihazı hangi sorunun etkilediğini belirlemek için kullanıcınızla temasa geçin. Daha sonra aşağıdaki çözümlerden size en uygun olanını tamamlayın:

- Kullanıcı test amaçlı bir VM kaydediyorsa, Intune’un VM seri numarasını ve donanım modelini tanıyabilmesi için bunun tamamen yapılandırıldığına emin olun. Intune’da [VM ayarlama](macos-enroll.md#enroll-virtual-macos-machines-for-testing) hakkında daha fazla bilgi edinin.
- Kuruluşunuz, kişisel macOS cihazları engelleyen bazı kayıt kısıtlamaları etkinleştirdiyse, Intune’a [kişisel cihazın seri numarasını el ile eklemelisiniz](corporate-identifiers-add.md#manually-enter-corporate-identifiers).  
- Cihaz hala Intune’da başka bir kullanıcıya atanmış durumdaysa, eski kullanıcı Şirket Portalı uygulamasını kullanarak cihazı kaldırmamış veya sıfırlamamış demektir. Eski cihaz kaydını Intune’dan kaldırmak için:  

    1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), yönetici kimlik bilgilerinizle oturum açın.
    2. **Cihazlar**  >  **tüm cihazlar**' ı seçin.  
    3. Kayıt sorunu yaşayan cihazı bulun. Sonuçları daraltmak için cihaz adına veya MAC/Donanım Adresine göre arayın.
    4. Cihazı seçin > **Sil**’e tıklayın. Cihazla ilişkili diğer tüm girişleri silin.  

## <a name="pc-issues"></a>Bilgisayar Sorunları

|Hata iletisi|Sorun|Çözüm|
|---|---|---|
|**Erişim için BT yöneticisinin lisans ataması gerekiyor**<br>BT yöneticiniz bu uygulamayı kullanmanız için size erişim vermemiş. BT yöneticinizden yardım isteyin veya daha sonra tekrar deneyin.|Cihaz kaydedilemiyor çünkü bu kullanıcının hesabında gerekli lisans yok.|Cihazlar kaydedilmeden önce kullanıcılara gerekli lisans atanmış olmalıdır. Bu ileti kullanıcının mobil cihaz yönetimi yetkilisi için yanlış lisans türüne sahip olduğu anlamına gelir. Örneğin aşağıdakilerin her ikisi de doğruysa kullanıcı bu hatayı görür: <ol><li>Intune mobil cihaz yönetim yetkilisi olarak ayarlanmıştır</li><li>Kullanıcı System Center 2012 R2 Configuration Manager lisansı kullanmaktadır.</li></ol>[Kullanıcı hesaplarınıza Intune lisansları atama](../fundamentals/licenses-assign.md) hakkında bilgi alın.|

### <a name="the-machine-is-already-enrolled---error-hr-0x8007064c"></a>Makine zaten kaydoldu - Hata hr 0x8007064c

**Sorun:** Kayıt işlemi **Makine zaten kaydoldu** hatasıyla başarısız oluyor. Kayıt günlüğünde **HR 0x8007064C**hatası gösteriliyor.

Bu hata bilgisayarda şu koşullarda oluşabilir:

- daha önce kaydedilmiştir veya
- daha önce kaydedilmiş bir bilgisayarın kopyalanmış bir görüntüsünü içeriyordur.
Önceki hesabın hesap sertifikası hala bilgisayarda duruyordur.

**Çözünürlüğüne**

1. **Başlangıç** menüsünde, **Çalıştır** -> **MMC** yazın.
1. **Dosya**  >  **Ekle/Kaldır ek bileşenlerini**seçin.
1. **Sertifikalar**’a çift tıklayın, **Bilgisayar hesabı** > **İleri**’yi ve sonra **Yerel Bilgisayar**’ı seçin.
1. **Sertifikalar (Yerel bilgisayar)** seçeneğine çift tıklayın ve **Kişisel/ Sertifikalar**’ı seçin.
1. Sc_Online_Issuing tarafından verilen Intune sertifikasını arayın ve bulursanız silin.
1. Şu kayıt defteri anahtarı varsa, tüm alt anahtarlarıyla birlikte silin: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\OnlineManagement regkey**.
1. Yeniden kaydetmeyi deneyin.
1. Bilgisayar yine kaydedilemiyorsa, şu anahtarı arayın ve bulursanız silin: **KEY_CLASSES_ROOT\Installer\Products\6985F0077D3EEB44AB6849B5D7913E95**.
1. Yeniden kaydetmeyi deneyin.

    > [!IMPORTANT]
    > Bu bölüm, yöntem veya görev kayıt defterinde nasıl değişiklik yapacağınızı gösteren adımlar içerir. Ancak, kayıt defterinde yanlış değişiklik yaparsanız önemli sorunlar oluşabilir. Bu nedenle, bu adımları dikkatle izlediğinizden emin olun. Ek koruma için değiştirmeden önce kayıt defterini yedekleyin. Böylece bir sorun ortaya çıktığında kayıt defterini geri yükleyebilirsiniz.
    > Kayıt defterini yedekleme ve geri yükleme hakkında daha fazla bilgi için, [Windows’da kayıt defterini yedekleme ve geri yükleme](https://support.microsoft.com/kb/322756) konusunu okuyun.

## <a name="general-enrollment-error-codes"></a>Genel kayıt hata kodları

|Hata kodu|Olası sorun|Önerilen çözüm|
|--------------|--------------------|----------------------------------------|
|0x80CF0437 |İstemci bilgisayarındaki saat doğru zamana ayarlanmamış.|İstemci bilgisayardaki saat ve saat diliminin doğru saat ve saat dilimine ayarlandığından emin olun.|
|0x80240438, 0x80CF0438, 0x80CF402C|Intune hizmetine bağlanılamıyor. İstemci proxy ayarlarını kontrol edin.|Intune'un istemci bilgisayarda proxy yapılandırmasını desteklediğini doğrulayın. İstemci bilgisayarın Internet erişimi olduğundan emin olun.|
|0x80240438, 0x80CF0438|Internet Explorer ve Yerel Sistem'de proxy ayarları yapılandırılmamış.|Intune hizmetine bağlanılamıyor. İstemci proxy ayarlarını kontrol edin. Intune'un istemci bilgisayarda proxy yapılandırmasını desteklediğini doğrulayın. İstemci bilgisayarın Internet erişimi olduğundan emin olun.|
|0x80043001, 0x80CF3001, 0x80043004, 0x80CF3004|Kayıt paketi güncel değil.|Yönetim çalışma alanından güncel istemci yazılımı paketini indirin ve yükleyin.|
|0x80043002, 0x80CF3002|Hesap bakım modunda.|Hesap bakım modunda olduğunda yeni istemci bilgisayarlar kaydedilemez. Hesap ayarlarınızı görüntülemek için hesabınızda oturum açın.|
|0x80043003, 0x80CF3003|Hesap silindi.|Hesabınızın ve Intune aboneliğinizin hala etkin olduğunu doğrulayın. Hesap ayarlarınızı görüntülemek için hesabınızda oturum açın.|
|0x80043005, 0x80CF3005|İstemci bilgisayar devre dışı bırakıldı.|Birkaç saat bekleyin, bilgisayardan istemci yazılımının daha eski sürümlerini kaldırın ve ardından istemci yazılımı yükleme işlemini yeniden deneyin.|
|0x80043006, 0x80CF3006|İzin verilen maksimum bilgisayar lisansı sayısına ulaşıldı.|Kuruluşunuzun hizmete daha fazla istemci bilgisayar kaydedebilmek için önce ek bilgisayar lisansları satın alması gerekir.|
|0x80043007, 0x80CF3007|Sertifika dosyası yükleyici programla aynı klasörde bulunamadı.|Yüklemeyi başlatmadan önce tüm dosyaları ayıklayın. Ayıklanan dosyaları yeniden adlandırmayın veya taşımayın: tüm dosyalar aynı klasörde bulunmalıdır; aksi takdirde yükleme başarısız olur.|
|0x8024D015, 0x00240005, 0x80070BC2, 0x80070BC9, 0x80CFD015|İstemci bilgisayarın yeniden başlatılması beklendiğinden yazılım yüklenemiyor.|Bilgisayarı yeniden başlatın ve ardından istemci yazılımı yükleme işlemini yeniden deneyin.|
|0x80070032|İstemci yazılımını yüklemek için bir veya birden çok önkoşul istemci bilgisayarda bulunamadı.|Gerekli tüm güncelleştirmelerin istemci bilgisayarda yüklü olduğundan emin olun ve ardından istemci yazılımı yükleme işlemini yeniden deneyin.|
|0x80043008, 0x80CF3008|Microsoft Online Management Güncelleştirmeleri hizmeti başlatılamadı.|[Microsoft Intune için destek alma konusunda](../fundamentals/get-support.md)açıklandığı gibi Microsoft desteği başvurun.|
|0x80043009, 0x80CF3009|İstemci bilgisayar hizmete zaten kayıtlı.|İstemci bilgisayarı bu hizmete yeniden kaydetmek için önce devre dışı bırakmanız gerekir.|
|0x8004300B, 0x80CF300B|İstemci üzerinde çalışan Windows sürümü desteklenmediğinden, istemci yazılımı yükleme paketi çalıştırılamıyor.|Intune istemci bilgisayarda çalışan Windows sürümünü desteklemiyor.|
|0xAB2|Windows Installer özel bir işlem için VBScript çalışma zamanına erişemedi.|Bu hata Dinamik Bağlantı Kitaplıkları'nı (DLLs) temel alan özel bir işlemden kaynaklanır. DLL sorunlarını giderirken, [Microsoft Desteği KB198038: Paket ve Dağıtım Sorunlarında Yararlı Araçlar](https://support.microsoft.com/kb/198038) makalesinde açıklanan araçları kullanmanız gerekebilir.|
|0x80cf0440|Hizmet uç noktası bağlantısı sonlandırıldı.|Deneme hesabı veya ücretli hesap askıya alındı. Yeni bir deneme hesabı veya ücretli hesap oluşturun ve yeniden kaydolun.|

## <a name="next-steps"></a>Sonraki adımlar

Bu sorun giderme bilgileri size yardımcı olmadıysa, [Microsoft Intune için destek alma konusunda](../fundamentals/get-support.md)açıklandığı gibi Microsoft desteği başvurun.