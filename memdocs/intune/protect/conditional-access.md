---
title: Microsoft Intune koşullu erişim
titleSuffix: Microsoft Intune
description: Kullanıcıların, cihazların ve uygulamaların Microsoft Intune içindeki şirket kaynaklarına erişmek için karşılaması gereken koşulları nasıl tanımlayacağınızı öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/06/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1973f38-ea55-43eb-a151-505fb34a8afb
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e2b8c8d715a7b60dd6111a6495b8f470cd92778
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329506"
---
# <a name="learn-about-conditional-access-and-intune"></a>Koşullu erişim ve Intune hakkında bilgi edinin

Koşullu erişimle, e-postanıza ve şirket kaynaklarınıza bağlanabilecek cihazları ve uygulamaları kontrol edebilirsiniz. 

Enterprise Mobility + Security (EMS) tek başına bir ürün değildir. Bu, EMS 'nin parçası olan tüm hizmet ve ürünlerin parçası olan bir çözümdür. Koşullu erişim, kullanıcılara herhangi bir cihazdan ve herhangi bir konumdan en iyi iş yapmasına izin veren bir deneyim sunarak kurumsal verilerinizi güvende tutmaya yönelik ayrıntılı erişim denetimi sağlar.

Kurumsal verilerinize erişim için konum, cihaz, kullanıcı durumu ve uygulama hassaslığı temelinde bir geçit oluşturan koşullar tanımlayabilirsiniz.

> [!NOTE]
> Koşullu Erişim, sahip olduğu özellikleri [Office 365 hizmetlerine](https://docs.microsoft.com/office365/enterprise/office-365-client-support-conditional-access) de yayar.

![Koşullu erişim diyagramı](./media/conditional-access/ca-diagram-1.png)

## <a name="use-conditional-access-with-intune"></a>Intune ile koşullu erişim kullanma

Koşullu erişim, bir Azure Active Directory Premium lisansıyla birlikte sunulan bir Azure Active Directory özelliğidir. Intune, çözüme mobil cihaz uyumluluğu ve mobil uygulama yönetimi ekleyerek bu özelliği geliştirir. 

![EMS kullanırken Intune ve koşullu erişim](./media/conditional-access/intune-with-ca-1.png)

Intune ile koşullu erişim kullanmanın yolları:

- **Cihaz tabanlı koşullu erişim**

  - Şirket içi Exchange için koşullu erişim

  - Ağ erişim denetimi tabanlı koşullu erişim

  - Cihaz riskine dayalı koşullu erişim

  - Windows bilgisayarları için koşullu erişim

    - Şirkete ait olanlar

    - Kendi cihazını getir (KCG)

- **Uygulama tabanlı koşullu erişim**

## <a name="next-steps"></a>Sonraki adımlar

[Intune ile koşullu erişim kullanmanın yaygın yolları](conditional-access-intune-common-ways-use.md)