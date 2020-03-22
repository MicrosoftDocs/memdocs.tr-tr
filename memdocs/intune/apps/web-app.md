---
title: Microsoft Intune’a web uygulamaları ekleme
titleSuffix: ''
description: Microsoft Intune için Web uygulamaları (istemci-sunucu uygulamaları) ekleme hakkında bilgi edinin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f08752f-0e87-4ad9-a34c-4991b3150775
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b30d2a3ef7c85557222aa39740417a1a6fd463f1
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084124"
---
# <a name="add-web-apps-to-microsoft-intune"></a>Microsoft Intune’a web uygulamaları ekleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune, web uygulamaları da dahil olmak üzere çeşitli uygulama türlerini destekler. Web uygulaması, bir istemci-sunucu uygulamasıdır. Sunucu; kullanıcı arabirimi, içerik ve işlevleri içeren web uygulamasını sağlar. Ayrıca modern web barındırma platformları çoğu zaman güvenlik, yük dengeleme ve diğer yararlar da sunar. Web uygulaması web’de ayrı olarak korunur. Bu uygulama türüne işaret etmek için Microsoft Intune kullanırsınız. Bu uygulamaya erişebilecek kullanıcı gruplarını da atarsınız. 

Kullanıcılarınız için uygulamaları yönetebilmek ve atayabilmek için önce uygulamayı Intune’a ekleyin. 

Intune, kullanıcının cihazında Web uygulaması için bir kısayol oluşturur. İOS/ıpados cihazlarında, giriş ekranına Web uygulaması için bir kısayol eklenir. Android Cihaz Yöneticisi cihazlarda, Intune şirket portalı pencere öğesine Web uygulaması için bir kısayol eklenir ve pencere öğesinin Kullanıcı tarafından el ile sabitlenilmesi gerekir. Windows cihazlarında, Web uygulamasının bir kısayolu Başlat menüsüne yerleştirilir.

> [!Note]
> Web uygulamalarını başlatmak için kullanıcının cihazında bir tarayıcı yüklü olmalıdır. 
> 
> Android kurumsal cihazlar için bkz. [yönetilen Google Play web bağlantıları](apps-add-android-for-work.md#managed-google-play-web-links).
> 
> İOS cihazlarında yeni web klipleri (sabitlenmiş Web uygulamaları), korumalı bir tarayıcıda açılması gerektiğinde Intune Managed Browser yerine Microsoft Edge 'de açılır. Daha eski iOS web klipleri için, bu web kliplerini, Managed Browser bunun yerine Microsoft Edge 'de açıldıklarından emin olmak için yeniden hedeflemeniz gerekir.

## <a name="add-a-web-app-to-intune"></a>Intune’a bir web uygulaması ekleme
Bir uygulamayı web’de uygulamanın kısayolu olarak Intune’a eklemek için:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Tüm uygulamalar** ** >  > ** **Ekle**' yi seçin.
3. **Uygulama türünü seçin** bölmesinde, kullanılabilir **diğer** türler altında **Web bağlantısı**' nı seçin.
4. **Seçin**’e tıklayın. **Uygulama ekleme** adımları görüntülenir.
5. **Uygulama bilgileri** sayfasında, aşağıdaki bilgileri ekleyin:
    - **Ad**: Şirket portalında görüntülendiği şekliyle uygulamanın adını girin. 

        > [!NOTE]
        > Uygulamayı dağıttıktan ve yükledikten sonra Intune Azure portalı aracılığıyla uygulamanın adını değiştirirseniz, uygulama artık komutlar kullanılarak hedeflenemez.

    - **Açıklama**: Uygulama için bir açıklama girin. Bu açıklama Şirket Portalı’nda kullanıcılara görüntülenir.Açıklama şirket portalında kullanıcılara görüntülenir.
    - **Yayımcı**: Bu uygulamanın yayımcısının adını girin.
    - **Uygulama URL’si**: Atamak istediğiniz uygulamayı barındıran web sitesinin URL’sini girin.
    - **Kategori**: İsteğe bağlı olarak, yerleşik uygulama kategorilerinden veya kendi oluşturduğunuz kategorilerden birini ya da birkaçını seçin. Böylelikle, Şirket Portalı’na göz atarken kullanıcıların uygulamayı bulmaları kolaylaşır.
    - **Bunu şirket portalı öne çıkan uygulama olarak göster**: kullanıcılar uygulamalara gözatarken, uygulama paketini Şirket portalının ana sayfasında göze çarpacak şekilde görüntülemek için bu seçeneği belirleyin.
    - **Bu bağlantının açılabilmesi için bir yönetilen tarayıcı gerektir**: Kullanıcılara, Intune ile yönetilen tarayıcıda açabilecekleri bir web sitesi veya web uygulaması bağlantısı atayın. Bu tarayıcı cihazlarında yüklü olmalıdır.
    - **Logo**: Uygulamayla ilişkilendirilecek bir simgeyi karşıya yükleyin. Bu simge, kullanıcılar şirket portalına gözatarken uygulamayla birlikte görüntülenir.
6. **İleri** ' ye tıklayarak **kapsam etiketleri** sayfasını görüntüleyin.
7. İsteğe bağlı olarak uygulamanın kapsam etiketlerini eklemek için **kapsam etiketlerini Seç** ' e tıklayın. Daha fazla bilgi için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi (RBAC) ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md).
8. **Atamalar** sayfasını göstermek için **İleri** ' ye tıklayın.
9. Uygulama için Grup atamalarını seçin. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları düzenlemek için grup ekleme](../fundamentals/groups-add.md). 
10. **İleri** ' ye tıklayarak **gözden geçir + oluştur** sayfasını görüntüleyin. Uygulama için girdiğiniz değerleri ve ayarları gözden geçirin.
11. İşiniz bittiğinde, uygulamayı Intune 'a eklemek için **Oluştur** ' a tıklayın.

    Oluşturduğunuz uygulamanın **genel bakış** dikey penceresi görüntülenir.

> [!Note]
> Şu anda, Intune Web uygulamalarının iOS/ıpados cihazlarına dağıtılması yönetim profiliyle ilişkili olduğundan el ile kaldırılamaz. Intune portalında dağıtım türünü **Kaldır** seçeneğine değiştirerek web uygulamasının otomatik olarak kaldırılmasını sağlayabilirsiniz. Ancak uygulama ataması amacını **Kaldır** seçeneğine değiştirmeden dağıtımı kaldırırsanız, cihazın kaydı Intune’dan kaldırılana kadar web uygulaması cihazda kalır.

Son kullanıcılar, Web uygulamasını seçip **tarayıcıda aç**seçeneğini belirleyerek web uygulamalarını doğrudan Windows Şirket portalı uygulamasından başlatabilir. Yayınlanan Web URL 'SI doğrudan Web tarayıcısında açılır. 

## <a name="next-steps"></a>Sonraki adımlar

Oluşturduğunuz uygulama, uygulamalar listesinde görüntülenir ve burada uygulamayı seçtiğiniz gruplara atayabilirsiniz. Yardım için bkz. [Uygulamaları gruplara atama](apps-deploy.md). 
