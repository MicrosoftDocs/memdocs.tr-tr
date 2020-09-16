---
title: Microsoft Intune için ağ uç noktaları
titleSuffix: ''
description: Intune için uç noktaları gözden geçirin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: e30ec0c695483b493a9df603f5c7501d494c6aec
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574856"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Microsoft Intune için ağ uç noktaları  

Bu sayfada, Intune dağıtımlarınızdaki ara sunucu ayarları için gereken IP adresleri ve bağlantı noktası ayarları listelenir.

Yalnızca bulutta yer alan bir hizmet olan Intune, sunucular veya ağ geçitleri gibi şirket içi altyapıya ihtiyaç duymaz.

## <a name="access-for-managed-devices"></a>Yönetilen cihazlara erişim  

Güvenlik duvarı ve ara sunucular arkasındaki cihazları yönetmek için Intune iletişimini etkinleştirmeniz gerekir.

> [!NOTE]
> Bölümündeki bilgiler Microsoft Intune Sertifika Bağlayıcısı için de geçerlidir. Bağlayıcı, yönetilen cihazlarla aynı ağ gereksinimlerine sahiptir

- Intune istemcileri her iki protokolü de kullandığından, proxy sunucusu hem **http (80)** hem de **https (443)** desteğine sahip olmalıdır. Windows Information Protection 444 numaralı bağlantı noktasını kullanır.
- Bazı görevler (Klasik bilgisayar Aracısı için yazılım güncelleştirmelerini indirme gibi) için Intune, manage.microsoft.com için kimliği doğrulanmamış proxy sunucu erişimi gerektirir

Ara sunucu ayarlarını istemci bilgisayarlardan değiştirebilirsiniz. Belirtilen ara sunucu arkasında yer alan tüm istemci bilgisayarların ayarlarını değiştirmek için Grup İlkesi ayarlarını da kullanabilirsiniz.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

Yönetilen cihazlar, **Tüm Kullanıcıların** güvenlik duvarları üzerinden hizmetlere erişmesine izin veren yapılandırmalar gerektirir.


Aşağıdaki tabloda Intune istemcisinin eriştiği bağlantı noktaları ve hizmetler listelenir:

|Etki Alanları    |IP adresi      |
|-----------|----------------|
| login.microsoftonline.com <br> *. officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | Daha fazla bilgi için [Office 365 URL’leri ve IP adres aralıkları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com<br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com<br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com<br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com<br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com<br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com<br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0202.manage.microsoft.com<br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com<br>m.fei.amsua0402.manage.microsoft.com<br>portal.fei.amsua0801.manage.microsoft.com<br>portal.fei.msua08.manage.microsoft.com<br>m.fei.msua08.manage.microsoft.com<br>m.fei.amsua0801.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com<br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com<br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com<br>portal.fei.msub02.manage.microsoft.com<br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com<br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com<br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com<br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com<br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com<br>portal.fei.amsub0601.manage.microsoft.com<br>m.fei.amsub0601.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua01.manage.microsoft.com|138.91.243.97|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>PowerShell betikleri ve Win32 uygulamaları için ağ gereksinimleri  

PowerShell betikleri veya Win32 uygulamaları dağıtmak için Intune kullanıyorsanız, kiracınızın Şu anda bulunduğu uç noktalara da erişim vermeniz gerekir.

|ASU | Depolama adı | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedataprı<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedataprı<br>euprodimedatasec<br>euprodımedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdımedataprı<br>approdımedatasec<br>approdımedatahotıx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Windows Push Bildirim Hizmetleri (WNS)  

Mobil cihaz yönetimi (MDM) kullanılarak yönetilen Intune ile yönetilen Windows cihazları için, cihaz eylemleri ve diğer anında Etkinlikler Windows Push Bildirim Hizmetleri (WNS) kullanılmasını gerektirir. Daha fazla bilgi için bkz. [Kurumsal güvenlik duvarları üzerinden Windows Notification trafiğine Izin verme](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config).  

## <a name="delivery-optimization-port-requirements"></a>Teslim Iyileştirme bağlantı noktası gereksinimleri  

### <a name="port-requirements"></a>Bağlantı noktası gereksinimleri  

Uçtan uca trafik için, teslim Iyileştirme, NAT çapraz geçişi (isteğe bağlı Teredo) için TCP/IP veya 3544 7680 kullanır. İstemci hizmeti iletişimi için 80/443 bağlantı noktası üzerinden HTTP veya HTTPS kullanılır.

### <a name="proxy-requirements"></a>Proxy gereksinimleri  

Teslim Iyileştirme 'yi kullanmak için, bayt aralığı isteklerine izin vermeniz gerekir. Daha fazla bilgi için bkz. [Windows Update Için proxy gereksinimleri](/windows/deployment/update/windows-update-troubleshooting).

### <a name="firewall-requirements"></a>Güvenlik duvarı gereksinimleri  

Dağıtım Iyileştirmesini desteklemek için güvenlik duvarınız aracılığıyla aşağıdaki ana bilgisayar adlarının kullanılmasına izin verin.
İstemcilerle teslim Iyileştirme bulut hizmeti arasındaki iletişim için:
- \*. do.dsp.mp.microsoft.com

Teslim Iyileştirme meta verileri için:
- \*. dl.delivery.mp.microsoft.com
- \*. emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Apple cihaz ağ bilgileri  

|Kullanıldığı yerler|Ana bilgisayar adı (IP adresi/alt ağ)|Protokol|Bağlantı noktası|
|-----|--------|------|-------|
|Apple sunucularından içerik alma ve görüntüleme|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|APNS sunucularıyla iletişim|#-courier.push.apple.com<br>"#", 0 ile 50 arasında rastgele bir sayıdır.|    TCP     |  5223 ve 443  |
|World Wide Web, iTunes Mağazası, macOS App Store, iCloud, mesajlaşma vb. erişim dahil çeşitli işlevler |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 veya 443   |

Daha fazla bilgi için bkz. [Apple yazılım ürünleri tarafından kullanılan Apple 'ın TCP ve UDP bağlantı noktaları](https://support.apple.com/HT202944), [MacOS, IOS/ıpados ve iTunes Server ana bilgisayar bağlantıları ve iTunes arka plan Işlemleriyle Ilgili](https://support.apple.com/HT201999), [MacOS ve IOS/ıpados istemcileriniz Apple anında iletme bildirimleri almıyorsanız](https://support.apple.com/HT203609).  

## <a name="android-port-information"></a>Android bağlantı noktası bilgileri

Android cihazlarını yönetmeyi seçme seçeneğine bağlı olarak, Google Android kurumsal bağlantı noktalarını ve/veya Android anında iletme bildirimini açmanız gerekebilir. Desteklenen Android yönetim yöntemleri hakkında daha fazla bilgi için bkz. [Android kayıt belgeleri](../enrollment/android-enroll.md). 

> [!NOTE]
> Google Mobile Services Çin 'de kullanılamadığından, Çin 'deki cihazlarda Intune tarafından yönetilen cihazlar Google Mobile Services gerektiren özellikleri kullanamaz. Bu özellikler şunlardır Google Play: SafetyNet cihaz kanıtlama gibi özellikleri koruma, uygulamaları Google Play Store, Android kurumsal özelliklerinden yönetme (Bu [Google belgelerine](https://support.google.com/work/android/answer/6270910)bakın). Ayrıca, Android Intune Şirket Portalı uygulaması Microsoft Intune hizmetiyle iletişim kurmak için Google Mobile Services kullanır. Çin 'de Google Play hizmetleri kullanılamadığından, bazı görevlerin tamamlanabilmesi için 8 saate kadar süre gerekebilir. Daha fazla bilgi için bu [makaleye](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable)bakın.

### <a name="google-android-enterprise"></a>Google Android kurumsal 

Google, bu belgenin **güvenlik duvarı** bölümü altında, [Android kurumsal Bluebook](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)'ta gerekli ağ bağlantı noktaları ve hedef ana bilgisayar adları için belgeler sağlar. 

### <a name="android-push-notification"></a>Android anında iletme bildirimi

Intune, cihaz eylemleri ve iadelerinin tetiklenmesi için anında iletme bildirimi için Google Firebase Cloud Messaging (FCM) kullanır. Bu, hem Android Cihaz Yöneticisi hem de Android Enterprise için gereklidir. FCM ağ gereksinimleri hakkında bilgi için bkz. Google 'ın [FCM bağlantı noktaları ve güvenlik duvarınız](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall).

## <a name="endpoint-analytics"></a>Uç nokta analizi

Endpoint Analytics için gerekli uç noktalar hakkında daha fazla bilgi için bkz. [Endpoint Analytics proxy yapılandırması](../../analytics/troubleshoot.md#bkmk_endpoints).