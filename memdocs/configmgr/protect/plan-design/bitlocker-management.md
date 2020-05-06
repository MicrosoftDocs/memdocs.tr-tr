---
title: BitLocker yönetimi için planlama
titleSuffix: Configuration Manager
description: Configuration Manager BitLocker Sürücü Şifrelemesi yönetmeyi planlayın
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 926d1483739b85f787ebc9e2a992ea7ed39633c2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722217"
---
# <a name="plan-for-bitlocker-management"></a>BitLocker yönetimi için planlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!-- 3601034 -->

Sürüm 1910 ' den başlayarak, şirket içi Windows istemcileri için BitLocker Sürücü Şifrelemesi (BDE) yönetmek üzere Configuration Manager kullanın. Microsoft BitLocker yönetim ve Izleme (MBAD) kullanımını değiştirecek tam BitLocker yaşam döngüsü yönetimi sağlar.

> [!Note]  
> Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Daha fazla bilgi için bkz. [BitLocker genel bakış](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> Microsoft Endpoint Manager bulut hizmetini kullanarak, ortak yönetilen Windows 10 cihazlarında şifrelemeyi yönetmek için [ **Endpoint Protection** iş yükünü](../../comanage/workloads.md#endpoint-protection) Intune 'a geçirin. Intune kullanma hakkında daha fazla bilgi için bkz. [Windows şifrelemesi](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## <a name="features"></a>Özellikler

Configuration Manager, BitLocker Sürücü Şifrelemesi için aşağıdaki yönetim özelliklerini sağlar:

### <a name="client-deployment"></a>İstemci dağıtımı

BitLocker istemcisini Windows 10 veya Windows 8.1 çalıştıran yönetilen Windows cihazlarına dağıtma

### <a name="manage-encryption-policies"></a>Şifreleme ilkelerini yönetme

- Örneğin: sürücü şifrelemeyi ve şifre gücünü seçin, Kullanıcı muafiyeti ilkesini yapılandırın, sabit veri sürücüsü şifreleme ayarları ' nı seçin.

- Cihazı şifrelemek için kullanılacak algoritmaları ve şifreleme için hedeflediğiniz diskleri belirleme.

- Cihazı kullanmadan önce kullanıcıları yeni güvenlik ilkeleriyle uyumlu hale getirmek için zorlayın.

- Kuruluşunuzun güvenlik profilini cihaz bazında özelleştirin.

- Bir kullanıcı işletim sistemi sürücüsünün kilidini açtığında, yalnızca bir işletim sistemi sürücüsünün mi yoksa tüm eklenen sürücülerin mi ekleneceğini belirtin.

### <a name="compliance-reports"></a>Uyumluluk raporları

İçin yerleşik raporlar:

- Birim veya cihaz başına şifreleme durumu
- Cihazın birincil kullanıcısı
- Uyumluluk durumu
- Uyumsuzluk nedenleri

### <a name="administration-and-monitoring-website"></a>Yönetim ve web sitesini izleme

Anahtar dönüşü ve BitLocker ile ilgili diğer destek de dahil olmak üzere, kuruluşunuzda Configuration Manager konsolunun dışındaki diğer kişilerin anahtar kurtarmaya yardımcı olması için izin verin. Örneğin, yardım masası yöneticileri kullanıcılara anahtar kurtarmaya yardımcı olabilir.

### <a name="user-self-service-portal"></a>Kullanıcı self servis portalı

Kullanıcıların, BitLocker şifreli bir cihazın kilidini açmak için tek kullanılan bir anahtarla yardım almasına izin verin. Bu anahtar kullanıldığında, cihaz için yeni bir anahtar oluşturur.

## <a name="prerequisites"></a>Önkoşullar

- Bir BitLocker yönetim ilkesi oluşturmak için, Configuration Manager ' de **tam yönetici** rolüne sahip olmanız gerekir.

- BitLocker kurtarma hizmeti, yapılandırma istemcisini yönetim noktasıyla ağ genelinde kurtarma anahtarlarını şifrelemek için HTTPS gerektirir. İki seçenek vardır:

  - HTTPS-kurtarma hizmetini barındıran yönetim noktasında IIS Web sitesini etkinleştirin. Bu seçenek yalnızca Configuration Manager sürüm 2002 için geçerlidir.<!-- 5925660 -->

  - HTTPS için yönetim noktasını yapılandırın. Bu seçenek 1910 veya 2002 Configuration Manager sürümleri için geçerlidir.

  Daha fazla bilgi için bkz. [kurtarma verilerini şifreleme](../deploy-use/bitlocker/encrypt-recovery-data.md).

- BitLocker yönetim raporlarını kullanmak için, Raporlama Hizmetleri noktası site sistemi rolünü yükler. Daha fazla bilgi için bkz. [raporlamayı yapılandırma](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > **Kurtarma denetim raporunun** yönetim ve izleme Web sitesinden çalışması için yalnızca birincil sitede bir raporlama hizmetleri noktası kullanın.

- Self Servis Portalı 'nı veya yönetim ve izleme Web sitesini kullanmak için, IIS çalıştıran bir Windows Server gerekir. Bir Configuration Manager site sistemini yeniden kullanabilir veya site veritabanı sunucusuna bağlantısı olan tek başına bir Web sunucusu kullanabilirsiniz. [Site sistemi sunucuları için desteklenen bir işletim sistemi sürümü](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)kullanın.

    > [!NOTE]
    > Yalnızca Self Servis Portalı 'nı ve yönetim ve izleme Web sitesini bir birincil site veritabanıyla birlikte yükler. Bir hiyerarşide, her birincil site için bu Web sitelerini yükler.

- Self Servis portalını barındıracak Web sunucusunda, [MICROSOFT ASP.NET MVC 4,0](https://docs.microsoft.com/aspnet/mvc/mvc4)' yi yükler.

- Portal yükleyici betiğini çalıştıran kullanıcı hesabı, site veritabanı sunucusunda SQL **sysadmin** haklarına sahip olmalıdır. Kurulum işlemi sırasında, betik Web sunucusu makine hesabı için oturum açma, Kullanıcı ve SQL rol haklarını ayarlar. Self Servis portalı ve yönetim ve izleme Web sitesinin kurulumunu tamamladıktan sonra bu kullanıcı hesabını sysadmin rolünden kaldırabilirsiniz.

- BitLocker Yönetimi sanal makinelerde (VM) desteklenmez. Bu nedenle, bazı özellikler sanal makinelerde beklendiği gibi çalışmayabilir. Örneğin, BitLocker Yönetimi, sanal makinelerin sabit sürücülerinde şifrelemeyi başlatmayacak. Sanal makinelerde ek sabit sürücüler, şifrelenmemesine rağmen uyumlu olarak gösterilebilir.

> [!TIP]
> Varsayılan olarak, **BitLocker 'ı etkinleştir** görev dizisi adımı yalnızca sürücüdeki *kullanılan alanı* şifreler. BitLocker Yönetimi *tam disk* şifrelemesi kullanır. **Tam disk şifrelemesi kullanma**seçeneğini etkinleştirmek için bu görev dizisi adımını yapılandırın. Daha fazla bilgi için bkz. [görev dizisi adımları-BitLocker 'ı etkinleştirme](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

## <a name="next-steps"></a>Sonraki adımlar

[Kurtarma verilerini şifreleme](../deploy-use/bitlocker/encrypt-recovery-data.md) (ilkeyi ilk kez dağıtılmadan önce isteğe bağlı bir önkoşul)

[BitLocker yönetim istemcisi dağıtma](../deploy-use/bitlocker/deploy-management-agent.md)