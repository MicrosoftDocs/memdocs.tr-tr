---
title: Öğretici-EMM ve uygulama yapılandırması için Intune 'U kullanmak üzere bolluk yapılandırma
titleSuffix: Microsoft Intune
description: Bu öğreticide, EMM ve uygulama yapılandırması için bir bolluk 'yi Intune kullanacak şekilde yapılandıracaksınız.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 55db37c5-0da7-4d9c-8027-525afb1c6349
Customer intent: As an Intune admin, I want to learn how to configure Slack to use Intune for EMM and app configuration..
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98ab8fd069b0542a29f61d9b0f5b69d7b82a8a1c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074784"
---
# <a name="tutorial-configure-slack-to-use-intune-for-emm-and-app-configuration"></a>Öğretici: EMM ve uygulama yapılandırması için Intune 'U kullanmak üzere bolluk yapılandırma

Bolluk, Microsoft Intune kullanabileceğiniz bir işbirliği uygulamasıdır.   

Bu öğreticide şunları yapacaksınız:
> [!div class="checklist"]
> - Intune 'U, bolluk kurumsal kılavuzunuzda Enterprise Mobility Management (EMM) sağlayıcısı olarak ayarlayın. Kılavuza ait çalışma alanlarınıza erişimi Intune tarafından yönetilen cihazlara sınırlayabilirsiniz.
> - İOS/ıpados üzerindeki EMM için bolluk uygulamasını ve Android iş profili cihazları için bolluk uygulamasını yönetmek üzere uygulama yapılandırma ilkeleri oluşturun.
> - Android ve iOS/ıpados cihazlarının uyumlu kabul edilmesi için uyması gereken koşulları ayarlamak için Intune cihaz uyumluluk ilkeleri oluşturun.

Intune aboneliğiniz yoksa [ücretsiz deneme hesabı için kaydolun](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Önkoşullar
Bu öğretici için aşağıdaki abonelik sahip bir test kiracısına ihtiyacınız olacak:
- Azure Active Directory Premium ([ücretsiz deneme](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Intune aboneliği ([ücretsiz deneme](../fundamentals/free-trial-sign-up.md))

Ayrıca, bir [bolluk kurumsal kılavuz](https://get.slack.help/hc/articles/360004150931-What-is-Slack-Enterprise-Grid-) planına de ihtiyacınız vardır.

## <a name="configure-your-slack-enterprise-grid-plan"></a>Bolluk kurumsal kılavuz planınızı yapılandırın
[Bolluk yönergelerini](https://get.slack.help/hc/articles/115002579426-Enable-Enterprise-Mobility-Management-for-your-org#step-2:-turn-on-emm) Izleyerek bolluk kurumsal kılavuz PLANıNıZ için EMM 'yi açın ve kılavuz planınızın kimlik sağlayıcısı (IDP) olarak [Azure Active Directory bağlayın](https://docs.microsoft.com/azure/active-directory/saas-apps/slack-tutorial) .

## <a name="sign-in-to-intune"></a>Intune'da oturum açma
[Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) genel yönetici veya Intune Hizmet Yöneticisi olarak oturum açın. Intune Deneme aboneliği oluşturduysanız aboneliği oluşturduğunuz hesap Genel yönetici rolüne sahip olur.

## <a name="set-up-slack-for-emm-on-ios-devices"></a>İOS cihazlarında EMM için bolluk ayarlama
Kuruluşunuz için iOS/ıpados uygulaması bolluğu ' nı Intune kiracınıza ekleyin ve kuruluşların iOS/ıpados kullanıcılarının bir EMM sağlayıcısı olarak Intune ile bolluk 'e erişmesine olanak tanımak için bir uygulama yapılandırma ilkesi oluşturun.

### <a name="add-slack-for-emm-to-intune"></a>Intune 'a EMM için bolluk ekleme
Intune 'da bir yönetilen iOS/ıpados uygulaması olarak EMM için bolluk ekleyin ve bolluk kullanıcılarınızı atayın. Uygulamalar platforma özgüdür, bu nedenle Android cihazlarda bolluk kullanıcılarınız için ayrı bir Intune uygulaması eklemeniz gerekir.
1. Yönetim merkezinde, **uygulamalar** > **tüm uygulamalar** > **Ekle**' yi seçin.
2. **Uygulama türü**altında **iOS** Mağazası uygulamasını seçin.
3. **App Store’da Ara**’yı seçin. "EMM için bolluk" arama terimini girin ve uygulamayı seçin. **App Store 'Da ara** bölmesinde **Seç** ' e tıklayın.
4. **Uygulama bilgileri** ' ni seçin ve tüm değişiklikleri uygun gördüğünüz şekilde yapılandırın. Uygulama bilgilerinizi ayarlamak için **Tamam ' ı** seçin.
5. **Ekle**'ye tıklayın.
6. **Atamalar**' ı seçin.
7. **Grup ekle**’ye tıklayın. Bolluk için EMM 'i açtığınızda kimin etkilenmesini seçtiğinize bağlı olarak, **atama türü** altında şunları seçebilirsiniz:
    - "Tüm Üyeler (konuklar dahil)" seçeneğini belirlediyseniz **Kayıtlı cihazlar Için kullanılabilir** "veya
    - "Tüm Üyeler (konukları hariç)" veya "Isteğe bağlı" seçeneğini belirlediyseniz **kayıt olmadan veya bunlarla birlikte kullanılabilir** .
8. **Dahil edilen grupları** seçin ve **Bu uygulamayı tüm kullanıcılar için kullanılabilir yap** altında **Evet**' i seçin.
9. **Tamam**' a tıklayın ve ardından grubu eklemek Için yeniden **Tamam** ' a tıklayın.
10. **Kaydet**’e tıklayın.

### <a name="add-an-app-configuration-policy-for-slack-for-emm"></a>EMM için bolluk için bir uygulama yapılandırma ilkesi ekleyin
EMM iOS/ıpados için bolluk için bir uygulama yapılandırma ilkesi ekleyin. Yönetilen cihazlar için uygulama yapılandırma ilkeleri platforma özgüdür. bu nedenle, Android cihazlarda bolluk kullanıcılarınıza ayrı bir ilke eklemeniz gerekir.
1. Yönetim merkezinde, **uygulamalar** > **uygulama yapılandırma ilkeleri** > **Add** > **yönetilen cihazlar**Ekle ' yi seçin.
2. Ad alanına ' bolluk uygulama yapılandırma ilkesi test ' girin.
3. Cihaz kayıt türü ' nün altında, **yönetilen cihazların** ayarlandığını onaylayın.
4. Platform altında **iOS**' u seçin.
5. **İlişkili uygulama**' yı seçin.
6. Arama çubuğuna "EMM için bolluk" yazın ve uygulamayı seçin.
7. **Tamam**' a tıklayın ve ardından **yapılandırma ayarları**' nı seçin. 
8. **Tamam**' ı ve ardından **Ekle**' yi seçin.
9. Arama çubuğuna "bolluk uygulama yapılandırma ilkesi sınaması" yazın ve yeni eklediğiniz ilkeyi seçin.
10. Yönet ' den **atamalar**' ı seçin.
11. Ata ' nın altında, **tüm kullanıcılar + tüm cihazlar**' ı seçin.
12. **Kaydet**’e tıklayın.

### <a name="optional-create-an-ios-device-compliance-policy"></a>Seçim İOS cihaz uyumluluk ilkesi oluşturma
Bir cihazın uyumlu sayılması için karşılaması gereken şartları ayarlamak için bir Intune cihaz uyumluluk ilkesi ayarlayın. Bu öğreticide iOS/ıpados cihazları için bir cihaz uyumluluk ilkesi oluşturacağız. Uyumluluk ilkeleri platforma özgüdür, bu nedenle Android cihazlarda bolluk kullanıcılarınız için ayrı bir ilke oluşturmanız gerekir.
1. Yönetim merkezinde **cihaz uyumluluk** > **ilkeleri** > **ilke oluştur**' u seçin.
2. Ad alanına "iOS uyumluluk ilkesi sınaması" yazın.
3. Açıklama ' da "iOS uyumluluk ilkesi sınaması" yazın.
4. Platform altında **iOS**' u seçin.
5. **Cihaz Durumu**’nı seçin. Jailbreak uygulanmış cihazlar ' ın yanındaki **Engelle**' yi seçin ve ardından **Tamam**' ı seçin.
6. **Sistem Güvenliği**’ni seçin ve Parola ayarlarını girin. Bu öğretici için aşağıdaki önerilen ayarları seçin:
    - Mobil cihazların kilidini açmak için parola gerektir için **gerektir**' i seçin.
    - Basit parolalar için **Engelle**' yi seçin.
    - En düşük parola uzunluğu’nu 4 olarak ayarlayın.
    - Gerekli parola türü için **alfasayısal**' i seçin.
    - Parola istenmeden önce ekran kilitlenmesinden sonra geçen en uzun dakika için **hemen**öğesini seçin.
    - Parola zaman aşımı (gün) için 41 değerini girin.
    - Yeniden kullanımı önlemek için önceki parola sayısı için 5 değerini girin.
7. **Tamam**' a tıklayın ve ardından yeniden **Tamam** ' ı seçin.
8. **Oluştur**' a tıklayın.

## <a name="set-up-slack-on-android-work-profile-devices"></a>Android iş profili cihazlarında bolluk ayarlama
, Kuruluşların Android kullanıcılarına bir EMM sağlayıcısı olarak Intune ile bolluk erişimi sağlamak için Google Play, bir uygulama yapılandırma ilkesi oluşturun ve bu uygulamaları Intune kiracınıza ekleyin.

### <a name="add-slack-to-intune"></a>Intune 'a bolluk ekleme
Intune 'da bir yönetilen Google Play uygulaması olarak bolluk ekleyin ve bolluk kullanıcılarınızı atayın. Uygulamalar platforma özgüdür, bu nedenle iOS/ıpados cihazlarındaki bolluk kullanıcılarınıza ayrı bir Intune uygulaması eklemeniz gerekir.
1. Intune 'da, **uygulamalar** > **tüm uygulamalar** > **Ekle**' yi seçin.
2. Uygulama türü altında **Mağaza uygulaması – yönetilen Google Play**seçin.
3. **Yönetilen Google Play-Onayla**' yı seçin. "EMM için bolluk" arama terimini girin ve uygulamayı seçin.
4. **Onayla**seçeneğini belirleyin.
5. Arama çubuğuna "bolluk" yazın ve yeni eklediğiniz uygulamayı seçin.
6. Yönet ' den **atamalar**' ı seçin.
7. **Grup Ekle**' yi seçin. Bolluk için EMM 'i açtığınızda kimin etkilenmesini seçtiğinize bağlı olarak, **atama türü** altında şunları seçebilirsiniz:
    - "Tüm Üyeler (konuklar dahil)" seçeneğini belirlediyseniz **Kayıtlı cihazlar Için kullanılabilir** "veya
    - "Tüm Üyeler (konukları hariç)" veya "Isteğe bağlı" seçeneğini belirlediyseniz **kayıt olmadan veya bunlarla birlikte kullanılabilir** .
8. Dahil edilen grupları seçin ve bu uygulamayı tüm kullanıcılar için kullanılabilir yap altında **Evet**' i seçin.
9. **Tamam**' a ve ardından yeniden **Tamam** ' a tıklayın.
10. **Kaydet**’e tıklayın.

### <a name="add-an-app-configuration-policy-for-slack"></a>Bolluk için bir uygulama yapılandırma ilkesi ekleyin
Bolluk için bir uygulama yapılandırma ilkesi ekleyin. Yönetilen cihazlar için uygulama yapılandırma ilkeleri platforma özgüdür, bu nedenle iOS/ıpados cihazlarındaki bolluk kullanıcılarınıza ayrı bir ilke eklemeniz gerekir.
1. Intune 'da **uygulamalar** > **uygulama yapılandırma ilkeleri** > **Ekle**' yi seçin.
2. Ad alanına bolluk uygulama yapılandırma ilkesi testi girin.
3. Cihaz kayıt türü ' nün altında, **yönetilen cihazlar**' ı seçin.
4. Platform altında **Android**' i seçin.
5. **İlişkili uygulama**' yı seçin.
6. Arama çubuğuna "bolluk" yazın ve uygulamayı seçin.
7. **Tamam**' ı ve ardından **yapılandırma ayarları**' nı seçin.
    - Yapılandırma anahtarları ve değerleri hakkında daha fazla bilgi için, [bolluk 'In AppConfig Web sayfasının](https://www.appconfig.org/company/slack/)"Teknik" sekmesindeki belgelere başvurun.
8. **Tamam**' a ve ardından **Ekle**' yi seçin.
9. Arama çubuğuna "bolluk uygulama yapılandırma ilkesi sınaması" yazın ve yeni eklediğiniz ilkeyi seçin.
10. Yönet ' den **atamalar**' ı seçin.
11. Ata ' nın altında, **tüm kullanıcılar + tüm cihazlar**' ı seçin.
12. **Kaydet**’e tıklayın.

### <a name="optional-create-an-android-device-compliance-policy"></a>Seçim Android cihaz uyumluluk ilkesi oluşturma
Bir cihazın uyumlu sayılması için karşılaması gereken şartları ayarlamak için bir Intune cihaz uyumluluk ilkesi ayarlayın. Bu öğreticide, Android cihazlar için bir cihaz uyumluluk ilkesi oluşturacağız. Uyumluluk ilkeleri platforma özgüdür, bu nedenle iOS/ıpados cihazlarında bolluk kullanıcılarınıza ayrı bir ilke oluşturmanız gerekir.
1. Intune 'da **cihaz uyumluluk** > **ilkeleri** > **ilke oluştur**' u seçin.
2. Ad alanına "Android uyumluluk ilkesi sınaması" yazın.
3. Açıklama ' da "Android uyumluluk ilkesi sınaması" yazın.
4. Platform altında **Android kurumsal**' i seçin.
5. Profil türü altında **iş profili**' ni seçin.
6. **Cihaz Durumu**’nı seçin. Kökü belirtilmiş cihazlar ' ın yanındaki **Engelle**' yi seçin ve ardından **Tamam**' ı seçin.
7. **Sistem güvenliği** ' ni seçin ve **parola ayarlarını**girin. Bu öğretici için aşağıdaki önerilen ayarları seçin:
    - Mobil cihazların kilidini açmak için parola gerektir için **gerektir**' i seçin.
    - Gerekli parola türü için en **az alfasayısal**' i seçin.
    - En düşük parola uzunluğu’nu 4 olarak ayarlayın.
    - Parola istenmeden önce ekran kilitlenmesinden sonra geçen en uzun dakika için **15 dakika**seçin.
    - Parola zaman aşımı (gün) için 41 değerini girin.
    - Yeniden kullanımı önlemek için önceki parola sayısı için 5 değerini girin.
8. **Tamam**' a ve ardından yeniden **Tamam** ' a tıklayın.
9. **Oluştur**' a tıklayın.

## <a name="launch-slack"></a>Başlatma bolluğu

Az önce oluşturduğunuz ilkeler sayesinde, çalışma alanlarınızdan birinde oturum açmaya çalışan tüm iOS/ıpados veya Android iş profili cihazları Intune 'a kaydolmaları gerekir. Bu senaryoyu test etmek için, Intune 'a kayıtlı bir iOS/ıpados cihazında EMM için bolluk başlatmayı veya Intune 'A kayıtlı bir Android iş profili cihazında bolluk başlatmayı deneyin. 

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide:
- Intune 'U, bolluk kurumsal kılavuzunuzda Enterprise Mobility Management (EMM) sağlayıcısı olarak ayarlarsınız. 
- İOS/ıpados üzerindeki EMM için bolluk uygulamasını ve Android iş profili cihazları için bolluk uygulamasını yönetmek üzere uygulama yapılandırma ilkeleri oluşturdunuz.
- Android ve iOS/ıpados cihazlarının uyumlu kabul edilmesi için uyması gereken koşulları ayarlamak için Intune cihaz uyumluluk ilkelerini oluşturdunuz.

Uygulama yapılandırma ilkeleri hakkında daha fazla bilgi için bkz. [Microsoft Intune Için uygulama yapılandırma ilkeleri](app-configuration-policies-overview.md). Cihaz uyumluluk ilkeleri hakkında daha fazla bilgi edinmek için bkz. [Intune kullanarak kuruluşunuzdaki kaynaklara erişime izin vermek için cihazlarda kuralları ayarlama](../protect/device-compliance-get-started.md).
