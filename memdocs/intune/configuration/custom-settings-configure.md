---
title: Microsoft Intune - Azure'da özel cihaz ayarlarını kullanma | Microsoft Docs
description: Microsoft Intune kullanarak Windows 8.1, Windows 10 ve üzeri, Android Cihaz Yöneticisi, Android Enterprise, macOS ve iOS/ıpados cihazları için özel ayarları kullanmak üzere bir profil ekleyin veya oluşturun.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: aaa0deaf2c6332965f40ae02a47b7541cf2f9e8e
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146414"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Intune'da özel ayarlarla profil oluşturma

Microsoft Intune, bir cihazdaki farklı özellikleri denetlemek için pek çok yerleşik ayar içerir. Ayrıca, yerleşik profillere benzer şekilde oluşturulan özel profiller de oluşturabilirsiniz. Özel profiller, Intune’da yerleşik olarak bulunmayan cihaz ayarları ve özelliklerini kullanabilmenizi sağlar. Bu profiller, kuruluşunuzdaki cihazlarda denetleyebileceğiniz bazı özellik ve ayarlar içerir. Örneğin, her iOS/ıpados cihazı için aynı özelliği ayarlayan özel bir profil oluşturabilirsiniz.

Özel ayarlar her platform için ayrı yapılandırılır. Örneğin Android ve Windows cihazlarındaki özellikleri denetlemek için, Open Mobile Alliance Tekdüzen Kaynak Tanımlayıcısı (OMA-URI) değerleri girebilirsiniz. Apple cihazlar için [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) veya [Apple Profile Manager](https://support.apple.com/profile-manager) ile oluşturduğunuz bir dosyayı içeri aktarabilirsiniz.

Yapılandırma profilleri hakkında daha fazla bilgi için bkz. [Microsoft Intune cihaz profili nedir?](device-profiles.md).

Bu makalede, Android Cihaz Yöneticisi, Android Enterprise, iOS/ıpados, macOS ve Windows için nasıl özel bir profil oluşturacağınız gösterilmektedir. Farklı platformlar için kullanılabilir tüm ayarları da görebilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:  

        - **Android cihaz yöneticisi**
        - **Android Kurumsal**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 ve üzeri**

    - **Profil**: **özel**' i seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **Windows 10: Allowvpnoverhücresel özel OMA-URI ' y i sağlayan özel profildir**.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:

    - [Android cihaz yöneticisi](custom-settings-android.md)
    - [Android Kurumsal](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows 10 Holographic for Business](custom-settings-windows-holographic.md)

8. **İleri**’yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak kullanıcıları veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="example"></a>Örnek

Aşağıdaki örnekte, **Connectivity/AllowVPNOverCellular** ayarı etkinleştirilmiştir. Bu ayar, bir Windows 10 cihazın hücresel bir ağdayken VPN bağlantısı açmasına izin verir.

> [!div class="mx-imgBorder"]
> ![Intune ve Endpoint Manager 'da VPN ayarlarını içeren özel ilke örneği](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu, ancak henüz bir şey yapmamış olabilir. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).
