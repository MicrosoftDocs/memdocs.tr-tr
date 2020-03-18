---
title: Intune’a kurumsal tanımlayıcılar ekleme
titleSuffix: ''
description: Microsoft Intune’a kurumsal tanımlayıcıları (kayıt yöntemi, IMEI ve seri numaraları) eklemeyi öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 566ed16d-8030-42ee-bac9-5f8252a83012
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d57e2af03ba1d035f8285c4075d5cbc8ff6cfd38
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331598"
---
# <a name="identify-devices-as-corporate-owned"></a>Cihazları şirkete ait olarak tanımlama

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Bir Intune yöneticisi olarak cihazları şirkete ait olarak tanımlayabilir, böylece yönetim ve tanımlama işlemlerini geliştirebilirsiniz. Intune, ek yönetim görevleri gerçekleştirebilir ve tam telefon numarası ile şirkete ait cihazların uygulama envanteri gibi ilave bilgiler toplayabilir. Şirkete ait olmayan cihazların kaydını engellemek için cihaz kısıtlamaları da ayarlayabilirsiniz.

Kayıt sırasında Intune, şu özellikleri taşıyan cihazlara otomatik olarak şirkete ait durumunu atar:

- [Cihaz kayıt yöneticisi](device-enrollment-manager-enroll.md) hesabıyla kaydedildi (tüm platformlar)
- Apple [Aygıt Kayıt Programı](device-enrollment-program-enroll-ios.md), [Apple School Manager](apple-school-manager-set-up-ios.md) veya [Apple Configurator](apple-configurator-enroll-ios.md) ile kaydedildi (yalnızca iOS)
- Bir uluslararası mobil ekipman tanımlayıcısı (IMEI) numarası (IMEI numarası olan tüm platformlar) veya seri numarası (iOS ve Android) ile [kayıttan önce şirkete ait olarak tanımlandı](#identify-corporate-owned-devices-with-imei-or-serial-number)
- İş veya okul kimlik bilgileriyle Azure Active Directory katıldı. [Azure Active Directory kayıtlı olan cihazlar](https://docs.microsoft.com/azure/active-directory/devices/overview) kişisel olarak işaretlenir.
- [Cihazın özellikler listesinde](#change-device-ownership) şirket olarak ayarlı

Kayıttan sonra [Kişisel](#change-device-ownership) veya **Şirket** arasında **sahiplik ayarını değiştirebilirsiniz**.

## <a name="identify-corporate-owned-devices-with-imei-or-serial-number"></a>Şirkete ait cihazları IMEI veya seri numarası ile belirleme

Bir Intune yöneticisi olarak, 14 basamaklı IMEI numaralarını veya seri numaraları listeleyen bir virgülle ayrılmış değer (.csv) dosyası oluşturup içeri aktarabilirsiniz. Intune, cihaz kaydı sırasında cihaz sahipliğini şirket olarak belirtmek için bu tanımlayıcıları kullanır. Listede her IMEI numarası veya seri numarasının yönetim amacıyla belirtilen ayrıntıları bulunabilir.

Bu özellik aşağıdaki platformlar için desteklenir:

| Platfveyam | IMEı numaraları | Seri numaraları |
|---|---|---|
| Windows | Desteklenen (Windows Phone) | Desteklenmez |
| iOS/macOS | Desteklenmez | Desteklenir |
| Cihaz Yöneticisi yönetilen Android OS ile v10 arasındaki | Desteklenmez | Desteklenmez |
| Diğer Android | Desteklenmez | Desteklenir |

<!-- When you upload serial numbers for corporate-owned iOS/iPadOS devices, they must be paired with a corporate enrollment profile. Devices must then be enrolled using either Apple's device enrollment program (DEP) or Apple Configurator to have them appear as corporate-owned. -->

[Apple cihaz seri numarasını bulmayı öğrenin](https://support.apple.com/HT204308).<br>
[Android cihaz seri numaranızı bulmayı öğrenin](https://support.google.com/store/answer/3333000).

## <a name="add-corporate-identifiers-by-using-a-csv-file"></a>Bir .csv dosyası kullanarak kurumsal tanımlayıcılar ekleme
Listeyi oluşturmak için iki sütunlu, üst bilgisi olmayan bir virgülle ayrılmış değerler (.csv) listesi oluşturun. 14 basamaklı IMEI numaralarını veya seri numaraları sol sütuna, ayrıntıları sağ sütuna ekleyin. Tek bir .csv dosyasında yalnızca tek bir kimlik türü: IMEI veya seri numarası içeri aktarılabilir. Ayrıntılar 128 karakterle sınırlıdır ve yalnızca yönetimsel kullanım içindir. Ayrıntılar cihazda görüntülenmez. Her .csv dosyası için geçerli sınır 5.000 satırdır.

**Seri numaraları olan bir .csv dosyası yükleme** – Üst bilgi içermeyen, iki sütunlu, virgülle ayrılmış değer (.csv) listesini oluşturun ve .csv dosyası başına 5.000 cihaz veya 5 MB ile sınırlayın.

|||
|-|-|
|&lt;Kimlik 1&gt;|&lt;Cihaz 1 Ayrıntıları&gt;|
|&lt;Kimlik 2&gt;|&lt;Cihaz 2 Ayrıntıları&gt;|

Bu .csv dosyası bir metin düzenleyicisinde görüntülendiğinde aşağıdaki gibi görünür:

```
01234567890123,device details
02234567890123,device details
```

> [!IMPORTANT]
> Bazı Android ve iOS/ıpados cihazlarında birden çok ıMEı numarası vardır. Intune, kayıtlı cihaz başına yalnızca bir IMEI numarasını okur. IMEI numarasını içeri aktarıyorsanız ancak bu numara Intune tarafından envantere alınan IMEI numarası değilse cihaz şirkete ait değil, kişisel cihaz olarak sınıflandırılır. Bir cihaz için birden fazla IMEI numarası içe aktarırsanız envantere alınmayan numaralar kayıt durumunda **Bilinmeyen** değerini görüntüler.<br>
>Ayrıca Note: seri numaralar ıios/ıpadosos cihazları için önerilen tanımlama biçimidir.
>Android Seri numaralarının mevcut veya benzersiz olacağı garanti değildir. Seri numarasının güvenilir bir cihaz kimliği olup olmadığını anlamak için cihaz sağlayıcınızla görüşün.
>Cihazın Intune’a gönderdiği seri numaralar, cihazdaki Android Ayarları/Hakkında menülerinde gösterilen kimlikle eşleşmeyebilir. Cihaz üreticisi tarafından belirtilen seri numarasının türünü doğrulayın.
>Nokta (.) içeren seri numaralara sahip bir dosya yükleme denemesi, karşıya yükleme işleminin başarısız olmasına yol açar. Nokta içeren seri numaraları desteklenmez.

### <a name="upload-a-csv-list-of-corporate-identifiers"></a>Kurumsal tanımlayıcıları içeren .csv listesini karşıya yükleme

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın, cihazlar ** > ** **cihazları** > **ŞIRKET cihaz tanımlayıcıları** >  > **karşıya yükleme CSV dosyası** **Ekle** ' yi seçin.

2. **Tanımlayıcı ekle** dikey penceresinde tanımlayıcı türünü belirtin: **IMEI**veya **Seri**.

3. Klasör simgesine tıklayın ve içeri aktarmak istediğiniz listenin yolunu belirtin. .csv dosyasına gidin ve **Ekle**’yi seçin. 

4. .csv dosyasında Intune’da zaten bulunan kurumsal tanımlayıcılar varsa ancak bunlar farkı ayrıntılara sahipse, **Yinelenen tanımlayıcıları gözden geçirin** açılır penceresi karşınıza çıkar. Intune’da üzerine yazmak istediğiniz tanımlayıcıları seçin ve **Tamam**’a tıklayarak bunları ekleyin. Her bir tanımlayıcı için yalnızca ilk yinelenen öğe karşılaştırılır.

## <a name="manually-enter-corporate-identifiers"></a>Kurumsal tanımlayıcıları el ile girme

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın, cihazlar ** > ** cihazları > **şirket cihaz tanımlayıcıları** > **kaydetme** > **el ile** **Ekle** ' ye tıklayın.

2. **Tanımlayıcı ekle** dikey penceresinde tanımlayıcı türünü belirtin: **IMEI**veya **Seri**.

3. Eklemek istediğiniz her tanımlayıcı için **tanımlayıcıyı** ve **ayrıntıları** girin. Tanımlayıcıları girmeyi tamamladığınızda **Ekle**’yi seçin.

5. Intune’da zaten bulunan ancak farklı ayrıntılara sahip kurumsal tanımlayıcılar girdiyseniz, **Yinelenen tanımlayıcıları gözden geçirin** açılır penceresi karşınıza çıkar. Intune’da üzerine yazmak istediğiniz tanımlayıcıları seçin ve **Tamam**’a tıklayarak bunları ekleyin. Her bir tanımlayıcı için yalnızca ilk yinelenen öğe karşılaştırılır.

Yeni cihaz tanımlayıcılarını görmek için **Yenile**'ye tıklayabilirsiniz.

İçeri aktarılan cihazlar her zaman kaydedilmez. Cihazlar, **Kayıtlı** veya **Bağlantı kurulmadı** durumunda olabilir. **Bağlantı kurulmadı**, cihazın Intune hizmetiyle hiç iletişim kurmadığı anlamına gelir.

## <a name="delete-corporate-identifiers"></a>Kurumsal tanımlayıcıları silme

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın **, cihazlar ' ı seçerek** cihazları **kurumsal cihaz tanımlayıcıları** > **kaydedin** > .
2. Silmek istediğiniz cihaz tanımlayıcılarını seçin ve **Sil**’e dokunun.
3. Silmeyi onaylayın.

Kayıtlı bir cihazın şirket tanımlayıcısını silmek, cihaz sahipliğini değiştirmez. Cihaz sahipliğini değiştirmek için **Cihazlar**’a gidip cihazı seçin, **Özellikler**’i seçin ve **Cihaz sahipliği**’ni değiştirin.

## <a name="imei-specifications"></a>IMEI belirtimleri
Uluslararası Mobil Donanım Kimlikleri (IMEI) hakkındaki ayrıntılı belirtimler için bkz. [3GGPP TS 23.003](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=729).

## <a name="change-device-ownership"></a>Cihaz sahipliğini değiştirme

Intune’daki tüm cihaz kayıtlarının cihaz özelliklerinde **Sahiplik** görüntülenir. Yönetici olarak, cihazları **Kişisel** veya **Şirkete ait** olarak belirtebilirsiniz. Bir cihazın sahiplik türü Şirket içinden kişisel 'e değiştirildiğinde, Intune bu cihazdan daha önce toplanan tüm uygulama bilgilerini 7 gün içinde siler. Uygulanabiliyorsa, Intune kayıttaki telefon numarasını da siler. 

**Cihaz sahipliğini değiştirmek için:**
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın, **cihazlar** > **tüm cihazlar** ' ı seçin > cihazı seçin.
2. **Özellikler**’i seçin.
3. **Cihaz sahipliği**’ni **Kişisel** veya **Şirkete ait** olarak belirtin.

   ![Cihaz kategorisi ve Cihaz sahipliği seçeneklerini gösteren cihaz özellikleri](./media/corporate-identifiers-add/device-properties.png)
