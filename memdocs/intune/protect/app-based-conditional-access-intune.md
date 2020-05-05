---
title: Intune ile uygulama tabanlı koşullu erişim
titleSuffix: Microsoft Intune
description: Uygulama tabanlı Koşullu erişimin Intune ile nasıl çalıştığını öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b399fba0-5dd4-4777-bc9b-856af038ec41
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 27033c2452224bc93e335f3517c9548ad65666c4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82080156"
---
# <a name="app-based-conditional-access-with-intune"></a>Intune ile uygulama tabanlı koşullu erişim

[Intune uygulama koruma ilkeleri](../apps/app-protection-policy.md) Intune’da kayıtlı cihazlarda şirket verilerinizi korumaya yardımcı olur. Uygulama koruma ilkelerini, yönetilmek üzere Intune’da kaydedilmemiş çalışan cihazları üzerinde de uygulayabilirsiniz. Bu durumda, şirketiniz cihazı yönetmiyor olmasına rağmen, şirket verilerinizin ve kaynaklarınızın korunmasını sağlamanız gerekir.

Uygulama tabanlı koşullu erişim ve istemci uygulama yönetimi, yalnızca Intune uygulama koruma ilkelerini destekleyen istemci uygulamalarının Exchange Online ve diğer Office 365 hizmetlerine erişebilmesini sağlayarak bir güvenlik katmanı ekler.

> [!NOTE]
> Yönetilen bir uygulama, uygulama koruma ilkelerinin uygulandığı ve Intune tarafından yönetilebilen bir uygulamadır.

Yalnızca Microsoft Outlook uygulamasının Exchange Online 'a erişmesine izin vermek için iOS/ıpados ve Android 'teki yerleşik posta uygulamalarını engelleyebilirsiniz. Ayrıca, Intune uygulama koruma ilkeleri, SharePoint Online 'a erişimi olmayan uygulamaları engelleyebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

Uygulama tabanlı bir koşullu erişim ilkesi oluşturmadan önce, şunları yapmanız gerekir:

- **Enterprise Mobility + Security (EMS)** veya bir **Azure Active Directory (AD) Premium aboneliği**
- Kullanıcıların EMS veya Azure AD lisansına sahip olması gerekir

Daha fazla bilgi için bkz. [Enterprise Mobility fiyatlandırması](https://www.microsoft.com/cloud-platform/enterprise-mobility-pricing) veya [Azure Active Directory fiyatlandırması](https://azure.microsoft.com/pricing/details/active-directory/).

## <a name="supported-apps"></a>Desteklenen uygulamalar

Uygulama tabanlı koşullu erişimi destekleyen uygulamaların listesi [Azure Active Directory Koşullu erişim teknik başvuru belgelerinde bulunabilir.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference)

Uygulama tabanlı koşullu erişim, [iş kolu (LOB) uygulamalarını da destekler](app-modern-authentication-block.md), ancak bu uygulamaların [Office 365 modern kimlik doğrulamasını](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)kullanması gerekir. 

## <a name="how-app-based-conditional-access-works"></a>Uygulama tabanlı Koşullu erişimin nasıl çalıştığı

Bu örnekte, yönetici Outlook uygulamasına uygulama koruma ilkeleri uygulamıştır ve ardından Outlook uygulamasını kurumsal e-postaya erişirken kullanılabilecek onaylanan uygulamalar listesine ekleyen bir koşullu erişim kuralı gelir.

> [!NOTE]
> Aşağıdaki akış çizelgesi diğer yönetilen uygulamalar için kullanılabilir.

![Akış grafiğinde gösterilen uygulama tabanlı koşullu erişim işlemi](./media/app-based-conditional-access-intune/ca-intune-common-ways-3.png)

1. Kullanıcı, Azure AD kimlik doğrulamasını Outlook uygulamasından gerçekleştirmeye çalışır.

2. Kullanıcı ilk kez kimlik doğrulamaya çalıştığında, aracı bir uygulama yüklemek üzere uygulama mağazasına yönlendirilir. Aracı uygulama, iOS için Microsoft Authenticator ya da Android cihazlar için Microsoft Şirket portalı olabilir.

   Kullanıcılar yerel bir e-posta uygulaması kullanmaya çalışırlarsa, daha sonra Outlook uygulamasını yüklemek için App Store 'a yönlendirilir.

3. Aracı uygulama cihaza yüklenir.

4. Aracı uygulama, Azure AD'de bir cihaz kaydı oluşturan Azure AD kayıt işlemini başlatır. Bu, mobil cihaz yönetimi (MDM) kayıt işlemiyle aynı değildir, ancak koşullu erişim ilkelerinin cihazda zorlanabilmesi için bu kayıt gereklidir.

5. Aracı uygulama, uygulamanın kimliğini doğrular. Bir güvenlik katmanı, uygulamanın kullanıcı tarafından kullanım için yetkilendirildiğini, aracı uygulamasının doğrulayabilmesini sağlayacak.

6. Aracı uygulaması, ilke onaylı listesinde olup olmadığını kontrol etmek için Kullanıcı kimlik doğrulama işleminin bir parçası olarak uygulama Istemci KIMLIĞINI Azure AD 'ye gönderir.

7. Azure AD, kullanıcının onaylı ilke listesine dayalı olarak uygulamanın kimliğini doğrulamasına ve kullanmasına olanak sağlar. Uygulama listede yoksa Azure AD uygulamaya erişimi engeller.

8. Outlook uygulaması, Exchange Online ile iletişim başlatmak için Outlook Bulut Hizmeti ile iletişim kurar.

9. Outlook Bulut Hizmeti, kullanıcı için Exchange Online hizmet erişim belirteci almak için Azure AD ile iletişim kurar.

10. Outlook uygulaması kullanıcının şirket e-postasını almak için Exchange Online ile iletişim kurar.

11. Şirket e-postası kullanıcının posta kutusuna gönderilir.

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama tabanlı bir koşullu erişim ilkesi oluşturma](app-based-conditional-access-intune-create.md)

[Modern kimlik doğrulaması olmayan uygulamaları engelleme](app-modern-authentication-block.md)
