---
title: Kiracı iliştirme-Yönetim merkezinde ConfigMgr istemci ayrıntıları (Önizleme)
titleSuffix: Configuration Manager
description: Yönetim merkezinden Configuration Manager cihazların istemci ayrıntılarını görüntüleyin.
ms.date: 09/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: fbe75e34465335450f3a09680b68a78520451bd1
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643389"
---
# <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview"></a><a name="bkmk_mem"></a> Kiracı iliştirme: Yönetim merkezinde ConfigMgr istemci ayrıntıları (Önizleme)
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir. Yönetim merkezinde belirli bir cihaz için Koleksiyonlar, sınır grubu üyeliği ve gerçek zamanlı istemci bilgilerini içeren ConfigMgr istemci ayrıntılarını görebilirsiniz.

> [!Important]
> - Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.
> - Sınır grupları sekmesi yalnızca tek başına siteler için çalışır. Sekme, tek başına birincil site dışında herhangi bir şey için yönetim merkezinde boş olur.

## <a name="prerequisites"></a>Önkoşullar

- [Karşıya yüklenen cihazlara kiracı eklenmiş](device-sync-actions.md)bir ortam.
- Aşağıdaki tarayıcılardan biri:
  - Microsoft Edge, sürüm 77 ve üzeri
  - Google Chrome
- **Microsoft Endpoint Manager Yönetim Merkezi** 'ndeki kiracı iliştirme özelliklerine erişen kullanıcı hesabının hem [Azure ACTIVE DIRECTORY (Azure AD) Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) hem de [Active Directory Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)ile bulunması gerekir.
  - Kullanıcı hesabının Azure 'da eşitlenmiş bir kullanıcı nesnesi olması gerektiği anlamına gelir.

## <a name="permissions"></a>İzinler

Microsoft Endpoint Manager Yönetim Merkezi 'ndeki kiracı iliştirme özelliklerine erişen kullanıcı hesabı aşağıdaki izinlere sahip olmalıdır:

- Configuration Manager içinde cihazın **koleksiyonu** için **okuma** izni.
- Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü.
  - Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir.
   > [!TIP]
   > [Azure AD 'Deki uygulama Yöneticisi rolü](/azure/active-directory/users-groups-roles/directory-assign-admin-roles) , uygulamanın **Yönetici Kullanıcı** rolüne bir kullanıcı eklemek için yeterli izinlere sahiptir.

## <a name="view-configmgr-client-details"></a>ConfigMgr istemcisi ayrıntılarını görüntüle

1. Bir tarayıcıda öğesine gidin [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. **Cihazlar** ve **tüm cihazlar**' ı seçin.
1. [Kiracı iliştirme](device-sync-actions.md)aracılığıyla Configuration Manager eşitlenen bir cihaz seçin.
1. **İstemci ayrıntılarını (Önizleme)** seçin.
   - Birincil site bir saat sonra aşağıdaki alanları güncelleştirir:
      - **Son ilke isteği**
      - **Son etkin saat**
      - **Son yönetim noktası**.

   :::image type="content" source="media/6024387-device-details.png" alt-text="Microsoft Endpoint Manager Yönetim Merkezi 'nde istemci ayrıntıları" lightbox="media/6024387-device-details.png":::

1. İstemcinin koleksiyonlarını listelemek için **koleksiyonları (Önizleme)** seçin. <!--6024390-->

   :::image type="content" source="media/6024387-device-collections.png" alt-text="Microsoft Endpoint Manager Yönetim Merkezi 'nde istemci koleksiyonları" lightbox="media/6024387-device-collections.png":::

## <a name="next-steps"></a>Sonraki adımlar

[İstemci ayrıntıları sorunlarını giderme](troubleshoot-client-details.md)
