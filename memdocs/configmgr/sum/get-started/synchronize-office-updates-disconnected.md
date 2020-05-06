---
title: Office 365 güncelleştirmelerini Internet bağlantısı olmadan eşitler
titleSuffix: Configuration Manager
description: Internet bağlantısı kesilen en üst düzey yazılım güncelleştirme noktasında Office 365 güncelleştirmelerini eşitler.
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3627d2f7772b7b9e133d742b0ee4f94dba6e457a
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110364"
---
# <a name="synchronize-office-365-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a>Bağlantısı kesilmiş bir yazılım güncelleştirme noktasından Office 365 güncelleştirmelerini eşitler

*Uygulama hedefi: Configuration Manager (geçerli dal)*
<!--4065163-->
Configuration Manager sürüm 2002 ' den başlayarak, bir aracı kullanarak Internet 'e bağlı bir WSUS sunucusundan Office 365 güncelleştirmelerini, bağlantısı kesilen bir Configuration Manager ortamına aktarabilirsiniz. Daha önce, bağlantısı kesilen ortamlarda güncelleştirilmiş yazılım için meta verileri verdiğinizde ve içeri aktardığınızda, Office 365 güncelleştirmelerini dağıtamazsınız. Office 365 güncelleştirmeleri Office API 'sinden ve Office CDN 'den indirilen, bağlantısı kesilen ortamlar için mümkün olmayan ek meta veriler gerektirir.

> [!Note]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](https://docs.microsoft.com/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- En az Windows Server 2012 çalıştıran, internet 'e bağlı bir WSUS sunucusu.
- WSUS sunucusunun bu iki Internet uç noktasına bağlanması gerekir:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Offlineupdatedışarı aktarıcı aracını ve bağımlılıklarını Internet 'e bağlı WSUS sunucusuna kopyalayın.
  - Araç ve bağımlılıkları ** &lt;configmgrınstalldir>/Tools/offlineupdatevericisi** dizininde bulunur.
- Aracı çalıştıran kullanıcının **WSUS yöneticileri** grubunun bir parçası olması gerekir.
- Office güncelleştirme meta verilerini ve içeriğini depolamak için oluşturulan dizin, dosyaların güvenliğini sağlamak için uygun erişim denetim listelerine (ACL 'Ler) sahip olmalıdır.
    - Bu dizin de boş olmalıdır.
- Çevrimiçi WSUS sunucusundan bağlantısı kesilen ortama taşınan veriler güvenli bir şekilde taşınmalıdır.

> [!IMPORTANT]
> Tüm Office 365 dilleri için içerik indirilir. Her güncelleştirmede yaklaşık 10 GB içerik bulunabilir.

## <a name="synchronize-then-decline-unneeded-office-365-updates"></a>Eşitlemeden sonra gereksiz Office 365 güncelleştirmelerini reddedin

1. İnternet 'e bağlı WSUS ' da WSUS konsolunu açın.
1. **Seçenekler** **, ürünler ve sınıflandırmalar '** ı seçin.
1. **Ürünler** sekmesinde **Office 365 istemcisi** ' ni seçin ve **sınıflandırmalar** sekmesinde **güncelleştirmeler** ' i seçin. [ ![WSUS 'de Office 365 güncelleştirmeleri için ürünler ve sınıflandırmalar](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Office 365 güncelleştirmelerini WSUS 'e almak için **eşitlemeler** 'e gidin ve **Şimdi eşitleme** ' yi seçin.
1. Eşitleme tamamlandığında Configuration Manager dağıtmak istemediğiniz Office 365 güncelleştirmelerini reddedin. İndirilebilmesi için Office 365 güncelleştirmelerini onaylamanız gerekmez.  
   - WSUS 'de istenmeyen Office 365 güncelleştirmelerinin reddediliyor, WsusUtil. exe dışarı aktarma sırasında dışarı aktarılmalarını engellemez, ancak Offlineupdatedışarı aktarıcı aracının içeriği indirmelerini durdurur.
   - Offlineupdateverme Aracı, Office 365 güncelleştirmelerini sizin için indirmeyi yapar. Bunlar için güncelleştirmeleri dışarı aktarıyorsanız diğer ürünlerin da indirilmek üzere onaylanması gerekir.
    - WSUS 'ta gereksiz Office 365 güncelleştirmelerini kolayca görmek ve reddetmek için [WSUS 'ta yeni bir güncelleştirme görünümü](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus) oluşturun.
1. İndirme ve dışarı aktarma için diğer ürün güncelleştirmelerini onayladıysanız, WsusUtil. exe ' yi çalıştırmadan önce içerik indirmenin tamamlanmasını bekleyin ve sunucusundaki WSUSContent klasörünün içeriğini kopyalayarak. Daha fazla bilgi için bkz. [bağlantısı kesilmiş bir yazılım güncelleştirme noktasından yazılım güncelleştirmelerini senkronize](synchronize-software-updates-disconnected.md) etme

## <a name="exporting-the-office-365-updates"></a>Office 365 güncelleştirmelerini dışarı aktarma

1. Offlineupdatedışarı aktarıcı klasörünü Configuration Manager ' dan Internet 'e bağlı WSUS sunucusuna kopyalayın.
    - Araç ve bağımlılıkları ** &lt;configmgrınstalldir>/Tools/offlineupdatevericisi** dizininde bulunur.
1. Internet 'e bağlı WSUS sunucusunda bir komut isteminden, aracı şu kullanımla çalıştırın: **Offlineupdatedışarı aktarma. exe-O-D &lt;hedef yolu>**

   |Offlineupdatedışarı aktarıcı parametresi|Açıklama|
   |---|---|
   |**-O**|  **-Office**. Güncelleştirmeler için ürünü, Office 365 dışa aktarma işlemini belirtir|
   |**-D**|**-Hedef**. Hedef, gerekli bir parametredir ve hedef klasörün tüm yolu gereklidir.|

   - **Offlineupdatedışarı aktarma** Aracı şunları yapar:
      - WSUS 'a bağlanır
      - WSUS 'de Office 365 güncelleştirme meta verilerini okur
      - İçerik ve Office 365 güncelleştirmelerinin gerektirdiği tüm ek meta verileri hedef klasöre indirir

1. Internet 'e bağlı WSUS sunucusunda komut isteminde, WsusUtil. exe dosyasını içeren klasöre gidin. Araç, varsayılan olarak%*ProgramFiles*% \ Update Services\Tools konumunda bulunur. Örneğin, araç varsayılan konumda bulunuyorsa **cd %ProgramFiles%\Update Services\Tools**yazın.
   - Windows Server 2012 kullanıyorsanız, [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) WSUS sunucularında yüklü olduğundan emin olun.
   - WsusUtil aracını çalıştıran kullanıcı, sunucuda yerel Yöneticiler grubunun bir üyesi olmalıdır.

1. Yazılım güncelleştirme meta verilerini bir GZIP dosyasına aktarmak için aşağıdakileri yazın:  

    **WsusUtil. exe dışarı aktarma**  *PackageName*  *logfile*  

    Örneğin:  

    **WsusUtil. exe Export Export. xml. gz Export. log**

1. **Dışarı aktarma. xml. gz** dosyasını, bağlantısı kesilen ağda en üst düzey WSUS sunucusuna kopyalayın.
1. Diğer ürünler için güncelleştirmeleri onayladıysanız, sunucusundaki WSUSContent klasörünün içeriğini üst düzey bağlantısı kesilen WSUS sunucusunun sunucusundaki WSUSContent klasörüne kopyalayın.
1. **Offlineupdatevericisi** için kullanılan hedef klasörü, bağlantısı kesilen ağdaki en üst düzey Configuration Manager site sunucusuna kopyalayın.

## <a name="import-the-office-365-updates"></a>Office 365 güncelleştirmelerini içeri aktarma

1. Bağlantısı kesilmiş üst düzey WSUS sunucusunda, internet 'e bağlı WSUS sunucusunda oluşturduğunuz **Export. xml. gz** dosyasından güncelleştirme meta verilerini alın.
   
    Örneğin:  

    **WsusUtil. exe Import Export. xml. gz Import. log**
    
    Varsayılan olarak, WsusUtil. exe aracı%*ProgramFiles*% \ Update Services\Tools konumunda bulunur.

1. İçeri aktarma işlemi tamamlandıktan sonra, bağlantısı kesik üst düzey Configuration Manager site sunucusunda bir site denetim özelliği yapılandırmanız gerekir. Bu yapılandırma değişikliği noktaları Office 365 içeriğine Configuration Manager. Özelliğin yapılandırmasını değiştirmek için:
   1. [O365OflBaseUrlConfigured PowerShell betiğini](#bkmk_o365_script) en üst düzey bağlantısı kesilen Configuration Manager site sunucusuna kopyalayın.
   1. `"D:\Office365updates\content"` Office Içeriğini ve Offlineupdatedışarı aktarıcı tarafından oluşturulan meta verileri içeren kopyalanmış dizinin tam yoluna geçin.
      > [!IMPORTANT]
      > O365OflBaseUrlConfigured özelliği için yalnızca yerel yollar çalışır.
   1. Betiği şu şekilde Kaydet`O365OflBaseUrlConfigured.ps1`
   1. Bağlantısı kesilmiş üst düzey Configuration Manager site sunucusundaki yükseltilmiş bir PowerShell penceresinden, öğesini çalıştırın `.\O365OflBaseUrlConfigured.ps1`.
   1. Site sunucusunda **SMS_Executive** hizmetini yeniden başlatın.
1. **Configuration Manager** konsolunda, **Yönetim** > **Site yapılandırması** > **siteler**' e gidin.
1. Üst düzey sitenize sağ tıklayın ve ardından **site bileşenlerini** > Yapılandır**yazılım güncelleştirme noktası**' nı seçin.
1. **Sınıflandırmalar** sekmesinde *güncelleştirmeler*' i seçin. **Ürünler** sekmesinde *Office 365 istemcisi*' ni seçin.
1. Configuration Manager için [yazılım güncelleştirmelerini eşitler](synchronize-software-updates.md#manually-start-software-updates-synchronization)
1. Eşitleme tamamlandığında, Office 365 güncelleştirmelerini dağıtmak için normal işleminizi kullanın.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a>Ara sunucu yapılandırması

- Proxy yapılandırması, araçta yerel olarak yerleşik değildir. Proxy, aracın çalıştığı sunucudaki Internet seçeneklerinde ayarlandıysa, teorik olarak kullanılır ve düzgün şekilde çalışır.
   - Bir komut isteminden, yapılandırılan proxy `netsh winhttp show proxy` 'yi görmek için komutunu çalıştırın.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a>O365OflBaseUrlConfigured özelliğini değiştir

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Sonraki adımlar

[Yazılım güncelleştirmelerini güncelleştirme grubuna ekleme](../deploy-use/add-software-updates-to-an-update-group.md)