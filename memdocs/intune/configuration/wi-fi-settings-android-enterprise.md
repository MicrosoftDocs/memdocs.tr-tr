---
title: Android Enterprise ve bilgi noktası cihazları için Wi-Fi ayarları-Microsoft Intune | Microsoft Docs
description: Android Kurumsal ve Android Bilgi Noktası için bir Wi-Fi cihaz yapılandırma profili oluşturun veya ekleyin. Microsoft Intune’da sertifika ekleme, EAP türü seçme ve bir kimlik doğrulama yöntemi seçme gibi farklı ayarları görün. Bilgi noktası cihazlarında ağınızın Önceden paylaşılan anahtarını da girin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65b5c7c0b9cb8a587213d237854e69705b5a7f63
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461700"
---
# <a name="add-wi-fi-settings-for-android-enterprise-dedicated-and-fully-managed-devices-in-microsoft-intune"></a>Microsoft Intune 'de Android kurumsal adanmış ve tam olarak yönetilen cihazlar için Wi-Fi ayarları ekleme

Belirli Wi-Fi ayarlarına sahip bir profil oluşturabilir ve ardından bu profili Android kurumsal tam olarak yönetilen ve adanmış cihazlarınıza dağıtabilirsiniz. Microsoft Intune; ağınızda kimlik doğrulama, bir önceden paylaşılan anahtar kullanma ve daha fazlası gibi pek çok özellik sunar.

Bu makalede bu ayarlar açıklanır. [Cihazlarınızda Wi-Fi kullanın](wi-fi-settings-configure.md) , Microsoft Intune Wi-Fi özelliği hakkında daha fazla bilgi içerir.

## <a name="before-you-begin"></a>Başlamadan önce

[Cihaz profili oluşturma](wi-fi-settings-configure.md).

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Tam olarak yönetilen, adanmış ve şirkete ait Iş profili

Android kurumsal adanmış veya tam olarak yönetilen bir cihaza dağıtım yapıyorsanız bu seçeneği belirleyin.  Android kurumsal adanmış ve tam olarak yönetilen cihazlar şu anda SCEP sertifika dağıtımını destekliyor, ancak PKCS değil.

### <a name="basic"></a>Temel

- **Wi-Fi türü**: **Temel**’i seçin.
- **Ağ adı**: Bu Wi-Fi bağlantısı için bir ad girin. Son kullanıcılar, kullanılabilir Wi-Fi bağlantıları için cihazına gözatarken bu adı görür. Örneğin, **contoso WiFi**girin.
- **SSID**: cihazların bağlandığı kablosuz ağın gerçek adı olan **hizmet kümesi tanımlayıcısını**girin. Ancak, kullanıcılar bağlantıyı seçerken yapılandırdığınız **ağ adını** görür.
- **Gizli ağ**: Cihazdaki kullanılabilir ağlar listesinde bu ağı gizlemek için **Etkinleştir**’i seçin. SSID yayınlanmaz. Cihazdaki kullanılabilir ağlar listesinde bu ağı göstermek için **Devre dışı bırak**’ı seçin.
- **Wi-Fi türü**: Wi-Fi ağında kimlik doğrulamak için kullanılacak güvenlik protokolünü seçin. Seçenekleriniz şunlardır:

  - **Açık (kimlik doğrulamasız)**: Bu seçeneği yalnızca ağ güvenlik altına alınmamış olduğunda kullanın.
  - **WEP-Önceden paylaşılan anahtar**: **Önceden paylaşılan anahtar** olarak parolayı girin. Kuruluşunuzun ağı ayarlandığında veya yapılandırıldığında bir parola veya ağ anahtarı da yapılandırılır. PSK değeri için bu parolayı veya ağ anahtarını girin.
  - **WPA-Önceden paylaşılan anahtar**: **Önceden paylaşılan anahtar** olarak parolayı girin. Kuruluşunuzun ağı ayarlandığında veya yapılandırıldığında bir parola veya ağ anahtarı da yapılandırılır. PSK değeri için bu parolayı veya ağ anahtarını girin.

### <a name="enterprise"></a>Enterprise

- **Wi-Fi türü**: **Kurumsal**’ı seçin.
- **SSID**: cihazların bağlandığı kablosuz ağın gerçek adı olan **hizmet kümesi tanımlayıcısını**girin. Ancak, kullanıcılar bağlantıyı seçerken yapılandırdığınız **ağ adını** görür.
- **Gizli ağ**: Cihazdaki kullanılabilir ağlar listesinde bu ağı gizlemek için **Etkinleştir**’i seçin. SSID yayınlanmaz. Cihazdaki kullanılabilir ağlar listesinde bu ağı göstermek için **Devre dışı bırak**’ı seçin.
- **EAP türü**: Güvenli kablosuz bağlantıların kimliğini doğrulamak için kullanılan Genişletilebilir Kimlik Doğrulama Protokolü (EAP) türünü seçin. Seçenekleriniz şunlardır:

  - **EAP-TLS**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur ve bağlantının kimliğini doğrular.

    - **Istemci kimlik doğrulaması**  -  **İstemci kimlik doğrulaması Için istemci sertifikası (kimlik sertifikası)**: CIHAZA dağıtılan SCEP istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

    - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

  - **EAP-TTLS**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur ve bağlantının kimliğini doğrular.

    - **Istemci kimlik doğrulaması**: bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:

      - **Kullanıcı adı ve Parola**: Bağlantının kimliğini doğrulamak için kullanıcıdan bir kullanıcı adı ve parola girmesini isteyin. Şunları da girin:
        - **EAP dışı yöntem (iç kimlik)**: Bağlantının kimliğini nasıl doğrulayacağınızı seçin. Wi-Fi ağınızda yapılandırılmış olan protokolü seçtiğinizden emin olun. Seçenekleriniz şunlardır:

          - **Şifrelenmemiş parola (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Sürüm 2 (MS-CHAP v2)**

      - **Sertifikalar**: cihaza de dağıtılan SCEP istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

      - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

  - **PEAP**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur ve bağlantının kimliğini doğrular.

    - **Istemci kimlik doğrulaması**: bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:

      - **Kullanıcı adı ve Parola**: Bağlantının kimliğini doğrulamak için kullanıcıdan bir kullanıcı adı ve parola girmesini isteyin. Şunları da girin:
        - **Kimlik doğrulaması için EAP dışı yöntem (iç kimlik)**: Bağlantının kimliğini nasıl doğrulayacağınızı seçin. Wi-Fi ağınızda yapılandırılmış olan protokolü seçtiğinizden emin olun. Seçenekleriniz şunlardır:

          - **Hiçbiri**
          - **Microsoft CHAP Sürüm 2 (MS-CHAP v2)**

      - **Sertifikalar**: cihaza de dağıtılan SCEP istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

      - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

## <a name="work-profile-only"></a>Yalnızca iş profili

### <a name="basic"></a>Temel

- **Wi-Fi türü**: **Temel**’i seçin.
- **SSID**: cihazların bağlandığı kablosuz ağın gerçek adı olan **hizmet kümesi tanımlayıcısını**girin. Ancak, kullanıcılar bağlantıyı seçerken yapılandırdığınız **ağ adını** görür.
- **Gizli ağ**: Cihazdaki kullanılabilir ağlar listesinde bu ağı gizlemek için **Etkinleştir**’i seçin. SSID yayınlanmaz. Cihazdaki kullanılabilir ağlar listesinde bu ağı göstermek için **Devre dışı bırak**’ı seçin.

### <a name="enterprise"></a>Enterprise

- **Wi-Fi türü**: **Kurumsal**’ı seçin.
- **SSID**: cihazların bağlandığı kablosuz ağın gerçek adı olan **hizmet kümesi tanımlayıcısını**girin. Ancak, kullanıcılar bağlantıyı seçerken yapılandırdığınız **ağ adını** görür.
- **Gizli ağ**: Cihazdaki kullanılabilir ağlar listesinde bu ağı gizlemek için **Etkinleştir**’i seçin. SSID yayınlanmaz. Cihazdaki kullanılabilir ağlar listesinde bu ağı göstermek için **Devre dışı bırak**’ı seçin.
- **EAP türü**: Güvenli kablosuz bağlantıların kimliğini doğrulamak için kullanılan Genişletilebilir Kimlik Doğrulama Protokolü (EAP) türünü seçin. Seçenekleriniz şunlardır:

  - **EAP-TLS**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur ve bağlantının kimliğini doğrular.

    - **Istemci kimlik doğrulaması**  -  **İstemci kimlik doğrulaması Için istemci sertifikası (kimlik sertifikası)**: CIHAZA dağıtılan SCEP veya PKCS istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

    - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

  - **EAP-TTLS**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur ve bağlantının kimliğini doğrular.

    - **Istemci kimlik doğrulaması**: bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:

      - **Kullanıcı adı ve Parola**: Bağlantının kimliğini doğrulamak için kullanıcıdan bir kullanıcı adı ve parola girmesini isteyin. Şunları da girin:
        - **EAP dışı yöntem (iç kimlik)**: Bağlantının kimliğini nasıl doğrulayacağınızı seçin. Wi-Fi ağınızda yapılandırılmış olan protokolü seçtiğinizden emin olun. Seçenekleriniz şunlardır:

          - **Şifrelenmemiş parola (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Sürüm 2 (MS-CHAP v2)**

      - **Sertifikalar**: Cihaza da dağıtılmış olan SCEP veya PKCS istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

      - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

  - **PEAP**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur ve bağlantının kimliğini doğrular.

    - **Istemci kimlik doğrulaması**: bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:

      - **Kullanıcı adı ve Parola**: Bağlantının kimliğini doğrulamak için kullanıcıdan bir kullanıcı adı ve parola girmesini isteyin. Şunları da girin:
        - **Kimlik doğrulaması için EAP dışı yöntem (iç kimlik)**: Bağlantının kimliğini nasıl doğrulayacağınızı seçin. Wi-Fi ağınızda yapılandırılmış olan protokolü seçtiğinizden emin olun. Seçenekleriniz şunlardır:

          - **Hiçbiri**
          - **Microsoft CHAP Sürüm 2 (MS-CHAP v2)**

      - **Sertifikalar**: Cihaza da dağıtılmış olan SCEP veya PKCS istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir.

      - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

- **Proxy ayarları**: kuruluşunuz tarafından kullanılan ara sunucu yapılandırmasını belirtin. Seçenekleriniz şunlardır:

  - **Hiçbiri** -proxy sunucusu kullanmazsınız.
  - **Otomatik** – ara *sunucu URL 'si* ayarını kullanılabilir hale getirmek için bu seçeneği belirleyin. proxy sunucusu veya proxy sunucularınızın bir listesini Içeren bir proxy otomatik yapılandırma (PAC) dosyası belirtin.

- **Proxy sunucusu URL 'si**: Bu ayar, *Ara sunucu ayarlarını* *Otomatik*olarak belirlediğinizde kullanılabilir. Cihazları proxy sunucunuza yönlendirmek için aşağıdaki seçeneklerden birini belirtin:

  - IP adresi. Örneğin, `10.0.0.11`
  - BIR URL. Örneğin, `http://proxyserver.contoso.com`.
  - Bir proxy otomatik yapılandırma (PAC) dosyasının URL 'SI. Örneğin: `http://proxy.contoso.com/proxy.pac`.

  PAC dosyaları hakkında daha fazla bilgi için bkz. [proxy otomatik yapılandırma (PAC) dosyası](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (Microsoft dışı bir site açar).

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu ancak hiçbir şey yapmıyor. Sonra, [Bu profili atayın](device-profile-assign.md) ve [durumunu izleyin.](device-profile-monitor.md)

[Android](wi-fi-settings-android.md), [IOS/ıpados](wi-fi-settings-ios.md), [macos](wi-fi-settings-macos.md), [Windows 10](wi-fi-settings-windows.md)ve [Windows 8.1](wi-fi-settings-import-windows-8-1.md) cihazları için Wi-Fi profilleri de oluşturabilirsiniz.
