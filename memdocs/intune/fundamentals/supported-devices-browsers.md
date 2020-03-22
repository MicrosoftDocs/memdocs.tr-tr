---
title: Microsoft Intune tarafından desteklenen işletim sistemleri ve tarayıcılar
titleSuffix: ''
description: Intune cihaz yönetimi için desteklenen cihaz platformlarını ve tarayıcıları listeler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d1ac59c-a885-4276-8576-f3cf81c2d268
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9622a89b8b689dab7ea2d6d332d1d29c38f5668
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80085749"
---
# <a name="supported-operating-systems-and-browsers-in-intune"></a>Desteklenen işletim sistemleri ve tarayıcılar ıntune

Microsoft Intune'u ayarlamadan önce, desteklenen işletim sistemleriyle tarayıcıları gözden geçirin.

Intune 'u cihazınıza yükleme konusunda yardım için bkz. iş ve [Intune ağ bant genişliği kullanımını](network-bandwidth-use.md) [almak için yönetilen cihazları kullanma](https://docs.microsoft.com/mem/intune/user-help/use-managed-devices-to-get-work-done) .

Yapılandırma hizmeti sağlayıcısı desteği hakkında daha fazla bilgi için [yapılandırma hizmeti sağlayıcı başvurusunu](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference)ziyaret edin.

> [!NOTE]
> Intune, uygulama ve cihazların Android için Şirket Portalı uygulaması ve Android için Intune uygulama SDK 'Sı aracılığıyla şirket kaynaklarına erişmesi için artık Android 5. x (Lollipop) veya üstünü gerektirir. Bu gereksinim 4,4 çalıştıran Polycom Android tabanlı takımlar cihazları için geçerlidir. Bu cihazlar desteklenmeye devam edecektir. 

## <a name="intune-supported-operating-systems"></a>Intune tarafından desteklenen işletim sistemleri

Aşağıdaki işletim sistemlerini çalıştıran cihazları yönetebilirsiniz:

[!INCLUDE [mdm-supported-devices](../includes/mdm-supported-devices.md)]

### <a name="supported-samsung-knox-standard-devices"></a>Desteklenen Samsung Knox Standard cihazları

MDM kaydını önleyen Knox etkinleştirme hatalarının önüne geçmek için Şirket Portalı uygulaması, yalnızca cihazın [desteklenen Knox cihazları listesinde](https://www.samsungknox.com/knox-supported-devices/knox-workspace) görüntülendiği durumlarda MDM kaydı sırasında Samsung Knox etkinleştirmesi yapmaya çalışır. Samsung Knox etkinleştirmesini desteklemeyen cihazlar, standart Android cihazlar olarak kaydedilir. Bir Samsung cihazının Knox’u destekleyen model numaraları olabilir, diğerlerinin olamaz. Samsung cihazlar satın alıp dağıtmadan önce, cihazınızın kurumsal bayisinden Knox uyumluluğunu doğrulayın.

> [!NOTE]
> Samsung Knox cihazlarının kaydı için [Samsung sunucularına erişimi etkinleştirmeniz](https://support.samsungknox.com/hc/articles/115013833108-Our-corporate-devices-are-behind-a-firewall-How-do-I-enable-Knox-Workspace-devices-to-contact-Samsung-servers) gerekebilir.

Aşağıdaki listede adı geçen Samsung cihaz modelleri, Knox desteklemez. Android için Şirket Portalı tarafından yerel Android cihazlar olarak kaydedilirler:

| **Cihaz Adı** | **Cihaz Model Numaraları** |
| --- | --- |
| Galaxy Avant | SM-G386T |
| Galaxy Core 2/Core 2 Duos | SM-G355H<br>SM-G355M |
| Galaxy Core Lite | SM-G3588V |
| Galaxy Core Prime | SM-G360H |
| Galaxy Core LTE | SM-G386F<br>SM-G386W |
| Galaxy Grand | GT-I9082L<br>GT-I9082<br>GT-I9080L |
| Galaxy Grand 3 | SM-G7200 |
| Galaxy Grand Neo | GT-I9060I |
| Galaxy Grand Prime Value Edition | SM-G531H |
| Galaxy J Max | SM-T285YD |
| Galaxy J1 | SM-J100H<br>SM-J100M<br>SM-J100ML |
| Galaxy J1 Ace | SM-J110F<br>SM-J110H |
| Galaxy J1 Mini | SM-J105M |
| Galaxy J2/J2 Pro | SM-J200H<br>SM-J210F |
| Galaxy J3 | SM-J320F<br>SM-J320FN<br>SM-J320H<br>SM-J320M |
| Galaxy K Zoom | SM-C115 |
| Galaxy Light | SGH-T399N |
| Galaxy Note 3 | SM-N9002<br>SM-N9009 |
| Galaxy Note 7/Note 7 Duos | SM-N930S<br>SM-N9300<br>SM-N930F<br>SM-N930T<br>SM-N9300<br>SM-N930F<br>SM-N930S<br>SM-N930T |
| Galaxy Note 10.1 3G | SM-P602 |
| Galaxy S2 Plus | GT-I9105P |
| Galaxy S3 Mini | SM-G730A<br>SM-G730V |
| Galaxy S3 Neo | GT-I9300<br>GT-I9300I |
| Galaxy S4 | SM-S975L |
| Galaxy S4 Neo | SM-G318ML |
| Galaxy S5 | SM-G9006W |
| Galaxy S6 Edge | 404SC |
| Galaxy Tab A 7.0&quot; | SM-T280<br>SM-T285 |
| Galaxy Tab 3 7&quot;/Tab 3 Lite 7&quot; | SM-T116<br>SM-T210<br>SM-T211 |
| Galaxy Tab 3 8.0&quot; | SM T311 |
| Galaxy Tab 3 10.1&quot; | GT-P5200<br>GT-P5210<br>GT-P5220 |
| Galaxy Trend 2 Lite | SM-G318H |
| Galaxy V Plus | SM-G318HZ |
| Galaxy Young 2 Duos | SM-G130BU |

### <a name="windows-pc-software-client"></a>Windows bilgisayarı yazılım istemcisi

Bir [Intune yazılım istemcisi](manage-windows-pcs-with-microsoft-intune.md) alternatif bir kayıt yöntemi olarak Windows bilgisayarlara dağıtılabilir ve yüklenebilir. Bu işlev, yalnızca klasik Intune portalında kullanılabilir. Intune yazılım istemcisini, Windows 10 Home Edition dışında 10 ve üzeri bilgisayarları yönetmek için kullanabilirsiniz.

> [!Note]
> Microsoft, Windows 7 desteğinin 14 Ocak 2020 tarihinde bittiğini duyurmuştur. Aynı tarihte Intune'da Windows 7 çalıştıran cihazlar için desteğini kaldıracaktır.
>
> Daha fazla bilgi için bkz. [Intune plan değişikliği: Windows 7 için destek sonu](whats-new.md#windows-7-ends-extended-support).
>
> Microsoft Intune, 15 Ekim 2020 ' de Silverlight tabanlı Intune Konsolu desteğini devre dışı bırakacaktır. Bu kullanımdan kaldırma, Silverlight konsolu yapılandırılmış bılgısayar yazılım istemcisi (bılgısayar Aracısı olarak da bilinir) için son desteği içerir.
>
> Daha fazla bilgi için bkz. [Silverlight tabanlı yönetim konsolu için Microsoft Intune desteği](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Take-Action-Microsoft-Intune-ending-support-for-the-Silverlight/ba-p/916249).

<!--  ### Exchange ActiveSync management

You can manage [Exchange ActiveSync devices](../enrollment/device-enrollment.md#mobile-device-management-with-exchange-activesync-and-intune) from the Intune console. This option provides a limited set of management capabilities when compared to the other methods. See [Capabilities of built-in Mobile Device Management in Office 365](https://support.office.com/article/Capabilities-of-built-in-Mobile-Device-Management-for-Office-365-a1da44e5-7475-4992-be91-9ccec25905b0) for a list of supported devices.  -->

## <a name="intune-supported-web-browsers"></a>Intune desteklenen web tarayıcıları

Farklı yönetim görevleri aşağıdaki yönetim web sitelerinden birini kullanmanızı gerektirir.

- [Microsoft 365 Yönetim Merkezi](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Azure portalı](https://portal.azure.com/)

Bu portallar için aşağıdaki tarayıcılar desteklenir:

- Microsoft Edge (en son sürüm)
- Microsoft Internet Explorer 11
- Safari (en so sürüm, yalnızca Mac)
- Chrome (en son sürüm)
- Firefox (en son sürüm)

### <a name="intune-classic-portal"></a>Intune klasik portalı

Klasik Intune portalı yalnızca Intune PC yazılım istemcisi (https://manage.microsoft.com)ile kaydedilmiş cihazların yönetilmesi için kullanılır. Klasik Intune portalı, Silverlight tarayıcı desteği gerektirir.

Aşağıdaki Silverlight tarayıcıları klasik Intune konsolunu destekler:

- Internet Explorer 10 veya üstü
- Google Chrome (42. sürümden önceki sürümler)
- Silverlight özellikli Mozilla Firefox (sürüm 56 ' den önceki sürümler)

> [!Note]
> Microsoft Edge ve mobil tarayıcılar, [Microsoft Silverlight](https://msdn.microsoft.com/library/cc838158(v=vs.95).aspx)’ı desteklemediklerinden klasik Intune portalı için desteklenmez.

Yalnızca hizmet yöneticisi izinlerine sahip olan veya genel yönetici rolüne sahip bir kiracı yöneticisi olan kullanıcılar bu portalda oturum açabilir. Yönetim konsoluna erişmek için hesabınız Intune kullanma lisansına ve **İzin Verildi** oturum açma durumuna sahip olmalıdır.
