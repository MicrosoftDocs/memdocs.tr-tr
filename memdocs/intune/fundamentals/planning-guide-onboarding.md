---
title: Intune ortama ekleme işlemi
titleSuffix: Microsoft Intune
description: Bu makale, ortamınıza bir Microsoft Intune yalnızca bulut çözümünü eklerken göz önünde bulundurmanız gereken tüm ayrıntıları sağlar.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ac7bd764-5365-4920-8fd0-ea57d5ebe039
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 19de56bfab6e4f4cf2f1243c6cbaf98053e6ba5e
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663268"
---
# <a name="implement-your-microsoft-intune-plan"></a>Microsoft Intune planınızı uygulama

Ekleme işlemi sırasında Intune’u üretim ortamınıza dağıtırsınız. Uygulama işlemi, [kullanım örneği gereksinimlerinize](planning-guide-requirements.md) dayalı olarak Intune ve (gerekirse) dış bağımlılıkların kurulması ve yapılandırılmasından oluşur.

Aşağıdaki bölümde, gereksinimleri ve üst düzey görevleri içeren Intune’un uygulanma işlemine genel bir bakış sağlanır.

## <a name="intune-requirements"></a>Intune gereksinimleri

Tek başına Intune temel gereksinimleri şöyledir:

- Enterprise Mobility + Security (EMS)/Intune aboneliği

- Office 365 aboneliği (Office uygulamaları ve uygulama koruma ilkesiyle yönetilen uygulamalar için)

- Apple APNs sertifikası (iOS/ıpados cihaz platformu yönetimini etkinleştirmek için)

- Azure AD Connect (dizin eşitleme için)

- Exchange için Intune şirket Içi Bağlayıcısı (gerekirse şirket Içi Exchange için koşullu erişim için)

- Intune Sertifika Bağlayıcısı (gerekirse SCEP sertifika dağıtımı için)

>[!TIP]
> Intune ile yönetebileceğiniz cihazların tam listesi için [desteklenen cihazlar](supported-devices-browsers.md) listesine bakın.

## <a name="intune-implementation-process"></a>Intune’un uygulanma işlemi

Bir Intune dağıtımı için 13 ayrı görev tanımladık. İş gereksinimlerinize, mevcut altyapınıza ve cihaz yönetim stratejinize bağlık olarak bu görevlerden bazılarını zaten tamamlamış olabilirsiniz. Bazıları ise planınıza uymayabilir.

### <a name="task-1-get-an-intune-subscription"></a>Görev 1: Intune aboneliği alma

Yukarıdaki Intune gereksinimleri bölümünde belirtildiği gibi bir EMS veya Intune aboneliği gereklidir. Kuruluşunuzun bu hizmetlere aboneliği yoksa Enterprise Mobility + Security (EMS) veya Intune satın almak istediğinize dair Microsoft’la veya Microsoft hesap ekibiyle iletişime geçin.

- [Microsoft Intune satın alma](https://www.microsoft.com/cloud-platform/microsoft-intune-pricing) hakkında daha fazla bilgi edinin.

### <a name="task-2-add-office-365-subscription"></a>Görev 2: Office 365 aboneliği ekleme

Bu adım isteğe bağlıdır. Exchange Online’ı kullanmak Office mobil uygulamalarını uygulama koruma ilkeleriyle yönetmek istiyorsanız Office 365 aboneliğiniz olmalıdır. Kuruluşunuzun Office 365 aboneliği yoksa Office 365 satın almak istediğinize dair Microsoft’la veya Microsoft hesap ekibiyle iletişime geçin.

- [Office 365 satın alma](https://products.office.com/business/compare-office-365-for-business-plans) hakkında daha fazla bilgi edinin.

### <a name="task-3-add-users-groups-in-azure-ad"></a>Görev 3: Azure AD'de kullanıcı grupları ekleme

Intune dağıtımı kullanım örneği senaryolarına ve gereksinimlerine bağlı olarak Active Directory veya Azure Active Directory’ye kullanıcı veya güvenlik grupları eklemeniz gerekebilir. Active Directory veya Azure Active Directory’deki mevcut kullanıcılarınızı ve güvenlik gruplarınızı gözden geçirerek gereksinimlerinizi tam olarak karşılayıp karşılamadıklarını belirleyin. Yeni kullanıcı ve güvenlik grupları eklerken, bunları Active Directory’ye ekleyip Azure AD Connect ile Azure Active Directory’ye eşitlemenizi öneririz.

- [Intune'a kullanıcılar/gruplar ekleme](users-add.md) hakkında daha fazla bilgi edinin.
<!---why not send them to the AAD connect topic? Question out to Andre: https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect--->


### <a name="task-4-assign-intune-and-office-365-user-licenses"></a>Görev 4: Intune ve Office 365 kullanıcı lisansları atama

EMS/Intune ve Office 365 dağıtımı için hedeflediğiniz tüm kullanıcıların kendilerine atanmış bir lisansı olması gerekir. Microsoft 365 Yönetim merkezinde EMS/Intune ve Office 365 lisansları atayabilirsiniz.

- [Intune lisansları atama](licenses-assign.md) hakkında daha fazla bilgi edinin.

### <a name="task-5-set-mobile-device-management-authority-to-intune"></a>Görev 5: Mobil cihaz yönetimi yetkilisi olarak Intune’u ayarlama

Intune kullanarak cihazları kurmaya, yapılandırmaya, yönetmeye ve kaydetmeye başlamadan önce cihaz yönetimi yetkilisi olarak Intune’u ayarlamanız gerekir.

- [Cihaz yönetimi yetkilisini ayarlama](mdm-authority-set.md)hakkında daha fazla bilgi edinin.

### <a name="task-6-enable-device-platforms"></a>Görev 6: Cihaz platformlarını etkinleştirme

Varsayılan olarak, çoğu cihaz platformu Apple cihazları (iOS/ıpados ve Mac) dışında etkindir. İOS/ıpados cihazlarının Intune 'A kaydedilebilmesi ve yönetilmesi için cihaz platformunun etkinleştirilmiş olması gerekir. Bunu yapmak için bir MDM Anında İletme sertifikası oluşturup bunu Intune’a eklemeniz gerekir.

- [Apple cihazların kaydını etkinleştirme](../enrollment/apple-mdm-push-certificate-get.md) hakkında daha fazla bilgi edinin.

### <a name="task-7-add-and-deploy-terms-and-conditions-policies"></a>Görev 7: Hüküm ve koşullar ilkeleri ekleme ve dağıtma

Intune, hüküm ve koşullar ilkelerini destekler. Hüküm ve koşullar ilkelerini gerektiği gibi ekleyin ve Intune dağıtım kullanım örneklerinize ve gereksinimlerinize göre hedeflenen gruplara dağıtın.

- [Hüküm ve koşullar ilkeleri ekleme ve dağıtma](../enrollment/terms-and-conditions-create.md) hakkında daha fazla bilgi edinin.

### <a name="task-8-add-and-deploy-configuration-policies"></a>Görev 8: Yapılandırma ilkeleri ekleme ve dağıtma

Intune, genel ve özel olmak üzere iki tür yapılandırma ilkesini destekler. Yapılandırma ilkelerini gerektiği gibi ekleyin ve Intune dağıtım kullanım örneklerinize ve gereksinimlerinize göre hedeflenen gruplara dağıtın.

- [Yapılandırma ilkeleri ekleme ve dağıtma](../configuration/device-profiles.md) hakkında daha fazla bilgi edinin.

### <a name="task-9-add-and-deploy-resource-profiles"></a>Görev 9: Kaynak profilleri ekleme ve dağıtma

Intune e-posta, Wi-Fi ve VPN profillerini destekler. Bu profilleri gerektiği gibi ekleyin ve Intune dağıtım kullanım örneklerinize ve gereksinimlerinize göre hedeflenen gruplara dağıtın.

- [Intune ile şirket kaynaklarına erişimi etkinleştirme](../configuration/device-profiles.md) hakkında daha fazla bilgi edinin.

### <a name="task-10-add-and-deploy-apps"></a>Görev 10: Uygulama ekleme ve dağıtma

Intune; web, iş kolu ve genel Mağaza uygulamalarının dağıtımını destekler. Ayrıca, uygulama koruma ilkeleriyle ilişkilendirerek Intune SDK’sını tümleştiren uygulamaları da yönetebilirsiniz. Uygulamaları gerektiği gibi ekleyin ve Intune dağıtım kullanım örneklerinize ve gereksinimlerinize göre hedeflenen gruplara dağıtın.

- [Uygulamaları ekleme ve dağıtma](../apps/app-management.md) hakkında daha fazla bilgi edinin.

### <a name="task-11-add-and-deploy-compliance-policies"></a>Görev 11: Uyumluluk ilkelerini ekleme ve dağıtma

Intune, uyumluluk ilkelerini destekler. Uyumluluk ilkelerini gerektiği gibi ekleyin ve Intune dağıtım kullanım örneklerinize ve gereksinimlerinize göre hedeflenen gruplara dağıtın.

- [Uyumluluk ilkeleri](../protect/device-compliance-get-started.md) hakkında daha fazla bilgi edinin.

### <a name="task-12-enable-conditional-access-policies"></a>Görev 12: koşullu erişim ilkelerini etkinleştirme

Intune, Exchange Online, şirket içi Exchange, SharePoint Online, Skype Kurumsal Çevrimiçi ve Dynamics CRM Online için koşullu erişimi destekler. Koşullu Erişimi Intune dağıtım kullanım örneklerinize ve gereksinimlerinize göre uygun şekilde etkinleştirin ve yapılandırın.

- [Koşullu Erişim](../protect/conditional-access.md) hakkında daha fazla bilgi edinin.

### <a name="task-13-enroll-devices"></a>Görev 13: Cihazları kaydetme

Intune, iOS/ıpados, Mac OS, Android ve Windows Masaüstü cihaz platformlarını destekler. Mobil cihaz platformlarını Intune dağıtımı kullanım örneklerinize ve gereksinimlerinize göre uygun şekilde kaydedin.

- [Cihazları kaydetme](../enrollment/device-enrollment.md) hakkında daha fazla bilgi edinin.


## <a name="next-steps"></a>Sonraki adımlar
[Intune dağıtımınızı sınama ve doğrulama](planning-guide-test-validation.md) rehberlerine göz atın.
