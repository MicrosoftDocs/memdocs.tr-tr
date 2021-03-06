---
title: Microsoft Intune’da cihaz profilleri atama | Microsoft Docs
description: Kullanıcılara ve cihazlara cihaz profilleri ve ilkeleri atamak için Microsoft Endpoint Manager yönetim merkezini kullanın. Microsoft Intune'da grupları bir profil atamasının dışında tutmayı öğrenin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d
ms.reviewer: altsou
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55835d5ee8527f54e530da5113f841ed108fa6f5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915815"
---
# <a name="assign-user-and-device-profiles-in-microsoft-intune"></a>Microsoft Intune'da kullanıcı ve cihaz profilleri atama

Bir profil oluşturursunuz ve girdiğiniz tüm ayarlar burada saklanır. Bir sonraki adım, profilinizi Kullanıcı veya cihaz gruplarınızı dağıtmaktır veya "atamanız". Atanan profiller kullanıcılara ve cihazlara ulaşır ve girdiğiniz ayarlar uygulanır.

Bu makalede profil atama yöntemlerinin yanı sıra profillerinizde kapsam etiketlerini kullanma adımları hakkında bilgilere yer verilmiştir.

> [!NOTE]  
> Bir profil kaldırıldığında veya bir cihaza artık atanmadıysa, profildeki ayarlara bağlı olarak farklı şeyler meydana gelebilir. Ayarlar CSP 'lere dayalıdır ve her CSP profil kaldırmayı farklı şekilde işleyebilir. Örneğin, bir ayar varolan değeri tutabilir ve varsayılan değere geri dönmeyebilir. Davranış, işletim sistemindeki her CSP tarafından denetlenir. Windows CSP 'lerin listesi için bkz. [yapılandırma hizmeti sağlayıcısı (CSP) başvurusu](/windows/client-management/mdm/configuration-service-provider-reference).
>
> Bir ayarı farklı bir değere değiştirmek için yeni bir profil oluşturun, ayarı **Yapılandırılmadı**olarak yapılandırın ve profili atayın. Cihaza uygulandıktan sonra, kullanıcıların ayarı tercih ettikleri değer olarak değiştirmesi gerekir.
>
> Bu ayarları yapılandırırken, bir pilot grubuna dağıtım yapmanız önerilir. Daha fazla Intune dağıtım önerisi için bkz. [dağıtım planı oluşturma](../fundamentals/planning-guide-rollout-plan.md).

## <a name="before-you-begin"></a>Başlamadan önce

Profiller atamak için doğru rolün bulunduğundan emin olun. Daha fazla bilgi için bkz. [Microsoft Intune Ile rol tabanlı erişim denetimi (RBAC)](../fundamentals/role-based-access-control.md).

## <a name="assign-a-device-profile"></a>Bir cihaz profili atama

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profillerini**seçin. Tüm profiller listelenir.
3. Atamak istediğiniz profili seçin > **Özellikler**  >  **atamaları**  >  **Düzenle**:

    :::image type="content" source="./media/device-profile-assign/properties-select-assignments.png" alt-text="Microsoft Intune ve uç nokta yöneticisinde profili kullanıcılara ve gruplara dağıtmak için atamaları seçin":::

4. **Dahil edilen grupları** veya **Dışlanan grupları**seçin ve ardından **dahil edilecek grupları seç**' i seçin. Gruplarınızı seçtiğinizde, bir Azure AD grubu seçersiniz. Birden çok grup seçmek için grupları seçerken **Ctrl** tuşunu basılı tutun.

    :::image type="content" source="./media/device-profile-assign/select-included-excluded-groups-profile-assignment.png" alt-text="Microsoft Intune ve uç nokta yöneticisinde bir profili atarken veya dağıtmada kullanıcıları ve grupları dahil etme veya hariç tutma.":::

5. **Gözden geçir + kaydet**' i seçin. Bu adım, profilinizi atamaz.
6. **Kaydet**’i seçin. Kaydettiğinizde profiliniz atanır. Cihazların Intune hizmetine iade edildiğinde gruplarınızı profil ayarlarınızı alır.

## <a name="use-scope-tags-or-applicability-rules"></a>Kapsam etiketlerini veya uygulanabilirlik kurallarını kullanma

Bir profil oluşturduğunuzda veya güncelleştirdiğinizde, profile kapsam etiketleri ve Uygulanabilirlik kuralları da ekleyebilirsiniz.

**Kapsam etiketleri** , veya gibi belirli gruplar için profilleri filtrelemek için harika bir yoldur `US-NC IT Team` `JohnGlenn_ITDepartment` . Daha fazla bilgi için bkz. [Dağıtılmış BT için RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

Windows 10 cihazlarında, profil yalnızca belirli bir işletim sistemi sürümü veya belirli bir Windows sürümü için geçerli olacak şekilde **uygulanabilirlik kuralları** ekleyebilirsiniz. [Uygulanabilirlik kurallarında](device-profile-create.md#applicability-rules) daha fazla bilgi bulunur.

## <a name="user-groups-vs-device-groups"></a>Kullanıcı grupları ve cihaz grupları karşılaştırması

Birçok kullanıcı, Kullanıcı gruplarını ne zaman kullanacağınızı ve cihaz gruplarının ne zaman kullanılacağını sorar. Yanıt, amacınız için farklılık gösterir. İşte başlamanıza yardımcı olacak bazı rehberlik.

### <a name="device-groups"></a>Device groups

Bir cihaza, kim oturum açmış olduğunuza bakılmaksızın ayarları uygulamak istiyorsanız, profillerinizi bir cihaz grubuna atayın. Cihaz gruplarına uygulanan ayarlar, Kullanıcı değil, her zaman cihaza gider.

Örnek:

- Cihaz grupları, adanmış bir kullanıcısı olmayan cihazları yönetmek için yararlıdır. Örneğin, anahtarları, tarama envanterini Yazdır, vardiya çalışanları tarafından paylaşılır, belirli bir ambara atanmış ve bu şekilde devam eden cihazlara sahip olursunuz. Bu cihazları bir cihaz grubuna koyun ve profillerinizi bu aygıtlar grubuna atayın.

- BIOS 'ta ayarları güncelleştiren bir [cihaz üretici yazılımı yapılandırma arabirimi (DFCı) Intune profili](device-firmware-configuration-interface-windows.md) oluşturursunuz. Örneğin, bu profili cihaz kamerayı devre dışı bırakacak şekilde yapılandırır veya kullanıcıların başka bir işletim sistemini önyüklemesine engel olmak için önyükleme seçeneklerini kilitler. Bu profil, bir cihazlar grubuna atamak için iyi bir senaryodur.

- Bazı belirli Windows cihazlarında, cihazı kimin kullandığını fark etmeksizin her zaman bazı Microsoft Edge ayarlarını denetlemek istersiniz. Örneğin, tüm indirmeleri engellemek, tüm tanımlama bilgilerini geçerli gözatma oturumuyla sınırlamak ve gözatma geçmişini silmek isteyebilirsiniz. Bu senaryo için, bu belirli Windows cihazlarını bir cihazlar grubuna yerleştirin. Ardından, [Intune 'da bir yönetim şablonu](administrative-templates-windows.md)oluşturun, bu cihaz ayarlarını ekleyin ve ardından bu profili cihazlar grubuna atayın.

Özetlemek gerekirse, cihazda oturum açmış olan kişileri veya herkes oturum açarsa cihaz gruplarını kullanın. Ayarlarınızı her zaman cihazda olmasını istiyorsunuz.

### <a name="user-groups"></a>Kullanıcı grupları

Kullanıcı gruplarına uygulanan profil ayarları her zaman kullanıcıya gider ve çok sayıda cihazda oturum açıldığında kullanıcıya gider. Kullanıcıların Surface Pro for Work ve bir kişisel iOS/ıpados cihazı gibi birçok cihazı olması normaldir. Ayrıca, bir kişinin e-postaya ve diğer kuruluş kaynaklarına bu cihazlardan erişmesi normaldir.

Bu genel kuralı izleyin: bir özellik, e-posta veya Kullanıcı sertifikaları gibi bir kullanıcıya aitse, ardından Kullanıcı gruplarına atayın.

Örnek:

- Tüm cihazlarındaki tüm kullanıcılar için bir yardım masası simgesi koymak istiyorsunuz. Bu senaryoda, bu kullanıcıları bir Users grubuna koyun ve yardım masası simgesi profilinizi bu kullanıcılar grubuna atayın.
- Kullanıcı, kuruluşa ait yeni bir cihaz alır. Kullanıcı, cihazda etki alanı hesabıyla oturum açar. Cihaz otomatik olarak Azure AD 'ye kaydedilir ve Intune tarafından otomatik olarak yönetilir. Bu profil, bir kullanıcılar grubuna atamak için iyi bir senaryodur.
- Bir Kullanıcı cihazda oturum açtığında, OneDrive veya Office gibi uygulamalardaki özellikleri denetlemek istersiniz. Bu senaryoda, OneDrive veya Office profil ayarlarınızı bir kullanıcılar grubuna atayın.

  Örneğin, Office uygulamalarınızda güvenilmeyen ActiveX denetimlerini engellemek isteyebilirsiniz. [Intune 'da bir yönetim şablonu](administrative-templates-windows.md)oluşturabilir, bu ayarı yapılandırabilir ve ardından bu profili bir Users grubuna atayabilirsiniz.

Özetlemek gerekirse, ayarlarınızı ve kurallarınızı her zaman kullanıcıya, hangi cihazdan kullandıklarından bağımsız olarak gitmek istediğinizde kullanıcı gruplarını kullanın.

## <a name="exclude-groups-from-a-profile-assignment"></a>Grupları bir profil atamasından dışlama

Intune cihaz yapılandırma profilleri, profil atamasından grupları eklemenizi ve dışlanmasını sağlar.

En iyi uygulama olarak, Kullanıcı gruplarınız için özel profiller oluşturun ve atayın. Ve, özel olarak cihaz gruplarınız için farklı profiller oluşturun ve atayın. Gruplar hakkında daha fazla bilgi için bkz. [kullanıcıları ve cihazları düzenlemek için grup ekleme](../fundamentals/groups-add.md).

Profillerinizi atadığınızda, grupları dahil etmek ve dışlamak için aşağıdaki tabloyu kullanın. Onay işareti, atamanın desteklendiği anlamına gelir:

:::image type="content" source="./media/device-profile-assign/include-exclude-user-device-groups.png" alt-text="Desteklenen seçenekler bir profil atamasında grupları içerir veya hariç tutar":::

### <a name="what-you-should-know"></a>Bilmeniz gerekenler

- Dışlama, aşağıdaki aynı grup türü senaryolarına dahil edilmeye göre önceliklidir:

  - Kullanıcı gruplarını dahil etme ve Kullanıcı gruplarını hariç tutma
  - Cihaz gruplarını ekleme ve cihaz grubunu hariç tutma

  Örneğin, **tüm kurumsal kullanıcılar** kullanıcı grubuna bir cihaz profili atarsınız, ancak üst **düzey yönetim personeli** Kullanıcı grubundaki üyeleri dışlayabilirsiniz. Her iki grup da Kullanıcı grupları olduğundan, üst **düzey yönetim personeli** hariç **tüm şirket kullanıcıları** profili alırlar.

- Intune, Kullanıcı-cihaz grubu ilişkilerini değerlendirmez. Bunları karışık gruplara atarsanız, sonuçlar istediğiniz veya beklediğiniz gibi olabilir.

  Örneğin, **tüm kullanıcılar** kullanıcı grubuna bir cihaz profili atarsınız, ancak **tüm kişisel cihazlar** cihaz grubunu dışlayamazsınız. Bu karma grup profili atamasında, **tüm kullanıcılar** profili alır. Dışlama uygulanmaz.

  Sonuç olarak, profillerin karışık gruplara atanması önerilmez.

## <a name="next-steps"></a>Sonraki adımlar

Profillerinizi ve profillerinizin çalıştığı cihazları izleme konusunda bilgi için bkz. [Cihaz profillerini izleme](device-profile-monitor.md).