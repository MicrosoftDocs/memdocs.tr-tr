---
title: Microsoft Intune-Azure 'da eğitim ayarları ekleme veya yapılandırma | Microsoft Docs
description: Microsoft Intune Windows 10 ve üzeri cihazlarda bir cihaz yapılandırma profilinde bir test yap uygulamasını kullanın. Eğitim ayarlarını kullanarak bir yapılandırma profili oluşturun ve bir test uygulaması URL 'SI girin, kullanıcıların oturum açma biçimini seçin, test sırasında ekranı izleyin ve test sırasında metin önerilerine izin verin veya bu önerileri önleyin.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 12d04869834691167c2f31be853029c9a939a338
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79333094"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Microsoft Intune 'da Windows 10 cihazlarda bir test alma uygulaması kullanın



Intune 'da eğitim profilleri, öğrenciler için cihazlarda bir test veya sınava yönelik olarak tasarlanmıştır. Bu özellik bir test URL 'SI eklemek için **bir test** uygulaması ve ayarlar alma, son kullanıcıların teste nasıl oturum açmasını ve daha fazlasını içerir. Bu özellik aşağıdaki platformu destekler:

- Windows 10 ve üzeri

Kullanıcı oturum açtığında, bir test al uygulaması girdiğiniz test ile otomatik olarak açılır. Test devam ederken cihazda başka hiçbir uygulama çalıştırılamaz. [Windows 10 ' da testleri al](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) test alma uygulaması hakkında daha fazla bilgi sağlar.

Bu makalede Microsoft Intune ' de bir cihaz yapılandırma profili oluşturma adımları listelenir. Ayrıca, Windows 10 cihazlarınıza yönelik kullanılabilir eğitim ayarları hakkında bilgi almak ve bunları öğrenmek için bilgileri de içerir.

## <a name="create-a-device-profile"></a>Bir cihaz profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Ad**: Yeni profil için açıklayıcı bir ad girin.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Platform**: **Windows 10 ve üzeri** seçeneğini belirleyin.
    - **Profil**: **eğitim profili**seçin.

4. Yapılandırmak istediğiniz ayarları girin:

    - [Windows 10 ve üzeri](education-settings-windows.md)

5. Değişikliklerinizi kaydetmek için **Tamam** > **Oluştur** ' u seçin.

Ayarlarınızı girdikten ve profili oluşturduktan sonra profiliniz profil listesinde gösterilir. Daha sonra [bu profili bazı gruplara atayın](device-profile-assign.md).

## <a name="next-steps"></a>Sonraki adımlar

[Windows 10 eğitim ayarlarının](education-settings-windows.md) ve açıklamalarının listesini görüntüleyin.

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).
