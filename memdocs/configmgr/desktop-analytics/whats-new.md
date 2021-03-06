---
title: Masaüstü Analizinizdeki yenilikler
titleSuffix: Configuration Manager
description: Masaüstü Analizi bulut hizmeti 'nin en son aylık sürümündeki yeni özelliklerin özeti.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd188b80375861cd08784d0574e737bfce7f2d92
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993155"
---
# <a name="whats-new-in-desktop-analytics"></a>Masaüstü Analizinizdeki yenilikler

Her ay masaüstü analizinden nelerin yeni olduğunu öğrenin.

> [!TIP]
> Her aylık güncelleştirmenin piyasaya çıkma üç güne kadar sürebilir. Bazı özelliklerin piyasaya çıkması birkaç haftayı bulabilir ve tüm özellikler ilk hafta bütün müşterilerimize sunulmamış olabilir.

Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="august-2020"></a>Ağustos 2020

### <a name="apps-deployed-from-configuration-manager-are-important-by-default"></a>Configuration Manager dağıtılan uygulamalar varsayılan olarak önemli öneme sahiptir

<!-- 4859763 -->

Bir uygulamanın **önem derecesi** , masaüstü analizinin, pilot dağıtımlar için dahil edilecek cihazların belirlenmesi açısından önemlidir. Masaüstü analizinden tüm uygulamaların önemini el ile yapılandırmak için gereken bir yönetici. Pilot uygulamayı doğruladıktan sonra bir üretim dağıtımıyla devam edebilirsiniz.

Artık Configuration Manager ile dağıttığınız tüm uygulamalar için, masaüstü Analizi varsayılan olarak otomatik olarak bunu önemli olarak yapılandırır. Bu davranış, ortamınızdaki uygulamaları daha hızlı bir şekilde bir üretim dağıtımında daha hızlı ilerlemesini sağlamak için yapılandırmanızı sağlar.

Daha fazla bilgi için bkz. [varlıklar-uygulamalar](about-assets.md#apps).

<!-- 6049643 -->

### <a name="improved-processing-of-diagnostic-data-during-snapshot-generation"></a>Anlık görüntü oluşturma sırasında tanılama verilerinin işlenmesi geliştirildi

Microsoft, masaüstü analizine kayıtlı cihazlardan Windows tanılama verilerini nasıl toplayıp işyacağını iyileştirmiştir. Bu geliştirmeler günlük anlık görüntü oluşturma güvenilirliğini artırır ve geliştirmede yeni özellikler hazırlar. Bu işin sonucunda, Microsoft bu uygulamayı başlatılan cihaz sayısını dağıtım planlarındaki **son 30 gün içinde** geçici olarak devre dışı bıraktı. Daha fazla bilgi için bkz. [varlıklar-uygulamalar](about-assets.md#usage).

## <a name="july-2020"></a>Temmuz 2020

### <a name="windows-10-version-2004-now-available-in-desktop-analytics"></a>Windows 10, sürüm 2004, artık Masaüstü Analizi 'nde kullanılabilir

<!-- 7370207 -->

Masaüstü Analizi portalında, güvenlik ve özellik güncelleştirmelerini izlerken artık Windows 10, sürüm 2004 ' i görürsünüz. Bir dağıtım planı oluşturduğunuzda, hedef sürüm olarak Windows 10, sürüm 2004 ' i seçebilirsiniz.

### <a name="improved-support-for-viewing-the-portal-from-any-device"></a>Portalı herhangi bir cihazdan görüntülemek için geliştirilmiş destek

<!-- 6270240 -->

Artık, Microsoft Endpoint Manager Yönetim merkezinde masaüstü Analizi portalını çeşitli cihaz türlerinden görüntüleyebilirsiniz. Artık, 320 x 256 piksel kadar düşük bir ekran çözünürlüğü için Web Içeriği erişilebilirlik yönergeleri (WCAG) 2,1 ' i karşılar. Örneğin, aşağıdaki görüntü, Apple iPhone 8 ' den portalın bir örneğidir:

:::image type="content" source="media/dashboard-iphone8.png" alt-text="İPhone 8 ' de masaüstü Analizi portalı":::

### <a name="notifications-for-service-impacting-events"></a>Hizmet tarafından etkileyen olaylar için bildirimler

<!-- 4982509 -->

Artık, masaüstü Analizi portalı bildirim başlık başlıklarını görüntüleyebilir. Bu bildirimler Microsoft 'un önemli olaylar ve sorunlar hakkında sizinle iletişim kurmasına olanak tanır. Örneğin, hizmetle ilgili bilinen sorunlar, veri gecikmesi veya yeni önkoşulları. Daha fazla bilgi için bkz. [hizmet bildirimleri](troubleshooting.md#service-notifications).

## <a name="june-2020"></a>Haziran 2020

### <a name="improvement-to-prerequisites"></a>Önkoşullardan iyileştirme

Masaüstü Analizi artık, Azure Active Directory (Azure AD) kiracınızda bir Microsoft 365 hizmeti dağıtmanızı gerektirmez. Azure AD 'de **Office 365 istemci Yöneticisi** uygulaması, hizmetten bilgi ve durum bilgilerinin Configuration Manager alınmasını sağlamak Için artık **Masaüstü Analizi** uygulamasıdır.

## <a name="may-2020"></a>Mayıs 2020

### <a name="reduce-the-number-of-apps-for-review"></a>Gözden geçirilecek uygulama sayısını azaltın

<!-- 5542186 -->

Portalda varlıklar sayfasında gösterilen uygulama sayısını birleştirmeye ve azaltmaya yardımcı olmak için artık aynı ad ve yayımcıya sahip tüm uygulama sürümlerini birleştirir. Önemli **uygulamalar** kutucuğunda uygulama sayısı bu ayarı yansıtır. Örneğin, Microsoft Edge 'in yüzlerce örneğini listelemek yerine, tüm sürümler için bir örnek vardır. Tüm sürümler için kararları bir kez daha yapabilirsiniz. Uygulamanın belirli sürümleriyle ilgili kararlar almanız gerekiyorsa, bu davranış yapılandırılabilir.

Daha fazla bilgi için bkz. [varlıklar-uygulamalar hakkında](about-assets.md#apps).

## <a name="march-2020"></a>Mart 2020

### <a name="support-for-multiple-hierarchies"></a>Birden çok hiyerarşi desteği

<!-- 4814075, 6079184 -->

Artık birden çok Configuration Manager hiyerarşilerini masaüstü analizi için tek bir ticari KIMLIKLE tek bir Azure Active Directory kiracısına bağlayabilirsiniz. Portal, farklı Hiyerarşilerden cihazları kategorilere ayırır ve küresel pilot 'lar ve dağıtım planları deneyimlerini geliştirir.

- Küresel pilot uygulamanızı yapılandırdığınızda, toplam kayıtlı cihazlarınızın %20 ' sini içeren koleksiyonlar eklerseniz, Portal bir uyarı görüntüler.
- Bir dağıtım planı oluşturduğunuzda, birden çok hiyerarşi için Koleksiyonlar ' ı seçerseniz, Portal bir uyarı görüntüler.

> [!NOTE]
> Birden çok hiyerarşi için destek, Configuration Manager sürüm 1910 veya üstünü gerektirir.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Küresel pilot](deploy-pilot.md#bkmk_GlobalPilot)
- [Dağıtım planları oluşturma](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>Uyumluluk korumalarını tanımla

<!-- 5746559 -->

Windows Uyumluluk verileri bazı uygulamaları ve sürücüleri bir *güvenlik önlemi*ile sınıflandırır, bu da Windows 10 güncelleştirmesinin başarısız olmasına veya geri alınmasına neden olabilir. Masaüstü Analizi artık bu korumaları önceden belirlemenize yardımcı olabilir. böylece, güncelleştirmeyi dağıtmadan önce varlığı düzeltebilirsiniz. Daha fazla bilgi için bkz. [Uyumluluk değerlendirmesi-korumalar](compat-assessment.md#safeguards).

## <a name="january-2020"></a>Ocak 2020

### <a name="additional-app-usage-detail"></a>Ek uygulama kullanımı ayrıntısı

<!-- 5533890 -->

Daha fazla bilgi görmek için bir uygulama seçtiğinizde, Ayrıntılar bölmesi artık ek kullanım bilgilerini içerir. Bu verileri, bir uygulama için yüklemenin kapsamını ve kullanıcıların düzenli olarak uygulamayı kullandıkları cihazları anlamanıza yardımcı olması için kullanabilirsiniz. Daha fazla bilgi için bkz. [varlıklar-uygulama kullanımı](about-assets.md#usage).

### <a name="provide-feedback-on-desktop-analytics"></a>Masaüstü analizi hakkında geri bildirim sağlama

<!-- 5451636 -->

Masaüstü Analizi hakkındaki görüşlerinizi paylaşmak için sağ taraftaki portalın en üstünde **gülümseme Gönder** simgesini seçin. Daha fazla bilgi için bkz. [ürün geri bildirimini paylaşma](get-support.md#bkmk_feedback).

## <a name="october-2019"></a>Ekim 2019

### <a name="improvements-to-compatibility-recommendations"></a>Uyumluluk önerilerinde iyileştirmeler

<!-- 3594545 -->

Masaüstü Analizi artık Windows yükseltmenin bir uygulamayı veya sürücüyü tamamen veya kısmen kaldıradığını algıladığında ek ayrıntı sağlar. Daha fazla bilgi için bkz. [Uyumluluk değerlendirmesi](compat-assessment.md#asset-is-removed-during-upgrade).

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Windows Analytics 'ten mevcut kiracıya geçiş

<!-- 5202803 -->

Artık, masaüstü analizine eklendikten sonra var olan bir Windows Analytics çalışma alanından girdileri geçirebilirsiniz.

## <a name="september-2019"></a>Eylül 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Windows Analytics 'ten girdileri geçirme

<!-- 4252663 -->

Ekleme sırasında artık mevcut bir Windows Analytics çalışma alanından girdileri geçirebilirsiniz.

### <a name="offboard-from-desktop-analytics"></a>Masaüstü analizinden kapalı Pano

<!-- 4972396 -->

Ortamınızda masaüstü analizlerini ayarlarsanız, ancak hizmeti kullanmayı durdurmak istiyorsanız hesabınızı kapatabilirsiniz. Fikrinizi 90 gün içinde değiştirirseniz, hesabı yeniden etkinleştirebilirsiniz. Daha fazla bilgi için bkz. [hesabınızı kapatma](account-close.md).

## <a name="august-2019"></a>Ağustos 2019

### <a name="reset-your-account"></a>Hesabınızı sıfırlama

<!-- 3733897 -->

Ortamınızda masaüstü analizlerini ayarlarsanız, ancak ekleme ve kayıt ile baştan başlamak istiyorsanız, şimdi sıfırlayabilirsiniz. İşlem hakkında daha fazla bilgi için bkz. [Hesabınızı sıfırlama](account-reset.md).

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Sistem ve Mağaza uygulamalarının otomatik yükseltme kararı

<!-- 3587232 -->

Önemli uygulamalara not ekleme çabalarınızı azaltmaya yardımcı olmak için bazı uygulama türleri otomatik olarak *önemli değil*olarak işaretlenir. Bu uygulamalar için dağıtım planı yükseltme kararı Ayrıca, *hazırlık*olarak işaretlenir. Aşağıdaki uygulamalar uyumludur ve Windows yükseltildikten sonra çalışmaya devam etmelidir:

- Microsoft tarafından yayınlanan sistem uygulamaları ve bileşenleri

- Microsoft Store yönetilen ve güncelleştirilmiş uygulamalar

Daha fazla bilgi için bkz. [sistem ve Mağaza uygulamalarının otomatik yükseltme kararı](about-assets.md#bkmk_plan-autoapp).

## <a name="whats-new-in-configuration-manager"></a>Configuration Manager yenilikleri

Masaüstü Analizi belgeleri her zaman Configuration Manager geçerli dalının en son sürümündeki işlevlere başvurur. Configuration Manager 'deki son değişiklikler hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [Sürüm 1906’daki yenilikler](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>Kullanım dışı bırakılan özellikler

Microsoft, masaüstü Analizi hizmeti 'nin önemli bir özelliğini kaldırmayı planlıyorsa, bu değişiklik kullanım dışı Configuration Manager bir özellik olarak önceden duyurulacaktır. Daha fazla bilgi için bkz. [kullanımdan kaldırılan özellikler](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).
