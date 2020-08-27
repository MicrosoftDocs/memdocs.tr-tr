---
title: Microsoft Intune-Azure 'da bir Telekom gider yönetimi hizmeti ayarlama | Microsoft Docs
titleSuffix: ''
description: Veri kullanımını izlemek ve Android Cihaz Yöneticisi, iOS ve ıpados cihazlarında eşikleri veya sınırları ayarlamak için Saaswedo Telekom gider yönetimi hizmeti ile Microsoft Intune tümleştirin.
keywords: Saaswedo
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/08/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b7bf5802-4b65-4aeb-ac99-8e639dd89c2a
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cabf3bad447ef3db8250d14fcb376cb86aefad3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907558"
---
# <a name="set-up-a-telecom-expense-management-service-in-intune"></a>Intune'da telekom gider yönetimi hizmeti ayarlama

Intune 'u kullanarak, kuruluşa ait mobil cihazlarda veri kullanımındaki Telekom giderlerini yönetebilirsiniz. Intune, Saaswedo 'ın [Datalert Telekom gider yönetimi](http://datalert.biz/get-started)ile tümleşir. Datalert, Telekom veri kullanımını yöneten gerçek zamanlı bir Telekom gider yönetimi çözümüdür. Intune tarafından yönetilen cihazlarınız için beklenmeyen verilerin ve dolaşım ücretlerinden kaçınmaya yardımcı olabilir.

Datalert ile tümleştirme, dolaşım ve yurtiçi veri kullanımı sınırlarını ayarlayabilir, izleyebilir ve uygulayabilir. Sınırlar eşiklerinizi aştığında, uyarılar otomatik olarak tetiklenir. Ayrıca, kullanıcıyı veya grupları dolaşımı devre dışı bırakma veya eşiği aşmaya yönelik farklı eylemler uygulayacak şekilde hizmeti yapılandırabilirsiniz. Datalert Yönetim Konsolu, veri kullanımı ve izleme bilgilerini gösteren raporlar içerir.

Aşağıdaki görüntüde, Intune 'un Datalert ile nasıl tümleştirildiğini gösterilmektedir:

> [!div class="mx-imgBorder"]
> ![Intune ile Datalert’ün tümleştirme diyagramı](./media/telecom-expenses-monitor/tem-datalert-intune-solution-diagram.png)

Datalert hizmetini Intune ile kullanmak için, Datalert ve Intune 'da bazı yapılandırma ayarları vardır. Bu makale, şunları nasıl yapacağınızı gösterir:

- Datalert hizmetini Intune 'a bağlamak için Datalert konsolundaki ayarları yapılandırın.
- Bu bağlantının etkin ve Intune 'da etkin olduğunu onaylayın.
- Intune 'u kullanarak Datalert uygulamasını cihazlarınıza ekleyin.
- Datalert hizmetini ve Intune için (isteğe bağlı) devre dışı bırakın.

## <a name="supported-platforms"></a>Desteklenen platformlar

- Android Cihaz Yöneticisi 4,4 ve Knox özellikli daha yeni cihazlar (Samsung)
- iOS 8,0 ve üzeri
- ıpados 13,0 ve üzeri

## <a name="prerequisites"></a>Önkoşullar

- [Microsoft Endpoint Manager yönetim merkezine](https://go.microsoft.com/fwlink/?linkid=2109431) Microsoft Intune ve erişim için bir abonelik
- [Datalert](http://www.datalert.biz/) aboneliği (datalert 'in Web sitesini açar)

## <a name="telecom-expense-management-providers"></a>Telekom gider yönetimi sağlayıcıları

Intune, aşağıdaki Telekom gider yönetimi sağlayıcısıyla tümleştirilir:

- [Saaswedo datalert Telekom gider yönetimi hizmeti](http://www.datalert.biz/) (datalert 'in Web sitesini açar)

## <a name="deploy-the-intune-and-datalert-solution"></a>Intune ve Datalert çözümünü dağıtma

### <a name="step-1-connect-the-datalert-service-to-intune"></a>1. Adım: Datalert hizmetini Intune 'a bağlama

1. Datalert yönetim konsolunda yönetici kimlik bilgileriyle oturum açın.

2. Konsolunda, **MDM yapılandırması**> **Ayarlar** sekmesine gidin.

3. **Engellemeyi kaldır**' ı seçin. **Engellemeyi kaldırma** , sayfadaki ayarları değiştirmenize veya güncelleştirmenize olanak tanır.

4. **Intune/datalert bağlantı**  >  **sunucusu MDM**'de **Microsoft Intune**' yi seçin.

5. **Azure AD etki alanı**için Azure kiracı kimliğinizi girin. **Bağlantı**' yı seçin.

    **Bağlantı**' yı seçtiğinizde, datalert hizmeti Intune ile iade eder. Mevcut bir Datalert bağlantısı olmadığını onaylar. Birkaç dakika sonra, bir Microsoft oturum açma sayfası görüntülenerek, Datalert Azure kimlik doğrulaması tarafından izlenir.

6. Microsoft kimlik doğrulaması sayfasında **Kabul Et**’i seçin.

    Birkaç dakika sonra kapatılan bir Datalert **teşekkür** sayfasına yönlendirilirsiniz. Datalert bağlantıyı doğrular ve doğrulanan öğelerin yanındaki yeşil onay işaretlerini gösterir. Doğrulama başarısız olursa, kırmızı renkte bir ileti görürsünüz. Yardım için Datalert desteğiyle iletişim kurun.

    Aşağıdaki görüntüde bağlantı başarılı olduğunda yeşil onay işaretleri gösterilmektedir:

      > [!div class="mx-imgBorder"]
      > ![Başarılı bağlantıyı gösteren Datalert sayfası](./media/telecom-expenses-monitor/tem-datalert-connection.png)

7. **Datalert uygulaması/adal onayı**' nda, anahtarı **Açık**olarak ayarlayın. Microsoft kimlik doğrulaması sayfasında **Kabul Et**’i seçin.

    Birkaç dakika sonra kapatılan bir Datalert **teşekkür** sayfasına yönlendirilirsiniz. Datalert bağlantıyı doğrular ve doğrulanan öğelerin yanındaki yeşil onay işaretlerini gösterir. Doğrulama başarısız olursa, kırmızı renkte bir ileti görürsünüz. Yardım için Datalert desteğiyle iletişim kurun.

    Aşağıdaki görüntüde bağlantı başarılı olduğunda yeşil onay işaretleri gösterilmektedir:

      > [!div class="mx-imgBorder"]
      > ![Başarılı bağlantıyı gösteren Datalert sayfası](./media/telecom-expenses-monitor/tem-datalert-adal-consent.png)

8. **MDM profilleri yönetimi 'nde (isteğe bağlı)**, anahtarını **Açık**olarak ayarlayın. Bu ayar, ilkeleri ayarlamanıza yardımcı olması için Datalert 'in Intune 'daki kullanılabilir profilleri okumasına izin verir. 

    Microsoft kimlik doğrulaması sayfasında **Kabul Et**’i seçin.

    Birkaç dakika sonra kapatılan bir Datalert **teşekkür** sayfasına yönlendirilirsiniz. Datalert bağlantıyı doğrular ve doğrulanan öğelerin yanındaki yeşil onay işaretlerini gösterir. Doğrulama başarısız olursa, kırmızı renkte bir ileti görürsünüz. Yardım için Datalert desteğiyle iletişim kurun.

    Aşağıdaki görüntüde bağlantı başarılı olduğunda yeşil onay işaretleri gösterilmektedir:

    > [!div class="mx-imgBorder"]
    > ![Başarılı bağlantıyı gösteren Datalert sayfası](./media/telecom-expenses-monitor/tem-datalert-mdm-profiles.png)

### <a name="step-2-confirm-telecom-expense-management-is-active-in-intune"></a>2. Adım: Telekom gider yönetiminin Intune 'da etkin olduğunu onaylayın

1. adımı tamamladıktan sonra bağlantınız otomatik olarak etkinleştirilir. Intune 'da bağlantı durumu **etkin**' i gösterir. Durumun etkin olduğunu doğrulamak için aşağıdaki adımları kullanın:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **Telekom gider yönetimi**' ni seçin. **Etkin** bağlantı durumunu arayın:

    > [!div class="mx-imgBorder"]
    > ![Datalert bağlantı durumunu Etkin olarak gösteren Intune sayfası](./media/telecom-expenses-monitor/tem-azure-portal-enable-service.png)

### <a name="step-3-deploy-the-datalert-app-to-devices"></a>3. Adım: Datalert uygulamasını cihazlara dağıtma

Veri kullanımının yalnızca kuruluşa ait satırlardan toplandığını doğrulamak için şunları yaptığınızdan emin olun:

- Intune 'da cihaz kategorileri oluşturun.
- Datalert uygulamasını yalnızca kurumsal telefonlarda hedefleyin.

Bu bölümde bu adımlar listelenmektedir.

#### <a name="create-device-categories-and-device-groups-mapped-to-your-categories"></a>Kategorilerinize eşlenmiş cihaz kategorileri ve cihaz grupları oluşturun

Kuruluş gereksinimlerinize bağlı olarak, kurumsal ve kişisel gibi en az iki cihaz kategorisi oluşturun. Ardından, her kategori için dinamik cihaz grupları oluşturun. Gerektikçe kuruluşunuz için daha fazla kategori oluşturabilirsiniz.

Intune 'da cihaz kategorileri oluşturmak için bkz. [cihazları gruplara eşleme](../enrollment/device-group-mapping.md).

Bu kategoriler, kayıt sırasında kullanıcılara gösterilir ([Android cihazlarını kaydetme](../enrollment/android-enroll.md)). Kullanıcıların seçim kategorisine bağlı olarak, kayıtlı cihaz ilgili cihaz grubuna taşınır.

> [!div class="mx-imgBorder"]
> ![İlke ekle bölmesinin ekran görüntüsü](./media/telecom-expenses-monitor/tem-dynamic-membership-rules.png)

#### <a name="add-the-datalert-app-to-intune"></a>Datalert uygulamasını Intune 'a ekleme

Aşağıdaki adımlarda Datalert uygulaması eklenir. Örnek olarak, iOS/ıpados kullanılır. [Uygulama ekleme](../apps/apps-add.md) ve [kapsam etiketlerini kullanma](../fundamentals/scope-tags.md) bu adımlarla ilgili daha belirgin bilgilere sahiptir.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **uygulamalar**  >  **tüm uygulamalar**  >  **Ekle**' yi seçin.

2. **Uygulama türü**' nü seçin. Örneğin, iOS/ıpados için **mağaza app-iOS/ıpados**' ı seçin.

3. **Uygulama mağazasını ara**bölümünde datalert uygulamasını bulmak Için **datalert** yazın.

4. **Datalert** uygulamasını seçin > **seçin**:

    > [!div class="mx-imgBorder"]
    > ![App Store 'dan Intune istemci uygulamalarına datalert uygulamasını ekleme](./media/telecom-expenses-monitor/tem-select-app-from-apple-app-store.png)

5. Uygulama bilgileri ve kapsam etiketleri gibi ek özellikleri girin:

    > [!div class="mx-imgBorder"]
    > ![Ad, açıklama, işletim sistemini seçme ve Intune 'da uygulamaya daha fazla ayar dahil olmak üzere uygulama özelliklerini girin](./media/telecom-expenses-monitor/tem-steps-to-create-the-app.png)

6. **OK**  >  Değişikliklerinizi kaydetmek için Tamam**Ekle** ' yi seçin. Datalert uygulaması listede gösterilmektedir.

#### <a name="assign-the-datalert-app-to-the-corporate-device-group"></a>Datalert uygulamasını kurumsal cihaz grubuna atama

1. **Uygulamalar**  >  **tüm uygulamalar**' da, önceki adımda eklediğiniz datalert uygulamasını seçin.

2. **Atamalar**  >  **grubu Ekle**' yi seçin. Uygulamanın nasıl atandığını seçin. [Intune 'daki gruplara uygulama atama](../apps/apps-deploy.md) , bu ayarlar hakkında daha fazla ayrıntı içerir.

    Bu adımlarda, uygulama yüklemesini gerekli veya grup için isteğe bağlı yapmayı tercih edeceksiniz. Aşağıdaki örnek, yükleme gereken şekilde gösterir. Gerektiğinde, kullanıcıların cihazlarını kaydettikten sonra Datalert uygulamasını yüklemeleri gerekir.

    > [!div class="mx-imgBorder"]
    > ![İlke ekle bölmesinin ekran görüntüsü](./media/telecom-expenses-monitor/tem-assign-datalert-app-to-device-group.png)

### <a name="step-4-add-organization-phone-lines-to-the-datalert-console"></a>4. Adım: Datalert konsoluna kuruluş telefon hatları ekleme

Intune ve Datalert Hizmetleri artık birbirleriyle iletişim kuracak şekilde yapılandırılmıştır. Ardından, kuruluşunuzun ücretli telefon hatlarını Datalert konsoluna ekleyin. Tüm hücresel veya dolaşım kullanım ihlalleri için eşikleri ve eylemleri girin. Şirket tarafından ödenen telefon hatlarını Datalert konsoluna el ile ekleyebilir veya cihaz Intune 'A kaydedildikten sonra otomatik olarak ekleyebilirsiniz.

Bu öğeleri ayarlamak için, [Microsoft Intune datalert kurulumuna](http://www.datalert.fr/microsoft-intune/intune-setup) gidin (datalert 'in Web sitesini açar). **Ayarlar** sekmesinde, kurulum sihirbazındaki adımları izleyin.

> [!div class="mx-imgBorder"]
> ![İlke ekle bölmesinin ekran görüntüsü](./media/telecom-expenses-monitor/tem-add-phone-lines-to-datalert-console.png)

Datalert hizmeti artık etkin. Veri kullanımını izlemeye başlar ve yapılandırılmış kullanım sınırlarını aşan cihazlarda hücresel ve dolaşım verilerini devre dışı bırakır.

## <a name="end-user-enrollment"></a>Son Kullanıcı kaydı

Son Kullanıcı deneyimi için aşağıdaki makaleler yardımcı olabilir:

- [İOS/ıpados cihazınızı Telekom gider yönetimine kaydetme](../user-help/enroll-your-device-with-telecom-expense-management-ios.md)
- [Android cihazınızı telekom gider yönetimine kaydetme](../user-help/enroll-your-device-with-telecom-expense-management-android.md)

## <a name="turn-off-the-datalert-service"></a>Datalert hizmetini kapatma

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **kiracı yönetim**  >  **bağlayıcıları ve belirteçleri**  >  **Telekom gider yönetimi**' ni seçin.
2. **Telekom gider yönetimini etkinleştir ' i ayarlayın ve devre dışı bırakmak için yapılandırdığınız kullanım kotalarını aşan cihazlarda hücresel veya dolaşım verilerini engelleyin** . **Disable**
3. Değişikliklerinizi **kaydedin** .

> [!IMPORTANT]
> Intune 'da Datalert hizmetini devre dışı bırakırsanız:
>
> - Kullanım limitlerinin geçmiş ihlallerine bağlı olarak cihazlara uygulanan tüm eylemler geri alınır.
> - Artık kullanıcıların veri erişimi ve dolaşımı engellenmez.
> - Intune, hizmetten gelen sinyalleri almaya devam eder, ancak Intune sinyalleri yoksayar.

## <a name="next-steps"></a>Sonraki adımlar

Veri kullanımı raporlaması, Saaswedo 'ın Datalert yönetim konsolunda kullanılabilir.