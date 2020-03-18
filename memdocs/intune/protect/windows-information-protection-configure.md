---
title: Microsoft Intune’da Windows Bilgi Koruması ayarları
titleSuffix: Microsoft Intune
description: Windows Bilgi Koruması’nı yönetmek için kullanabileceğiniz Microsoft Intune ayarlarını öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18f353a6888ee30af2371ebb5a7f705ac0c060f0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328482"
---
# <a name="how-to-configure-windows-information-protection-in-microsoft-intune"></a>Microsoft Intune’da Windows Bilgi Koruması’nı yapılandırma

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Kuruluşta çalışanlara ait cihazların artmasıyla, kuruluşun denetimi dışında kalan e-posta, sosyal medya ve genel bulut gibi uygulamalar ve hizmetler üzerinden yanlışlıkla veri sızıntılarının oluşma riski de artar. Örneğin, bir çalışan en son mühendislik çalışmalarının resimlerini kişisel bir e-posta hesabından gönderebilir, ürün bilgilerini bir tweet’e kopyalayıp yapıştırabilir veya hazırlanması devam eden satış raporunu genel bulut depolama alanına kaydedebilir.

**Windows Bilgi Koruması**, çalışanın deneyimine başka hiçbir şekilde müdahale etmeden bu olası veri sızıntılarına karşı koruma sağlamaya yardımcı olur. Ayrıca, ortamınızda veya diğer uygulamalarda değişiklik yapmaya gerek kalmadan, kuruluşa ait cihazlarda ve çalışanların iş yerine getirdiği kişisel cihazlarda yanlışlıkla ortaya çıkabilecek veri sızıntılarına karşı kurumsal uygulamaları ve verileri korumaya da yardımcı olur.

Bu Intune ilkesi, Windows Information Protection tarafından korunan uygulamalar listesini, kurumsal ağ konumlarını, koruma düzeyini ve şifreleme ayarlarını yönetir.

>[!NOTE]
> Windows 10 Şirket Portalı uygulamasını Windows Bilgi Koruması ile kullanmak için Şirket Portalı uygulamasını Windows Bilgi Koruması’nın **Muaf** modu altına eklemeniz gerekir. 

Daha fazla bilgi için bkz.:
- [Windows Bilgi Koruması’nı kullanarak kuruluş verilerinizi koruma](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
- [Microsoft Intune klasik konsolunu kullanarak bir Windows Bilgi Koruması (WIP) ilkesi oluşturma](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune)
- [Microsoft Intune Azure portalını kullanarak MDM ile bir Windows Bilgi Koruması (WIP) ilkesi oluşturma](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune-azure)
- [Microsoft Intune Azure portalını kullanarak MAM ile bir Windows Bilgi Koruması (WIP) ilkesi oluşturma](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure)
