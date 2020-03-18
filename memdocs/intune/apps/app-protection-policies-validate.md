---
title: Uygulama koruma ilkesi kurulumunuzu doğrulama
titleSuffix: Microsoft Intune
description: Microsoft Intune'da uygulama koruma ilkenizin kurulduğunu ve doğru şekilde çalıştığını sınamayı öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 15f8a838-0b69-412b-a42e-c6edb61f0cae
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e7ed0aa1d45c66c5688cde07b385cf95081a3c3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326238"
---
# <a name="how-to-validate-your-app-protection-policy-setup-in-microsoft-intune"></a>Microsoft Intune'da uygulama koruma ilkesi kurulumunuzu doğrulama

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Uygulama koruma ilkenizin doğru kurulduğunu ve çalıştığını doğrulayın. Bu kılavuz, Azure portaldaki uygulama koruma ilkeleri için geçerlidir.

## <a name="checking-for-symptoms"></a>Belirtileri denetleme
Uygulama koruma bir veri koruması aracı olduğundan, kullanıcıların soruları bildirme olasılığı düşüktür. Uygulama koruma yapılandırmasında bir sorun varsa, kullanıcılar uygulama korumanın olmadığı durumlardaki gibi sınırsız erişime sahip olur ve bir sorun olduğunun farkına varmazlar. Bu nedenle uygulama koruma kısıtlamalarını bilinçli olarak sınayabilecek küçük bir grup kullanıcıya uygulama koruma ilkelerinizin pilot dağıtımını yaparak, uygulama koruma yapılandırmanızı doğrulamanızı öneririz.

## <a name="what-to-check"></a>Denetlenmesi gerekenler

Sınama, uygulama koruma ilkelerinizin davranışının beklendiği gibi çalışmadığını gösteriyorsa şu öğeleri kontrol etmenizi öneririz:

- Kullanıcılar uygulama koruma için lisanslı mı?
- Kullanıcılar O365 için lisanslı mı?
- Her kullanıcının uygulama koruma uygulamalarındaki durumu beklendiği gibi mi? Uygulamalar için olabilecek durumlar **İade edildi** ve **İade edilmedi** şeklindedir.

### <a name="user-app-protection-status"></a>Kullanıcı uygulama koruma durumu
1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Uygulama koruma durumu** >  **uygulamalar** ' ı seçin ve ardından **atanan kullanıcılar** kutucuğunu seçin. 
4. **Uygulama raporlama** sayfasında **Kullanıcı seçin**'i belirterek kullanıcı ve grupların bulunduğu listeyi açın. 
5. Arama yapıp listeden bir kullanıcı seçin ve sonra **Kullanıcı seçin**’i belirtin. **Uygulama raporlama** bölmesinin en üstünde kullanıcının uygulama koruması için lisanslı olup olmadığını görebilirsiniz. Ayrıca, kullanıcının O365 lisansının olup olmadığını ve kullanıcının tüm cihazları için uygulama durumunu göreceksiniz.

## <a name="what-to-do"></a>Yapılması gereken
Kullanıcı durumuna göre gerçekleştirilecek eylemler şunlardır:

- Kullanıcının uygulama koruma lisansı yoksa bir [Intune lisansı](../fundamentals/licenses.md) atayın.
- Kullanıcının O365 lisansı yoksa bir [lisans](../fundamentals/licenses.md) edinin.
- Kullanıcının lisansı **İade edilmedi** olarak listeleniyorsa bu uygulama için doğru biçimde bir [uygulama koruma ilkesi](app-protection-policies-validate.md) yapılandırıp yapılandırmadığınıza bakın.
- Bu koşulların, [uygulama koruma ilkelerinin](app-protection-policies-monitor.md) geçerli olmasını istediğiniz tüm kullanıcılara uygulandığından emin olun.

## <a name="see-also"></a>Ayrıca bkz.

- [Intune uygulama koruma ilkesi nedir?](app-protection-policies.md)
- [Intune içeren lisanslar](../fundamentals/licenses.md)
- [Cihazlarını Intune’a kaydedebilmeleri için kullanıcılara lisans atama](../fundamentals/licenses-assign.md)
- [Uygulama koruma ilkesi kurulumunuzu doğrulama](app-protection-policies-validate.md)
- [Uygulama koruma ilkelerini izleme](app-protection-policies-monitor.md)

