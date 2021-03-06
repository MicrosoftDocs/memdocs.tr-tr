---
title: BitLocker portallarını ayarlama
titleSuffix: Configuration Manager
description: Self Servis portalı ve yönetim ve izleme Web sitesi için BitLocker yönetim bileşenlerini yükler
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6834090cd2a58113fb26e298c0c451f846f5ce9
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574601"
---
# <a name="set-up-bitlocker-portals"></a>BitLocker portallarını ayarlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

Aşağıdaki BitLocker yönetim bileşenlerini Configuration Manager kullanmak için, önce bunları yüklemeniz gerekir:

- Kullanıcı self servis portalı
- Yönetim ve izleme Web sitesi (yardım masası portalı)

Portalları, IIS yüklü olan mevcut bir site sunucusuna veya site sistemi sunucusuna yükleyebilir veya tek başına bir Web sunucusu kullanarak bunları barındırabilirsiniz.

> [!NOTE]
> Sürüm 2006 ' den başlayarak, merkezi yönetim sitesinde BitLocker Self-Service Portal ve yönetim ve izleme Web sitesini yükleyebilirsiniz.<!-- 5925693 -->
>
> Sürüm 2002 ve önceki sürümlerde, yalnızca Self Servis Portalı 'nı ve yönetim ve izleme Web sitesini birincil site veritabanıyla birlikte yükler. Bir hiyerarşide, her birincil site için bu Web sitelerini yükler.

Başlamadan önce, bu bileşenlere ilişkin [önkoşulları](../../plan-design/bitlocker-management.md#prerequisites) onaylayın.

## <a name="run-the-script"></a>Betiği çalıştırın

Hedef Web sunucusunda, aşağıdaki işlemleri yapın:

> [!NOTE]
> Sitenizin tasarımına bağlı olarak, betiği birden çok kez çalıştırmanız gerekebilir. Örneğin, yönetim ve izleme Web sitesini yüklemek için betiği yönetim noktasında çalıştırın. Sonra Self Servis Portalı 'nı yüklemek için tek başına bir Web sunucusunda yeniden çalıştırın.

1. Aşağıdaki dosyaları, `SMSSETUP\BIN\X64` site sunucusundaki Configuration Manager yükleme klasöründen hedef sunucudaki bir yerel klasöre kopyalayın:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. PowerShell 'i yönetici olarak çalıştırın ve ardından aşağıdaki komut satırına benzer betiği çalıştırın:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Örneğin,

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > Bu örnek komut satırı, kullanımlarını göstermek için tüm olası parametreleri kullanır. Ortamınızdaki gereksinimlerinize göre kullanım alanınızı ayarlayın.

Yükleme sonrasında portallara aşağıdaki URL 'Ler aracılığıyla erişin:

- Self Servis Portalı: `https://webserver.contoso.com/SelfService`
- Yönetim ve izleme Web sitesi: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Microsoft, HTTPS kullanımını önerir, ancak gerektirmez. Daha fazla bilgi için bkz. [IIS 'de SSL ayarlama](/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="script-usage"></a>Betik kullanımı

Bu işlem, Web sunucusuna bu bileşenleri yüklemek için MBAMWebSiteInstaller.ps1 bir PowerShell betiği kullanır. Aşağıdaki parametreleri kabul eder:

- `-SqlServerName <ServerName>` (gerekli): birincil site veritabanı sunucusunun tam etki alanı adı.

- `-SqlInstanceName <InstanceName>`: Birincil site veritabanı için SQL Server örnek adı. SQL varsayılan örneği kullanıyorsa bu parametreyi eklemeyin.

- `-SqlDatabaseName <DatabaseName>` (gerekli): birincil site veritabanının adı (örneğin,) `CM_ABC` .

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: Birincil sitenin raporlama hizmet noktasının Web hizmeti URL 'SI. **Reporting Services Configuration Manager** **Web hizmeti URL 'si** değeridir.

    > [!NOTE]
    > Bu parametre, yönetim ve izleme Web sitesinden bağlantılı **Kurtarma denetim raporunu** yüklemektir. Varsayılan olarak Configuration Manager diğer BitLocker yönetim raporlarını içerir.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Örneğin, `contoso\BitLocker help desk users` . Üyeleri yönetim ve izleme Web sitesinin **TPM** ve **sürücü kurtarma** alanlarında erişimi olan bir etki alanı kullanıcı grubu. Bu seçenekleri kullanırken, bu rolün, kullanıcının etki alanı ve hesap adı da dahil olmak üzere tüm alanları doldurması gerekir.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Örneğin, `contoso\BitLocker help desk admins` . Üyeleri yönetim ve izleme Web sitesinin tüm kurtarma bölgelerine erişimi olan bir etki alanı kullanıcı grubu. Kullanıcıların sürücülerinin kurtarılmasına yardımcı olurken, bu rolün yalnızca kurtarma anahtarını girmesi gerekir.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Örneğin, `contoso\BitLocker report users` . Üyeleri yönetim ve izleme Web sitesinin **raporlar** alanına salt okuma erişimi olan bir etki alanı kullanıcı grubu.

    > [!NOTE]
    > Yükleyici betiği, **-helpdeskusersgroupname**, **-helpdeskadminsgroupname**ve **-mbamreportusersgroupname** parametrelerinde belirttiğiniz etki alanı kullanıcı gruplarını oluşturmaz. Betiği çalıştırmadan önce, bu grupları seçtiğinizden emin olun.
    >
    > **-Helpdeskusersgroupname**, **-helpdeskadminsgroupname**ve **-mbamreportusersgroupname** parametrelerini belirttiğinizde, hem etki alanı adını hem de grup adını belirttiğinizden emin olun. `"domain\user_group"` biçimini kullanın. Etki alanı adını dışmayın. Etki alanı adı veya grup adı boşluk veya özel karakterler içeriyorsa, parametreyi tırnak işaretleri () içine alın `"` .

- `-SiteInstall Both`: Hangi bileşenlerin yükleneceğini belirtin. Geçerli seçenekler şunlardır:
  - `Both`: Her iki bileşeni de yükler
  - `HelpDesk`: Yalnızca yönetim ve izleme Web sitesini yükler
  - `SSP`: Yalnızca Self Servis Portalı 'nı yükler

- `-IISWebSite`: Betiğin MBAMWEB uygulamalarını yüklediği Web sitesi. Varsayılan olarak, IIS varsayılan Web sitesini kullanır. Bu parametreyi kullanmadan önce özel Web sitesini oluşturun.

- `-InstallDirectory`: Betiğin Web uygulaması dosyalarını yüklediği yol. Varsayılan olarak, bu yol olur `C:\inetpub` . Bu parametreyi kullanmadan önce özel dizini oluşturun.

- `-DomainName`*sürüm 2002 ve üzeri için geçerlidir*: sunucunun, yardım masası veya self servis web portalı rolüyle NetBIOS etki alanı adını belirtin. Yalnızca NetBIOS etki alanı adının DNS etki alanı adıyla eşleşmemesi durumunda gereklidir. Bu yapılandırma ayrık etki alanı ad alanı olarak da bilinir. Örneğin, `-DomainName fabrikham` DNS etki alanı adı `contoso.com` .<!-- MEMDocs #759 -->

- `-Uninstall`: BitLocker yönetim yardım masası/Self Servis Web portalı sitelerini daha önce yüklenmiş oldukları bir Web sunucusunda kaldırır.

## <a name="verify"></a>Doğrulama

Aşağıdaki günlükleri kullanarak izleyin ve sorun giderin:

- **Microsoft-Windows-MBAD-Web**altında Windows olay günlükleri. Daha fazla bilgi için bkz. [BitLocker olay günlükleri](../../tech-ref/bitlocker/about-event-logs.md) ve [sunucu olay günlükleri](../../tech-ref/bitlocker/server-event-logs.md)hakkında.

- Her bileşene ait izleme günlükleri aşağıdaki varsayılan konumlarda bulunur:

  - Self Servis Portalı: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Yönetim ve izleme Web sitesi: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Daha fazla sorun giderme bilgisi için bkz. [BitLocker sorunlarını giderme](../../tech-ref/bitlocker/troubleshoot.md).

## <a name="next-steps"></a>Sonraki adımlar

[Self servis portalı özelleştirme](customize-self-service-portal.md)

Yüklediğiniz bileşenleri kullanma hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [BitLocker yönetim ve izleme Web sitesi](helpdesk-portal.md)
- [BitLocker Self Servis portalı](self-service-portal.md)
