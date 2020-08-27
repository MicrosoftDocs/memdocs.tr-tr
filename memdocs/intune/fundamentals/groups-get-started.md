---
title: Azure portalında klasik Intune grupları
titleSuffix: Microsoft Intune
description: Microsoft Intune Azure portalında gruplarla ilgili yenilikleri öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/31/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 323f384d-8a76-4adc-999b-e508d641bfa1
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 82834dc3a7fc60292228acbd62c7c6a8b8a94ee3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909797"
---
# <a name="microsoft-intune-classic-groups-in-the-azure-portal"></a>Azure portalında klasik Microsoft Intune grupları

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Geri bildirimlerinizi aldık ve Microsoft Intune’da gruplarla çalışma konusunda bazı değişiklikler yaptık.
Intune’u Azure Portal’dan kullanıyorsanız, Intune gruplarınız Azure Active Directory güvenlik gruplarına geçirilmiştir.

Bunun size yararı, artık tüm Enterprise Mobility + Security ve Azure AD uygulamalarınızda aynı grup deneyimini kullanabilecek olmanızdır. Ayrıca, bu yeni işlevi genişletmek ve özelleştirmek için PowerShell ve Graph API’si kullanmanız da mümkündür.

Azure AD güvenlik grupları hem kullanıcılara hem de cihazlara tüm Intune dağıtımı türlerini destekler. Ayrıca, sağladığınız özniteliklere bağlı olarak otomatik güncelleştirilen Azure AD dinamik gruplarını kullanabilirsiniz. Örneğin, iOS 9 çalıştıran cihazlardan bir grup oluşturabilirsiniz. iOS 9 çalıştıran bir cihaz kaydedildiğinde otomatik olarak dinamik grupta görünür.

## <a name="what-is-not-available"></a>Neler kullanılamıyor?

Intune gruplarının daha önce kullanıyor olabileceğiniz bazı özellikleri Azure AD’de kullanılamıyor:

- **Gruplanmamış Kullanıcılar** ve **Gruplanmamış Cihazlar** Intune grupları artık yoktur.
- Bir gruptan **Belirli üyeleri hariç tut** seçeneği Azure Portal’da bulunmamaktadır. Ancak, bu davranışı tekrarlamak için gelişmiş kurallara sahip bir Azure AD güvenlik grubu kullanabilirsiniz. Örneğin, Satış departmanınızda çalışan herkesi bir güvenlik grubuna dahil eden ancak unvanında “Asistan” kelimesi bulunanları gruptan dışlayan gelişmiş bir kural oluşturmak için aşağıdaki gelişmiş kuralı kullanabilirsiniz:

  `(user.department -eq "Sales") -and -not (user.jobTitle -contains "Assistant")`.
- Klasik Intune konsolundaki **Tüm Exchange ActiveSync Tarafından Yönetilen Cihazlar** grubu Azure AD’ye geçirilmemiştir. Ancak, EAS tarafından yönetilen cihazlar hakkındaki bilgilere Azure portalından erişmeye devam edebilirsiniz.

## <a name="how-to-get-started"></a>Nereden başlayacaksınız?

- Azure AD güvenlik grupları ve nasıl çalıştıkları hakkında bilgi edinmek için aşağıdaki konuları okuyun:
  - [Azure Active Directory gruplarıyla kaynaklara erişimi yönetme](/azure/active-directory/fundamentals/active-directory-manage-groups).
  - [Azure Active Directory grupları yönetme](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal).
  - [Gelişmiş kurallar oluşturmak için öznitelikleri kullanma](/azure/active-directory/users-groups-roles/groups-dynamic-membership).
- Grup oluşturması gereken yöneticilerin **Intune Hizmet Yöneticisi** Azure AD rolüne eklenmesini sağlayın. Azure AD Hizmet Yöneticisi rolü, **Grubu Yönet** izinlerine sahip değildir.
- Intune gruplarınız **Belirli üyeleri dışla** seçeneğini kullandıysa, bu grupları dışlamalar olmadan yeniden tasarlama ya da iş gereksinimlerini karşılamak için gelişmiş kurallar kullanma arasında karar verin.


## <a name="what-happened-to-intune-groups"></a>Intune gruplarına ne oldu?
Gruplar Azure portalından Azure portalında Intune’a geçirilirken aşağıdaki kurallar uygulanır:

| Intune'da Gruplar|Azure AD grupları|
|-----------------------------------------------------------------------|-------------------------------------------------------------|
|Statik kullanıcı grubu|Statik Azure AD güvenlik grubu|
|Dinamik kullanıcı grubu|Bir Azure AD güvenlik grubu hiyerarşisi ile statik Azure AD güvenlik grupları|
|Statik cihaz grubu|Statik Azure AD güvenlik grubu|
|Dinamik cihaz grubu|Dinamik Azure AD güvenlik grubu|
|Dahil etme koşullu bir grup|Intune’da dahil etme koşulundan herhangi bir statik veya dinamik üye içeren Statik Azure AD güvenlik grubu|
|Dışlama koşullu bir grup|Geçirilmez|
|Yerleşik gruplar:<br>- **Tüm kullanıcılar**<br>- **Gruplanmamış Kullanıcılar**<br>- **Tüm cihazlar**<br>- **Gruplandırılmamış cihazlar**<br>- **Tüm bilgisayarlar**<br>- **Tüm mobil cihazlar**<br>- **MDM tarafından yönetilen tüm cihazlar**<br>- **EAS tarafından yönetilen tüm cihazlar**|Azure AD güvenlik grupları|

## <a name="group-hierarchy"></a>Grup hiyerarşisi

Intune konsolunda tüm grupların bir üst grubu vardı. Gruplar yalnızca üst gruplarının üyelerini içerebiliyordu. Azure AD’de alt gruplar, üst gruplarında yer almayan üyeler içerebilir.

## <a name="group-attributes"></a>Grup öznitelikleri
Öznitelikler, grupları tanımlamak için kullanılabilen cihaz özellikleridir. Bu tablo, bu ölçütlerin Azure AD güvenlik gruplarına nasıl geçirileceğini açıklar.

| Intune'da Öznitelik|Azure AD’de Öznitelik|
|-----------------------------------------------------------------------|-------------------------------------------------------------|
|Cihaz grupları için Kuruluş Birimi (OU) özniteliği|Dinamik gruplar için OU özniteliği.|
|Cihaz grupları için etki alanı adı özniteliği|Dinamik gruplar için Etki Alanı Adı özniteliği.|
|Kullanıcı grupları için bir öznitelik olarak güvenlik grubu|Azure AD dinamik sorgularda gruplar öznitelik olarak kullanılamaz. Dinamik gruplar yalnızca kullanıcı veya cihaza özel öznitelikler içerebilir.|
|Kullanıcı grupları için yönetici özniteliği|Dinamik gruplarda *yönetici* özniteliği için Gelişmiş Kural|
|Üst kullanıcı grubundan tüm kullanıcılar|O grubun üye olduğu statik grup|
|Üst cihaz grubundaki tüm mobil cihazlar|O grubun üye olduğu statik grup|
|Intune tarafından yönetilen tüm mobil cihazlar|Dinamik grup için değer olarak ' MDM ' olan Yönetim türü özniteliği|
|Statik gruplar içinde iç içe geçmiş gruplar |Statik gruplar içinde iç içe geçmiş gruplar|
|Dinamik gruplar içinde iç içe geçmiş gruplar|Bir iç içe geçme düzeyine sahip dinamik grup|

## <a name="what-happens-to-policies-and-apps-you-previously-deployed"></a>Daha önce dağıtmış olduğunuz ilkelere ve uygulamalara ne olur?

İlkeler ve uygulamalar daha önce olduğu gibi gruplara dağıtılmaya devam edilecektir. Ancak artık bu grupları Intune konsolu yerine Azure portalından yöneteceksiniz.