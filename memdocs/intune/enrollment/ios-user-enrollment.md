---
title: İOS/ıpados cihazlarını kaydetme-Kullanıcı kaydı
titleSuffix: Microsoft Intune
description: İOS/ıpados ve ıpados Kullanıcı kaydını ayarlamayı öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/2/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d98f3f8205490848d9f5137e97e7796eee67a67
ms.sourcegitcommit: 7a5196d4d9736c5cd52a23155c479523e52a097d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84436780"
---
# <a name="set-up-iosipados-and-ipados-user-enrollment-preview"></a>İOS/ıpados ve ıpados Kullanıcı kaydını ayarlama (Önizleme)

Intune 'u, Apple 'ın Kullanıcı kayıt işlemini kullanarak iOS/ıpados ve ıpados cihazlarını kaydedecek şekilde ayarlayabilirsiniz. Kullanıcı kaydı, yöneticilere diğer kayıt yöntemleriyle karşılaştırıldığında yönetim seçeneklerinin kolaylaştırılmış bir alt kümesini sağlar.

Kullanıcı kaydında kullanılabilen seçenekler hakkında daha fazla bilgi için bkz. [Kullanıcı kaydı desteklenen eylemler, parolalar ve diğer seçenekler](ios-user-enrollment-supported-actions.md).

> [!NOTE]
> Apple 'ın Intune 'da Kullanıcı kaydı desteği şu anda önizlemededir.

## <a name="prerequisites"></a>Önkoşullar
- [Mobil Cihaz Yönetimi (MDM) Yetkilisi](../fundamentals/mdm-authority-set.md)
- [Apple MDM anında Iletme sertifikası](apple-mdm-push-certificate-get.md)

## <a name="create-a-user-enrollment-profile-in-intune"></a>Intune 'da Kullanıcı kayıt profili oluşturma

Kayıt profili, kayıt sırasında bir cihaz grubuna uygulanan ayarları tanımlar. 

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) **cihazlar**  >  **iOS**  >  **iOS kayıt**  >  **kayıt türleri (Önizleme)**  >  **Profil oluştur**  >  **iOS/ıpados**' ı seçin. Bu profil, iOS/ıpados ve ıpados son kullanıcılarınızın kurumsal bir Apple yöntemiyle kaydedilmeyen cihazlarda sahip olacağı kayıt deneyimini belirtebileceğiniz yerdir. Değişiklik yapmak isterseniz, bu profili oluşturduktan sonra düzenleyebilirsiniz.

    ![Apple kayıt profili oluştur](./media/ios-user-enrollment/create-profile.png)

2. **Temel bilgiler** sayfasında, yönetim amaçları için profil Için bir **ad** ve **Açıklama** girin. Kullanıcılar bu ayrıntıları göremez. Azure Active Directory’de dinamik bir grup oluşturmak için **Ad** alanını kullanabilirsiniz. enrollmentProfileName parametresini, bu kayıt profiliyle cihazlara atamak amacıyla tanımlamak için profil adını kullanın. [Azure Active Directory dinamik grupları](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#rules-for-devices) hakkında daha fazla bilgi edinin.

    ![Temel bilgiler sayfası](./media/ios-user-enrollment/basics-page.png)

3. **İleri**’yi seçin.

4. **Ayarlar** sayfasında, **kayıt türü**için aşağıdaki seçeneklerden birini belirleyin:

    ![Ayarlar sayfası](./media/ios-user-enrollment/settings-page.png)

    - **Cihaz kaydı**: Bu profildeki tüm kullanıcılar cihaz kaydını kullanacaktır.
    - **Kullanıcı kaydı**: Bu profildeki tüm kullanıcılar Kullanıcı kaydını kullanacaktır.
    - **Kullanıcı seçimine göre belirlenir**: Bu gruptaki tüm kullanıcılara hangi kayıt türünün kullanılacağı tercih edilir. Kullanıcılar cihazlarını kaydettiğinde, bu cihazdan ve **(Şirket) bu cihazın sahibi** **olduğumu** arasında seçim yapmak için bir seçenek görür. İkincisini seçtiyse cihaz, cihaz kaydı kullanılarak kaydedilir. Kullanıcı **Bu cihaza sahip olduğumu**seçerse, tüm cihazı güvenli hale getirmek veya yalnızca iş ile ilgili uygulamaları ve verileri güvenli hale getirmek için başka bir seçenek alırlar. Son kullanıcının, cihazında hangi kayıt türünün uygulandığını belirler. Bu Kullanıcı seçeneği, Intune 'daki cihaz sahipliği özniteliğinde de yansıtılır. Kullanıcı deneyimi hakkında daha fazla bilgi edinmek için bkz. [şirket kaynaklarınıza iOS/ıpados cihaz erişimini ayarlama](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).
    
5. **İleri**’yi seçin.

6. **Atamalar** sayfasında, bu profilin atanmasını istediğiniz kullanıcıları içeren Kullanıcı gruplarını seçin. Profili tüm kullanıcılara veya belirli gruplara atamayı seçebilirsiniz. Seçili gruplardaki tüm kullanıcılar, yukarıda seçilen kayıt türünü kullanır. Özellik, cihazlar yerine Kullanıcı kimliklerini temel aldığı için, Kullanıcı kayıt senaryolarında cihaz grupları desteklenmez. Profili tüm kullanıcılara veya belirli gruplara atamayı seçebilirsiniz.

    ![Atamalar sayfası](./media/ios-user-enrollment/assignments-page.png)

7. **İleri**’yi seçin.

8. **İnceleme ve oluşturma** sayfasında, seçimlerinizi gözden geçirin ve ardından profili kullanıcılara atamak için **Oluştur** ' u seçin.

    ![Atamalar sayfası](./media/ios-user-enrollment/assignments-page.png)


## <a name="profile-priority"></a>Profil önceliği

Birden fazla kayıt türü profili oluşturduktan sonra, uygulandıkları öncelik sırasını değiştirebilirsiniz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS**  >  **iOS kayıt**  >  **kayıt türleri (Önizleme)** öğesini seçin.
2. Listedeki profilleri, uygulanmasını istediğiniz sırada sürükleyip bırakın.

Herhangi bir kullanıcının profilleri arasındaki çakışmalar söz konusu olduğunda, Kullanıcı için daha yüksek öncelikli profil uygulanır.


