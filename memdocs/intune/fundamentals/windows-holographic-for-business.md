---
title: Microsoft Intune ile Windows Holographic cihazları kullanma - Azure | Microsoft Docs
description: Microsoft Intune kullanarak Windows Holographic for Business ve HoloLens çalıştıran cihazlarda Şirket Portalı’nı yapılandırmak, bir uyumluluk ilkesi oluşturmak, OMA-URI ayarlarını özelleştirmek, uygulama dağıtmak, gruplarda cihazları kategorilere ayırmak, profil oluşturmak, cihazları kısıtlamak, yazılım güncelleştirmelerini etkinleştirmek, hüküm ve koşullar ayarlamak, VPN ve Wi-Fi ayarları yapılandırmak ve İş İçin Hello kullanmak gibi farklı görevler gerçekleştirebilir ve yönetebilirsiniz.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 585a2f17-106b-4f02-adf7-05f08a92dbc1
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a463742a9511f21a98c277394f8c0d29084d379
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791756"
---
# <a name="manage-and-use-different-device-management-features-on-windows-holographic-and-hololens-devices-with-intune"></a>Intune ile Windows holographic ve HoloLens cihazlarda farklı cihaz yönetimi özelliklerini yönetme ve kullanma

Microsoft Intune, [Microsoft HoloLens](https://docs.microsoft.com/hololens/) gibi Windows Holographic for Business çalıştıran cihazları yönetmenize yardımcı olan birçok özelliğe sahiptir. Intune ile cihazlarınızın kuruluş kurallarına uygun olduğunu onaylayabilir ve VPN veya WiFi profili ekleyerek cihazları özelleştirebilirsiniz. Bir diğer önemli özellik de cihazı Bilgi noktası olarak kullanmak ve belirli bir uygulamayı veya belirli bir uygulama dizisini çalıştırmaktır.

Bu makaledeki görevler yazılım güncelleştirmeleri ve Windows Hello for Business kullanımı dahil olmak üzere Windows Holographic for Business çalıştıran cihazlarınızı yönetme, özelleştirme ve güvenliğini sağlama konusunda yardımcı olacaktır.

Windows Holographic cihazlarını Intune ile birlikte kullanmak için bir Sürüm Yükseltme profili oluşturun. Bu yükseltme profili, cihazları Windows Holographic’ten Windows Holographic for Business’a yükseltir. Microsoft HoloLens için ise yükseltme için gereken lisansı almak üzere Commercial Suite satın alabilirsiniz. Daha fazla bilgi için bkz. [Windows Holographic çalıştıran cihazları Windows Holographic for Business’a yükseltme](../configuration/holographic-upgrade.md).

## <a name="azure-active-directory"></a>Azure Active Directory

Azure Active Directory (AD), Windows Holographic for Business çalıştıran cihazlarınızı yönetmeye ve denetlemeye yardımcı olmak için mükemmel bir kaynaktır. Intune ve Azure AD kullanarak şunları yapabilirsiniz: 

- **[Cihazları Azure Active Directory 'a](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)** ekleyin: Azure ACTIVE DIRECTORY (ad) Içinde, Windows holographic for Business çalıştıran cihazlar dahil olmak üzere, Işe ait Windows 10 cihazlarınızı ekleyebilirsiniz. Bu özellik, Azure AD’nin cihazı denetlemesini sağlar. Kullanıcıların şirket kaynaklarına güvenlik ve uyumluluk standartlarına uygun cihazlardan eriştiğini doğrulamaya yardımcı olur.

  [Azure AD 'de cihaz yönetimi](https://docs.microsoft.com/azure/active-directory/devices/overview) daha fazla ayrıntı sağlar.

- **[Windows cihazlar için toplu kayıt](../enrollment/windows-bulk-enroll.md)**: Çok sayıda yeni Windows cihazı Azure Active Directory (AD) ve Intune’a dahil edebilirsiniz. Bu özellik, toplu kayıt olarak adlandırılır ve sağlama paketleri kullanır. Bu paketler, Windows Holographic for Business çalıştıran cihazları Azure AD kiracınıza dahil eder ve Intune’a kaydeder.

## <a name="company-portal"></a>Şirket Portalı

**[Şirket Portalı uygulamasını yapılandırma](../apps/company-portal-app.md)**

Intune; kullanıcıların şirket verilerine erişmesi, cihaz kaydetmesi, uygulama yüklemesi, BT departmanıyla iletişime geçmesi ve benzeri pek çok işlemi yapması için kullanıcılara Şirket Portalı uygulamasını sağlar. Windows Holographic for Business çalıştıran cihazlarınız için Şirket Portalı uygulamasını özelleştirebilirsiniz.

Şirket Portalı uygulamasını kullanarak aşağıdaki eylemleri de çalıştırabilirsiniz:

- Ayarlar uygulamasını veya Şirket Portalı uygulamasını kullanarak [bir cihazı Intune’dan kaldırma](../user-help/unenroll-your-device-from-intune-windows.md)
- [Bir cihazı yeniden adlandırma](../user-help/rename-your-device-cpapp.md)
- Bir cihaza [uygulama yükleme](../user-help/install-apps-cpapp-windows.md)
- Ayarlar uygulamasını veya Şirket Portalı uygulamasını kullanarak [cihazları el ile eşitleme](../user-help/sync-your-device-manually-windows.md)

## <a name="compliance-policy"></a>Uyumluluk ilkesi

**[Cihaz uyumluluk ilkesi oluşturma](../protect/compliance-policy-create-windows.md)**

Uyumluluk ilkeleri, cihazların uyumlu olmak için karşılaması gereken kurallar ve ayarlardır. Uyumsuz cihazların şirket kaynaklarına erişimini engellemek için bu ilkeleri koşullu erişimle birlikte kullanın. Intune’da Windows Holographic for Business çalıştıran cihazlar için erişime izin vermek veya erişimi engellemek üzere uyumluluk ilkeleri oluşturun. Örneğin, BitLocker 'ın etkinleştirilmesini gerektiren bir ilke oluşturabilirsiniz.

Ayrıca bkz. **[Uyumluluk ilkelerini kullanmaya başlama](../protect/device-compliance-get-started.md)**.

## <a name="deploy-and-manage-apps"></a>Uygulamaları dağıtma ve yönetme

**[Intune’a uygulama ekleme](../apps/apps-add.md)**

Intune kullanarak Windows Holographic for Business çalıştıran cihazlarınıza uygulama ekleyebilirsiniz. Uygulama dağıtmanın pek çok yolu vardır, örneğin:

- [Microsoft Store uygulamaları ekleme](../apps/store-apps-windows.md)
- [Oluşturduğunuz uygulamaları ekleme](../apps/lob-apps-windows.md)
- [Gruplara uygulama ekleme](../apps/apps-deploy.md)

Microsoft Intune, Windows Holographic for Business çalıştıran Microsoft HoloLens cihazlara Evrensel Windows Uygulamaları dağıtabilir. Uygulama paketlerinizi doğrudan Intune Azure portalından karşıya yükleyebilir veya İş İçin Microsoft Store’dan dağıtabilirsiniz. İlgili alanlar hakkında daha fazla bilgi için aşağıdaki makalelere bakın:
- Intune Azure portalını kullanarak İş Kolu (LOB) uygulamalarını dağıtmak için bkz. [Windows iş kolu uygulamalarını Microsoft Intune’a ekleme](../apps/lob-apps-windows.md).

    > [!NOTE]
    > Intune, en fazla 8 GB’lık paket boyutuna izin verir. Bu paket boyutu, yalnızca Intune’a yüklenen LOB uygulamaları için geçerlidir.

- İş İçin Microsoft Store kullanarak uygulama dağıtmak için bkz. [Microsoft Intune ile İş İçin Microsoft Mağazası’ndan satın aldığınız uygulamaları yönetme](../apps/windows-store-for-business.md). 
- Microsoft Intune ile uygulama yönetimi hakkında daha fazla bilgi edinmek için bkz. [Microsoft Intune’da uygulama yönetimi nedir?](../apps/app-management.md).
- Microsoft HoloLens için uygulama geliştirmek hakkında daha fazla bilgi edinmek için bkz. [Microsoft HoloLens için karma gerçeklik uygulamaları](https://www.microsoft.com/hololens/apps). 

> [!NOTE]
> Windows 10 Holographic for Business 1607 çalıştıran HoloLens cihazlar, İş İçin Microsoft Store’dan çevrimiçi lisanslandırılmış uygulamaları desteklemez. Daha fazla bilgi için bkz. [HoloLens’te uygulama yükleme](/hololens/holographic-store-apps).

## <a name="device-actions"></a>Cihaz eylemleri

Intune’da BT yöneticilerinin gerek cihazda yerel olarak gerekse Azure portalında Intune yoluyla uzaktan farklı görevler yapmasına imkan veren bazı yerleşik eylemler vardır. Kullanıcılar Intune'a kayıtlı kişiye ait cihazlara Intune Şirket Portalı’ndan uzaktan komut da verebilir.

Windows Holographic for Business çalıştıran cihazlar kullanırken şu eylemler kullanılabilir: 

- **[Silme](../remote-actions/devices-wipe.md#wipe)**: **Silme** eylemi, cihazı Intune’dan kaldırır ve cihazın varsayılan fabrika ayarlarını geri yükler. Bu eylemi cihazı yeni bir kullanıcıya vermeden önce veya cihazın kaybolma/çalınma durumu söz konusu olduğunda kullanın.

- **[Kullanımdan kaldırma](../remote-actions/devices-wipe.md#retire)**: **Kullanımdan kaldırma** eylemi, cihazı Intune’dan kaldırır. Ayrıca Intune tarafından atanmış yönetilen uygulama verilerini, ayarları ve e-posta profillerini de kaldırır. Kullanıcının kişisel verileri cihazda kalır.

- **[En son ilke ve eylemleri almak için cihazları eşitleme](../remote-actions/device-sync.md)**: **Eşitle** eylemi, cihazın hemen Intune’a iade etmesi için cihazı zorlar. Bir cihaz iade ettiğinde, kendisine atanan beklemedeki eylem veya ilkeleri hemen alır. Bu özellik, atadığınız ilkeleri bir sonraki zamanlanmış iadeyi beklememenize gerek kalmadan doğrulamanıza ve sorunlarını gidermenize yardımcı olur.

**[Microsoft Intune cihaz yönetimi nedir?](../remote-actions/device-management.md)** makalesi, Azure portalını kullanarak cihaz yönetmeyi öğrenmek iyi bir kaynaktır. 

## <a name="device-categories-and-groups"></a>Cihaz kategorileri ve gruplar

**[Cihazları gruplar halinde kategorilere ayırma](../enrollment/device-group-mapping.md)**

Intune ile cihaz kategorileri oluşturarak cihazları Satış, Muhasebe, İnsan Kaynakları vb. gibi kategorilere göre gruplara otomatik olarak ekleyebilirsiniz. Burada amaç, Windows Holographic for Business çalıştıran cihazlarınızı yönetmeyi kolaylaştırmaktır.

## <a name="device-configuration-profiles"></a>Cihaz yapılandırma profilleri

**[Yapılandırma profilleri ile çalışmaya başlayın](../configuration/device-profiles.md)ve [profile genel bakış](../configuration/device-profile-create.md)**

Intune, kuruluşunuzdaki farklı cihazlarda etkinleştirebileceğiniz veya devre dışı bırakabileceğiniz ayarları ve özellikleri içerir. Bu ayarlar ve özellikler, profiller kullanılarak yönetilir. Örneğin, Cortana 'yı sağlayan veya Windows holographic for Business çalıştıran cihazlarınızda Microsoft Defender akıllı ekranını kullanan bir profil oluşturabilirsiniz.

Profillerinizde bazı ayarları özelleştirmek, cihaz kısıtlamaları oluşturmak ve sanal özel ağ (VPN) ve Wi-Fi yapılandırmak için OMA-URI kullanabilirsiniz.

### <a name="custom-device-settings"></a>[Özel cihaz ayarları](../configuration/custom-settings-windows-holographic.md)

OMA-URI (Açık Mobil Birlik Tekdüzen Kaynak Tanımlayıcısı) ayarlarını yapılandırmak için Intune’da özel bir profil oluşturabilirsiniz. Windows Holographic for Business cihazlarınızda VPN’i etkinleştirmek veya Microsoft Update’te güncelleştirmeleri denetlemek gibi farklı özellikleri kontrol etmek için OMA-URI ayarlarını kullanın.

[Windows Defender uygulama denetimi (WDAC) CSP](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp) 'sini [kullanarak, uygulamaların](../configuration/custom-profile-hololens.md) HoloLens 2 cihazlarında açılmasına izin verin veya bunları engelleyin.

### <a name="configure-kiosk-mode"></a>[Bilgi noktası modunu yapılandırma](../configuration/kiosk-settings-holographic.md)

Intune’un paylaşılan veya misafir bilgisayar özelliklerini kullanarak Windows Holographic for Business cihazları bilgi noktası olarak çalışacak şekilde yapılandırabilirsiniz. Bu cihazlar, tek uygulama (tekli uygulama bilgi noktası modu) veya birden fazla uygulama (çoklu uygulama bilgi noktası modu) çalıştırabilir.

### <a name="device-restrictions"></a>[Cihaz kısıtlamaları](../configuration/device-restrictions-windows-holographic.md)

Cihaz kısıtlamaları; cihazlarınızda bir parola gerektirme, [Microsoft Store](https://www.microsoft.com/store/apps/windows?icid=CNavAppsWindowsApps)’dan uygulama indirme, Bluetooth’u etkinleştirme gibi pek çok farklı ayar ve özelliği denetlemenize olanak tanır. Bu kısıtlamalar bir Intune profilinde oluşturulur. Bu profil, Windows Holographic for Business çalıştıran birden fazla cihaza uygulanabilir.

### <a name="configure-vpn"></a>[VPN’i yapılandırma](../configuration/vpn-settings-configure.md)

Sanal özel ağlar (VPN’ler), kullanıcılarınıza şirket ağınıza güvenli uzaktan erişim vermenize olanak tanır. Intune’da Windows Holographic for Business çalıştıran cihazlarınız için belirli ayarları barındıran bir VPN profili oluşturabilirsiniz. Örneğin tüm Windows Holographic for Business cihazların bağlantı türü olarak Citrix VPN kullanması için bir VPN profili oluşturabilirsiniz.

### <a name="configure-wi-fi"></a>[Wi-Fi yapılandırma](../configuration/wi-fi-settings-configure.md)

Windows Holographic for Business cihazlarınıza kablosuz ağ ayarları atamak için bir Wi-Fi profili de oluşturabilirsiniz. Bir Wi-Fi profili atadığınızda son kullanıcılarınız, hiçbir ağ yapılandırmasına gerek kalmadan kuruluş ağ erişimi kazanır. Örneğin yalnızca Windows Holographic for Business cihazlarınıza adanmış bir Wi-Fi ağı oluşturabilirsiniz.

## <a name="shared-multi-user-devices"></a>Paylaşılan çok kullanıcılı cihazlar

[Paylaşılan cihazlar](../configuration/shared-user-device-settings-windows-holographic.md)

Microsoft HoloLens gibi Windows holographic for Business çalıştıran cihazların birden çok kullanıcısı olabilir. Intune, bu paylaşılan cihazlarda güç yönetimi, yerel depolama ve hesap yönetimi gibi farklı özellikleri denetlemeye yönelik ayarları içerir. Yapılandırma profilleri, farklı işletim sistemlerine sahip cihazlara de uygulanabilir. Örneğin, Devices grubu, RS2 ve RS3 çalıştıran cihazlara aynı grupta sahip olabilir.

## <a name="software-updates"></a>Yazılım güncelleştirmeleri

**[Yazılım güncelleştirmelerini yönetme](../protect/windows-update-for-business-configure.md)**

Intune’da Windows 10 cihazlar için güncelleştirme halkaları adı verilen bir özellik vardır. Bu güncelleştirme halkaları, güncelleştirmelerin nasıl yüklendiğini belirleyen bir grup ayar barındırır. Örneğin güncelleştirmeleri yüklemek için bir bakım penceresi oluşturabilir veya güncelleştirmeler yüklendikten sonra yeniden başlatmayı seçebilirsiniz. Güncelleştirme halkası, Windows Holographic for Business çalıştıran birden fazla cihaza uygulanabilir.

## <a name="terms-and-conditions"></a>hüküm ve koşullar

**[Kullanıcı erişimi için şirketinizin hüküm ve koşullarını ayarlama](../enrollment/terms-and-conditions-create.md)**

Kullanıcıların cihazlarını kaydedip e-posta gibi şirket uygulamalarına erişmesi için önce şirket hüküm ve koşullarını kabul etmelerini gerekli kılın. Intune’da hüküm ve koşulların Şirket Portalı’nda nasıl gösterildiğini belirleyin ve bu hüküm ve koşulları Windows Holographic for Business çalıştıran cihazlara atayın.

## <a name="windows-hello-for-business"></a>İş İçin Windows Hello

**[Iş için Windows Hello 'Yu kullanma](../protect/windows-hello.md)**

İş İçin Hello bir parolayı, akıllı kartı ya da sanal akıllı kartı değiştirmek için bir Azure Active Directory hesabı kullanan alternatif bir oturum açma yöntemidir. İş İçin Hello ile Windows Holographic for Business cihazlarınız, ayarladığınız en düşük uzunlukta bir PIN ile oturum açabilir.

## <a name="next-steps"></a>Sonraki adımlar

[Intune 'U ayarlayın](setup-steps.md).
