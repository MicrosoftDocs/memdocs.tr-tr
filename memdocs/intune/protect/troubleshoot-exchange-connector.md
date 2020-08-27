---
title: Exchange bağlayıcısı sorunlarını giderme
titleSuffix: Microsoft Intune
description: Intune şirket içi Exchange bağlayıcısı ile ilgili sorunları giderin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 57a7b232b7391d6b8716d4c2a56d69b44f6c07ee
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914761"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Intune Exchange Connector sorunlarını giderme

Bu makalede, Intune Exchange Connector ile ilgili sorunların nasıl giderileceği açıklanmaktadır.

> [!IMPORTANT]
>
> 2020 Temmuz 'dan başlayarak Exchange Connector için destek kullanım dışıdır ve Exchange [karma modern kimlik doğrulaması](/office365/enterprise/hybrid-modern-auth-overview) (HMA) ile değiştirilir ve Intune 'A bir Exchange Connector ekleme özelliği kaldırılmıştır.
>
> Exchange bağlayıcısını daha önce yapılandırmış ve kullanan müşteriler bağlayıcı için destek sağlamaya devam eder.


## <a name="before-you-start"></a>Başlamadan önce

Intune 'da bir Exchange Connector sorununu gidermeye başlamadan önce, bir Solid Foundation üzerinde çalışırken bazı temel bilgiler toplayın. Bu yaklaşım, sorunun doğasını daha iyi anlamanıza ve daha hızlı bir şekilde çözümlemenize yardımcı olabilir.

- İşleminizin yükleme gereksinimlerini karşıladığını doğrulayın. Bkz. Şirket [Içi Intune Exchange bağlayıcısını ayarlama](exchange-connector-install.md).
- Hesabınızda hem Exchange hem de Intune yönetici izinlerinin olduğunu doğrulayın.
- Tam ve tam hata iletisi metnini, ayrıntılarını ve iletinin nerede görüntülendiğini aklınızda yapın.
- Sorunun ne zaman başlatıldığını belirle: 
  - Bağlayıcıyı ilk kez ayarlıyor musunuz? 
  - Bağlayıcı doğru şekilde çalışıyor ve başarısız oldu mu?
  - Çalışıyorsa, Intune ortamında, Exchange ortamında veya bağlayıcı yazılımını çalıştıran bilgisayarda hangi değişiklikler meydana geldi?
- MDM yetkilisi nedir?
- Hangi Exchange sürümünü kullanıyorsunuz?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Exchange Connector sorunları hakkında daha fazla veri almak için PowerShell 'i kullanma

- Bir posta kutusunun tüm mobil cihazlarının listesini almak için, şunu kullanın `Get-ActiveSyncDeviceStatistics -mailbox mbx`
- Posta kutusu için SMTP adreslerinin bir listesini almak için kullanın `Get-Mailbox -Identity user | select emailaddresses | fl`
- Bir cihazın erişim durumu hakkında ayrıntılı bilgi almak için şunu kullanın `Get-CASMailbox <upn> | fl`

## <a name="review-the-connector-configuration"></a>Bağlayıcı yapılandırmasını gözden geçirme

Ortamınızın ve bağlayıcının doğru yapılandırıldığından emin olmak için [Şirket Içi Exchange Connector gereksinimlerini](exchange-connector-install.md#intune-exchange-connector-requirements) gözden geçirin. 

### <a name="general-considerations-for-the-connector"></a>Bağlayıcı için genel hususlar

- Güvenlik duvarınızın ve proxy sunucularınızın, Intune Exchange bağlayıcısını ve Intune hizmetini barındıran sunucu arasında iletişime izin verdiğinizden emin olun.

- Intune Exchange bağlayıcısını ve Exchange Istemci erişim sunucusunu (CAS) barındıran bilgisayar, etki alanına katılmış ve aynı LAN üzerinde olmalıdır. Intune Exchange Connector tarafından kullanılan hesap için gerekli izinlerin eklendiğinden emin olun.

- Bildirim hesabı otomatik *bulma* ayarlarını almak için kullanılır. Exchange 'de otomatik kaldır hakkında daha fazla bilgi için bkz. [Exchange Server 'da otomatik bulma hizmeti](/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- Intune Exchange Bağlayıcısı, bildirim e-posta iletilerini (Intune 'a kaydolmak için) kullanmaya *başlama* bağlantısıyla birlikte göndermek üzere bildirim hesabı kimlik BILGILERINI kullanarak EWS URL 'sine bir istek gönderir. Kayıt için kullanmaya *başlama* bağlantısı, Android Knox olmayan cihazlar için bir gereksinimdir. Aksi takdirde, bu cihazlar koşullu erişim tarafından engellenir.

### <a name="common-issues-for-connector-configurations"></a>Bağlayıcı yapılandırmalarına ilişkin genel sorunlar

- **Hesap izinleri**: Microsoft Intune Exchange Connector iletişim kutusunda, [gerekli Windows PowerShell Exchange cmdlet 'lerini](exchange-connector-install.md#exchange-cmdlet-requirements)çalıştırmak için uygun izinlere sahip bir kullanıcı hesabı belirttiğinizden emin olun.
- **Bildirim e-posta iletileri**: bildirimleri etkinleştirin ve bir bildirim hesabı belirtin.
- **Istemci erişimi sunucusu eşitleme**: Exchange bağlayıcısını yapılandırırken, Exchange bağlayıcısını barındıran sunucuda mümkün olan en düşük ağ gecikmesi olan bir CA belirtin. CA 'LAR ve Exchange Connector arasındaki iletişim gecikmesi, özellikle Exchange Online adanmış kullanılırken cihaz bulmayı geciktirebilirler.
- **Eşitleme zamanlaması**: Exchange Connector Exchange CA 'ları ile eşitlenene kadar, yeni kaydedilmiş bir cihaza sahip bir Kullanıcı erişim elde etme ile gecikebilir. Tam eşitleme günde bir kez gerçekleşirken delta eşitlemesi (hızlı eşitleme) birkaç kez gerçekleşir. Gecikmeleri olabildiğince azaltmak için [bir hızlı veya tam eşitlemeyi el ile zorlayabilirsiniz](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync).

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki makaleler, yaygın sorunların ve belirli hataların çözümlenmesine yardımcı olabilir:

- [Intune Exchange Connector için sık karşılaşılan sorunları çözün](troubleshoot-exchange-connector-common-problems.md).
- [Intune Exchange Connector için sık karşılaşılan hataları çözün](troubleshoot-exchange-connector-common-errors.md).

Destek veya Intune Community 'den yardım arama:

- Sorunu gidermeye yardımcı olması veya Microsoft ile bir destek talebi açmak için bkz. Intune konsolunu kullanma [desteği alın](../fundamentals/get-support.md) . 
- Sorununuzu [Microsoft Intune forumlarına](/answers/products/mem)gönderin.  
