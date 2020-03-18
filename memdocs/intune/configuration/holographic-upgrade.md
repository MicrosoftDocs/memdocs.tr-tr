---
title: Windows Holographic for Business için yükseltme
titleSuffix: Microsoft Intune
description: Windows Holographic çalıştıran cihazları nasıl Windows Holographic for Business’a yükselteceğinizi öğrenin
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e809a888fc2696e54540ee6baa2271d7340579
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332086"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Windows Holographic çalıştıran cihazları Windows Holographic for Business’a yükseltme

Microsoft Intune cihazlarınızı yönetmenize ve korumanıza yardımcı olacak birçok ayar içerir. Bu makalede Windows holographic cihazlarını Windows holographic for Business 'a yükseltme ayarlarını listeler ve açıklanmaktadır. Bu ayarlar, Intune 'da gönderilen veya cihazlara dağıtılan bir yükseltme yapılandırma profilinde oluşturulur.

Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, Windows holographic cihazlarınızı yükseltmek için bu ayarları kullanın. Microsoft HoloLens için, yükseltme için gerekli lisansı almak üzere ticari paketi satın alabilirsiniz. Daha fazla bilgi için bkz. [Windows Holographic for Business özelliklerini etkinleştirme](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Bu özellik hakkında daha fazla bilgi için bkz. [Windows 10 sürümlerini yükseltme veya S modunu etkinleştirme](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Sürüm yükseltme

- **Yükseltilecek sürüm**: **iş Için Windows 10 holographic**' u seçin.
- **Lisans dosyası**: sıze sunulan XML Lisans dosyasına gidin ve seçin.

  ![Holographic for Business lisans bilgilerini içeren XML dosya adını girin](./media/holographic-upgrade/Holographic-edition-upgrade.png)
 
## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu, ancak henüz bir şey yapmamış olabilir. [Profili atadığınızdan](device-profile-assign.md)emin olun ve [durumunu izleyin](device-profile-monitor.md).

Ayrıca, [Windows 10 ve üzeri](edition-upgrade-windows-settings.md) cihazlar için sürüm yükseltme profilleri de oluşturabilirsiniz.
