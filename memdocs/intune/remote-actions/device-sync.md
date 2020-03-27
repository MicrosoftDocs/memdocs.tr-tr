---
title: Cihazları Microsoft Intune ile eşitleme-Azure | Microsoft Docs
description: En son ilkeleri ve eylemleri almak için Microsoft Intune ile kayıtlı veya yönetilen cihazları eşitleyin. Azure portalını kullanarak eşitleme adımlarını içerir ve yeniden denenebilecek hata kodlarını listeler.
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
ms.assetid: 02ad249e-f098-421f-861f-6b2ff733ac7c
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 54271edb7f9c4de240992ca2ca620866c9ca469c
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326238"
---
# <a name="sync-devices-to-get-the-latest-policies-and-actions-with-intune"></a>Intune ile en son ilkeleri ve eylemleri almak için cihazları eşitleme


Cihazı **Eşitle** eylemi, seçili cihazı Intune’a hemen giriş yapmaya zorlar. Bir cihaz giriş yaptığında, kendisine atanan beklemedeki eylem veya ilkeleri hemen alır. Bu özellik, atadığınız ilkeleri bir sonraki zamanlanmış iadeyi beklemenize gerek kalmadan hızla doğrulamanıza ve ilkelerin sorunlarını gidermenize yardımcı olur.

## <a name="supported-platforms"></a>Desteklenen platformlar

- Windows
- Windows Phone
- iOS
- Mac OS
- Android

## <a name="sync-a-device"></a>Cihaz eşitleme

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın. 
3. **Cihazlar** > **Tüm cihazlar**’ı seçin.
4. Yönettiğiniz cihazların listesinde, *genel bakış* bölmesini açmak için bir cihaz seçin ve ardından **Eşitle**' yi seçin.
5. Onaylamak için **Evet**'i seçin.

Eşitleme eyleminin durumunu görmek için **cihazlar** > **izleme** > **cihaz eylemleri**' ni seçin.

[Yenileme çevrimi süreleriyle](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)standart Intune ilke iade sıklıklarını bulabilirsiniz.

## <a name="retryable-error-codes"></a>Yeniden denenebilir hata kodları

Bir yönetici **eşitleme** cihazı eylemini çalıştırdığında, başarısız olan ve yeniden denenebilir bir hata kodu veren IOS/ıpados ve Android Uygulamaları hala cihaz için kullanılabilir. Ancak yeniden denenemez bir hata kodu vermiş uygulamalar, cihaz için kullanılabilir hale gelmeden önce yedi gün beklemek zorundadır.


| Hata kodu  | Önerilen açıklama | Yeniden denenebilir |
|---|---|---|
| 2016330898 | Bilinmeyen bir hata oluştu. | Hayır |
| 2016330897 | Intune bağlantınız zaman aşımına uğradı. Bağlantınızı sıfırlayın. | Evet |
| 2016330896 | İnternet bağlantınız kesildi. Bağlantınızı sıfırlayın. | Evet |
| 2016330895 | İnternet bağlantınız kesildi. Bağlantınızı sıfırlayın. | Evet |
| 2016330894 | İnternet bağlantınız kesildi. Bağlantınızı sıfırlayın. | Evet |
| 2016330893 | İnternet bağlantınız kesildi. Bağlantınızı sıfırlayın. | Evet|
| 2016330892 | Uluslararası dolaşım devre dışı bırakıldı. | Hayır|
| 2016330891 | Telefon araması sırasında bu cihaz için hücresel veri bağlantısına erişilemiyor. Görüşmenin sonlanmasını bekleyin. | Evet|
| 2016330890 | Bu cihaz için hücresel ağ. Bu cihazlar şu anda kullanılamıyor. | Hayır|
| 2016330889 | Güvenli bağlantı başarısız oldu. Bağlantınızı sıfırlayın. | Evet|
| 2016330888 | Sunucu güven değerlendirmesi başarısız oldu. | Hayır|

## <a name="next-steps"></a>Sonraki adımlar

Cihazın [ayrıntılarını denetleyebilirsiniz](device-inventory.md).
 
