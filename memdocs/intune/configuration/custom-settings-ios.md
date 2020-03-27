---
title: Microsoft Intune-Azure 'da iOS/ıpados cihazlarına özel ayarlar ekleme | Microsoft Docs
titleSuffix: ''
description: Apple Configurator veya Apple Profile Manager araçlarından iOS ve ıpados ayarlarını dışa aktarın ve ardından bu ayarları Microsoft Intune içine aktarın. Bu ayarlar iOS/ıpados cihazlarında özel ayarları ve özellikleri oluşturabilir, kullanabilir ve denetleyebilir. Bu özel profil daha sonra, bir taban çizgisi veya standart oluşturmak için kuruluşunuzdaki iOS/ıpados cihazlarına atanabilir veya dağıtılabilir.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c84c8f044fe5a1554a8e156a5c7c0a7087d98224
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326161"
---
# <a name="use-custom-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Microsoft Intune 'de iOS ve ıpados cihazları için özel ayarlar kullanın

Microsoft Intune kullanarak, "özel profiller" i kullanarak iOS/ıpados cihazlarınız için özel ayarlar ekleyebilir veya oluşturabilirsiniz. Özel profiller, bir Intune özelliğidir. Intune’da yerleşik olarak bulunmayan cihaz ayarları ve özelliklerini eklemek için tasarlanmıştır.

İOS/ıpados cihazları kullanılırken, Intune 'a özel ayarlar almanın iki yolu vardır:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple Profile Manager](https://support.apple.com/profile-manager)

Bir yapılandırma profiline ayar aktarmak için bu araçları kullanabilirsiniz. Intune 'da, bu dosyayı içeri aktarır ve ardından profili iOS/ıpados kullanıcılarınıza ve cihazlarınıza atarsınız. Atandıktan sonra ayarlar dağıtılır. Ayrıca, kuruluşunuzda iOS/ıpados için bir taban çizgisi veya standart oluşturur.

Bu makalede, Apple Configurator ve Apple Profile Manager kullanımı hakkında bazı yönergeler sağlanır ve yapılandırabileceğiniz özellikler açıklanmaktadır.

## <a name="before-you-begin"></a>Başlamadan önce

[Profili oluşturun](custom-settings-configure.md).

## <a name="what-you-need-to-know"></a>Bilmeniz gerekenler

- Yapılandırma profilini oluşturmak için **Apple Configurator** kullanırken, dışarı aktarma yaptığınız ayarların cihazlarda IOS/ıpados sürümüyle uyumlu olduğundan emin olun. Uyumsuz ayarların çözümlenmesi hakkında bilgi için **Apple Developer** web sitesinde **Configuration Profile Reference** ve [Mobile Device Management Protocol Reference](https://developer.apple.com/) başlıklarını arayın.

- **Apple Profile Manager**’ı kullanırken şunları yapmayı unutmayın:

  - Profile Manager’da [mobil cihaz yönetimini](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) etkinleştirin.
  - Profil Yöneticisi 'ne [iOS/ıpados cihazları](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) ekleyin.
  - Profile Manager’a cihaz ekledikten sonra **Under the Library (Kitaplık Altında)**  > **Devices** (Cihazlar) seçeneğine gidip cihazınızı seçin ve **Settings** (Ayarlar) seçeneğine gidin. Cihazın genel ayarlarını girin.

    Bu dosyayı indirin ve kaydedin. Intune profilinde bu dosyayı girmeniz istenir.

  - Apple Profile Manager 'dan dışarı verdiğiniz ayarların cihazlarda iOS/ıpados sürümüyle uyumlu olduğundan emin olun. Uyumsuz ayarların çözümlenmesi hakkında bilgi için **Apple Developer** web sitesinde **Configuration Profile Reference** ve [Mobile Device Management Protocol Reference](https://developer.apple.com/) başlıklarını arayın.

## <a name="custom-configuration-profile-settings"></a>Özel yapılandırma profili ayarları

- **Özel yapılandırma profili adı**: İlke için bir ad girin. Bu ad, cihazda ve Intune durumunda gösterilir.
- **Yapılandırma profili dosyası**: Apple Configurator veya Apple Profile Manager’ı kullanarak oluşturduğunuz yapılandırma profiline gidin. En büyük dosya boyutu 1000000 bayttır (yalnızca 1MB ' in altında). İçeri aktardığınız dosya, **Dosya içeriği** alanında görüntülenir.

  Ayrıca, özel yapılandırma dosyalarınıza cihaz belirteçleri ekleyebilirsiniz. Cihaz belirteçleri cihaza özgü bilgileri eklemek için kullanılır. Örneğin, seri numarasını göstermek için `{{serialnumber}}`girin. Cihazda, metin her bir cihaz için benzersiz olan `123456789ABC` benzer şekilde görünür. Değişken girerken `{{ }}`kaşlı ayraç kullandığınızdan emin olun. [Uygulama yapılandırma belirteçleri](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) , kullanılabilecek değişkenlerin bir listesini içerir. `deviceid` veya başka bir cihaza özgü değeri de kullanabilirsiniz.

  > [!NOTE]
  > Değişkenler kullanıcı arabiriminde doğrulanmaz ve büyük/küçük harfe duyarlıdır. Sonuç olarak, yanlış girişle kaydedilmiş profiller görebilirsiniz. Örneğin, `{{deviceid}}`yerine `{{DeviceID}}` girerseniz, aygıtın benzersiz KIMLIĞI yerine değişmez dize gösterilir. Doğru bilgileri girdiğinizden emin olun.

Değişikliklerinizi kaydetmek için **Tamam** > **Oluştur**’u seçin. Profil oluşturulur ve profiller listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulur ancak henüz herhangi bir işlem gerçekleştirmez. Daha sonra, [profili atayın](device-profile-assign.md).

Bkz. [macOS cihazlarda profil oluşturma](custom-settings-macos.md). 
