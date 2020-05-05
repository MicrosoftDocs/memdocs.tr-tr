---
title: Microsoft Intune Windows güncelleştirmeleri için Güncelleştirme Uyumluluğu raporlarını kullanın
titleSuffix: Microsoft Intune
description: Intune ile dağıttığınız Windows güncelleştirmelerinin rapor verilerini görüntülemek için OMS Güncelleştirme Uyumluluğu kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 157c61e9f145295f5ef728d12385fa44697a88e2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81725635"
---
# <a name="intune-compliance-reports-for-updates"></a>Güncelleştirmeler için Intune uyumluluk raporları

Windows 10 cihazlarına Windows Update dağıtmak için Intune kullandığınızda, Intune 'U veya *güncelleştirme uyumluluğu*adlı ücretsiz bir çözümü kullanarak güncelleştirme uyumluluğu hakkındaki ayrıntıları görüntüleyin. Güncelleştirme Uyumluluğu, Microsoft Operations Management Suite (OMS) bir parçasıdır.

## <a name="use-intune"></a>Intune 'U kullanma

Yapılandırdığınız Windows 10 güncelleştirme halkaları için dağıtım durumundaki bir ilke raporunu gözden geçirmek için:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihazlara** > **genel bakış** > **yazılım güncelleştirme durumunu**seçin. Atadığınız tüm güncelleştirme halkalarının durumu hakkında genel bilgileri görebilirsiniz.

3. Ek ayrıntıları görüntülemek için **izleyici**' yi seçin. Ardından **yazılım güncelleştirmeleri**' nin altında, **güncelleştirme halkası dağıtım durumu** ' nu seçin ve gözden geçirilecek dağıtım halkasını seçin.

   **İzle** bölümünde, güncelleştirme halkası hakkında ayrıntılı bilgileri görüntülemek için aşağıdaki raporlardan birini seçin:

   - **Cihaz durumu**-bu işlem cihaz yapılandırma durumunu gösterir, Ayrıntılar için bkz. [deviceConfigurationDeviceStatus güncelleştirme]( https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0).

   - **Kullanıcı durumu**-bu işlem Kullanıcı adı, durum ve son rapor tarihini gösterir, Ayrıntılar için bkz. [Deviceconfigurationuserdurumlarının listesi](https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0).

   - **Son Kullanıcı güncelleştirme durumu**-bu işlem Windows cihaz güncelleştirme durumunu gösterir, Ayrıntılar için bkz. [windowsupdatestate](https://docs.microsoft.com/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta).

## <a name="use-update-compliance"></a>Güncelleştirme Uyumluluğu kullan

[Güncelleştirme uyumluluğu](https://technet.microsoft.com/itpro/windows/manage/update-compliance-monitor)kullanarak Windows 10 Update piyasaya çıkarma ' i izleyebilirsiniz. Güncelleştirme Uyumluluğu Azure portal sunulur ve [önkoşullarını](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites)karşılayan cihazlarda ücretsiz olarak kullanılabilir.  

Bu çözümü kullandığınızda, güncelleştirme uyumluluğunu raporlamak istediğiniz Intune ile yönetilen Windows 10 cihazlarınızdan birine ticari bir KIMLIK dağıtırsınız.  

Intune 'da, ticari KIMLIĞI yapılandırmak için özel bir ilkenin OMA-URI ayarlarını kullanırsınız. Bkz. [Intune 'Da Windows 10 cihazları için özel ayarları kullanma](../configuration/custom-settings-windows-10.md).

Ticari KIMLIĞI yapılandırmaya yönelik OMA-URI (büyük/küçük harfe duyarlı) yolu: *./Vendor/MSFT/DMClient/Provider/MS DM Server/Commercial Cıalıd*

Örneğin, **OMA-URI Ayarı Ekle veya Düzenle** bölümünde aşağıdaki değerleri kullanabilirsiniz:

- **Ayar Adı**: Windows Analytics Ticari Kimliği
- **Ayar açıklaması**: Windows Analytics çözümleri IÇIN ticari kimliği yapılandırma
- **OMA-URI** (büyük/küçük harfe duyarlı): *./Vendor/MSFT/DMClient/Provider/MS DM Server/ticari IDID*
- **Veri Türü:** Dize
- **Değer**: \<OMS çalışma alanınızdaki Windows telemetri sekmesinde gösterilen GUID 'yi kullanın>

> [!NOTE]
> MS DM Sunucusu hakkında daha fazla bilgi için bkz. [DMClient yapılandırma hizmet sağlayıcısı (CSP)]( https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp).

## <a name="next-steps"></a>Sonraki adımlar

[Intune’da yazılım güncelleştirmelerini yönetme](windows-update-for-business-configure.md)
