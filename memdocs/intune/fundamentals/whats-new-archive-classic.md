---
title: Klasik Microsoft Intune portalı arşivindeki yenilikler
description: Microsoft Intune için Yenilikler duyuruları arşivi
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/08/2017
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ed2db991-4729-49a7-a1e6-be2ffa0d03d1
ROBOTS: noindex,nofollow
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: e3c939b2b21bc8bfbf82a997c05f24d91c487a9e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81681979"
---
# <a name="whats-new-in-the-intune-classic-portal---previous-months"></a>Klasik Intune portalındaki yenilikler - önceki aylar

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Bu sayfa, klasik Intune portalı için [Yenilikler sayfasında](whats-new.md) daha önceden açıklanan yeni özellikleri ve bildirimleri listeler.

## <a name="april-2017"></a>Nisan 2017

### <a name="new-capabilities"></a>Yeni özellikler

#### <a name="myapps-available-for-managed-browser---822308-822303--"></a>MyApps, Managed Browser ile kullanılabilir  <!--822308, 822303-->

Managed Browser için Microsoft MyApps desteği geliştirildi. Yönetim hedefinde yer almayan Managed Browser kullanıcıları doğrudan MyApps hizmetine alınarak yöneticileri tarafından sağlanan SaaS uygulamalarına erişebilecekler. Intune yönetimi hedefinde yer alan kullanıcılar ise MyApps içeriğine yerleşik Managed Browser yer işaretinden erişim sağlayabilecekler.

#### <a name="new-icons-for-the-managed-browser-and-the-company-portal---918433-918431-971473--"></a>Managed Browser ve Şirket Portalı için yeni simgeler  <!--918433, 918431, 971473-->

Managed Browser uygulamasının hem Android hem de iOS sürümlerinin simgesi güncelleştiriliyor. Yeni simgede Enterprise Mobility + Security (EM+S) paketindeki diğer uygulamalarla tutarlı hale getirmek için güncelleştirilmiş Intune rozeti bulunacak. Managed Browser'ın yeni simgesini [Intune uygulama arabirimindeki yenilikler sayfasında](whats-new-app-ui.md) görebilirsiniz.

Şirket Portalı uygulamasının da Android, iOS ve Windows sürümlerinin simgeleri EM+S paketindeki diğer uygulamalarla daha tutarlı hale getirilmek üzere güncelleştiriliyor. Bu simgeler nisan ayından başlayarak mayıs ayının sonuna kadar kademeli olarak kullanıma sunulacak.

#### <a name="sign-in-progress-indicator-in-android-company-portal---953374--"></a>Android Şirket Portalı uygulamasında oturum açma ilerleme göstergesi  <!--953374-->

Android Şirket Portalı uygulamasında yapılan güncelleştirme ile kullanıcı uygulamayı başlattığında veya sürdürdüğünde oturum açma ilerleme göstergesi görüntüleniyor. Kullanıcının uygulamaya erişmesine izin verilmeden önce göstergede "Bağlanıyor..." ile başlayıp sırasıyla "Oturum açılıyor..." ve "Güvenlik gereksinimleri denetleniyor..."durumları gösteriliyor. Android için Şirket Portalı uygulamasının yeni ekran görüntülerini [Intune uygulama arabirimindeki yenilikler sayfasında](whats-new-app-ui.md) görebilirsiniz.

#### <a name="block-apps-from-accessing-sharepoint-online----679339---"></a>Uygulamaların SharePoint Online’a erişmesini engelleyin  <!-- 679339 -->

Artık, uygulama koruma ilkelerinin uygulanmadığı uygulamaları engellemek için uygulama tabanlı bir koşullu erişim ilkesi oluşturabilirsiniz. bu sayede [SharePoint Online](../protect/app-based-conditional-access-intune-create.md)'a erişebilirsiniz. Uygulama tabanlı koşullu erişim senaryosunda, Azure portal kullanarak SharePoint Online 'a erişmesini istediğiniz uygulamaları belirtebilirsiniz.

#### <a name="single-sign-on-support-from-the-company-portal-for-ios-to-outlook-for-ios---834012--"></a>iOS Şirket Portalından iOS için Outlook uygulamasına çoklu oturum açma desteği  <!--834012-->
Aynı cihazda aynı hesapla iOS için Şirket Portalı uygulamasında oturum açmış kullanıcıların artık Outlook uygulamasında oturum açmasına gerek yok. Kullanıcılar Outlook uygulamasını başlattıktan sonra hesaplarını seçip otomatik olarak oturum açabilecekler. Bu işlevi diğer Microsoft uygulamalarına da eklemek için çalışıyoruz.

#### <a name="improved-status-messaging-in-the-company-portal-app-for-ios---744866--"></a>iOS için Şirket Portalı uygulamasında geliştirilmiş durum iletileri  <!--744866-->
iOS için Şirket Portalı uygulamasında artık daha açıklayıcı hata iletileri görüntülenecek ve cihazlardaki gelişmeler hakkında daha açıklayıcı bilgiler verilecek. Bu hata durumları önceden "Şirket Portalı Geçici Olarak Devre Dışı" konulu genel bir hata iletisi içinde listeleniyordu. Ayrıca İnternet bağlantısı olmayan bir kullanıcı iOS üzerinde Şirket Portalı uygulamasını başlattığında ana sayfada "İnternet Bağlantısı Yok" yazan kalıcı bir durum çubuğu görecek.

#### <a name="improved-app-install-status-for-the-windows-10-company-portal-app---676495--"></a>Geliştirilmiş Windows 10 Şirket Portalı uygulaması yükleme durumu  <!--676495-->

Windows 10 Şirket Portalı uygulamasında uygulama yüklemesi için yeni geliştirmeler şunları içerir:
- MSI paketleri için daha hızlı yükleme durumu raporlaması
- Windows 10 Yıldönümü Güncelleştirmesi ve üzerini çalıştıran cihazlardaki modern uygulamalar için daha hızlı yükleme durumu raporlaması
- Windows 10 Yıldönümü Güncelleştirmesi ve üzerini çalıştıran cihazlardaki modern uygulama yüklemeleri için yeni ilerleme çubuğu

Yeni ilerleme çubuğunu [Intune uygulama arabirimindeki yenilikler sayfasında](whats-new-app-ui.md) görebilirsiniz.

#### <a name="bulk-enroll-windows-10-devices----747607---"></a>Windows 10 cihazlarını toplu kaydetme <!-- 747607 -->

Artık, Windows Yapılandırma Tasarımcısı (WCD) kullanarak Windows 10 Creators Update çalıştıran çok sayıda cihazın Azure Active Directory ve Intune’a katılmasını sağlayabilirsiniz. Azure AD kiracınız için [Toplu MDM kaydını](../enrollment/windows-bulk-enroll.md) etkinleştirmek için Windows Yapılandırma Tasarımcısı kullanarak cihazların Azure AD kiracınıza katılmasını sağlayan bir sağlama paketi oluşturun ve paketi toplu kaydetmek ve yönetmek istediğiniz şirkete ait cihazlara uygulayın. Paket cihazlarınıza uygulandıktan sonra cihazlar Azure AD'ye katılır, Intune'a kaydolur ve Azure AD kullanıcılarınızın oturum açmasına hazır hale gelir.  Azure AD kullanıcıları, bu cihazlarda standart kullanıcılardır ve atanan ilkeleri ve gerekli uygulamaları alırlar. Self Servis ve Şirket Portalı senaryoları şu anda desteklenmiyor.

### <a name="whats-new-in-the-public-preview-of-intune-in-the-azure-portal--736542--"></a>Azure portalında Intune’un genel önizlemesindeki yenilikler <!--736542-->

Erken takvim yılında 2017, grafik API 'Leri kullanılarak genişletilebilen modern bir hizmet platformunda çekirdek EMS iş akışlarının güçlü ve tümleşik yönetimine olanak tanıyacak şekilde tam yönetici deneyimimizi Azure 'a geçiririz.

Yeni deneme kiracıları, yeni yönetici deneyiminin genel önizlemesini bu ay Azure portalında görmeye başlayacaklar. Önizleme durumundayken, mevcut Intune konsolu ile gelen yetenekler ve eşlik, yinelemeli olarak sağlanır.

Azure portalındaki yönetici deneyimi, duyurulan yeni gruplandırma ve hedefleme işlevselliğini kullanır; mevcut kiracınız yeni gruplandırma deneyimine geçirildiğinde, siz de kiracınıza yönelik yeni yönetici deneyimini önizlemek üzere geçirilirsiniz. Bu sırada, kiracınız geçirilene kadar yeni işlevleri sınamak veya bunlara göz atmak isterseniz yeni bir Intune deneme hesabına kaydolun veya [yeni belgelere](whats-new.md) bakın.

Azure’da Intune önizlemesindeki yenilikleri [buradan](whats-new.md) bulabilirsiniz.

### <a name="notices"></a>Bildirimler

#### <a name="direct-access-to-apple-enrollment-scenarios---951869--"></a>Apple kayıt senaryolarına doğrudan erişim <!--951869-->

Intune, Azure Önizleme Portalı'ndaki Cihaz Kaydetme iş yükünü kullanarak Apple kayıt senaryolarına doğrudan erişimi Ocak 2017 sonrasında oluşturulan Intune hesapları için etkinleştirdi. Daha önce, Apple kayıt önizleme sürümüne yalnızca Azure portalı bağlantıları ile erişilebiliyordu. Bu özelliklerin Azure’da kullanılabilmesi için, Ocak 2017 öncesi oluşturulan Intune hesaplarında tek seferlik bir geçiş yapılması gerekir. Geçiş için zaman çizelgesi henüz açıklanmamıştır, ancak konuya ilişkin ayrıntılar olabildiğince çabuk duyurulacaktır. Mevcut hesabınız önizleme sürümüne erişemiyorsa, yeni deneyimi test etmek için bir deneme hesabı oluşturmanızı kesinlikle öneririz.

#### <a name="whats-coming-for-appx-in-intune-in-the-azure-portal----1000270---"></a>Azure portalında Intune’da Appx için yenilikler  <!-- 1000270 -->

Azure portalında Intune’a geçişin bir parçası olarak üç appx değişikliği yapıyoruz:

1. Intune konsoluna yalnızca MDM kayıtlı cihazlara dağıtılabilen yeni bir appx uygulama türü ekliyoruz.
2. Var olan appx uygulama türünü yalnızca Intune PC aracısı ile yönetilen PC'lerin hedefleneceği şekilde değiştiriyoruz.
3. Var olan tüm appx'leri geçiş ile MDM appx'leri haline getiriyoruz.

##### <a name="how-does-this-affect-me"></a>Bu değişiklik beni nasıl etkileyecek?

Bu durum Intune PC aracısı üzerinden yönetilen mevcut cihazlarınızı etkilemeyecek. Ancak geçiş yapıldıktan sonra geçişi yapılan bu appx'leri Intune PC aracısı ile yönetilen ve daha önceden hedef alınmayan yeni cihazlara dağıtamayacaksınız.

##### <a name="what-action-do-i-need-to-take"></a>Ne yapmam gerekiyor?

Yeni PC dağıtımları gerçekleştirmek istiyorsanız geçiş işleminden sonra appx'i PC appx'i olarak yeniden yüklemeniz gerekecek. Daha fazla bilgi için Intune Destek ekibi blog sayfasındaki [Azure portalında Intune Appx’lerinde yapılan değişiklikler](https://aka.ms/appxchange) konusuna bakın.  

#### <a name="administration-roles-being-replaced-in-azure-portal"></a>Yönetim rolleri Azure portalında değiştiriliyor

Klasik Intune portalında (Silverlight) kullanılan mevcut mobil uygulama yönetimi (MAM) yönetim rolleri (Katkıda bulunan, Sahibi ve Salt okunur) yerine Intune Azure portalında yeni rol tabanlı yönetim denetimleri (RBAC) geliyor. Azure portalına geçiş yaptıktan sonra, yöneticilerinizi bu yeni yönetim rollerine yeniden atamanız gerekiyor. RBAC ve yeni roller hakkında daha fazla bilgi için bkz. [Microsoft Intune için rol tabanlı erişim denetimi](role-based-access-control.md).

### <a name="whats-coming"></a>Yakında

#### <a name="improved-sign-in-experience-across-company-portal-apps-for-all-platforms---user-story-1132123--"></a>Tüm platformlar için Şirket Portalı uygulamalarında gelişmiş oturum açma deneyimi  <!--User Story 1132123-->

Android, iOS ve Windows için Intune Şirket Portalı uygulamalarında oturum açma deneyimini geliştirecek bir değişikliği önümüzdeki birkaç ay içinde piyasaya süreceğiz. Yeni kullanıcı deneyimi, Azure AD bu değişikliği gerçekleştirdiğinde Şirket Portalına yönelik tüm platformlarda görünecektir. Ayrıca, kullanıcılar artık tek kullanımlık bir kod ile başka bir cihazdan Şirket Portalında oturum açabilir. Bu, özellikle kullanıcıların kimlik bilgileri olmadan oturum açması gerektiğinde faydalıdır.

[Uygulamanın kullanıcı arabirimindeki yenilikler](whats-new-app-ui.md) sayfasında önceki oturum açma deneyiminin, yeni kimlik bilgileriyle oturum açma deneyiminin ve yeni başka bir cihazdan yeni oturum açma deneyiminin ekran görüntülerini bulabilirsiniz.

#### <a name="plan-for-change-intune-is-changing-the-intune-partner-portal-experience----1050016---"></a>Değişiklik planı: Intune, Intune İş Ortağı Portalı deneyimini değiştiriyor  <!-- 1050016 -->

2017 Mayıs ayı ortalarındaki hizmet güncelleştirmesinden başlayarak, manage.microsoft.com’dan Intune İş Ortağı sayfasını kaldırıyoruz.  

İş ortağı yöneticisiyseniz, artık Intune İş Ortağı sayfasında müşterileriniz adına görüntüleyemeyecek ve işlem yapamayacaksınız; bunun yerine Microsoft’taki diğer iki iş ortağı portalından birinde oturum açmanız gerekecektir.

Hem [Microsoft Iş Ortağı Merkezi](https://partnercenter.microsoft.com/) hem de [Microsoft 365 Yönetim Merkezi](https://admin.microsoft.com/) , yönettiğiniz müşteri hesaplarında oturum açmanızı sağlayacak. İş ortağı olarak ilerlemek için, lütfen müşterilerinizi bu sitelerimizden birini kullanarak yönetin.


#### <a name="apple-to-require-updates-for-application-transport-security---748318--"></a>Apple, Uygulama Taşıma Güvenliği için güncelleştirmeler gerektirecek  <!--748318-->

Apple, Uygulama Taşıma Güvenliği (ATS) için belirli gereksinimler uygulayacağını açıkladı. ATS, HTTPS üzerinden yapılan tüm uygulama iletişimlerinde daha sıkı güvenlik uygulamak için kullanılır. Bu değişiklik, iOS Şirket Portalı uygulamaları kullanan Intune müşterilerini etkiler.

Yeni ATS gereksinimlerinin kullanılmasını zorunlu kılan Apple TestFlight programı aracılığıyla iOS için Şirket Portalı uygulamasının yeni bir sürümünü kullanıma sunduk. Bunu denemek istiyorsanız, ATS uyumluluğunu, adınızı, soyadını, e-posta adresinizi ve <a href="mailto:CompanyPortalBeta@microsoft.com?subject=Register to TestFlight ATS Company Portal app">CompanyPortalBeta@microsoft.com</a> şirket adınızla e-postanızı test edebilirsiniz. Daha fazla ayrıntı için bkz. [Intune destek blogu](https://aka.ms/compportalats).

## <a name="march-2017"></a>Mart 2017

### <a name="new-capabilities"></a>Yeni Özellikler

#### <a name="support-for-skycure"></a>Skycure desteği

Artık, Microsoft Intune ile tümleşen bir mobil tehdit savunması çözümü olan ufuk tarafından gerçekleştirilen risk değerlendirmesine dayalı koşullu erişimi kullanarak mobil cihaz erişimini kontrol edebilirsiniz. Risk, Skycure çalıştıran cihazlardan toplanan ve aşağıdakileri içeren telemetriye göre değerlendirilir:

- Fiziksel savunma
- Ağ savunması
- Uygulama savunması
- Güvenlik açıkları savunması

Intune cihaz uyumluluk ilkeleri aracılığıyla etkinleştirilen Symantec Endpoint Protection Mobile (ufuk) risk değerlendirmesi temelinde EMS koşullu erişim ilkelerini yapılandırabilirsiniz. Algılanan tehditler temelinde, uyumsuz cihazların şirket kaynaklarına erişimine izin vermek ya da erişimi engellemek için bu ilkeleri kullanabilirsiniz. Daha fazla bilgi için bkz. [Symantec Endpoint Protection Mobile Bağlayıcısı](../protect/skycure-mobile-threat-defense-connector.md).

#### <a name="new-user-experience-for-the-company-portal-app-for-android---621622--"></a>Android Şirket Portalı uygulaması için yeni kullanıcı deneyimi  <!--621622-->

Android için Şirket Portalı uygulamasının kullanıcı arabirimi daha modern görünüm ve daha iyi kullanıcı deneyimi için güncelleştiriliyor. Önemli güncelleştirmeler şunlardır:

- Renkler: Şirket Portalı sekmesinin üstbilgileri BT tarafından tanımlanan marka rengindedir.
- Uygulamalar: **Uygulamalar** sekmesindeki **Öne Çıkan Uygulamalar** ve **Tüm Uygulamalar** düğmeleri güncelleştirildi.
- Arama: **Uygulamalar** sekmesinde, **Arama** düğmesi kayan eylem düğmesi şeklinde.
- Uygulamalarda Gezinme: **Tüm Uygulamalar** görünümü daha kolay gezinme için **Öne Çıkan Uygulamalar**, **Tüm Uygulamalar** ve **Kategoriler** bölümlerini sekmeler halinde gösterir.
- Destek: **Cihazlarım** ve **BT İletişim** sekmeleri okunabilirliği artırmak için güncelleştirildi.

Bu değişiklikler hakkında daha ayrıntılı bilgi için bkz. [Intune son kullanıcı uygulamaları için kullanıcı arabirimi güncelleştirmeleri](whats-new-app-ui.md).

#### <a name="non-managed-devices-can-access-assigned-apps---664691--"></a>Yönetilmeyen cihazlar atanmış uygulamalara erişebilir <!--664691-->

Şirket Portalı web sitesinde yapılan tasarım değişikliklerinin bir parçası olarak iOS ve Android kullanıcılar yönetilmeyen cihazlarında kendilerine "kayıtsız kullanılabilir" olarak atanmış uygulamaları yükleyebilecek. Kullanıcılar Intune kimlik bilgilerini kullanarak Şirket Portalı web sitesine girebilecek ve kendilerine atanan uygulamaların listesini görebilecek. "Kayıtsız kullanılabilir" uygulamaların uygulama paketleri Şirket Portalı web sitesinden indirilebilir. Yükleme için kayıt gerektiren uygulamalar bu değişikten etkilenmeyecek ve bu uygulamaları yüklemek isteyen kullanıcılardan cihazlarını kaydetmeleri istenecektir.

#### <a name="signing-script-for-windows-10-company-portal---941642--"></a>Windows 10 Şirket Portalı için İmzalama Betiği  <!--941642-->

Windows 10 Şirket Portalı uygulamasını indirmeniz ve dışarıdan yüklemeniz gerekiyorsa, artık bir betik kullanarak uygulama imzalama işlemini kuruluşunuz için basitleştirebilir ve kolaylaştırabilirsiniz.   Betiği ve kullanma yönergelerini indirmek için bkz. TechNet galerisinde [Windows 10 için Microsoft Intune Imzalama betiği Şirket portalı](https://aka.ms/win10cpscript) . Bu duyuru hakkında daha ayrıntılı bilgi edinmek için Intune Destek Ekibi Blogundaki [Windows 10 Şirket Portalı uygulamanızı güncelleştirme](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) yazısına bakın.


### <a name="notices"></a>Bildirimler

#### <a name="support-for-ios-103"></a>iOS 10.3 desteği

iOS 10.3 sürümü 27 Mart 2017 tarihinden itibaren iOS kullanıcılarına sunulmaya başlandı. Tüm mevcut Intune MDM ve MAM senaryoları Apple 'ın işletim sisteminin en son sürümüyle uyumludur. Kullanıcılarınız cihazlarını ve uygulamalarını iOS 10.3 sürümüne yükselttiklerinde, şu anda iOS cihazlarını yönetmeye dair mevcut tüm Intune özelliklerinin sorunsuz bir şekilde çalışmaya devam etmesini bekliyoruz.

Şu anda bilinen bir sorun yoktur. iOS 10.3 ile ilgili soruna karşılaşırsanız lütfen [Intune destek ekibine](get-support.md) ulaşın.

#### <a name="improved-support-for-android-users-based-in-china---720444--"></a>Çin'de bulunan Android kullanıcıları için gelişmiş destek  <!--720444-->

Çin’de Google Play Mağazası olmaması nedeniyle, Android cihazlarının uygulamaları Çin’deki uygulama mağazalarından edinmeleri gerekir. Şirket Portalı, Çin’deki Android kullanıcılarını Şirket Portalı ve Outlook uygulamalarını yerel mağazalardan yüklemeleri için yeniden yönlendirerek bu iş akışını destekler. Bu, Koşullu Erişim ilkeleri, mobil aygıt yönetimi ve mobil uygulama yönetimi için etkinleştirildiğinde, kullanıcı deneyimini geliştirir. Android için Şirket Portalı ve Outlook uygulamaları aşağıdaki Çin uygulama mağazalarında bulunabilir:

- [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
- [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
- [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
- [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

#### <a name="best-practice-make-sure-your-company-portal-apps-are-up-to-date---879465--"></a>En iyi uygulama: Şirket Portalı uygulamalarınızın güncel olduğundan emin olun  <!--879465-->

Aralık 2016’da, iOS, Android, Windows 8.1+ veya Windows Phone 8.1+ cihazı kaydeden bir grup kullanıcı için çok faktörlü kimlik doğrulamasının (MFA) zorlanmasını sağlayan bir güncelleştirme yayımladık. Bu özellik, Android (v5.0.3419.0+) ve iOS (v2.1.17+) için Şirket Portalı uygulamasının belirli temel sürümleri olmadan çalışamaz.

Microsoft, Intune’u sürekli olarak geliştirmek amacıyla hem konsola hem de Şirket Portalı uygulamasına tüm desteklenen platformlarda yeni işlevler ekliyor. Bunun sonucunda, Microsoft yalnızca Şirket Portalı uygulamasının geçerli sürümünde karşılaşılan sorunlara yönelik düzeltmeler yayımlamaktadır. Bu nedenle, en iyi kullanıcı deneyiminden yararlanabilmeniz için Şirket Portalı uygulamalarının en son sürümlerini kullanmanızı öneririz.

>[!Tip]
> Kullanıcılarınızın, cihazlarında uygulamaları ilgili uygulama mağazasından otomatik olarak güncelleştirecek şekilde ayarlamalar yapmasını sağlayın. Android Şirket Portalı uygulamasını bir ağ paylaşımında kullanıma sunduysanız en son sürümü [Microsoft İndirme Merkezi](https://www.microsoft.com/download/details.aspx?id=49140)’nden indirebilirsiniz.

#### <a name="microsoft-teams-is-now-enabled-for-mam-on-ios-and-android"></a>Microsoft Teams artık iOS ve Android’de MAM özelliğini kullanabiliyor

Microsoft, Microsoft Teams’in genel kullanıma sunulduğunu açıkladı. iOS ve Android için güncelleştirilmiş Microsoft Teams uygulamaları artık Intune mobil uygulama yönetimi (MAM) özelliklerine sahip olduğundan ekiplerinizin tüm cihazlarda rahatça çalışmasına olanak tanıyıp bir yandan da görüşmeleri ve kurumsal verileri her aşamada koruyabilirsiniz. Daha ayrıntılı bilgi edinmek için Enterprise Mobility and Security blogundaki [Microsoft Teams duyurusuna](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) bakın.


## <a name="february-2017"></a>Şubat 2017

### <a name="new-capabilities"></a>Yeni Özellikler

### <a name="modernizing-the-company-portal-website---753980--"></a>Şirket Portalı web sitesi modernleştiriliyor  <!--753980-->
Şirket Portalı web sitesi, yönetilen cihazlara sahip olmayan kullanıcıları hedefleyen uygulamaları destekleyecek. Karşıt renklerden oluşan yeni renk düzeni ve dinamik çizimlerle yeniden tasarlanan web sitesi, yardım masası ilgili kişisine ilişkin ayrıntıların yanı sıra yönetilen mevcut cihazlara yönelik bilgilerin bulunduğu bir "hamburger menüsü" ![Şirket Portalı web sitesinin sol üst köşesine eklenmiş olan hamburger menüsünün küçük resmi](./media/whats-new-archive-classic/CP_hamburger_menu.png).

### <a name="notices"></a>Bildirimler

#### <a name="group-migration-will-not-require-any-updates-to-groups-or-policies-for-ios-devices---898837--"></a>Grup geçişi için iOS cihazlarda grup veya ilke güncelleştirmesi gerekmeyecek  <!--898837-->
Bir kurumsal cihaz kayıt profili tarafından önceden atanan her Intune cihaz grubu için, Azure Active Directory cihaz gruplarına geçiş sırasında kurumsal cihaz kayıt profili adına göre AAD 'de karşılık gelen bir dinamik cihaz grubu oluşturulur. Bu sayede kaydı yapılan cihazların otomatik olarak gruplanması ve özgün Intune grubundakilerle aynı ilkeleri ve uygulamaları alması sağlanacaktır.

Bir kiracı gruplama ve hedefleme için geçiş işlemine girdiğinde Intune, otomatik olarak Şirket Cihaz Kaydı profili tarafından hedeflenen Intune grubuna karşılık gelecek bir dinamik AAD grubu oluşturacaktır. Intune Yöneticisinin hedef Intune grubunu silmesi halinde karşılık gelen dinamik AAD grubu silinmeyecektir. Grubun üyeleri ve dinamik sorgu silinecek ancak BT Yöneticisi AAD portalı üzerinden kaldırılana kadar grubun kendisi kalacaktır.

Benzer şekilde, BT Yöneticisinin bir Şirket Cihaz Kaydı profili ile hedeflenen Intune grubunu değiştirmesi halinde, Intune yeni profil atamasını yansıtan yeni bir dinamik grup oluşturacak ancak eski atama için oluşturulan dinamik grubu kaldırmayacaktır.

### <a name="defaulting-to-managing-windows-desktop-devices-through-windows-settings---663050--"></a>Windows masaüstü cihazları Windows ayarları aracılığıyla yönetmek varsayılanlara sıfırlıyor  <!--663050-->
Windows 10 masaüstü cihazları kaydetmek için varsayılan davranış değişiyor. Yeni kayıtlar artık bilgisayar aracısı üzerinden değil, tipik MDM aracısı kayıt akışını izleyerek yapılacaktır. Şirket Portalı web sitesi, Windows 10 masaüstü kullanıcılarına Windows 10 masaüstü bilgisayarları mobil cihaz olarak ekleme işlemi için yönergeler sağlayacak kayıt yönergeleri temin edecektir. Bu, zaten kayıtlı olan bilgisayarları etkilemez ve [tercihe göre](manage-windows-pcs-with-microsoft-intune.md) kuruluşunuz bilgisayar aracısını kullanarak Windows 10 masaüstü cihazları yönetmeye devam edebilir.

#### <a name="improving-mobile-app-management-support-for-selective-wipe---581242--"></a>Seçici silme için mobil uygulama yönetimi desteğini iyileştirme  <!--581242-->
Bu verilerin "Uygulama verileri silinmeden önce çevrimdışı zaman aralığı" ilkesi nedeniyle otomatik olarak kaldırılması durumunda, son kullanıcılara iş veya okul verilerine yeniden erişim sağlama konusunda ek yönergeler verilir.<!--, or the removal of the Intune Company Portal on Android.-->

#### <a name="company-portal-for-ios-links-open-inside-the-app---665954--"></a>iOS için Şirket Portalı bağlantıları uygulamanın içinde açılır  <!--665954-->
Belge ve uygulamalara yönlendirilen bağlantılar da dahil olmak üzere iOS için Şirket Portalı uygulaması içinde bulunan bağlantılar, Safari’nin uygulama içi görünümü kullanılarak doğrudan Şirket Portalı uygulamasında açılır. Bu güncelleştirme Ocak’taki hizmet güncelleştirmesinden ayrı olarak sevk edilir.

#### <a name="new-mdm-server-address-for-windows-devices---893007--"></a>Windows cihazları için yeni MDM sunucusu adresi  <!--893007-->
MDM sunucusu adresi olarak __manage.microsoft.com__ giren (sorulursa) Windows ve Windows Phone kullanıcıları, cihaz kaydetmeye çalıştıklarında başarısız olacaklardır. MDM sunucusu adresi __manage.microsoft.com__ yerine __enrollment.manage.microsoft.com__ olarak değiştirilmektedir. Kullanıcılarınızı, Windows veya Windows Phone cihazı kaydetmeye çalışırken sorulması halinde MDM sunucusu adresi olarak __enrollment.manage.microsoft.com__ girmeleri konusunda bilgilendirin. CNAME kurulumunuzda herhangi bir değişiklik gerekmez. Bu değişiklik hakkında daha fazla bilgi için [aka.ms/intuneenrollsvrchange](https://aka.ms/intuneenrollsvrchange) adresini ziyaret edin.

#### <a name="new-user-experience-for-the-company-portal-app-for-android---621622--"></a>Android Şirket Portalı uygulaması için yeni kullanıcı deneyimi  <!--621622-->
Mart ayından itibaren Android Şirket Portalı uygulaması [Material Design kılavuzuna](https://material.io/guidelines/material-design/introduction.html) uygun olarak modern bir tasarıma sahip olacak. Bu gelişmiş kullanıcı deneyimi şunları içeriyor olacak:

* __Renkler__: Sekme başlıklarının renkleri özel renk paletinize göre değiştirilebilir.
* __Arabirim__: uygulamalar sekmesindeki öne çıkan uygulamalar ve tüm uygulamalar düğmeleri güncelleştirilmiştir. Arama düğmesi artık kayan bir eylem düğmesidir.
* __Gezinti__: tüm uygulamalar, daha kolay gezinme Için öne çıkan, hepsi ve kategorilerin sekmeli bir görünümünü gösterir.
* __Hizmet__: Cihazlarım ve BT'ye Başvur sekmelerinin okunabilirliği geliştirildi.

Önce ve sonra görüntülerini [UI güncelleştirmeleri sayfasında](whats-new-app-ui.md) bulabilirsiniz.

### <a name="associate-multiple-management-tools-with-the-microsoft-store-for-business---926135--"></a>İş İçin Microsoft Mağazası’yla birden çok yönetim aracını ilişkilendirme <!--926135-->
İş İçin Microsoft Mağazası uygulamalarını dağıtmak için birden fazla yönetim aracı kullanmanız durumunda önceden bunların yalnızca birini İş İçin Microsoft Mağazası ile ilişkilendirebiliyordunuz. Artık mağaza ile Intune ve Configuration Manager gibi birden fazla yönetim aracını ilişkilendirebilirsiniz. Ayrıntılar için bkz. [Microsoft Intune ile İş İçin Microsoft Mağazası'ndan satın aldığınız uygulamaları yönetme](../apps/windows-store-for-business.md).

## <a name="whats-new-in-the-public-preview-of-intune-in-the-azure-portal---736542--"></a>Azure portalında Intune’un genel önizlemesindeki yenilikler  <!--736542-->

Erken takvim yılında 2017, grafik API 'Leri kullanılarak genişletilebilen modern bir hizmet platformunda çekirdek EMS iş akışlarının güçlü ve tümleşik yönetimine olanak tanıyacak şekilde tam yönetici deneyimimizi Azure 'a geçiririz.

Yeni deneme kiracıları, yeni yönetici deneyiminin genel önizlemesini bu ay Azure portalında görmeye başlayacaklar. Önizleme durumundayken, mevcut Intune konsolu ile gelen yetenekler ve eşlik, yinelemeli olarak sağlanır.

Azure portalındaki yönetici deneyimi, duyurulan yeni gruplandırma ve hedefleme işlevselliğini kullanır; mevcut kiracınız yeni gruplandırma deneyimine geçirildiğinde, siz de kiracınıza yönelik yeni yönetici deneyimini önizlemek üzere geçirilirsiniz. Bu sırada, kiracınız geçirilene kadar yeni işlevleri sınamak veya bunlara göz atmak isterseniz yeni bir Intune deneme hesabına kaydolun veya [yeni belgelere](whats-new.md) bakın.

Azure’da Intune önizlemesindeki yenilikleri [buradan](whats-new.md) bulabilirsiniz.

## <a name="january-2017"></a>Ocak 2017

### <a name="new-capabilities"></a>Yeni Özellikler

#### <a name="in-console-reports-for-mam-without-enrollment---677961--"></a>Kayıtsız MAM için konsol içi raporlar  <!--677961-->
Hem kayıtlı hem kayıtlı olmayan cihazlar için yeni uygulama koruma raporları eklenmiştir. [Intune ile mobil uygulama yönetimi ilkelerini nasıl izleyebileceğinizi](../apps/app-protection-policies-monitor.md)öğrenmek için daha fazla bilgi edinin.

#### <a name="android-711-support---694397--"></a>Android 7.1.1 desteği  <!--694397-->
Intune artık Android 7.1.1 sürümünü tam olarak destekler ve yönetir.

#### <a name="resolve-issue-where-ios-devices-are-inactive-or-the-admin-console-cannot-communicate-with-them---unknown--"></a>iOS cihazlarının etkin olmaması veya yönetim konsolunun cihazlarla iletişim kuramaması sorununu çözme <!--unknown-->
Kullanıcıların cihazları Intune ile ilgili kişiyi kaybederse, bunlara şirket kaynaklarına yeniden erişim kazanmalarına yardımcı olmak için yeni sorun giderme adımları verebilirsiniz. Bkz. [Cihazlar etkin değil veya yönetim konsolu cihazlarla iletişim kuramıyor](../enrollment/troubleshoot-device-enrollment-in-intune.md#devices-are-inactive-or-the-admin-console-cant-communicate-with-them).

### <a name="notices"></a>Bildirimler

#### <a name="defaulting-to-managing-windows-desktop-devices-through-windows-settings---663050--"></a>Windows masaüstü cihazları Windows ayarları aracılığıyla yönetmek varsayılanlara sıfırlıyor  <!--663050-->
Windows 10 masaüstü cihazları kaydetmek için varsayılan davranış değişiyor. Yeni kayıtlar artık bilgisayar aracısı üzerinden değil, tipik MDM aracısı kayıt akışını izleyerek yapılacaktır.

Şirket Portalı web sitesi, Windows 10 masaüstü kullanıcılarına Windows 10 masaüstü bilgisayarları mobil cihaz olarak ekleme işlemi için yönergeler sağlayacak kayıt yönergeleri temin edecektir. Bu, zaten kayıtlı olan bilgisayarları etkilemez ve [tercihe göre](manage-windows-pcs-with-microsoft-intune.md) kuruluşunuz bilgisayar aracısını kullanarak Windows 10 masaüstü cihazları yönetmeye devam edebilir.

#### <a name="improving-mobile-app-management-support-for-selective-wipe---581242--"></a>Seçici silme için mobil uygulama yönetimi desteğini iyileştirme  <!--581242-->
Bu verilerin "Uygulama verileri silinmeden önce çevrimdışı zaman aralığı" ilkesi nedeniyle otomatik olarak kaldırılması durumunda, son kullanıcılara iş veya okul verilerine yeniden erişim sağlama konusunda ek yönergeler verilir.<!--, or the removal of the Intune Company Portal on Android.-->

#### <a name="company-portal-for-ios-links-open-inside-the-app---665954--"></a>iOS için Şirket Portalı bağlantıları uygulamanın içinde açılır  <!--665954-->
Belge ve uygulamalara yönlendirilen bağlantılar da dahil olmak üzere iOS için Şirket Portalı uygulaması içinde bulunan bağlantılar, Safari’nin uygulama içi görünümü kullanılarak doğrudan Şirket Portalı uygulamasında açılır. Bu güncelleştirme Ocak’taki hizmet güncelleştirmesinden ayrı olarak sevk edilir.

#### <a name="modernizing-the-company-portal-website---753980--"></a>Şirket Portalı web sitesi modernleştiriliyor  <!--753980-->
Şubat ayından itibaren Şirket Portalı web sitesi, yönetilen cihazlara sahip olmayan kullanıcıları hedefleyen uygulamaları destekleyecek. Karşıt renklerden oluşan yeni renk düzeni ve dinamik çizimlerle yeniden tasarlanan web sitesi, yardım masası ilgili kişisine ilişkin ayrıntıların yanı sıra yönetilen mevcut cihazlara yönelik bilgilerin bulunduğu bir "hamburger menüsü" ![Şirket Portalı web sitesi hamburger menüsü](./media/whats-new-archive-classic/CP_hamburger_menu.png).

#### <a name="new-documentation-for-app-protection-policies---583398--"></a>Uygulama koruma ilkeleri için yeni belgeler  <!--583398-->
Intune Uygulama Sarmalama Aracı veya Intune Uygulama SDK’sı kullanarak iOS ve Android uygulamalarında uygulama koruma ilkelerini (MAM ilkeleri olarak da bilinir) etkinleştirmek isteyen yöneticiler ve uygulama geliştiricilerine yönelik belgelerimizi güncelleştirdik.

Aşağıdaki makaleler güncelleştirilmiştir:

* [Microsoft Intune ile uygulamaların mobil uygulama yönetimine nasıl hazırlanacağına karar verme](../developer/apps-prepare-mobile-application-management.md)
* [Intune Uygulama Sarmalama Aracı’nı kullanarak iOS uygulamalarını mobil uygulama yönetimine hazırlama](../developer/app-wrapper-prepare-ios.md)
* [Microsoft Intune Uygulama SDK’sını kullanmaya başlama](../developer/app-sdk-get-started.md)
* [İOS için Intune uygulama SDK 'Sı Geliştirici Kılavuzu](../developer/app-sdk-ios.md)

Aşağıdaki makaleler belgeler kitaplığına yeni eklenmiştir:

* [Intune uygulama SDK 'Sı Cordova eklentisi](../developer/app-sdk.md)
* [Intune uygulama SDK 'Sı Xamarin bileşeni](../developer/app-sdk-xamarin.md)

#### <a name="progress-bar-when-launching-the-company-portal-on-ios---665978--"></a>iOS’ta Şirket Portalını başlatılırken ilerleme çubuğu  <!--665978-->
iOS için Şirket Portalı, kullanıcıya gerçekleşen yükleme işlemleri hakkında bilgi sağlamak için başlatma ekranında bir ilerleme çubuğu yeniliği sunuyor. Değer değiştiricinin yerini alması için ilerleme çubuğunun aşamalı dağıtımı yapılacaktır. Yani bazı kullanıcılarınız yeni ilerleme çubuğunu görecek, diğerleri ise değer değiştiriciyi görmeye devam edecektir.

## <a name="december-2016"></a>Aralık 2016

### <a name="public-preview-of-intune-in-the-azure-portal--736542--"></a>Azure portalında Intune’un genel önizlemesi <!--736542-->
Erken takvim yılı 2017 ' de, tam yönetici deneyimimizi Azure 'a geçiririz. böylece grafik API 'Leri kullanılarak Genişletilebilir olan modern bir hizmet platformunda çekirdek EMS iş akışlarının güçlü ve tümleşik yönetimi sağlanır. Tüm Intune kiracıları için bu portalın genel kullanılabilirliğinin yanı sıra, kiracı seçmek için bu yeni yönetici deneyiminin önizlemesini bu ay içinde kullanıma sunmaya başlayacağımızı duyurmak isteriz.

Azure portalındaki yönetici deneyimi, duyurulan yeni gruplandırma ve hedefleme işlevselliğini kullanır; mevcut kiracınız yeni gruplandırma deneyimine geçirildiğinde, siz de kiracınıza yönelik yeni yönetici deneyimini önizlemek üzere geçirilirsiniz. Bu sırada, Azure portalında Microsoft Intune hakkında bilgilere [yeni belgelerimizden](what-is-intune.md) ulaşabilirsiniz.

__Azure portal genel önizlemede Telekom gider yönetimi tümleştirmesi__ <!--747605-->
Artık Azure portalında üçüncü taraf telekom gider yönetimi (TEM) hizmetleri ile tümleştirme önizlemesine başlıyoruz. Yurt içi verilerin ve dolaşım verilerinin kullanımına yönelik sınırlamalarını zorunlu olarak uygulamak için Intune'u kullanabilirsiniz. Bu tümleştirmelere [Saaswedo](http://www.saaswedo.com/) ile başlıyoruz. Deneme kiracınızda bu özelliği etkinleştirmek için lütfen [Microsoft desteğe başvurun](get-support.md).

### <a name="new-capabilities"></a>Yeni Özellikler

__Tüm platformlar genelinde çok faktörlü kimlik doğrulaması__ <!--747590-->
Belirli bir kullanıcı grubu Azure Active Directory’de Microsoft Intune Kaydı uygulamasında MFA’yı yapılandırarak Azure Yönetim Portalı’ndan bir iOS, Android, Windows 8.1+ veya Windows Phone 8.1+ cihazını kaydettiklerinde, bu kullanıcılara çok faktörlü kimlik doğrulaması (MFA) kullanma zorunluluğu getirebilirsiniz.

__Mobil cihaz kaydını kısıtlama özelliği__ <!--747596-->
Intune, katılmasına izin verilecek mobil cihaz platformlarını denetleyen yeni kayıt kısıtlamaları ekliyor. Intune, mobil cihaz platformlarını iOS, macOS, Android, Windows ve Windows Mobile şeklinde ayırıyor.
* Mobil cihaz kaydının kısıtlanması, bilgisayar istemcisi kaydını etkilemez.
* Yalnızca iOS için kişisel cihazların kaydedilmesini engelleyen ek seçenek vardır.

Intune, BT yöneticileri [bu makalede](../enrollment/device-enrollment.md) anlatılan şekilde kuruluş cihazı olarak işaretlemediği sürece tüm yeni cihazları kişisel cihaz olarak işaretler.

### <a name="notices"></a>Bildirimler

__Kayıt sırasında Multi-Factor Authentication Azure portal taşıma__ <!--VSO 750545-->
Daha önce yöneticiler Intune kaydı sırasında MFA ayarlamak için Intune konsoluna veya Configuration Manager (Ekim 2016'dan önceki sürümler) konsoluna gitmek durumundaydı. Bu güncelleştirilmiş özellik sayesinde, artık [Microsoft Azure portalında](https://manage.windowsazure.com) Intune kimlik bilgilerinizi kullanarak oturum açar ve MFA ayarlarını Azure AD ile yapılandırırsınız. Bunun hakkında daha fazla bilgi için [burayı](/azure/active-directory/authentication/howto-mfa-mfasettings) okuyun.

__Android için Şirket Portalı uygulaması artık Çin 'de kullanıma sunuldu__ <!--VSO 658093-->
Android için Şirket Portalı uygulamasını karşıdan yüklenebilir olarak Çin’de yayımlıyoruz.Çin’de Google Play Mağazası olmaması nedeniyle, Android cihazlarının uygulamaları Çin’deki uygulama mağazalarından edinmeleri gerekir. Android için Şirket Portalı uygulaması aşağıdaki mağazalardan yüklenebilir:
* [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
* [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
* [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
* [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

Android için Şirket Portalı uygulaması Microsoft Intune hizmetiyle iletişim kurmak için Google Play Hizmetleri’ni kullanır. Google Play Hizmetleri henüz Çin'de kullanılamadığından, aşağıdaki görevlerin tamamlanması 8 saate kadar sürebilir.

|Intune Yönetici Konsolu| Android için Intune Şirket Portalı uygulaması |Intune Şirket Portalı Web Sitesi|
|---|---|---|
|Tam temizleme| Uzak bir cihazı kaldırma| Cihaz kaldırma (yerel ve uzak)|
|Seçmeli temizleme| Cihaz sıfırlama| Cihaz sıfırlama|
|Yeni veya güncelleştirilmiş uygulamaların dağıtımı| Kullanılabilir iş kolu uygulamalarını yükleme| Cihaz geçiş kodu sıfırlama|
|Uzaktan kilitleme|||
|Geçiş kodu sıfırlama|||

### <a name="deprecations"></a>Kullanım dışı bırakılanlar

__Firefox artık Silverlight 'ı desteklemiyor__ <!--VSO TBA-->
Mozilla Mart 2017’den itibaren [Firefox tarayıcısı](https://www.mozilla.org/firefox) sürüm 52’de Silverlight desteğini kaldırıyor. Sonuç olarak, 51 üzeri Firefox sürümleri kullanarak mevcut Intune konsolunda oturum açmanız artık mümkün olmayacaktır. Yönetici konsoluna erişmek için Internet Explorer 10 veya 11 ya da [Sürüm 52'den önceki bir Firefox sürümü](https://ftp.mozilla.org/pub/firefox/releases/) kullanmanızı öneririz. Intune'un Azure portalına geçişi, Silverlight bağımlılığı olmadan bir dizi [modern tarayıcı](/azure/azure-preview-portal-supported-browsers-devices) desteğine olanak sağlayacaktır.

__Exchange Online mobil gelen kutusu ilkelerini kaldırma__ <!--770687-->
Aralık’tan itibaren yöneticilerin artık Intune konsolu içinde Exchange Online (EAS) mobil gelen kutusu ilkelerini görüntülemesi veya yapılandırması mümkün olmayacaktır. Bu değişiklik, Aralık ve Ocak boyunca tüm Intune kiracılarına gönderilecektir. Tüm mevcut ilkeler yapılandırıldığı gibi kalır; yeni ilkeler yapılandırmak için Exchange Yönetim Kabuğu'nu kullanın. Daha fazla bilgi için [buraya](https://technet.microsoft.com/library/bb123783%28v=exchg.150%29.aspx) göz atın.

__Intune AV oynatıcı, resim görüntüleyici ve PDF görüntüleyici uygulamaları artık Android 'de desteklenmiyor__ <!--747553-->
2016 Aralık ortasından itibaren, kullanıcılar Intune AV Oynatıcı, Resim Görüntüleyici ve PDF Görüntüleyici uygulamalarını kullanamayacaktır. Bu uygulamaların yerini Azure Information Protection uygulaması almıştır. Azure Information Protection hakkında daha fazla bilgiyi [burada](/information-protection/rms-client/mobile-app-faq) bulabilirsiniz.

## <a name="november-2016"></a>Kasım 2016

### <a name="new-capabilities"></a>Yeni özellikler

__Windows 10 cihazları için Yeni Microsoft Intune Şirket Portalı__ Microsoft, [Windows 10 cihazları için yeni bir Microsoft Intune Şirket Portalı uygulaması](https://www.microsoft.com/store/apps/9wzdncrfj3pz) piyasaya sürdü. Yeni Windows 10 Evrensel biçiminden yararlanan bu uygulama, kullanıcıya uygulama içinden güncelleştirilmiş bir kullanıcı deneyimi ve kullanıcının bugün kullanmakta olduğu işlevselliğin tümünü olanaklı kılmaya devam ederken, ister bilgisayar ister Mobil tüm Windows 10 cihazlarında aynı deneyimi sunacak.

Yeni uygulama, kullanıcının Windows 10 cihazlarında çoklu oturum açma (SSO) ve sertifika tabanlı kimlik doğrulama gibi ek platform özelliklerinden yararlanmasını da sağlar. Uygulama, mevcut Windows 8.1 Şirket Portalı ve Windows Phone 8.1 Şirket Portalı için güncelleştirme olarak Microsoft Mağazası'ndan yüklenir. Daha fazla ayrıntı için bkz. [aka.ms/intunecp_universalapp](https://aka.ms/intunecp_universalapp).

> [!IMPORTANT]
> __Intune ve Android for Work hakkında bir Güncelleştirme__ Android for Work uygulamalarını __Gerekli__ eylemiyle dağıtabilirsiniz ancak uygulamaları __Kullanılabilir__ olarak dağıtmak için Intune gruplarınızın yeni Azure AD grupları deneyimine geçirilmiş olması gerekir.

__Cordova Için Intune uygulama SDK 'sı eklentisi artık kayıt olmadan mam destekliyor__ Uygulama geliştiricileri artık Cordova için Intune uygulama SDK 'Sı eklentisini kullanarak, Android ve iOS/ıpados için Cordova tabanlı uygulamalarında cihaz kaydı olmadan MAM işlevselliğini etkinleştirebilir.

__Intune uygulama SDK 'Sı Xamarin bileşeni artık kayıt olmadan mam destekliyor__ Uygulama geliştiricileri artık Android ve iOS/ıpados için Xamarin tabanlı uygulamalarında cihaz kaydı olmadan MAM işlevselliğini etkinleştirmek için Intune uygulama SDK 'Sı Xamarin bileşenini kullanabilir. Xamarin için Intune Uygulama SDK'sı bileşenine [buradan](https://www.npmjs.com/package/cordova-plugin-ms-intune-mam) ulaşabilirsiniz.

### <a name="notices"></a>Bildirimler

__Symantec imzalama sertifikası artık yükleme için imzalanmış Windows Phone 8 Şirket Portalı gerektirmiyor__ Symantec imzalama sertifikasını yüklemek için artık imzalı Windows Phone 8 Şirket Portalı uygulaması kullanılması gerekmiyor. Sertifika tek başına yüklenebilir.

### <a name="deprecations"></a>Kullanım dışı bırakılanlar

__Windows Phone 8 Şirket Portalı Desteği__ Windows Phone 8 Şirket Portalı desteği artık kullanım dışı bırakılacak. Windows Phone 8 ve WinRT platformları için sunulan destek de Ekim 2016'da kullanım dışı bırakıldı. Windows Phone 8 Şirket Portalı için sunulan destek de Ekim 2016'da kullanım dışı bırakıldı.


## <a name="see-also"></a>Ayrıca bkz.
Son geliştirmelerin ayrıntıları için [Microsoft Intune](whats-new.md) yenilikleri inceleyin.
