---
title: Microsoft Intune kullanarak macOS cihazlarına Microsoft Edge ekleme
titleSuffix: ''
description: Microsoft Intune kullanarak macOS cihazlarına Microsoft Edge ekleme hakkında bilgi edinin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kellieei
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0d9267f989988ae33d56696d424de56a649bca2
ms.sourcegitcommit: 9908de7d30991ee499cc462d2eb730e1e4fd75a9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80900482"
---
# <a name="add-microsoft-edge-to-macos-devices-using-microsoft-intune"></a>Microsoft Intune kullanarak macOS cihazlarına Microsoft Edge ekleme

Uygulamaları dağıtmadan, yapılandırmadan, izleyebilmeniz veya koruyabilmeniz için önce bunları Intune 'a eklemeniz gerekir. Kullanılabilir [uygulama türlerinden](apps-add.md#app-types-in-microsoft-intune) biri Microsoft Edge *Sürüm 77 ve üzeri*. Intune 'da bu uygulama türünü seçerek, Microsoft Edge *sürüm 77 ve üstünü* , MacOS çalıştıran yönettiğiniz cihazlara atayabilir ve yükleyebilirsiniz. Bu uygulama türü, macOS uygulaması sarmalama aracı 'nı kullanmanıza gerek kalmadan, macOS cihazlarına Microsoft Edge 'i atamanızı kolaylaştırır. Uygulamalar daha güvenli ve güncel tutmaya yardımcı olmak için, uygulama Microsoft otomatik güncelleştirme (MAU) ile birlikte gelir.

> [!IMPORTANT]
> Bu uygulama türü, macOS için geliştirici ve Beta kanalları sunmaktadır. Dağıtım yalnızca Ingilizce (EN) ' dir, ancak son kullanıcılar tarayıcıdaki görüntüleme dilini **ayarlar** > **dilleri**altında değiştirebilir. 

> [!NOTE]
> Microsoft Edge *sürüm 77 ve üzeri sürümleri* de Windows 10 ' da kullanılabilir.

## <a name="prerequisites"></a>Önkoşullar

- MacOS cihazı, Microsoft Edge 'i yüklemeden önce macOS 10,12 veya sonraki bir sürümü çalıştırmalıdır.

## <a name="add-microsoft-edge-to-intune"></a>Microsoft Edge 'i Intune 'a ekleme

Aşağıdaki adımları kullanarak Intune 'a Microsoft Edge sürüm 77 ve üstünü ekleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Tüm uygulamalar** ** >  > ** **Ekle**' yi seçin.
3. **Microsoft Edge, sürüm 77 ve üzeri**altındaki **uygulama türü** listesinde **MacOS**' u seçin.

## <a name="configure-app-information"></a>Uygulama bilgilerini yapılandırma
Bu adımda, bu uygulama dağıtımı hakkında bilgi sağlarsınız. Bu bilgiler, uygulamayı Intune 'da tanımanıza yardımcı olur ve kullanıcıların uygulamayı şirket portalı 'nda bulmasına yardımcı olur.

1. **Uygulama bilgileri bölmesini göstermek** için **uygulama bilgileri** ' ne tıklayın.
2. **Uygulama bilgileri** bölmesinde, bu uygulama dağıtımı hakkında bilgi sağlarsınız. Bu bilgiler, uygulamayı Intune 'da tanımanıza yardımcı olur ve kullanıcıların uygulamayı şirket portalı 'nda bulmasına yardımcı olur.
    - **Ad**: uygulamanın şirket portalında görüntülenecek olan adını girin. Tüm adların benzersiz olduğundan emin olun. Aynı uygulama adı iki kez kullanılmışsa uygulamalardan yalnızca biri şirket portalında kullanıcılara görüntülenir.
    - **Açıklama**: Uygulama için bir açıklama girin. Örneğin, açıklamada hedeflenen kullanıcıları listeleyebilirsiniz.
    - **Yayımcı**: Yayımcı olarak Microsoft gösterilir.
    - **Kategori**: İsteğe bağlı olarak, yerleşik uygulama kategorilerinden veya kendi oluşturduğunuz kategorilerden birini ya da birkaçını seçin. Bu ayar, kullanıcıların şirket portalına gözatarken uygulamayı bulmasını kolaylaştırır.
    - **Bunu şirket portalı öne çıkan uygulama olarak görüntüle**: kullanıcılar uygulamalara gözatarken, uygulamayı şirket portalının ana sayfasında göze çarpacak şekilde göstermek için bu seçeneği belirleyin.
    - **Bilgi URL’si**: İsteğe bağlı olarak, bu uygulama hakkında bilgi içeren bir web sitesinin URL’sini girin. URL, şirket portalında kullanıcılara görüntülenir.
    - **Gizlilik URL’si**: İsteğe bağlı olarak, bu uygulamayla ilgili gizlilik bilgilerini içeren bir web sitesinin URL’sini girin. URL, şirket portalında kullanıcılara görüntülenir.
    - **Geliştirici**: Geliştirici olarak Microsoft gösterilir.
    - **Sahip**: Sahip olarak Microsoft gösterilir.
    - **Notlar**: İsteğe bağlı olarak bu uygulamayla ilişkilendirmek istediğiniz notları girin.
3. **Tamam**’ı seçin.

## <a name="configure-microsoft-edge-settings"></a>Microsoft Edge ayarlarını yapılandırma
Bu adımda, uygulama için yükleme seçeneklerini yapılandırın.

1. **Uygulama Ekle** bölmesinde **uygulama ayarları**' nı seçin.
2. Uygulama **ayarları** bölmesinde, uygulamayı hangi Edge kanalını dağıtacağınızı belirlemek için **Kanal** listesinden **Stable**, **Beta** veya **dev** ' ı seçin.

    - **Kararlı** kanal, kurumsal ortamlarda büyük ölçüde dağıtım için önerilen kanaldır. Her altı haftada bir güncelleştirilir, her sürüm beta kanalından geliştirmeler içerir.
    - **Beta** kanalı, en kararlı Microsoft Edge önizleme deneyimidir ve kuruluşunuzdaki tam bir pilot için en iyi seçenektir. Her sürüm altı haftada bir olan önemli güncelleştirmelerle, geliştirme kanalından dersleri ve geliştirmeleri içerir.
    - **Geliştirme** kanalı Windows, Windows Server ve MacOS 'ta kurumsal geri bildirimde bulunmak için hazırlayın. Her hafta güncelleştirilir ve en son geliştirmeleri ve düzeltmeleri içerir.

    > [!NOTE]
    > Microsoft Edge tarayıcı logosu, kullanıcılar şirket portalına gözatarken uygulamayla birlikte görüntülenir.

3.    **Tamam**’ı seçin.

## <a name="select-scope-tags-optional"></a>Kapsam etiketlerini seçin (isteğe bağlı)
Intune 'da istemci uygulama bilgilerini kimlerin görebileceğini anlamak için kapsam etiketlerini kullanabilirsiniz. Kapsam etiketleri hakkında tam Ayrıntılar için bkz. dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma.
1.    **Ekle** > **kapsam (Etiketler)** seçin.
2.    Kapsam etiketlerini aramak için **Seç** kutusunu kullanın.
3.    Bu uygulamaya atamak istediğiniz kapsam etiketlerinin yanındaki onay kutusunu işaretleyin.
4.    **Tamam** > **Seç** ' e tıklayın.

## <a name="add-the-app"></a>Uygulama ekleme
Yapılandırmayı tamamladıktan sonra **uygulama uygulaması** bölmesinden **Ekle** ' yi seçin. 

Oluşturduğunuz uygulama, uygulamalar listesinde görüntülenir ve burada uygulamayı seçtiğiniz gruplara atayabilirsiniz. 

> [!NOTE]
> Şu anda Apple, Intune 'un macOS cihazlarında Microsoft Edge 'i kaldırması için bir yol sağlamaz.

## <a name="next-steps"></a>Sonraki adımlar
- MacOS cihazlarında Microsoft Edge 'i yapılandırma hakkında bilgi edinmek için bkz. [macOS cihazlarında Microsoft Edge 'ı yapılandırma](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
- Kullanıcı gruplarında uygulama atamalarını dahil etme ve dışlama hakkında bilgi edinmek için, bkz. [Uygulama atamalarını dahil etme ve dışlama](apps-inc-exl-assignments.md).
- [Gruplara uygulama ekleme](apps-deploy.md)
