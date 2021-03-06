---
title: Cihazları Microsoft Intune - Azure ile kilitleme | Microsoft Docs
description: PIN veya parola ile korunan bir cihazı kilitlemek için Microsoft Intune'daki Uzaktan kilitleme eylemini kullanın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e558c885098b8b396ca0e6304bd18ef36e3c28b
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252246"
---
# <a name="remotely-lock-devices-with-intune"></a>Intune ile cihazları uzaktan kilitleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**Uzaktan kilitleme** cihaz eylemi, cihazı kilitler. Cihazın kilidini açmak için cihaz sahibi geçiş kodunu girer. PIN veya parolası bulunan cihazları uzaktan kilitleyebilirsiniz. PIN veya parolası olmayan cihazlar uzaktan kilitlenemez.

## <a name="supported-platforms"></a>Desteklenen platformlar

**Uzaktan kilitleme**, aşağıdaki platformlarda desteklenir:

- Android
- Android kurumsal bilgi noktası cihazları
- Android kurumsal iş profili cihazları
- Android kurumsal tam yönetilen cihazlar
- Android kurumsal şirkete ait iş profili cihazları
- iOS
- macOS

Şu platformlarda **Uzaktan kilitleme** desteklenmez:
- Windows 10 masaüstü

> [!NOTE]
> macOS cihazlar için 6 basamaklı bir kurtarma PIN’i ayarlarsınız. Cihaz kilitliyken, **Cihaz genel bakışı** başka bir cihaz eylemi gönderilene kadar PIN’i görüntüler. Lütfen PIN 'i yazdığınızdan emin olun çünkü yalnızca, uzaktan kilitleme komutu gönderildikten sonra 30 gün boyunca kullanılabilir olacak. 30 günden sonra Intune artık PIN 'e sahip olmayacaktır. Ayrıca, bu komutu aynı cihaz için yeniden başlatırsanız, bu komutu, cihazın kilidini başarıyla açmak için ilk PIN kullanılmadığından, raporlama sırasında başarısız bir durum görürsünüz. Bu komutu yalnızca bir kez göndermeniz, PIN 'i yazmanız ve macOS cihazına başarıyla ulaşmak için kullanana kadar bu komutu aynı cihaza yeniden göndermeye çalışmayın.


## <a name="remote-lock-a-device"></a>Cihazı uzaktan kilitleme

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Cihazlar**  >  **tüm cihazlar**' ı seçin.
4. Cihaz listesinde bir cihaz seçin ve ardından **Uzaktan kilitle** eylemini seçin.

## <a name="next-steps"></a>Sonraki adımlar

- Bu eylemin durumunu görmek için **Microsoft Intune**  >  **cihazlar**  >  **cihaz eylemleri**' ni seçin. 
- Cihazlarınızı yönetmenize yardımcı olabilecek diğer eylemler için bkz. [Kullanılabilir eylemler](device-management.md).
