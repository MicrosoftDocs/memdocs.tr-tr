---
title: Intune ile Sophos Mobile tümleştirmesini ayarlama
titleSuffix: Intune on Azure
description: Şirket kaynaklarınıza mobil cihaz erişimini denetlemek için Microsoft Intune ile Sophos Mobile çözümünü ayarlama.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3298c2759b14fd2579fc51513177033c792b9c83
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988270"
---
# <a name="integrate-sophos-mobile-with-intune"></a>Sophos Mobile 'ı Intune ile tümleştirme  

Sophos Mobile Threat Defense çözümünü Intune ile bütünleştirmek için aşağıdaki adımları izleyin.  

> [!NOTE]
> Bu mobil tehdit savunma satıcısı, kayıtlı olmayan cihazlar için desteklenmez.

## <a name="before-you-begin"></a>Başlamadan önce  

Sophos Mobile 'ı Intune ile tümleştirme işlemine başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:  
- Microsoft Intune aboneliği  
- Şu izinleri vermek için Azure Active Directory yönetici kimlik bilgileri:  
  - Oturum açma ve kullanıcı profilini okuma  
  - Dizine oturum açmış kullanıcı olarak erişin  
  - Dizin verilerini oku  
  - Intune’a cihaz bilgilerini gönderme  
- Sophos Mobile Yönetici konsoluna erişmek için yönetici kimlik bilgileri.  


### <a name="sophos-mobile-app-authorization"></a>Sophos mobil uygulama yetkilendirmesi  
  
Sophos mobil uygulama yetkilendirme işlemi aşağıdaki gibidir:  
- Sophos Mobile hizmetinin cihaz sistem durumu ile ilgili bilgileri Intune 'a geri iletmesini sağlar.  
- Sophos Mobile, cihazının veritabanını doldurmak için Azure AD kayıt grubu üyeliğiyle eşitlenir.  
- Sophos Mobile yönetici konsolunun Azure AD çoklu oturum açma (SSO) kullanmasına izin verin.  
- Sophos Mobile uygulamasının Azure AD SSO kullanarak oturum açmasını sağlar.  


## <a name="to-set-up-sophos-mobile-integration"></a>Sophos Mobile tümleştirmesini ayarlamak için  

1. [Azure Portal]( https://portal.azure.com/)oturum açın, **Intune**  >  **cihaz uyumluluğu**  >  **Mobil tehdit savunması** > gidin ve **Ekle**' yi seçin.  
2. **Bağlayıcı Ekle** sayfasında, açılan menüyü kullanın ve **Sophos**' ı seçin. Sonra **Oluştur**' u seçin.  
3. *Sophos yönetici konsolunu açmak*için bağlantıyı seçin.  
4. Sophos kimlik bilgilerinizle, [Sophos yönetici konsolunda](https://central.sophos.com/) oturum açın.  
5. **Mobil**  >  **Ayarlar**  >  **Kurulum**  >  **Sophos Setup**' a gidin.  
6. **Sophos kurulum** sayfasında, **Intune MTD** sekmesini seçin.  
   ![Sophos kurulumu](./media/sophos-mtd-connector-integration/sophos-setup.png) 
 
7. **Bağla**' yı seçin ve ardından **Evet**' i seçin. Sophos, Intune 'a bağlanır ve Intune aboneliğinizde oturum açmanızı gerektirir. 
8. Microsoft Intune kimlik doğrulaması penceresinde, Intune kimlik bilgilerinizi girin ve *Sophos Mobile Iş parçacığı savunması*için Izin Isteğini **kabul edin** .  
   ![Intune kimlik doğrulaması](./media/sophos-mtd-connector-integration/intune-authentication.png)

9. **Sophos kurulum** sayfasında, Intune yapılandırmasını gerçekleştirmek için **Kaydet** ' i seçin:  
   ![Sophos kurulumunu Kaydet](./media/sophos-mtd-connector-integration/save-sophos-configuration.png)  

1. **Başarılı Tümleştirme** iletisi göründüğünde tümleştirme tamamlanmıştır.  
1. Intune konsolunda, Sophos artık kullanılabilir.  


## <a name="next-steps"></a>Sonraki Adımlar  
[Sophos istemci uygulamalarını yapılandırma](mtd-apps-ios-app-configuration-policy-add-assign.md)
