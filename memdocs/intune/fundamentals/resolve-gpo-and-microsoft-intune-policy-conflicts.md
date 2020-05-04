---
title: GPO ve Intune ilkesi çakışmalarını çözümleme
titleSuffix: Microsoft Intune
description: Grup İlkesi ile Intune yapılandırma ilkeleri arasındaki çakışmaları çözmeyi öğrenin.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e76af5b7-e933-442c-a9d3-3b42c5f5868b
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a159d9d2cb31090fdb38ef2fc692f6af0297166
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330686"
---
# <a name="resolve-group-policy-objects-gpo-and-microsoft-intune-policy-conflicts"></a>Grup İlkesi Nesneleri (GPO) ve Microsoft Intune ilke çakışmalarını çözme

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> Bu konudaki bilgiler, yalnızca Intune yazılım istemcisini kullanarak bilgisayar olarak yönettiğiniz Windows masaüstü cihazlar için geçerlidir.

Intune, Windows bilgisayarlarda ayarları yönetmenize yardımcı olan ilkeler kullanır. Örneğin, bilgisayarlardaki Windows Güvenlik Duvarı’nın ayarlarını denetlemek için bir ilke kullanabilirsiniz. Birçok Intune ayarı Windows Grup İlkesi'yle yapılandırdığınız ayarlara benzer. Ancak, bazen iki yöntemin birbiriyle çakışması mümkündür.

Çakışmalar gerçekleştiğinde, bılgısayar etki alanında oturum açamadıkça etki alanı düzeyi grup ilkesi Intune ilkesi üzerinden önceliklidir. Etki alanında oturum açılamadığı durumda, istemci bilgisayara Intune ilkesi uygulanır.

## <a name="what-to-do-if-you-are-using-group-policy"></a>Grup İlkesi kullanıyorsanız yapmanız gerekenler
Uyguladığınız ilkelerin Grup İlkesi tarafından yönetilmediğinden emin olun. Çakışmaları önlemek için aşağıdaki yöntemlerden bir veya birkaçını kullanabilirsiniz:

- Intune istemcisini yüklemeden önce bilgisayarlarınızı Grup İlkesi ayarları uygulanmamış bir Active Directory kuruluş birimine (OU) taşıyın. Ayrıca, Intune’a kaydolmuş ve Grup İlkesi ayarları uygulamak istemediğiniz bilgisayarlar içeren OU’larda Grup İlkesi devralmayı engelleyebilirsiniz.

- GPO’ları yalnızca Intune tarafından yönetilmeyen bilgisayarlarla kısıtlamak için bir güvenlik grubu filtresi kullanın.

- Intune ilkeleriyle çakışan Grup İlkesi Nesnelerini devre dışı bırakın veya kaldırın.

Active Directory ve Windows Grup İlkesi hakkında daha fazla bilgi için, Windows Server Belgelerinize bakın.

## <a name="how-to-filter-existing-gpos-to-avoid-conflicts-with-intune-policy"></a>Intune ilkesiyle Çakışmaları önlemek için mevcut GPO’ları filtreleme
Intune ilkeleriyle çakışan ayarlara sahip GPO’lar belirlediyseniz, bu GPO’ları yalnızca Intune tarafından yönetilmeyen bilgisayarlarla kısıtlamak için güvenlik grubu filtreleri kullanabilirsiniz.

<!--- ### Use WMI filters
WMI filters selectively apply GPOs to computers that satisfy the conditions of a query. To apply a WMI filter, deploy a WMI class instance to all PCs in the enterprise before you enroll any PCs in the Intune service.

#### To apply WMI filters to a GPO

1. Create a management object file by copying and pasting the following into a text file, and then saving it to a convenient location as **WIT.mof**. The file contains the WMI class instance that you deploy to PCs that you want to enroll in the Intune service.

    ```
    //Beginning of MOF file.
    #pragma classflags("forceupdate")
    #pragma namespace ("\\\\.\\Root")
    instance of __Namespace
    {
       Name = "WindowsIntune";
    };

    #pragma namespace ("\\\\.\\Root\\WindowsIntune")
    [
       Description("This class defines Microsoft Intune common properties")
    ]
    class WindowsIntune_ManagedNode
    {
       [ read, Description("This defines whether Microsoft Intune Policy is enabled"): DisableOverride ToSubClass ]
       boolean WindowsIntunePolicyEnabled;
       [ read, key, Description("This property defines the version." "Example: 1.0"): ToSubClass ]
       string Version;
    };

    instance of WindowsIntune_ManagedNode
    {
       Version = "1.0";
       WindowsIntunePolicyEnabled = 1;
    };
    ```

2. Use either a startup script or Group Policy to deploy the file. The following is the deployment command for the startup script. The WMI class instance must be deployed before you enroll client PCs in the Intune service.

    **C:/Windows/System32/Wbem/MOFCOMP &lt;path to MOF file&gt;\wit.mof**

3. Run either of the following commands to create the WMI filters, depending on whether the GPO you want to filter applies to PCs that are managed by using Intune or to PCs that are not managed by using Intune.

    - For GPOs that apply to PCs that are not managed by using Intune, use the following:

        ```
        Namespace:root\WindowsIntune
        Query:  SELECT WindowsIntunePolicyEnabled FROM WindowsIntune_ManagedNode WHERE WindowsIntunePolicyEnabled=0
        ```

    - For GPOs that apply to PCs that are managed by Intune, use the following:

        ```
        Namespace:root\WindowsIntune
        Query:  SELECT WindowsIntunePolicyEnabled FROM WindowsIntune_ManagedNode WHERE WindowsIntunePolicyEnabled=1
        ```

4. Edit the GPO in the Group Policy Management console to apply the WMI filter that you created in the previous step.

    - For GPOs that should apply only to PCs that you want to manage by using Intune, apply the filter **WindowsIntunePolicyEnabled=1**.

    - For GPOs that should apply only to PCs that you do not want to manage by using Intune, apply the filter **WindowsIntunePolicyEnabled=0**.

For more information about how to apply WMI filters in Group Policy, see the blog post [Security Filtering, WMI Filtering, and Item-level Targeting in Group Policy Preferences](https://go.microsoft.com/fwlink/?LinkId=177883). --->


GPO'ları yalnızca seçili bir GPO için Grup İlkesi Yönetimi konsolunun **Güvenlik Filtrelemesi** alanında belirtilen güvenlik gruplarına uygulayabilirsiniz. Varsayılan olarak, GPO'lar *Kimliği Doğrulanmış Kullanıcılara* uygulanır.

- **Active Directory Kullanıcıları ve Bilgisayarları** ek bileşeninde, Intune tarafından yönetilmesini istemediğiniz bilgisayarlar ve kullanıcı hesaplarını içeren yeni bir güvenlik grubu oluşturun. Örneğin, grubu *Microsoft Intune’da Değil* olarak adlandırabilirsiniz.

- Grup İlkesi Yönetimi konsolunda, seçili GPO için **Temsilci** sekmesinde, güvenlik grubundaki kullanıcılar ve bilgisayarlar için uygun **Okuma** ve **Grup İlkesi Uygulama** izinlerini vermek için yeni güvenlik grubuna sağ tıklayın. (**Grup İlkesi Uygulama** izinleri **Gelişmiş** iletişim kutusunda bulunur.)

- Daha sonra, yeni güvenlik grubu filtresini seçili bir GPO'ya uygulayın ve **Kimliği Doğrulanmış Kullanıcılar** varsayılan filtresini kaldırın.

Yeni güvenlik grubu Intune hizmet değişikliklerinde kayıt olarak korunmalıdır.

## <a name="see-also"></a>Ayrıca bkz.
[Microsoft Intune ile Windows bilgisayarları yönetme](manage-windows-pcs-with-microsoft-intune.md)
