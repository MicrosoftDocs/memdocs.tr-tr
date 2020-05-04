---
title: Microsoft Store uygulamalarını Microsoft Intune’a ekleme
titleSuffix: ''
description: Microsoft Intune’a Microsoft Store (Windows Store) uygulamalarını ekleme hakkında bilgi edinin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 07241b6d-86d8-4abb-83a2-3fc5feae5788
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 23bb882c7dbf06264b3c8e5aa29947f8e4cb712c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325763"
---
# <a name="add-microsoft-store-apps-to-microsoft-intune"></a>Microsoft Store uygulamalarını Microsoft Intune’a ekleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Uygulamaları atama, izleme, yapılandırma veya korumadan önce bunları Intune’a eklemelisiniz. 

## <a name="add-an-app-to-intune"></a>Intune’a uygulama ekleme
Aşağıdakileri yaparak Intune’a bir Microsoft Store uygulaması ekleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar** > **tüm uygulamalar** > **Ekle**' yi seçin.
3. **Uygulama türünü seçin** bölmesinde, kullanılabilir **Mağaza uygulama** türleri altında, **Windows Mağazası uygulaması**' nı seçin.
4. **Seç**' e tıklayın. **Uygulama ekleme** adımları görüntülenir.
5. Windows Mağazası uygulamalarına yönelik **uygulama bilgilerini** yapılandırmak için [Microsoft Store](https://www.microsoft.com/store/apps) ' a gidin ve dağıtmak istediğiniz uygulamayı arayın. Uygulama sayfasını görüntüleyin ve uygulama ayrıntılarını bir yere göz önünde yapın. 
6. **Uygulama bilgileri** sayfasında, uygulama ayrıntılarını ekleyin:
    - **Ad**: uygulamanın şirket portalında görüntülenecek olan adını girin. Kullandığınız uygulama adlarının benzersiz olduğundan emin olun. Bir uygulama adı iki kez kullanılırsa, Şirket Portalı’nda kullanıcılara yalnızca bir ad gösterilir.
    - **Açıklama**: Uygulama için bir açıklama girin. Bu açıklama Şirket Portalı’nda kullanıcılara görüntülenir.Açıklama şirket portalında kullanıcılara görüntülenir.
    - **Yayımcı**: Uygulama yayımcısının adını girin.
    - **Uygulama mağazası URL’si**: Oluşturmak istediğiniz uygulamanın App Store URL’sini yazın. URL, istenen uygulama için [Microsoft Store](https://www.microsoft.com/store/apps) arayarak bulunabilir. Tarayıcı adres çubuğundan URL 'YI kullanın.
    - **Kategori**: İsteğe bağlı olarak, yerleşik uygulama kategorilerinden veya kendi oluşturduğunuz kategorilerden birini ya da birkaçını seçin. Böylelikle, Şirket Portalı’na göz atarken kullanıcıların uygulamayı bulmaları kolaylaşır.
    - **Bunu şirket portalı öne çıkan uygulama olarak göster**: kullanıcılar uygulamalara gözatarken, uygulama paketini Şirket portalının ana sayfasında göze çarpacak şekilde görüntülemek için bu seçeneği belirleyin.
    - **Bilgi URL’si**: İsteğe bağlı olarak, bu uygulama hakkında bilgi içeren bir web sitesinin URL’sini girin. URL, şirket portalında kullanıcılara görüntülenir.
    - **Gizlilik URL’si**: İsteğe bağlı olarak, bu uygulamayla ilgili gizlilik bilgilerini içeren bir web sitesinin URL’sini girin. URL, şirket portalında kullanıcılara görüntülenir.
    - **Geliştirici**: İsteğe bağlı olarak, uygulama geliştiricisinin adını girin.
    - **Sahip**: isteğe bağlı olarak, bu uygulamanın sahibi olarak *İK departmanı*gibi bir ad girin.
    - **Notlar**: İsteğe bağlı olarak bu uygulamayla ilişkilendirmek istediğiniz notları girin.
    - **Logo**: İsteğe bağlı olarak, uygulamayla ilişkilendirilecek bir simgeyi karşıya yükleyin. Bu simge, kullanıcılar şirket portalına gözatarken uygulamayla birlikte görüntülenir.
7. **İleri** ' ye tıklayarak **kapsam etiketleri** sayfasını görüntüleyin.
8. İsteğe bağlı olarak uygulamanın kapsam etiketlerini eklemek için **kapsam etiketlerini Seç** ' e tıklayın. Daha fazla bilgi için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi (RBAC) ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md).
9. **Atamalar** sayfasını göstermek için **İleri** ' ye tıklayın.
10. Uygulama için Grup atamalarını seçin. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları düzenlemek için grup ekleme](../fundamentals/groups-add.md). 
11. **İleri** ' ye tıklayarak **gözden geçir + oluştur** sayfasını görüntüleyin. Uygulama için girdiğiniz değerleri ve ayarları gözden geçirin.
12. İşiniz bittiğinde, uygulamayı Intune 'a eklemek için **Oluştur** ' a tıklayın.

Oluşturduğunuz uygulamanın **genel bakış** dikey penceresi görüntülenir.

Oluşturduğunuz uygulama, uygulamalar listesinde görüntülenir ve burada uygulamayı seçtiğiniz gruplara atayabilirsiniz.

> [!IMPORTANT]
> Microsoft Store uygulamaları, yalnızca **Kayıtlı cihazlar için kullanılabilir** atama türüne sahip gruplara atanabilir (kullanıcılar uygulamayı Şirket Portalı uygulamasından veya web sitesinden yükler).

## <a name="next-steps"></a>Sonraki adımlar

- [Gruplara uygulama ekleme](apps-deploy.md)
