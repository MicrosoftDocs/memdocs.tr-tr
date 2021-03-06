---
title: Microsoft Intune temel kurulumu
description: Bu makalede, Microsoft Intune’u ayarlamak için gerekli adımlar sağlanmaktadır.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60cfa440-0723-4ea0-bacf-3c5d26f9a1d3
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: c39174dded9fae0055786b6132b3f964f187b1b1
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992717"
---
# <a name="basic-setup"></a>Temel kurulum

Ortamınızı değerlendirdikten sonra Microsoft Intune ayarlama zamanı vardır.

## <a name="external-dependencies-for-an-intune-deployment"></a>Intune dağıtımı için dış bağımlılıklar

### <a name="identity"></a>Kimlik

Intune, kimlik ve Kullanıcı gruplama sağlayıcısı olarak Azure Active Directory (Azure AD) gerektirir. Aşağıdakiler hakkında daha fazla bilgi edinin:

- [Kimlik gereksinimleri](/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview#design-considerations-overview)

- [Dizin eşitleme gereksinimleri](/azure/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements)

- [Multi-Factor Authentication (MFA)](/azure/active-directory/authentication/concept-mfa-howitworks)

- [Kullanıcı ve cihaz gruplarınızı planlama](users-add.md)

- [Kullanıcı ve cihaz grupları oluşturma](groups-get-started.md)

Kuruluşunuz zaten Microsoft 365 kullanıyorsa, Intune 'un aynı Azure Active Directory ortamını kullanması gerekir.

### <a name="pki-optional"></a>PKI (isteğe bağlı)

Intune ile VPN, Wi-Fi veya e-posta profilleri için sertifika tabanlı kimlik doğrulama kullanmayı planlıyorsanız, sertifika profillerini oluşturmaya ve dağıtmaya hazırsınız ve desteklenen bir [PKI altyapısına](../protect/certificates-configure.md)sahip olduğunuzdan emin olmanız gerekir. Intune’da sertifikaları yapılandırma hakkında daha fazla bilgi edinin:

- [SCEP için sertifika altyapısını yapılandırma](/intune/certificates-scep-configure)

- [PFX için sertifika altyapısını yapılandırma](/intune/certficates-pfx-configure).

## <a name="task-list-for-an-intune-setup"></a>Intune kurulumu için görev listesi

### <a name="task-1-intune-subscription"></a>1. Görev: Intune aboneliği

Intune 'a geçirebilmeniz için önce bir [Intune aboneliğine](account-sign-up.md)ihtiyacınız vardır.

### <a name="task-2-assign-intune-user-licenses"></a>2. Görev: Intune kullanıcı lisanslarını atayın

- [Intune kullanıcı lisanslarının nasıl atanacağını](licenses-assign.md) öğrenin.

- Yeni bir Azure Active Directory kiracısı oluşturduysanız [yeni kullanıcılar oluşturma veya şirket içi Active Directory’den (AD) kullanıcı eşitleme.](/azure/active-directory/connect/active-directory-aadconnect)

### <a name="task-3-set-your-mdm-authority-to-intune"></a>3. Görev: MDM yetkilinizi Intune olarak ayarlayın

Intune 'U [Microsoft Endpoint Manager yönetim merkezini](https://go.microsoft.com/fwlink/?linkid=2109431)kullanarak yönetmenizi öneririz.

MDM yetkilinizi **Intune**olarak ayarlayın. Farklı bir MDM yetkilisi kullanmak, Intune’un MDM yönetimini diğer Microsoft yönetim konsollarına aktarmasını sağlar. Bu durum nadiren oluşur.

> [!IMPORTANT]
> Mobil cihaz yönetiminizi ilk defa Intune'a aktarıyorsanız MDM yetkilinizi Intune olarak ayarlamanız gerekir.

[Mobil yönetim yetkilisini ayarlamayı](mdm-authority-set.md) öğrenin.

## <a name="next-step"></a>Sonraki adım

[Cihaz ve uygulama yönetimi ilkelerini](migration-guide-configure-policies.md)yapılandırın.