---
title: Microsoft Intune-Azure ile kayıp iOS/ıpados cihazları bulma | Microsoft Docs
description: Microsoft Intune içindeki cihazı Bul özelliğini kullanarak kayıp veya çalınan iOS/ıpados cihazlarını bulun. Cihazı bulma eylemini kullanılırken güvenlik ve gizlilik bilgileri hakkındaki ayrıntıları alabilirsiniz.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3e544286-12ad-4a3a-86f8-d2cf16940b1f
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 433bea6442ef52cd970513213d1623faf8aae2ca
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327476"
---
# <a name="locate-lost-or-stolen-iosipados-devices-with-intune"></a>Intune ile kaybolan veya çalınan iOS/ıpados cihazlarını bulma

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Bir haritadaki kayıp veya çalınmış bir iOS/ıpados cihazının konumunu almak için **Cihazı bul** eylemini kullanın. Cihazın denetimli modda olması gerekir. Bu eylemi kullanmadan önce cihazın [kayıp modunda](device-lost-mode.md) olduğundan emin olun.

## <a name="supported-platforms"></a>Desteklenen platformlar

- iOS/ıpados 9,3 ve üzeri

Bu özellik aşağıdaki sistemlerde desteklenmez: 
- Windows
- Windows Phone
- Mac OS
- Android

## <a name="locate-a-lost-or-stolen-device"></a>Kaybolan veya çalınan bir cihazın yerini bulma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Cihazlar**’ı ve ardından **Tüm Cihazlar**’ı seçin.
4. Yönettiğiniz cihazların listesinden bir iOS/ıpados cihazı seçin ve... seçeneğini belirleyin **. Daha fazla**. Ardından **Cihazı bul** uzak eylemini seçin.
5. Cihaz bulunduktan sonra, konumu **Cihazı bul** kısmında gösterilir.
    ![Azure'da Intune kullanarak Cihazı bulma eyleminin ekran görüntüsü](./media/device-locate/locate-device.png)


## <a name="activate-lost-mode-sound-alert-on-an-ios-device"></a>iOS cihazında kayıp modu ses uyarısını etkinleştirme

Birisi iOS/ıpados 9,3 veya üzeri cihazını kaybetmişse, kullanıcının bulması için cihazı bir uyarı sesi çalmak üzere uzaktan tetikleyebilirsiniz. Cihazın [kayıp modunda](device-lost-mode.md) olması gerekir.

[Azure Portal Intune](https://aka.ms/intuneportal)' da, **cihazlar** > **tüm cihazlar** ' ı seçin > iOS/ıpados cihazı seçin > **genel bakış** > kayıp modu**daha fazla** > **çal (yalnızca denetimli)**.

Kullanıcı cihazda sesi devre dışı bırakana veya cihaz kayıp modundan çıkarılana kadar ses çalmaya devam eder.


## <a name="security-and-privacy-information-for-lost-mode-and-locate-device-actions"></a>Kayıp modu ve cihazı bul eylemleri için güvenlik ve gizlilik bilgileri
- Siz bu eylemi açana kadar Intune'a hiçbir cihaz konum bilgisi gönderilmez.
- Cihazı bul eylemini kullandığınızda, cihazın enlem ve boylam koordinatları Graph API kullanılarak alınabilir.
- Veriler 24 saat depolandıktan sonra kaldırılır. Konum verilerini el ile kaldıramazsınız.
- Konum verileri hem depolanma hem de aktarım sırasında şifrelenir.
- Kayıp modunu yapılandırdığınızda, kilit ekranında gösterilen iletiyi özelleştirebilirsiniz. Bu iletiye, cihazı bulan kişiye yardımcı olmak üzere, kayıp cihazı iade etmesi için belirli ayrıntıları eklediğinizden emin olun.

## <a name="next-steps"></a>Sonraki adımlar

Cihazı bulmayı etkinleştirme durumunu görmek için **cihazlar**' ı açın ve **cihaz eylemleri**' ni seçin.
