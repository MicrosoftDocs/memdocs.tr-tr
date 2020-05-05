---
title: Windows bilgisayarlar için kullanıcı-cihaz bağlamayı yönetme
titleSuffix: Microsoft Intune
description: Bir kullanıcı Intune tarafından yönetilen bir Windows bilgisayara nasıl bağlanır?
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 53c99d63-c312-442a-8a71-de1b10fcd39b
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: a8c501eee596a64015eeb332d4d1b96d46356ba1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077878"
---
# <a name="manage-user-device-linking-for-windows-pcs"></a>Windows bilgisayarlar için kullanıcı-cihaz bağlamayı yönetme

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Bu konudaki bilgiler, yalnızca Intune yazılım istemcisini kullanarak bilgisayar olarak yönettiğiniz Windows masaüstü cihazlar için geçerlidir. 

Bir kullanıcı için yazılım dağıtmadan önce kullanıcıyı bir bilgisayara bağlamanız gerekir. Bir kullanıcıyı birden çok bilgisayara bağlayabilirsiniz, ancak her bilgisayara yalnızca bir kullanıcı bağlanabilir. Kullanıcılar şirket portalını kullanarak Intune kaydını yaptıkları bilgisayarlara otomatik olarak bağlanır.

Bir cihazın birincil kullanıcısı hakkında daha fazla bilgi için bkz. [birincil kullanıcıyı bulma](../remote-actions/find-primary-user.md).

Bir kullanıcıyı bir bilgisayara bağlamak için:

1. [Microsoft Intune yönetim konsolunda](https://manage.microsoft.com/)**Gruplar** &gt; **Tüm Cihazlar**’ı (veya bir kullanıcıya bağlamak istediğiniz bilgisayarı içeren başka bir grubu) seçin.

2. Kullanıcıya bağlamak istediğiniz bilgisayarı seçin ve ardından **Kullanıcı Bağla**'yı seçin.

   **Kullanıcı Bağla** iletişim kutusu mevcut kullanıcıların görünen adı, kullanıcı kimliği ve her kullanıcının bağlı olduğu bilgisayar sayısını içeren bir liste görüntüler. Bir Kullanıcı seçili BILGISAYARA zaten bağlıysa, o kullanıcının adı ve Kullanıcı KIMLIĞI **Geçerli Kullanıcı**altında görüntülenir. Bilgisayar hiçbir kullanıcıya bağlanmamışsa **Geçerli Kullanıcı** altında **Kullanıcı Yok**görüntülenir.

3. Aşağıdakilerden birini yapın:

   - Bilgisayarın bağlı olduğu bir kullanıcı varsa bilgisayarı bu kullanıcıya bağlı olarak bırakmak için **İptal**'i seçin.

   - Varsa, geçerli kullanıcının bağlantısını kaldırmak için <strong> **&gt;** bağlantıyı kaldır Tamam</strong>' ı seçin.

   - Bilgisayarı yeni bir kullanıcıya bağlamak için **Tüm kullanıcılar** listesinde bir kullanıcı seçin. Kullanıcı verilerinin doğru olduğundan emin olun ve ardından **Tamam**' ı seçin.

> [!TIP]
> Son kullanıcıların bilgisayarlara bağlanma yeteneğini kısıtlamak istiyorsanız **Microsoft Intune Aracı Ayarları** ilkesinde **Kullanıcıların bilgisayarlara bağlanma yeteneğini kısıtla** seçeneğini etkinleştirin.

## <a name="see-also"></a>Ayrıca bkz.

[Intune yazılım istemcisi ile genel Windows bilgisayar yönetim görevleri](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
