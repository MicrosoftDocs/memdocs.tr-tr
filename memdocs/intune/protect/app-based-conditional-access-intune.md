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
ms.openlocfilehash: 04a8cd4ce64b566bf2d90ef301c1be44589a53e4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329974"
---
# <a name="app-based-conditional-access-with-intune"></a>Intune ile uygulama tabanlı koşullu erişim

[Intune uygulama koruma ilkeleri](../apps/app-protection-policy.md) Intune’da kayıtlı cihazlarda şirket verilerinizi korumaya yardımcı olur. Uygulama koruma ilkelerini, yönetilmek üzere Intune’da kaydedilmemiş çalışan cihazları üzerinde de uygulayabilirsiniz. Bu durumda, şirketiniz cihazı yönetmiyor olmasına rağmen, şirket verilerinizin ve kaynaklarınızın korunmasını sağlamanız gerekir.

Uygulama tabanlı koşullu erişim ve istemci uygulama yönetimi, Exchange Online ve diğer Office 365 hizmetlerine yalnızca Intune uygulama koruma ilkelerini destekleyen istemci uygulamaların erişmesine izin vererek bir güvenlik katmanı ekler.

> [!NOTE]
> Yönetilen bir uygulama, uygulama koruma ilkelerinin uygulandığı ve Intune tarafından yönetilebilen bir uygulamadır.

Yalnızca Microsoft Outlook uygulamasının Exchange Online 'a erişmesine izin vermek için iOS/ıpados ve Android 'teki yerleşik posta uygulamalarını engelleyebilirsiniz. Ayrıca, Intune uygulama koruma ilkelerinin uygulanmadığı uygulamaların SharePoint Online'a erişmesini engelleyebilirsiniz.

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

   Kullanıcılar yerel bir e-posta uygulaması kullanmaya çalışırsa önce uygulama mağazasına yeniden yönlendirilir ve ardından Outlook uygulamasını yüklemeleri gerekir.

3. Aracı uygulama cihaza yüklenir.

4. Aracı uygulama, Azure AD'de bir cihaz kaydı oluşturan Azure AD kayıt işlemini başlatır. Bu, mobil cihaz yönetimi (MDM) kayıt işlemiyle aynı değildir, ancak koşullu erişim ilkelerinin cihazda zorlanabilmesi için bu kayıt gereklidir.

5. Aracı uygulama, uygulamanın kimliğini doğrular. Aracı uygulamanın kullanıcı tarafından kullanılma yetkisi olup olmadığının doğrulayabilmesi için bir güvenlik katmanı vardır.

6. Aracı uygulama, kullanıcı kimlik doğrulama işleminin bir parçası olarak Uygulama İstemci kimliğini Azure AD’ye gönderir ve böylece bunun onaylı ilke listesinde olup olmadığı denetlenebilir.

7. Azure AD, kullanıcının onaylı ilke listesine dayalı olarak uygulamanın kimliğini doğrulamasına ve kullanmasına olanak sağlar. Uygulama listede yoksa Azure AD uygulamaya erişimi engeller.

8. Outlook uygulaması, Exchange Online ile iletişim başlatmak için Outlook Bulut Hizmeti ile iletişim kurar.

9. Outlook Bulut Hizmeti, kullanıcı için Exchange Online hizmet erişim belirteci almak için Azure AD ile iletişim kurar.

10. Outlook uygulaması kullanıcının şirket e-postasını almak için Exchange Online ile iletişim kurar.

11. Şirket e-postası kullanıcının posta kutusuna gönderilir.

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama tabanlı bir koşullu erişim ilkesi oluşturma](app-based-conditional-access-intune-create.md)

[Modern kimlik doğrulaması olmayan uygulamaları engelleme](app-modern-authentication-block.md)
