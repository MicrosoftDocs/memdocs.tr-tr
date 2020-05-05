---
title: Azure 'da eski Intune PC istemcisi ve Intune
description: Kuruluşunuzun Windows cihazlarını yönetmek için Azure 'da Intune 'U kullanmayla ilgili önemli noktalar.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/15/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 1f104923-12df-453c-9c20-942ef65a0945
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41b5b4116359864c4d1251515d29005b9d9af425
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077946"
---
# <a name="intune-on-azure-console-and-legacy-intune-pc-client"></a>Azure konsolu ve eski Intune PC istemcisinde Intune

Intune, Azure tabanlı SaaS uygulama hizmeti mimarisini kullanır. Azure, ölçek, kapasite ve performans açısından önemli gelişmeler sağlar. Bu, Azure portal gelişmiş Intune yönetim deneyimleri ve iyileştirilmiş iş akışları sunar. 

Kuruluşunuzun Windows cihazlarını yönetmek için Intune 'u Azure 'da kullanırken aşağıdaki noktaları göz önünde bulundurun:

## <a name="manage-windows-10-devices-by-using-mdm"></a>MDM kullanarak Windows 10 cihazları yönetme

Eski Intune PC istemcisini kullanmak yerine Windows 10 cihazlarınızı yönetmek için [Mobil Cihaz Yönetimi'ni (MDM)](../configuration/device-restrictions-windows-10.md) kullanmanızı öneririz. MDM aracılığıyla Windows 10'u yönetme olanağı Intune on Azure portalında bulunur. Windows 10 MDM, eski Intune PC istemcisi aracılığıyla bulunmayan pek çok yeni yönetim ve güvenlik özelliği sunar.

## <a name="legacy-pc-client-features-are-only-available-in-the-silverlight-console"></a>Eski PC İstemcisi özellikleri yalnızca Silverlight konsolunda bulunur

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Intune PC İstemci yönetimi iş akışları, [Silverlight tabanlı Intune Yönetici Konsolu](https://manage.microsoft.com/)'nu kullanır; bu da aşağıdaki sonuçları doğurur:

- Intune bilgisayar istemcisini kullanarak tüm gruplandırma olmayan yönetim görevleri için Silverlight konsolunu kullanmanız gerekir.
- Grupları yönetirken [Intune on Azure portal](https://portal.azure.com/)'ı kullanmalısınız. Bu gereklilik, Intune artık eski Intune Grupları yerine Azure AD Gruplarını kullandığı için ortaya çıkar. 

Azure AD gruplarına geçiş nedeniyle, Silverlight konsolu Pano görünümlerinde "grup tabanlı" filtreleme biraz değişmiş. Güncelleştirilmiş Silverlight Arabiriminde filtre uygulamak için şu adımları izleyin:

1. Bir görünüm seçin.
2. **Filtreler** kutusuna filtrelemek istediğiniz grubun adını girin ve enter tuşuna basın. Bu liste görünümü belirli bu gruptaki cihazlar için filtre uygular.

   ![Seçili olmayan filtre açılan girişi](./media/intune-legacy-pc-client/image01.png)


## <a name="continue-to-manage-windows-7-by-using-intune-pc-client"></a>Intune PC Client'ı kullanarak Windows 7'yi yönetmeye devam etme

MDM kullanılarak yönetilebilecek Windows 7 için yalnızca Silverlight konsolundaki mevcut Intune bılgısayar Istemci yeteneklerini desteklemeye devam edeceğiz. Windows 10'a yükselttiğinizde MDM yönetimine geçmeyi düşünün.

## <a name="mdm-capabilities"></a>MDM Özellikleri

PC İstemcisi ve MDM özellikleri arasında ayrıntılı bir karşılaştırma için bkz. [Windows PC'leri bilgisayarlar veya mobil cihazlar olarak yönetmeyi karşılaştırma](pc-management-comparison.md). MDM güncellemeleri, Win 32 uygulamaları için seçenekler de dahil olmak üzere MDM'ye kaydolan Windows 10 cihazlarına yeni yönetim özellikleri getirmeye devam edecektir. Hizmete en son sürüm eklemeleri için [yenilikleri](whats-new.md) görüntüleyin.

## <a name="switch-from-pc-client-to-mdm"></a>PC istemciden MDM’ye geçiş yapmak için

Intune PC İstemcisi ile Windows 10 cihazlarını yönetmekten MDM ile yönetime geçiş yapmak için şu adımları izleyin:

1. Silverlight konsolunda, cihazın kaydını PC İstemcisi'nden kaldırmak için bir **Seçmeli silme** gerçekleştirin.
  ![' Cihazı seçmeli olarak sil ' radyo düğmesi seçili olan uyarı açılan penceresi](./media/intune-legacy-pc-client/image02.png)
2. [MDM (ve/veya Azure AD Join)](../enrollment/windows-enroll.md)'i kullanarak cihazı yeniden kaydedin.

## <a name="next-steps"></a>Sonraki adımlar
[Windows cihazlarını kaydetme](../enrollment/windows-enroll.md)
