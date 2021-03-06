---
title: Intune ile uygulama tabanlı koşullu erişim ilkesini ayarlama
titleSuffix: Microsoft Intune
description: Intune ile uygulama tabanlı bir koşullu erişim ilkesi oluşturmayı öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a61e92265447f8ceced83d493b9397713b67dca6
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909440"
---
# <a name="set-up-app-based-conditional-access-policies-with-intune"></a>Intune ile uygulama tabanlı koşullu erişim ilkeleri ayarlama

Onaylanan uygulamalar listesinin parçası olan uygulamalar için uygulama tabanlı koşullu erişim ilkeleri ayarlayın. Liste, Microsoft tarafından sınanan onaylı uygulamalardan oluşur.

Uygulama tabanlı koşullu erişim ilkelerini kullanabilmeniz için uygulamalarınıza [Intune uygulama koruma ilkelerinin](../apps/app-protection-policies.md) uygulanması gerekir.

> [!IMPORTANT]
> Bu makalede, basit uygulama tabanlı bir koşullu erişim ilkesi ekleme adımlarında izlenecek yol gösterilmektedir. Diğer bulut uygulamaları için de aynı adımları kullanabilirsiniz. Daha fazla bilgi için bkz. [koşullu erişim dağıtımını planlayın](/azure/active-directory/conditional-access/plan-conditional-access)

## <a name="create-app-based-conditional-access-policies"></a>Uygulama tabanlı koşullu erişim ilkeleri oluşturma

Koşullu Erişim, bir Azure Active Directory (Azure AD) teknolojisidir. *Intune* 'Dan erişebileceğiniz koşullu erişim düğümü, *Azure AD*'den erişebileceğiniz düğümdür. Aynı düğüm olduğundan, ilkeleri yapılandırmak için Intune ile Azure AD arasında geçiş yapmanız gerekmez.

Microsoft Endpoint Manager yönetim merkezinden koşullu erişim ilkeleri oluşturabilmeniz için önce bir Azure AD Premium lisansınızın olması gerekir.

### <a name="to-create-an-app-based-conditional-access-policy"></a>Uygulama tabanlı bir koşullu erişim ilkesi oluşturmak için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) oturum açın

2. **Endpoint Security**  >  **koşullu erişim**  >  **Yeni ilke**' yi seçin.

3. Bir ilke **adı**girin ve ardından *atamalar*' ın altında **Kullanıcılar ve gruplar**' ı seçin. İlke için grupları eklemek üzere Dahil Et veya Hariç Tut seçeneklerini kullanın ve **Bitti**’yi seçin.

4. **Bulut uygulamaları veya eylemler**' i seçin ve korunacak uygulamaları seçin. Örneğin, **Uygulama Seç**' i seçin ve **Office 365 (Önizleme)** öğesini seçin.

   Değişikliklerinizi kaydetmek için **Bitti**’yi seçin.

5. **Conditions**  >  İlkeyi uygulamalara ve tarayıcılara uygulamak için koşullar**istemci uygulamaları** ' nı seçin. Örneğin **Evet**’i seçin ve ardından **Tarayıcı** ve **Mobil uygulamalar ve masaüstü istemciler**’i etkinleştirin.

   Değişikliklerinizi kaydetmek için **Bitti**’yi seçin.

6. *Erişim denetimleri*altında, cihaz uyumluluğuna göre koşullu erişim uygulamak Için **izin ver** ' i seçin. Örneğin, **erişim izni ver**  >  **onaylı istemci uygulaması gerektir** ' i seçin ve **Uygulama koruma ilkesi (Önizleme) gerektir** ' i seçin ve **Seçilen denetimlerden birini gerektir** ' i seçin

   Değişikliklerinizi kaydetmek için **Seçin**’e tıklayın.

7. **Ilkeyi etkinleştir**için **Açık**' ı seçin ve sonra değişikliklerinizi kaydetmek için **Oluştur** ' u seçin.





## <a name="next-steps"></a>Sonraki adımlar
[Modern kimlik doğrulaması olmayan uygulamaları engelleme](app-modern-authentication-block.md)

## <a name="see-also"></a>Ayrıca bkz.

Uygulama [koruma ilkeleriyle](../apps/app-protection-policies.md) 
 uygulama verilerini koruma [Azure Active Directory Koşullu erişim](/azure/active-directory/active-directory-conditional-access)