---
title: Microsoft Intune-Azure 'da ilke kullanarak cihaz özelliklerini kısıtlama | Microsoft Docs
description: Android, macOS, iOS, ıpados, Windows Phone ve Windows 10 cihazlarında özellikleri kısıtlamak için bir cihaz profili ekleyin Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28cf0b8bffc06a0b5a56165c1e9eeab780c453c7
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332322"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Microsoft Intune’da cihaz kısıtlama ayarlarını yapılandırma



Intune, yöneticilerin Android, iOS/ıpados, macOS ve Windows cihazlarını denetlemesine yardımcı olan cihaz kısıtlama ilkeleri içerir. Bu kısıtlamalar, kuruluşunuzun kaynaklarını korumak için çok çeşitli ayarları ve özellikleri denetlemenize olanak tanır. Örneğin, yöneticiler şunları yapabilir:

- Cihaz kamerasına izin ver veya engelle
- Google Play, uygulama mağazalarına erişimi denetleme, belgeleri ve oyunları görüntüleme
- Yerleşik uygulamaları engelleyin veya izin verilen veya yasaklanmış uygulamaların bir listesini oluşturun
- Dosyaları bulut ve depolama hesaplarına yedeklemeye izin ver veya engelle
- En az parola uzunluğu ayarla ve basit parolaları engelle

Bu özellikler Intune 'da kullanılabilir ve yönetici tarafından yapılandırılabilir. Intune, kuruluşunuzun ihtiyaçlarına göre bu ayarları oluşturmak ve özelleştirmek için "yapılandırma profillerini" kullanır. Bu özellikleri bir profile ekledikten sonra, profili kuruluşunuzdaki cihazlara gönderebilir veya dağıtabilirsiniz.

Bu makalede bir cihaz kısıtlama profili oluşturma yöntemi gösterilmektedir. Farklı platformlar için kullanılabilir tüm ayarları da görebilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **iOS/ıpados: cihazlarda kamera blok**' dır.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:  

        - **Android**
        - **Android kurumsal**
        - **iOS/ıpados**
        - **macOS**
        - **Windows Phone 8.1**
        - **Windows 8.1 ve üzeri**
        - **Windows 10 ve üzeri**

    - **Profil türü**: **cihaz kısıtlamalarını**seçin.

        Windows 10 Team cihazları için Surface Hub gibi bir cihaz kısıtlama profili oluşturmak için, **cihaz kısıtlamaları (Windows 10 ekibi)** öğesini seçin.

4. Seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklılık gösterir. Ayrıntılı ayarlar için platformunuzu seçin:

    - [Android ayarları](device-restrictions-android.md)
    - [Android kurumsal ayarları](device-restrictions-android-for-work.md)
    - [iOS/ıpados ayarları](device-restrictions-ios.md)
    - [macOS ayarları](device-restrictions-macos.md)
    - [Windows Phone 8.1 ayarları](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 ayarları](device-restrictions-windows-10.md)
    - [Windows 10 Team ayarları](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business ayarları](device-restrictions-windows-holographic.md)

5. İşiniz bittiğinde **Tamam** > **Oluştur**’u seçerek değişikliklerinizi kaydedin.

Profil oluşturulur ve profiller listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulduktan sonra atanmak için hazırlanın. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
