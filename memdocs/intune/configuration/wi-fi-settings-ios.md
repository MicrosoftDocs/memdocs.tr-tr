---
title: Microsoft Intune-Azure 'da iOS/ıpados cihazları için Wi-Fi ayarlarını yapılandırma | Microsoft Docs
titleSuffix: ''
description: İOS/ıpados cihazları için bir WiFi cihaz yapılandırma profili oluşturun veya ekleyin. Microsoft Intune’da sertifika ekleme, EAP türü seçme ve bir kimlik doğrulama yöntemi seçme gibi farklı ayarları görün.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 01231bc54372dcafb46c58af4ae3169875bed888
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815081"
---
# <a name="add-wi-fi-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Microsoft Intune 'de iOS ve ıpados cihazları için Wi-Fi ayarları ekleme

Belirli bir WiFi ayarlarına sahip bir profil oluşturabilir ve ardından bu profili iOS/ıpados cihazlarınıza dağıtabilirsiniz. Microsoft Intune, ağınızda kimlik doğrulaması, PKCS veya SCEP sertifikası ekleme ve daha fazlası dahil olmak üzere birçok özellik sunar.

Bu Wi-Fi ayarları iki kategoriye ayrılır: Temel ayarlar ve Kurumsal düzeydeki ayarlar.

Bu makalede bu ayarlar açıklanır.

## <a name="before-you-begin"></a>Başlamadan önce

[İOS/ıpados Wi-Fi cihaz yapılandırma profili](wi-fi-settings-configure.md)oluşturun.

> [!NOTE]
> Bu ayarlar tüm kayıt türleri için kullanılabilir. Kayıt türleri hakkında daha fazla bilgi için bkz. [iOS/ıpados kaydı](../enrollment/ios-enroll.md).
>
> Bu ayarlar [Apple Wi-Fi yükünü](https://developer.apple.com/documentation/devicemanagement/wifi) (Apple 'ın Web sitesini açar) kullanır.

## <a name="basic-profiles"></a>Temel profiller

- **Wi-Fi türü**: **temel**öğesini seçin.
- **Ağ adı**: Bu Wi-Fi bağlantısı için bir ad girin. Bu değer, kullanıcıların cihazlarında kullanılabilir bağlantılar listesine göz attıklarında görecekleri addır.
- **SSID**: **Hizmet kümesi tanımlayıcısının** kısaltması. Bu özellik, cihazların bağlandığı kablosuz ağın gerçek adıdır. Bununla birlikte, bağlantıyı seçen kullanıcılar yalnızca yapılandırdığınız ağ adını görür.
- **Otomatik olarak bağlan** **: cihaz** , Aralık içinde olduğunda otomatik olarak bu ağa bağlanır. **Disable** , cihazların otomatik olarak bağlanmasını engeller.
- **Gizli ağ**: **Etkinleştir** ayarı, yönlendirici Wi-Fi yapılandırmasındaki ayarla bu cihaz ayarıyla eşleşir. Bu nedenle, ağ gizli olarak ayarlandıysa Wi-Fi profilinde da gizlenir. Ağ SSID 'si yayınlandıysanız ve görünür durumdaysa **devre dışı bırak** ' ı seçin.
- **Güvenlik türü**: Wi-Fi ağında kimlik doğrulamak için kullanılacak güvenlik protokolünü seçin. Seçenekleriniz şunlardır:

  - **Açık (kimlik doğrulamasız)**: Bu seçeneği yalnızca ağ güvenlik altına alınmamış olduğunda kullanın.
  - **WPA/WPA2 - Kişisel**: **Önceden paylaşılan anahtar** olarak parolayı girin. Kuruluşunuzun ağı ayarlandığında veya yapılandırıldığında bir parola veya ağ anahtarı da yapılandırılır. PSK değeri için bu parolayı veya ağ anahtarını girin.
  - **4**

- **Proxy ayarları**: Seçenekleriniz şunlardır:
  - **Hiçbiri**: Hiçbir ara sunucu ayarı yapılandırılmaz.
  - **El ile**: IP adresi olarak **Proxy sunucu adresini** girin ve sunucunun **Bağlantı noktası numarasını** girin.
  - **Otomatik**: Proxy sunucusunu yapılandırmak için bir dosya kullanın. Yapılandırma dosyasını içeren **Proxy sunucu URL’si** (örneğin `http://proxy.contoso.com`) değerini girin.

- **Mac adresi rastgele seçimini devre dışı bırak**: IOS/ıpados 14 ile başlayarak, cihazlar bir ağa BAĞLANıRKEN fiziksel MAC adresi yerine rastgele bir MAC adresi sunar. Bir cihazı MAC adresine göre izlemek daha zor olduğundan, gizlilik için rastgele MAC adreslerinin kullanılması önerilir. Ancak, rastgele MAC, ağ erişim denetimi (NAC) dahil olmak üzere statik bir MAC adresini temel alan kesme işlevlerini ele alır.

  Seçenekleriniz şunlardır:

  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, bir ağa bağlanırken, cihazlar yeni bir ağa bağlanırken fiziksel MAC adresi yerine rastgele bir MAC adresi sunacaktır.
  - **Evet**: cihazları rastgele bir MAC adresi yerine gerçek Wi-Fi MAC adresini sunacak şekilde zorlar. **Evet** SEÇENEĞI cihazların MAC adresleri tarafından izlenmesini sağlar. Ağ erişim denetimi (NAC) desteği gibi, gerektiğinde yalnızca MAC adresi rastgele seçimini devre dışı bırakın.
  - **Hayır**: cihazlarda Mac adresini rastgele seçme özelliği etkinleştirilir. Kullanıcılar bu uygulamayı kapatamaz. Yeni bir ağa bağlanırken, cihazlar fiziksel MAC adresi yerine rastgele bir MAC adresi sunar.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 14,0 ve üzeri
  - ıpados 14,0 ve üzeri

## <a name="enterprise-profiles"></a>Kurumsal profiller

- **Wi-Fi türü**: **Kurumsal**' i seçin.
- **SSID**: **Hizmet kümesi tanımlayıcısının** kısaltması. Bu özellik, cihazların bağlandığı kablosuz ağın gerçek adıdır. Bununla birlikte, bağlantıyı seçen kullanıcılar yalnızca yapılandırdığınız ağ adını görür.
- **Otomatik olarak bağlan** **: cihaz** , Aralık içinde olduğunda otomatik olarak bu ağa bağlanır. **Disable** , cihazların otomatik olarak bağlanmasını engeller.
- **Gizli ağ**: **Etkinleştir** ayarı, yönlendirici Wi-Fi yapılandırmasındaki ayarla bu cihaz ayarıyla eşleşir. Bu nedenle, ağ gizli olarak ayarlandıysa Wi-Fi profilinde da gizlenir. Ağ SSID 'si yayınlandıysanız ve görünür durumdaysa **devre dışı bırak** ' ı seçin.
- **Güvenlik türü**: Wi-Fi ağında kimlik doğrulamak için kullanılacak güvenlik protokolünü seçin. Seçenekleriniz şunlardır:
  - **WPA-Kuruluş**
  - **WPA/WPA2-Kuruluş**

- **EAP türü**: güvenli kablosuz bağlantıların kimliğini doğrulamak Için kullanılan Genişletilebilir Kimlik Doğrulama Protokolü (EAP) türünü seçin. Seçenekleriniz şunlardır:

  - **EAP-FAST**: **Korumalı Erişim Kimlik Bilgisi (PAC) Ayarları**’nı girin. Bu seçenek, istemci ile kimlik doğrulama sunucusu arasında kimliği doğrulanmış bir tünel oluşturmak için korumalı erişim kimlik bilgilerini kullanır. Seçenekleriniz şunlardır:
    - **(PAC) kullanma**
    - **(PAC) kullan**: Mevcut bir PAC dosyası varsa bunu kullanın.
    - **PAC’yi kullan ve sağla**: PAC dosyasını oluşturun ve cihazlarınıza sağlayın.
    - **PAC’yi anonim olarak kullan ve sağla**: PAC dosyasını sunucuda kimlik doğrulamadan oluşturun ve cihazlarınıza ekleyin.

  - **EAP-SIM**

  - **EAP-TLS**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sertifika sunucusu adları**: güvenilir sertifika yetkiliniz (CA) tarafından kablosuz ağ erişim sunucularınıza verilen sertifikalarda kullanılan bir veya daha fazla ortak ad **ekleyin** . Örneğin, veya ekleyin `mywirelessserver.contoso.com` `mywirelessserver` . Bu bilgiyi girdikten sonra bu Wi-Fi ağına bağlanırken kullanıcının cihazında görüntülenen dinamik güven penceresini atlayabilirsiniz.
    - **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. Bu sertifika, istemcinin kablosuz ağ erişim sunucusunun sertifikasına güvenmesini sağlar.

    - **Istemci kimlik doğrulaması** Bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:

      - **Türetilmiş kimlik bilgileri**: kullanıcının akıllı kartından türetilmiş bir sertifika kullanın. Türetilmiş bir kimlik bilgisi veren yapılandırılmamışsa, Intune sizden bir tane eklemeniz istenir. Daha fazla bilgi için bkz. [Microsoft Intune türetilmiş kimlik bilgilerini kullanma](../protect/derived-credentials.md).

      - **Sertifikalar**: cihaza de dağıtılan SCEP veya PKCS istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

    - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

  - **EAP-TTLS**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sertifika sunucusu adları**: güvenilir sertifika yetkiliniz (CA) tarafından kablosuz ağ erişim sunucularınıza verilen sertifikalarda kullanılan bir veya daha fazla ortak ad **ekleyin** . Örneğin, veya ekleyin `mywirelessserver.contoso.com` `mywirelessserver` . Bu bilgiyi girdikten sonra bu Wi-Fi ağına bağlanırken kullanıcının cihazında görüntülenen dinamik güven penceresini atlayabilirsiniz.
    - **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. Bu sertifika, istemcinin kablosuz ağ erişim sunucusunun sertifikasına güvenmesini sağlar.

    - **Istemci kimlik doğrulaması**: bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:

      - **Türetilmiş kimlik bilgileri**: kullanıcının akıllı kartından türetilmiş bir sertifika kullanın. Türetilmiş bir kimlik bilgisi veren yapılandırılmamışsa, Intune sizden bir tane eklemeniz istenir. Daha fazla bilgi için bkz. [Microsoft Intune türetilmiş kimlik bilgilerini kullanma](../protect/derived-credentials.md).

      - **Kullanıcı adı ve Parola**: Bağlantının kimliğini doğrulamak için kullanıcıdan bir kullanıcı adı ve parola girmesini isteyin. Şunları da girin:
        - **EAP dışı yöntem (iç kimlik)**: Bağlantının kimliğini nasıl doğrulayacağınızı seçin. Wi-Fi ağınızda yapılandırılmış olan protokolü seçtiğinizden emin olun.

          Seçenekleriniz şunlardır: **Şifrelenmemiş parola (PAP)**, **Karşılıklı Kimlik Doğrulama Protokolü (CHAP)**, **Microsoft CHAP (MS-CHAP)** veya **Microsoft CHAP Sürüm 2 (MS-CHAP v2)**

      - **Sertifikalar**: cihaza de dağıtılan SCEP veya PKCS istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

      - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

  - **LEAP**

  - **PEAP**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sertifika sunucusu adları**: güvenilir sertifika yetkiliniz (CA) tarafından kablosuz ağ erişim sunucularınıza verilen sertifikalarda kullanılan bir veya daha fazla ortak ad **ekleyin** . Örneğin, veya ekleyin `mywirelessserver.contoso.com` `mywirelessserver` . Bu bilgiyi girdikten sonra bu Wi-Fi ağına bağlanırken kullanıcının cihazında görüntülenen dinamik güven penceresini atlayabilirsiniz.
    - **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. Bu sertifika, istemcinin kablosuz ağ erişim sunucusunun sertifikasına güvenmesini sağlar.

    - **Istemci kimlik doğrulaması**: bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:

      - **Türetilmiş kimlik bilgileri**: kullanıcının akıllı kartından türetilmiş bir sertifika kullanın. Türetilmiş bir kimlik bilgisi veren yapılandırılmamışsa, Intune sizden bir tane eklemeniz istenir. Daha fazla bilgi için bkz. [Microsoft Intune türetilmiş kimlik bilgilerini kullanma](../protect/derived-credentials.md).

      - **Kullanıcı adı ve Parola**: Bağlantının kimliğini doğrulamak için kullanıcıdan bir kullanıcı adı ve parola girmesini isteyin. 

      - **Sertifikalar**: cihaza de dağıtılan SCEP veya PKCS istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

      - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

- **Proxy ayarları**: Seçenekleriniz şunlardır:
  - **Hiçbiri**: Hiçbir ara sunucu ayarı yapılandırılmaz.
  - **El ile**: IP adresi olarak **Proxy sunucu adresini** girin ve sunucunun **Bağlantı noktası numarasını** girin.
  - **Otomatik**: Proxy sunucusunu yapılandırmak için bir dosya kullanın. Yapılandırma dosyasını içeren **Proxy sunucu URL’si** (örneğin `http://proxy.contoso.com`) değerini girin.

- **Mac adresi rastgele seçimini devre dışı bırak**: IOS/ıpados 14 ile başlayarak, cihazlar bir ağa BAĞLANıRKEN fiziksel MAC adresi yerine rastgele bir MAC adresi sunar. Bir cihazı MAC adresine göre izlemek daha zor olduğundan, gizlilik için rastgele MAC adreslerinin kullanılması önerilir. Rastgele MAC adresleri, ağ erişim denetimi (NAC) dahil olmak üzere statik bir MAC adresine dayanan işlevselliği de kesintiye uğratır.

  Seçenekleriniz şunlardır:

  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, bir ağa bağlanırken cihazlar fiziksel MAC adresi yerine rastgele bir MAC adresi sunabilir.
  - **Evet**: cihazları rastgele bir MAC adresi yerine gerçek Wi-Fi MAC adresini sunacak şekilde zorlar. **Evet** SEÇENEĞI cihazların MAC adresleri tarafından izlenmesini sağlar. Ağ erişim denetimi (NAC) desteği gibi, gerektiğinde yalnızca MAC adresi rastgele seçimini devre dışı bırakın.
  - **Hayır**: cihazlarda Mac adresini rastgele seçme özelliği etkinleştirilir. Kullanıcılar bu uygulamayı kapatamaz. Bir ağa bağlanırken, cihazlar fiziksel MAC adresi yerine rastgele bir MAC adresi sunar.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 14,0 ve üzeri
  - ıpados 14,0 ve üzeri

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu ancak hiçbir şey yapmıyor. Sonra, [Bu profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

[Android](wi-fi-settings-android.md), [Android Enterprise](wi-fi-settings-android-enterprise.md), [MacOS](wi-fi-settings-macos.md)ve [Windows 10](wi-fi-settings-windows.md) cihazlarında Wi-Fi ayarlarını yapılandırın.
