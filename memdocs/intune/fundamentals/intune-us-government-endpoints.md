---
title: ABD kamu dağıtımları için ağ uç noktaları-Microsoft Intune
titleSuffix: ''
description: Intune için ABD devlet bitiş noktalarını gözden geçirin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 97298bba752f4af29c9dc7c2483c324cbd77a6bc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80438771"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>Microsoft Intune için ABD devlet uç noktaları

Bu sayfada, Intune dağıtımlarınızdaki ara sunucu ayarları için gereken ABD kamu uç noktaları listelenir.

Güvenlik duvarı ve ara sunucular arkasındaki cihazları yönetmek için Intune iletişimini etkinleştirmeniz gerekir.

- Intune istemcileri iki protokolü de kullandığından, proxy sunucusu hem **HTTP (80)** hem de **HTTPS (443)** desteklemelidir
- Intune bazı görevler (yazılım güncelleştirmelerini indirme gibi) için manage.microsoft.com adresine kimliği doğrulanmamış ara sunucu erişimine ihtiyaç duyar.

Ara sunucu ayarlarını istemci bilgisayarlardan değiştirebilirsiniz. Belirtilen ara sunucu arkasında yer alan tüm istemci bilgisayarların ayarlarını değiştirmek için Grup İlkesi ayarlarını da kullanabilirsiniz.

Yönetilen cihazlar, **Tüm Kullanıcıların** güvenlik duvarları üzerinden hizmetlere erişmesine izin veren yapılandırmalar gerektirir.

ABD kamu müşterileri için Windows 10 otomatik kaydı ve cihaz kaydı hakkında daha fazla bilgi için bkz. [Windows cihazları için kayıt ayarlama](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

Aşağıdaki tabloda Intune istemcisinin eriştiği bağlantı noktaları ve hizmetler listelenir:

|**Uç Nokta**|**IP adresi**|
|---------------------|-----------|
|*. manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>ABD devlet müşteri tarafından belirlenen uç noktalar:
- Azure portal: https:\//Portal.Azure.us/ 
- Office 365: https:\//Portal.office365.us/ 
- Intune Şirket Portalı: https:\//Portal.Manage.Microsoft.us/ 
- Microsoft Uç Nokta Yöneticisi Yönetim Merkezi: https\/:/Endpoint.Microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Intune 'un bağımlı olduğu iş ortağı hizmeti uç noktaları:
- AAD Eşitleme hizmeti: https:\//SyncService.gov.us.microsoftonline.com/DirectoryService.svc
- EVO STS: https:\//Login.microsoftonline.us
- Dizin proxy 'Si: https\/:/directoryproxy.MicrosoftAzure.us/DirectoryProxy.svc
- AAD grafiği: https:\//Directory.MicrosoftAzure.us ve https:\//Graph.MicrosoftAzure.us
- MS Graph: https:\//Graph.Microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

## <a name="windows-push-notification-services"></a>Windows anında Iletme Bildirim Hizmetleri
Mobil cihaz yönetimi (MDM) kullanılarak yönetilen Intune tarafından yönetilen cihazlarda, cihaz eylemleri ve diğer anında etkinlikler için Windows Push Bildirim Hizmetleri (WNS) gereklidir. Daha fazla bilgi için bkz. [WNS trafiğini desteklemek Için kurumsal güvenlik duvarı ve proxy yapılandırması](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config)

## <a name="apple-device-network-information"></a>Apple cihaz ağ bilgileri

|**Kullanıldığı yerler**|**Ana bilgisayar adı (IP adresi/alt ağ)**|**Protocol**|**Bağ**|
|------------|-----------|------------|-----------|
|Apple sunucularından içerik alma ve görüntüleme|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|APNS sunucularıyla iletişim|#-courier.push.apple.com<br>"#", 0 ile 50 arasında rastgele bir sayıdır.|TCP|5223 ve 443|
|Internet, iTunes Mağazası, macOS App Store, iCloud, mesajlaşma vb. gibi çeşitli işlevler|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 veya 443|

Daha fazla bilgi için bkz.

- [Apple yazılım ürünleri tarafından kullanılan TCP ve UDP bağlantı noktaları](https://support.apple.com/HT202944)
- [MacOS, iOS/ıpados ve iTunes Server ana bilgisayar bağlantıları ve iTunes arka plan işlemi hakkında](https://support.apple.com/HT201999)
- [MacOS ve iOS/ıpados istemcileriniz Apple anında iletme bildirimleri almıyorsanız](https://support.apple.com/HT203609)

## <a name="next-steps"></a>Sonraki adımlar
[Microsoft Intune için ağ uç noktaları](intune-endpoints.md)

