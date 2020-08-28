---
title: Microsoft Intune’a kaydolma veya Intune’da oturum açma
description: Microsoft Intune aboneliğine kaydolma veya aboneliğinizle başlamak için oturum açma.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f3ce07a-b718-42a9-bace-f99a8b8abd94
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae034699d3a07311ca6a51557cbbc673916569bf
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994285"
---
# <a name="sign-up-or-sign-in-to-microsoft-intune"></a>Microsoft Intune’a kaydolma veya Intune’da oturum açma

Bu konu, sistem yöneticilerinin Intune hesabına nasıl kaydolacaklarını açıklar.

Intune’a kaydolmadan önce bir Microsoft Online Services hesabı, Kurumsal Anlaşma veya bunlara denk bir toplu lisanslama anlaşmanızın olup olmadığını belirleyin. Microsoft Toplu Lisanslama Sözleşmesi veya Microsoft 365 gibi diğer Microsoft bulut hizmetleri aboneliği, genellikle bir iş veya okul hesabı içerir.

Zaten bir iş veya okul hesabınız varsa bu hesapla **oturum açın** ve aboneliklerinize Intune’u ekleyin. Veya bunun yerine kuruluşunuz için Intune kullanmak üzere yeni bir hesaba **kaydolun**.

>[!WARNING]
>Yeni bir hesap için kaydolduktan sonra mevcut bir iş veya okul hesabını birleştirmeniz mümkün olmayacaktır.

## <a name="how-to-sign-up-for-intune"></a>Intune 'a kaydolma

1. [Intune Oturum Açma sayfasını](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20) ziyaret edin.

   ![Microsoft Intune Deneme hesabına kaydolma web sayfasının ekran görüntüsü](./media/account-sign-up/account-sign-up-site.png)

2. Kaydol sayfasında, yeni Intune aboneliğinizi yönetmek için oturum açın veya kaydolun.

## <a name="post-sign-up-considerations"></a>Kayıttan sonra dikkate alınacak noktalar

Yeni abonelik için kaydolduktan sonra, kayıt işlemi sırasında sağladığınız e-posta adresine hesap bilgilerinizi içeren bir e-posta iletisi alırsınız. Bu e-posta, aboneliğinizin etkin olduğunu doğrular.

Kaydolma işlemini tamamladıktan sonra, Kullanıcı eklemek ve lisansları atamak için kullanılan Microsoft 365 yönetim merkezine yönlendirilirsiniz. Yalnızca varsayılan onmicrosoft.com etki alanı adınızın kullanıldığı bulut tabanlı hesaplarınız varsa devam edip bu noktada kullanıcıları ekleyebilir ve lisansları atayabilirsiniz. Öte yandan, kuruluşunuzun [özel etki alanı adını](custom-domain-name-configure.md) kullanmayı veya şirket içi Active Directory’den [kullanıcı hesabı bilgilerini eşitlemeyi](users-add.md#sync-active-directory-and-add-users-to-intune) planlıyorsanız, bu tarayıcı penceresini kapatabilirsiniz.

## <a name="sign-in-to-microsoft-intune"></a>Microsoft Intune oturum açın

Intune 'a kaydolduktan sonra, hizmeti yönetmek üzere [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) 'da oturum açmak için [desteklenen bir tarayıcıyla](supported-devices-browsers.md#intune-supported-web-browsers) herhangi bir cihazı kullanabilirsiniz.

Varsayılan olarak, hesabınız Azure AD 'de aşağıdaki izinlerden birine sahip olmalıdır:

- Genel Yönetici
- Intune Hizmet Yöneticisi (Intune Yöneticisi olarak da bilinir)

Farklı izinlere sahip kullanıcılar için hizmeti yönetmek üzere erişim vermek için, bkz. [rol tabanlı Access Control](role-based-access-control.md)

### <a name="intune-admin-portal-url"></a>Intune yönetim portalı URL 'SI

Microsoft Uç Nokta Yöneticisi Yönetim Merkezi: https://endpoint.microsoft.com

Intune Azure portal: https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade

Eğitim için Intune: https://intuneeducation.portal.azure.com

Klasik Intune Portalı: https://manage.microsoft.com Klasik Intune portalı yalnızca ıNTUNE bilgisayar yazılım istemcisiyle kaydedilen cihazları yönetmek için kullanılır

### <a name="urls-for-intune-services-provided-by-microsoft-365"></a>Microsoft 365 tarafından sunulan Intune Hizmetleri için URL 'Ler

Microsoft 365 İş: https://portal.microsoft.com/adminportal

Microsoft 365 mobil cihaz yönetimi: https://admin.microsoft.com/adminportal/home#/MifoDevices

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft 365, Azure veya Intune 'da oturum açamazsınız](https://support.microsoft.com/help/2412085)
