---
title: Windows 10 için uygulama koruma ilkelerini yapılandırma
titleSuffix: Microsoft Intune
description: Bu konu başlığında Windows 10 cihazlar için uygulama koruma ilkelerini (APP) yapılandırma adımları anlatılmaktadır.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 949fddec-5318-4c9a-957e-ea260e6e05be
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98cff5540c6eaf571cc6b542a92dffb433820f4c
ms.sourcegitcommit: fe7484e86ec8a109fa5f54fe9cceef8aac94bd9f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80274396"
---
# <a name="get-ready-for-windows-information-protection-in-windows-10"></a>Windows 10 ' da Windows Information Protection hazırlanın 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Azure AD’de MAM sağlayıcısını ayarlayarak Windows 10 için mobil uygulama yönetimini (MAM) etkinleştirin. Azure AD’de bir MAM sağlayıcısı ayarlamak, Intune ile yeni bir Windows Bilgi Koruması (WIP) ilkesi oluştururken kayıt durumunu belirtmenizi sağlar. Kayıt durumu MAM ya da mobil cihaz yönetimi (MDM) olabilir.

## <a name="to-configure-the-mam-provider"></a>MAM sağlayıcısını yapılandırmak için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Tüm hizmetler** ' i seçin ve panoları değiştirmek için **M365 Azure Active Directory** seçin.
3. **Azure Active Directory**seçin.
4. **Yönet** grubunda **Mobilite (MDM ve MAM)** öğesini seçin.
5. **Microsoft Intune**’a tıklayın.
6. **Yapılandırma** BÖLMESINDEKI **varsayılan mam URL 'lerini geri yükle** grubundaki ayarları yapılandırın.

   **MAM kullanıcı kapsamı**  
   Çalışanlarınızın Windows cihazlarındaki kurumsal verileri yönetmek için MAM otomatik kaydı kullanın. MAM otomatik kayıt, kendi cihazını getir senaryoları için yapılandırılacaktır.<ul><li>**Yok.**<br>MAM’a kaydedilecek kullanıcı yoksa bunu seçin.</li><li>**Bazı**<br>MAM’a kayıt olacak kullanıcıları içeren Azure AD gruplarını seçin.</li><li>**Tümü**<br>Tüm kullanıcıların MAM’a kayıt olup olamayacağını seçin.</li></ul>

   **MDM kullanım koşulları URL’si**  
   MAM kullanım koşulları URL’si Microsoft Intune’da desteklenmez. Koruma ilkelerinin uygulanması için bu giriş kutusu boş bırakılmalıdır.

   **MDM bulma URL’si**  
   MAM hizmeti kayıt uç noktası URL'si. Kayıt uç noktası, cihazları MAM hizmetine yönetim için kaydetmek üzere kullanılır.

   **MAM uyumluluk URL’si**  
   MAM uyumluluk URL’si Microsoft Intune’da desteklenmez. Koruma ilkelerinin uygulanması için bu giriş kutusu boş bırakılmalıdır. 

7. **Kaydet**'e tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

[WıP ilkesi oluşturma](windows-information-protection-policy-create.md)
