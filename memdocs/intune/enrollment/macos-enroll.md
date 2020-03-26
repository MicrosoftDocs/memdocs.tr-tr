---
title: macOS cihazların kaydını ayarlama
titleSuffix: Microsoft Intune
description: Intune’da macOS cihazların kaydının nasıl ayarlandığını öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26fe64cbaebf385c0d51d3e7b96c46b3ff6e3cae
ms.sourcegitcommit: 71f26a0756fd40c1a06f885f3d31e49734fe97fe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2020
ms.locfileid: "80256836"
---
# <a name="set-up-enrollment-for-macos-devices-in-intune"></a>Intune’da macOS cihazların kaydını ayarlama

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune, kullanıcılara şirket e-postasına ve uygulamalarına erişim vermek için macOS cihazlarını yönetmenize olanak tanır.

Intune yöneticisi olarak, şirkete ait macOS cihazları ile kişilere ait macOS cihazları ("kendi cihazını getir" veya KCG) için kaydı ayarlayabilirsiniz. 

## <a name="prerequisites"></a>Önkoşullar

macOS cihaz kaydını ayarlamadan önce, aşağıdaki önkoşulları tamamlayın:

- [Cihazınızın Apple cihaz kaydına uygun olduğundan emin olun](https://support.apple.com/en-us/HT204142#eligibility).
- [Etki alanlarını yapılandırma](../fundamentals/custom-domain-name-configure.md)
- [MDM Yetkilisini ayarlama](../fundamentals/mdm-authority-set.md)
- [Grup oluşturma](../fundamentals/groups-add.md)
- [Şirket Portalı’nı yapılandırma](../apps/company-portal-app.md)
- [Microsoft 365 yönetim merkezinde](https://go.microsoft.com/fwlink/p/?LinkId=698854) kullanıcı lisanslarını atama
- [Bir MDM anında iletme sertifikası alma](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="user-owned-macos-devices-byod"></a>Kullanıcıya ait macOS cihazları (KCG)

Kullanıcıların kendi kişisel cihazlarını Intune yönetimine kaydetmelerini sağlayabilirsiniz. Bu, "kendi cihazını getir" veya KCG olarak bilinir. Önkoşulları ve atanan kullanıcı lisanslarını tamamladıktan sonra, kullanıcılarınız cihazlarını şu şekilde kaydedebilir:
- [Şirket Portalı web sitesine](https://portal.manage.microsoft.com) gidebilir veya
- [aka.MS/EnrollMyMac](https://aka.ms/EnrollMyMac)adresindeki Mac Şirket portalı uygulaması indiriliyor.

Kullanıcılarınıza çevrimiçi kayıt adımları için bir bağlantı da gönderebilirsiniz: [macOS cihazınızı Intune 'A kaydetme](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).

Diğer son kullanıcı görevleri hakkında daha fazla bilgi için şu makalelere bakın:

- [Microsoft Intune’da son kullanıcı deneyimi hakkında kaynaklar](../fundamentals/end-user-educate.md)
- [macOS cihazınızı Intune ile kullanma](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>Şirkete ait macOS cihazları
Kullanıcılarına cihaz sağlayan kuruluşlar için Intune, aşağıdaki şirkete ait macOS cihazı kayıt yöntemlerini destekler:
- [Apple 'ın otomatik cihaz kaydı (ade)](device-enrollment-program-enroll-macos.md): kuruluşlar MacOS cihazlarını Ade aracılığıyla satın alabilir. ADE, cihazları yönetime getirmek için bir kayıt profilini "hava üzerinden" dağıtmanızı sağlar.
- [Cihaz kayıt yöneticisi (DEM)](device-enrollment-manager-enroll.md): En çok 1.000 cihazı kaydetmek için DEM hesabı kullanabilirsiniz.

## <a name="block-macos-enrollment"></a>macOS kaydını engelleme
Varsayılan olarak, Intune macOS cihazlarının kaydına izin verir. macOS cihazlarının kaydedilmesini engellemek için bkz. [Cihaz türü kısıtlamaları ayarlama](enrollment-restrictions-set.md).

## <a name="enroll-virtual-macos-machines-for-testing"></a>Sanal macOS makineleri sınama için kaydetme

> [!NOTE]
> macOS sanal makinelerin yalnızca sınama desteği vardır. macOS sanal makineleri son kullanıcılarınız için üretim cihazları olarak kullanmamalısınız. 

macOS sanal makineleri, Parallels Desktop veya VMware Fusion kullanarak sınama için kaydedebilirsiniz. 

Parallels Desktop kullanırsanız, Intune’un sanal makineleri tanıyabilmesi için bunların donanım türü ve seri numaralarını ayarlamanız gerekir. Sınama için gerekli ayarları yapmak üzere Parallels’in donanım türünü ve [seri numarasını](http://kb.parallels.com/123455) ayarlama yönergelerini izleyin. Sanal makineleri çalıştıran cihazın donanım türünü, oluşturduğunuz sanal makinelerin donanım türüyle eşleştirmenizi öneririz. Bu donanım türünü **Apple menüsü** > **Bu Mac hakkında** > **Sistem Raporu** > **Model Tanımlayıcı**’da bulabilirsiniz. 

VMware Fusion kullanırsanız, sanal makinenin donanım türü ve seri numarasını ayarlamak için [.vmx dosyasını düzenlemeniz](https://kb.vmware.com/s/article/1014782) gerekir. Sanal makineleri çalıştıran cihazın donanım türünü, oluşturduğunuz sanal makinelerin donanım türüyle eşleştirmenizi öneririz. Bu donanım türünü **Apple menüsü** > **Bu Mac hakkında** > **Sistem Raporu** > **Model Tanımlayıcı**’da bulabilirsiniz. 

## <a name="user-approved-enrollment"></a>Kullanıcı Onaylı kayıt
Kullanıcı Onaylı MDM kaydı, güvenlik açısından hassas bazı ayarları yönetmek için kullanabileceğiniz bir macOS kayıt türüdür. Daha fazla bilgi için [Apple'ın destek belgelerine](https://support.apple.com/HT208019) bakın.  
 
KCG kayıt işlemi sırasında, kullanıcıdan Apple Yönetim profilini el ile onaylaması istenir. Yönergeler macOS için Şirket Portalı uygulamasında sunulmaktadır. Kayıt işleminin tamamlanabilmesi için yönetim profili onayı gerekli olmasa da, Intune kullanıcı onaylı kayıtları önerir. Kullanıcı kayıt sırasında profili onaylamadıysanız, Kullanıcı **sistem tercihleri** > **profiller**' e gidebilir, yönetim profilini seçebilir ve **Onayla**' yı seçebilirler.    

### <a name="find-out-if-a-device-is-user-approved"></a>Bir cihazın Kullanıcı tarafından onaylanmış olup olmadığını bulma
1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Tüm cihazlar** > **cihazları** seçin > Cihaz > **donanımını**seçin.
3. **Kullanıcının onayladığı kayıt** alanını denetleyin.


## <a name="next-steps"></a>Sonraki adımlar

macOS cihazları kaydedildikten sonra, [macOS cihazları için özel ayarlar oluşturabilirsiniz](../configuration/custom-settings-macos.md).
