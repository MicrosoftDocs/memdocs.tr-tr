---
title: Microsoft Intune-Azure ile macOS çekirdek uzantıları cihaz profili oluşturma | Microsoft Docs
titleSuffix: ''
description: Bir macOS cihaz profili ekleyin veya oluşturun ve ardından Kullanıcı geçersiz kılması, takım tanımlayıcısı eklemek ve Microsoft Intune bir paket ve takım tanımlayıcısı sağlamak için çekirdek uzantıları yapılandırın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8f9212d275b17db6a40e3133b5363cd13c9d13d6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551408"
---
# <a name="add-macos-kernel-extensions-in-intune"></a>Intune 'A macOS çekirdek uzantıları ekleme

> [!NOTE]
> macOS çekirdek uzantıları sistem uzantıları ile değiştiriliyor. Daha fazla bilgi için bkz. [destek İpucu: Intune 'Da macOS Catalina 10,15 için çekirdek uzantıları yerine sistem uzantılarını kullanma](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

MacOS cihazlarında, çekirdek düzeyinde özellikler ekleyebilirsiniz. Bu özellikler, işletim sisteminin normal programların erişememe bölümlerine erişir. Kuruluşunuz, bir uygulamada ve bir cihaz özelliğinde bulunmayan belirli gereksinimlere veya gereksinimlere sahip olabilir. 

Cihazlarınızda her zaman yüklenmesine izin verilen çekirdek uzantıları eklemek için, Microsoft Intune ' de "çekirdek uzantıları" (KEXT) ekleyin ve ardından bu uzantıları cihazlarınıza dağıtın.

Örneğin, cihazınızı kötü amaçlı içeriğe karşı tarayan bir virüs tarama programı vardır. Bu virüs tarama programının çekirdek uzantısını Intune 'da izin verilen bir çekirdek uzantısı olarak ekleyebilirsiniz. Ardından, uzantıyı macOS cihazlarınıza "atayın".

Yöneticiler, bu özellik ile kullanıcıların çekirdek uzantılarını geçersiz kılmasına, takım tanımlayıcıları eklemesine ve Intune 'A belirli çekirdek uzantıları eklemesine izin verebilir.

Bu özellik şu platformlarda geçerlidir:

- macOS 10.13.2 ve üzeri

Bu özelliği kullanmak için cihazların şu olması gerekir:

- Apple 'ın Aygıt Kayıt Programı (DEP) kullanılarak Intune 'A kayıtlı. [MacOS cihazlarının otomatik olarak kaydedilmesi](../enrollment/device-enrollment-program-enroll-macos.md) daha fazla bilgi içerir.

  OR

- "Kullanıcı onaylı kayıt" (Apple 'ın dönemi) ile Intune 'A kaydolmuş. [MacOS High Sierra içindeki çekirdek uzantılarında değişikliklere hazırlanma](https://support.apple.com/en-us/HT208019) (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

Intune, kuruluşunuzun ihtiyaçlarına göre bu ayarları oluşturmak ve özelleştirmek için "yapılandırma profillerini" kullanır. Bu özellikleri bir profile ekledikten sonra, profili kuruluşunuzdaki macOS cihazlarına gönderebilir veya dağıtabilirsiniz.

Bu makalede, Intune 'da çekirdek uzantıları kullanılarak bir cihaz yapılandırma profili oluşturma konusu gösterilmektedir.

> [!TIP]
> Çekirdek uzantıları hakkında daha fazla bilgi için bkz. [çekirdek uzantısına genel bakış](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (Apple 'ın Web sitesini açar).

## <a name="what-you-need-to-know"></a>Bilmeniz gerekenler

- İmzasız eski çekirdek uzantıları eklenebilir.
- Çekirdek uzantısının doğru takım tanımlayıcısını ve paket KIMLIĞINI girdiğinizden emin olun. Intune girdiğiniz değerleri doğrulamaz. Yanlış bilgi girerseniz, uzantı cihazda çalışmaz. Bir takım tanımlayıcısı, tam olarak 10 alfasayısal karakter uzunluğundadır. 

> [!NOTE]
> Apple tüm yazılımlar için imzalama ve imza hakkında bilgi yayımladı. MacOS 10.14.5 ve daha yeni sürümlerde, Intune aracılığıyla dağıtılan çekirdek uzantıları Apple 'ın önemli ilkesini karşılamak zorunda kalmaz.
>
> Bu ilke ve tüm güncelleştirmeler veya değişiklikler hakkında bilgi için aşağıdaki kaynaklara bakın:
>
> - [Dağıtıma başlamadan önce uygulamanızı yeniden dağıtma](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (Apple 'ın Web sitesini açar) 
> - [MacOS High Sierra içindeki çekirdek uzantılarında değişikliklere hazırlanma](https://support.apple.com/en-us/HT208019) (Apple 'ın Web sitesini açar)

> [!NOTE]
> Intune kullanıcı arabirimi (UI) tam ekran deneyimine sahiptir ve birkaç hafta sürebilir. Kiracınız bu güncelleştirmeyi alıncaya kadar, bu makalede açıklanan ayarları oluştururken veya düzenlerken biraz farklı bir iş akışına sahip olursunuz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **MacOS** seçin
    - **Profil**: **uzantıları**seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **MacOS: cihazlara çekirdek uzantıları ekleme**.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda ayarlarınızı yapılandırın:

    - [Mac OS](kernel-extensions-settings-macos.md)

8. **İleri**’yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, `US-NC IT Team` veya `JohnGlenn_ITDepartment`gibi belirli BT gruplarına filtrelemek için bir etiket atayın. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak kullanıcıları veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulduktan sonra atanmak için hazırlanın. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).
