---
title: Microsoft Intune - Azure’da cihaz profillerini görüntüleme | Microsoft Docs
description: Microsoft Intune’da cihaz yapılandırma profili ayrıntılarını görüntüleyin ve yönetin; ayrıca bir profile atanmış olan cihaz sayısının grafik gösterimine bakın ve hangi cihazların atanmış veya dağıtılmış profilleri olduğunu görün. Çakışan ayarlara sahip profillerde sorun da giderebilirsiniz.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9deaed87-fb4b-4689-ba88-067bc61686d7
ms.reviewer: karthib
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 23594bd1e728e20deba6d978fc2a1f678d692ff3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333138"
---
# <a name="monitor-device-profiles-in-microsoft-intune"></a>Microsoft Intune’da cihaz profillerini izleme



Intune, cihaz yapılandırma profillerinizi izlemeye ve yönetmeye yardımcı olacak bazı özellikler içerir. Örneğin, profilin durumunu denetleyebilir, hangi cihazların atandığına bakabilir ve profilin özelliklerini güncelleştirebilirsiniz.

## <a name="view-existing-profiles"></a>Mevcut profilleri görüntüleme

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Yapılandırma profillerinin** > **cihazları** ' nı seçin.

Tüm mevcut profilleriniz listelenir, ayrıca platform gibi ayrıntılar ve profilin herhangi bir cihaza atanıp atanmadığı gösterilir.

## <a name="view-details-on-a-profile"></a>Profildeki ayrıntıları görüntüleme

Cihaz profilinizi oluşturduktan sonra, Intune grafikler sağlar. Bu grafikler profilin durumunu, örneğin cihazlara başarıyla atandığını veya çakışma gösterip göstermediğini görüntüler.

1. Mevcut bir profil seçin. Örneğin, bir macOS profili seçin.
2. **Genel Bakış** sekmesini seçin.

    Üstteki grafik grafik, cihaz profiline atanan cihazların sayısını gösterir. Örneğin, yapılandırma cihaz profili macOS cihazlarında geçerliyse, grafik macOS cihazlarının sayısını listeler.

    Ayrıca ayrı cihaz profiline atanmış olan diğer platformlardaki cihazların sayısını da gösterir. Örneğin, macOS olmayan cihazların sayısını gösterir.

    ![Cihaz profiline atanmış olan cihazların sayısını görüntüleme](./media/device-profile-monitor/device-configuration-profile-graphical-chart.png)

    Alt grafik grafik, cihaz profiline atanan kullanıcı sayısını gösterir. Örneğin, yapılandırma cihaz profili macOS kullanıcılarında geçerliyse, grafik macOS kullanıcılarının sayısını listeler.

3. Üstteki grafikte yer alan daireyi seçin. **Cihaz durumu** açılır.

    Profile atanmış olan cihazlar listelenir ve profilin başarıyla dağıtılıp dağıtılmadığı gösterilir. Yalnızca belirli bir platformdaki (örneğin, macOS) cihazların listelendiğine de dikkat edin.

    **Cihaz durumu** ayrıntılarını kapatın.

4. Alttaki grafikte yer alan daireyi seçin. **Kullanıcı durumu** açılır. 

    Profile atanmış olan kullanıcılar listelenir ve profilin başarıyla dağıtılıp dağıtılmadığı gösterilir. Yalnızca belirli bir platformdaki (örneğin, macOS) kullanıcıların listelendiğine de dikkat edin.

    **Kullanıcı durumu** ayrıntılarını kapatın.

5. **Profiller** listesine dönerek belirli bir profil seçin. Ayrıca mevcut özellikleri değiştirebilirsiniz:
    - **Özellikler**: Adı değiştirin veya mevcut ayarlardan herhangi birini güncelleştirin.
    - **Atamalar**: İlkenin uygulanacağı cihazları dahil edin veya dışlayın. Belirli grupları seçmek için **Seçili Gruplar**'ı seçin.
    - **Cihaz durumu**: Profile atanmış olan cihazlar listelenir ve profilin başarıyla dağıtılıp dağıtılmadığı gösterilir. Belirli bir cihazı seçerek, yüklü uygulamalar da dahil olmak üzere daha da fazla ayrıntı görebilirsiniz.
    - **Kullanıcı durumu**: bu profilden etkilenen cihazların bulunduğu Kullanıcı adlarını ve profil başarıyla dağıtılırsa listeler. Belirli bir kullanıcı seçerek daha da fazla ayrıntı görebilirsiniz.
    - **Ayar başına durum**: Profil içindeki tek tek ayarları göstererek çıkışa filtre uygular ve ayarın başarıyla uygulanıp uygulanmadığını gösterir.

## <a name="view-conflicts"></a>Çakışmaları görüntüleme

**Cihazlar** > **Tüm cihazlar**’da çakışma yaratan ayarları görebilirsiniz. Bir çakışma olduğunda, bu ayarı içeren tüm yapılandırma profillerini de görürsünüz. Yöneticiler bu özelliği kullanarak sorun gidermeye ve profiller arasındaki herhangi bir uyuşmazlığı düzeltmeye yardımcı olabilir.

1. Intune’da **Cihazlar** > **Tüm Cihazlar**’ı seçtikten sonra listeden mevcut bir cihazı seçin. Son kullanıcılar, Şirket Portalı uygulamasından cihaz adını alabilir.
2. **Cihaz yapılandırması**’nı seçin. Cihaza uygulanan tüm yapılandırma ilkeleri listelenir.
3. İlkeyi seçin. İlke, cihaza uygulanan ilkedeki tüm ayarları gösterir. Bir cihaz **Çakışma** durumundaysa, o satırı seçin. Açılan yeni pencerede, çakışma yaratan ayara sahip tüm profilleri ve profil adlarını görürsünüz.

Çakışma yaratan ayarı ve bunu içeren ilkelerin hangileri olduğunu bulduğunuza göre çakışmayı çözümlemeniz daha kolay olacaktır. 

## <a name="device-firmware-configuration-interface-profile-reporting"></a>Cihaz üretici yazılımı yapılandırma arabirimi profil raporlaması

> [!WARNING]
> İzleme DFCı profilleri şu anda oluşturuluyor. DFCı genel önizlemede olduğundan, izleme verileri eksik veya eksik olabilir.

DFCı profilleri, diğer cihaz yapılandırma profillerinde olduğu gibi, ayar temelinde raporlanır. Üreticinin DFCı desteğine bağlı olarak bazı ayarlar uygulanmayabilir.

DFCı profil ayarlarınız ile aşağıdaki durumları görebilirsiniz:

- **Uyumlu**: Bu durum profildeki ayar değeri cihazdaki ayarla eşleştiğinde gösterir. Bu durum, aşağıdaki senaryolarda oluşabilir:

  - DFCı profili, profildeki ayarı başarıyla yapılandırdı.
  - Cihazda, bu ayar tarafından denetlenen donanım özelliği yok ve profil ayarı **devre dışı bırakıldı**.
  - UEFı, DFCı 'ın özelliği devre dışı bırakmasına izin vermez ve profil ayarı **etkinleştirilir**.
  - Cihazda özelliği devre dışı bırakma donanımı eksik ve profil ayarı **etkin**.

- **Uygulanamaz**: Bu durum, profildeki bir ayar değerinin **etkin**olduğu ve cihazdaki eşleşen ayar bulunamadığı zaman gösterir. Cihaz donanımının özelliği yoksa, bu durum oluşabilir.

- **Uyumsuz**: Bu durum profildeki ayar değerinin cihazdaki ayarla eşleşmediği zaman gösterir. Bu durum, aşağıdaki senaryolarda oluşabilir:

  - UEFı, DFCı 'nin bir ayarı devre dışı bırakmasına izin vermez ve profil ayarı **devre dışı bırakılır**.
  - Cihazda özelliği devre dışı bırakma donanımı eksik ve profil ayarı **devre dışı bırakıldı**.
  - Cihazda en son DFCı bellenim sürümü yok.
  - DFCı, UEFı menüsünde yerel bir "opt" denetimi kullanılarak Intune 'A kaydedilmeden önce devre dışı bırakıldı.
  - Cihaz Intune 'a Autopilot kaydı dışında kaydedildi.
  - Cihaz bir Microsoft CSP tarafından Autopilot 'e kaydolmadı veya doğrudan OEM tarafından kaydolmadı.

## <a name="next-steps"></a>Sonraki adımlar

[Cihaz profilleriyle ilgili yaygın sorular, sorunlar ve çözümler](device-profile-troubleshoot.md)  
[İlke ve profillerin ve Intune 'da sorun giderme](troubleshoot-policies-in-microsoft-intune.md)
