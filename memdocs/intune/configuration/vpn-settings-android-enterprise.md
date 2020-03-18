---
title: Microsoft Intune-Azure 'da Android Enterprise için VPN ayarlarını kullanma | Microsoft Docs
description: Microsoft Intune 'de Android kurumsal cihazlarda VPN bağlantıları oluşturmak için tüm ayarları görüntüleyin. VPN sunucusunun bağlantı adını, IP adresini veya FQDN 'sini girin, kullanıcıların kimlik doğrulamasını yapın ve Citrix, SonicWall, Check Point kapsül ve Pulse Secure bağlantı türlerini seçin.
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
ms.openlocfilehash: 58069b074db2d885ad63f03c4ba5877458bc7bc1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333014"
---
# <a name="android-enterprise-device-settings-to-configure-vpn-in-intune"></a>Intune 'da VPN yapılandırmak için Android kurumsal cihaz ayarları

Bu makalede, Android kurumsal cihazlarda denetleyebilmeniz için kullanabileceğiniz farklı VPN bağlantısı ayarları listelenir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, bu ayarları kullanarak bir VPN bağlantısı oluşturun, VPN 'in kimlik doğrulamasını yapın, bir VPN sunucusu türü seçin ve daha fazlasını yapın.

Bir Intune Yöneticisi olarak, Android kurumsal cihazlarına VPN ayarları oluşturabilir ve atayabilirsiniz. 

Intune 'da VPN profilleri hakkında daha fazla bilgi edinmek için bkz. [VPN profilleri](vpn-settings-configure.md).

> [!NOTE]
> Always on VPN 'yi yapılandırmak için, bir VPN profili oluşturmanız ve ayrıca her zaman açık VPN ayarıyla bir [cihaz kısıtlamaları](device-restrictions-android-for-work.md#connectivity) profili oluşturmanız gerekir.

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](vpn-settings-configure.md#create-a-device-profile)ve **Android kurumsal**' i seçin.

## <a name="device-owner-only"></a>Yalnızca cihaz sahibi

- **Bağlantı adı**: Bu bağlantı için bir ad girin. Cihazlarındaki kullanılabilir VPN bağlantılarına göz atan son kullanıcılar bu adı görür. Örneğin, şunu girin: `Contoso VPN`.
- **IP adresi veya FQDN**: Cihazların bağlandığı VPN sunucusunun IP adresini veya tam etki alanı adını (FQDN) girin. Örneğin, **192.168.1.1** veya **vpn.contoso.com** yazın.

  - **Kimlik doğrulama yöntemi**: Cihazların VPN sunucusunda kimliklerini nasıl doğrulayacaklarını seçin. Seçenekleriniz şunlardır:
  
    - **Sertifikalar**: Bağlantının kimliğini doğrulamak için mevcut bir SCEP veya PKCS sertifika profili seçin. [Sertifikaları yapılandırın](../protect/certificates-configure.md), sertifika profili oluşturma adımlarını listeler.
    - **Kullanıcı adı ve parola**: VPN sunucusunda oturum açarken son kullanıcılardan Kullanıcı adını ve parolasını girmesi istenir.

- **Bağlantı türü**: VPN bağlantısının türünü seçin. Seçenekleriniz şunlardır:

  - **Cisco AnyConnect**
  - **F5 erişimi**
  - **Pulse Secure**

## <a name="work-profile-only"></a>Yalnızca iş profili

- **Bağlantı adı**: Bu bağlantı için bir ad girin. Cihazlarındaki kullanılabilir VPN bağlantılarına göz atan son kullanıcılar bu adı görür. Örneğin, şunu girin: `Contoso VPN`.
- **IP adresi veya FQDN**: Cihazların bağlandığı VPN sunucusunun IP adresini veya tam etki alanı adını (FQDN) girin. Örneğin, **192.168.1.1** veya **vpn.contoso.com** yazın.

  - **Kimlik doğrulama yöntemi**: Cihazların VPN sunucusunda kimliklerini nasıl doğrulayacaklarını seçin. Seçenekleriniz şunlardır:
  
    - **Sertifikalar**: Bağlantının kimliğini doğrulamak için mevcut bir SCEP veya PKCS sertifika profili seçin. [Sertifikaları yapılandırın](../protect/certificates-configure.md), sertifika profili oluşturma adımlarını listeler.
    - **Kullanıcı adı ve parola**: VPN sunucusunda oturum açarken son kullanıcılardan Kullanıcı adını ve parolasını girmesi istenir.

- **Bağlantı türü**: VPN bağlantısının türünü seçin. Seçenekleriniz şunlardır:

  - **Cisco AnyConnect**
  - **F5 erişimi**
  - **Pulse Secure**
  - **SonicWall Mobile Connect**
  - **Check Point Capsule VPN**

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[Android](vpn-settings-android.md), [IOS/ıpados](vpn-settings-ios.md), [MacOS](vpn-settings-macos.md), [Windows 10 ve üzeri](vpn-settings-windows-10.md), [Windows 8.1](vpn-settings-windows-8-1.md)ve [Windows Phone 8,1](vpn-settings-windows-phone-8-1.md) cihazları için de VPN profilleri oluşturabilirsiniz.
