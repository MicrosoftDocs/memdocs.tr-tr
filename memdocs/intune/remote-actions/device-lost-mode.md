---
title: Microsoft Intune-Azure ile iOS/ıpados kayıp modunu etkinleştirme | Microsoft Docs
description: Microsoft Intune kullanarak kayıp veya çalınan bir iOS/ıpados cihazının kilit ekranında görüntülenen bir iletiyi özelleştirmek için kayıp modunu açın veya başlatın. Kayıp modu eylemini kullanırken güvenlik ve gizlilik bilgileri hakkındaki ayrıntıları alın.
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
ms.assetid: 126a7489-fe3e-43fd-a681-defb2fe0bb66
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cf638ba82d1b6e91e3c4c24d5cfd3433df3b010
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80326529"
---
# <a name="enable-lost-mode-on-iosipados-devices-with-intune"></a>Intune ile iOS/ıpados cihazlarında kayıp modunu etkinleştirme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**Kayıp modu** cihaz eylemi, kayıp veya çalınan IOS/ıpados cihazlarında kayıp modunu etkinleştirmenize yardımcı olur. Bu mod, cihazın kilit ekranında gösterilecek iletiyi ve telefon numarasını girmenize olanak tanır. Kayıp modu kullanmak için, cihazın denetimli modda olan şirkete ait bir iOS/ıpados cihazı olması gerekir.

## <a name="supported-platforms"></a>Desteklenen platformlar

- iOS 9.3 ve üzeri
- ıpados 13,0 veya üzeri

Bu özellik aşağıdakilerde desteklenmez: 
- Windows
- Windows Phone
- Mac OS
- Android

## <a name="enable-lost-mode"></a>Kayıp modunu etkinleştirme

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Cihazlar**’ı ve ardından **Tüm Cihazlar**’ı seçin.
4. Yönettiğiniz cihazların listesinden bir iOS/ıpados cihazı seçin ve **kayıp modu (yalnızca denetimli)** seçin.
5. **Kayıp modu**altında **Etkinleştir**' i seçin.
6. **Kilit ekranında görüntülenecek ileti**içinde, cihazın kilit ekranında görüntülenecek bir ileti yazın.
7. İsteğe bağlı olarak, **görüntülenecek telefon numarası** kutusuna bir telefon numarası girin.
6. Değişikliklerinizi kaydetmek için **Tamam**’ı seçin.

Kayıp modunu etkinleştirdiğinizde cihazın tüm kullanımı engellenir. Siz kayıp modunu devre dışı bırakmadıkça son kullanıcı cihaza erişemez. Kayıp modu etkin durumdayken, cihazı bulmak için [Cihazı bul](device-locate.md) eylemini kullanın.

## <a name="security-and-privacy-information-for-the-lost-mode-and-locate-device-actions"></a>Kayıp modu ve cihazı bul eylemleri için güvenlik ve gizlilik bilgileri
- Siz bu eylemi açana kadar Intune'a hiçbir cihaz konum bilgisi gönderilmez.
- Cihazı bul eylemini kullandığınızda, cihazın enlem ve boylam koordinatları Intune'a gönderilir ve Azure portalında gösterilir.
- Veriler 24 saat depolandıktan sonra kaldırılır. Konum verilerini el ile kaldıramazsınız.
- Konum verileri hem depolanma hem de aktarım sırasında şifrelenir.
- Kilit ekranında gösterilecek iletide, kaybolan cihazın iade edilmesi için belirli ayrıntıları eklediğinizden emin olun.

## <a name="next-steps"></a>Sonraki adımlar

Kayıp modunu etkinleştirme durumunu görmek için **cihazlar**' ı açın ve **cihaz eylemleri**' ni seçin.
