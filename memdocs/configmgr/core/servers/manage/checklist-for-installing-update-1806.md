---
title: 1806 için denetim listesi
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1806 ' e güncelleştirmeden önce gerçekleştirilecek eylemler hakkında bilgi edinin.
ms.date: 08/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb0a87a6-fd65-440b-90a5-2fef35622c9d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f5323360e8c64e1ea0e1c2eb7152d16d2525f85e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723239"
---
# <a name="checklist-for-installing-update-1806-for-configuration-manager"></a>Configuration Manager için güncelleştirme 1806 yükleme denetim listesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli Configuration Manager dalını kullandığınızda, hiyerarşinizi önceki bir sürümden güncelleştirmek için sürüm 1806 ' e yönelik konsol içi güncelleştirmeyi yükleyebilirsiniz. <!-- baseline only statement: (Because version 1802 is also available as [baseline media](updates.md#a-namebkmkbaselinesa-baseline-and-update-versions), you can use the installation media to install the first site of a new hierarchy.)-->

Sürüm 1806 ' e yönelik güncelleştirmeyi almak için, hiyerarşinizin en üst düzey sitesinde bir hizmet bağlantı noktası kullanmanız gerekir. Bu site sistemi rolü çevrimiçi veya çevrimdışı modda olabilir. Hiyerarşiniz güncelleştirme paketini Microsoft 'tan indirdikten sonra, konsolunda bulun. **Yönetim** çalışma alanında, **güncelleştirmeler ve bakım** düğümünü seçin.

-   Güncelleştirme **kullanılabilir**olarak listelendiğinde güncelleştirme yüklenmeye hazırdır. Sürüm 1806 ' ü yüklemeden önce [güncelleştirme 1806](#about-installing-update-1806) ' yi yükleme ve güncelleştirme işlemine başlamadan önce yapılacak yapılandırmaların [Denetim listesi](#checklist) hakkında aşağıdaki bilgileri gözden geçirin.

-   Güncelleştirme, **indirme** ve değiştirme olarak görüntüleniyorsa, hatalar için **HMAN. log** ve **DMPDownloader. log** ' u gözden geçirin.

    -   DMPDownloader. log, DMPDownloader işleminin güncelleştirmeleri denetlemeden önce bir Aralık beklediğini işaret ediyor olabilir. Güncelleştirmenin yeniden dağıtım dosyalarını indirmeyi yeniden başlatmak için, site sunucusunda **SMS_Executive** hizmetini yeniden başlatın.

    -   Proxy sunucu ayarları, ve ' `silverlight.dlservice.microsoft.com` `download.microsoft.com`den indirmelere engel olduğunda başka bir yaygın yükleme sorunu oluşur.

Güncelleştirmeleri yükleme hakkında daha fazla bilgi için bkz. [konsol içi güncelleştirmeler ve bakım](updates.md#bkmk_inconsole).

Güncel dal sürümleri hakkında daha fazla bilgi için bkz. [temel ve güncelleştirme sürümleri](updates.md#bkmk_Baselines).



## <a name="about-installing-update-1806"></a>Güncelleştirme 1806 ' i yükleme hakkında

#### <a name="sites"></a>Siteler
Güncelleştirme 1806, hiyerarşinizin en üst düzeyindeki siteye yüklenir. Yüklemeyi merkezi yönetim sitenizden veya tek başına birincil sitenizden başlatın. Güncelleştirme, üst düzey sitede yüklendikten sonra, alt siteler aşağıdaki güncelleştirme davranışına sahiptir:

-   Alt birincil siteler güncelleştirmeyi merkezi yönetim sitesi yüklemeyi tamamladıktan sonra otomatik olarak yükler. Bir sitenin güncelleştirmeyi ne zaman yüklei denetlemek için hizmet pencerelerini kullanabilirsiniz. Daha fazla bilgi için bkz. [site sunucuları Için hizmet pencereleri](service-windows.md).

-   Birincil üst site güncelleştirme yüklemesini tamamladıktan sonra, tüm ikincil siteleri Configuration Manager konsolunun içinden el ile güncelleştirin. İkincil site sunucularının otomatik güncelleştirilmesi desteklenmiyor.

#### <a name="site-system-roles"></a>Site sistemi rolleri
Bir site sunucusu güncelleştirmeyi yüklediğinde, tüm site sistem rollerini otomatik olarak güncelleştirir. Bu roller site sunucusudur veya uzak sunuculara yüklenir. Güncelleştirmeyi yüklemeden önce, her site sistem sunucusunun yeni güncelleştirme sürümü için geçerli önkoşulları karşıladığından emin olun.

#### <a name="configuration-manager-consoles"></a>Configuration Manager konsolları   
Güncelleştirme tamamlandıktan sonra Configuration Manager konsolunu ilk kez kullandığınızda, bu konsolu güncelleştirmeniz istenir. Ayrıca, konsolunu barındıran bilgisayarda Configuration Manager kurulumunu çalıştırabilir ve Konsolu güncelleştirme seçeneğini belirleyebilirsiniz. Güncelleştirmeyi en kısa sürede konsola yükler. Daha fazla bilgi için [Configuration Manager konsolunu yüklemeye](../deploy/install/install-consoles.md)bakın.

> [!IMPORTANT]  
> Merkezi yönetim sitesinde bir güncelleştirme yüklediğinizde, tüm alt birincil siteler güncelleştirme yüklemesini de tamamlayana kadar aşağıdaki sınırlamalara ve gecikmelerden haberdar olun:    
> - **İstemci yükseltmeleri** başlamaz. Bu, istemcilerin ve ön üretim istemcilerinin otomatik güncelleştirmelerini içerir. Ayrıca, son site güncelleştirme yüklemesini tamamlana kadar üretim öncesi istemcileri üretime yükseltemede olursunuz. Son site güncelleştirme yüklemesini tamamladıktan sonra, istemci yükseltmeleri yapılandırma seçimlerinize bağlı olarak başlayacaktır.   
> - Güncelleştirme ile etkinleştirdiğiniz **yeni özellikler** kullanılamaz. Bunun nedeni, bu özellik ile ilgili verilerin çoğaltılmasını, bu özellik için henüz desteği yüklememiş bir siteye gönderilmesini önlemektir. Tüm birincil siteler güncelleştirmeyi yükledikten sonra özellik kullanıma sunulacaktır.   
> - Merkezi Yönetim sitesi ve alt birincil siteleri arasındaki **çoğaltma bağlantıları** yükseltilmeyen olarak görüntülenir. Bu, güncelleştirme paketi yükleme durumu ' nu, çoğaltma başlatmayı Izleme için uyarıyla tamamlandı durumu olarak gösterir. Konsolunun Izleme düğümünde bu, *bağlantı yapılandırılmakta*olarak görüntülenir.


## <a name="checklist"></a>Denetim Listesi

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Tüm siteler Configuration Manager desteklenen bir sürümünü çalıştırır  
Güncelleştirme 1806 ' i yüklemeye başlayabilmeniz için hiyerarşideki her site sunucusu aynı Configuration Manager sürümünü çalıştırmalıdır. 1806 sürümüne güncelleştirmek için 1706, 1710 veya 1802 sürümünü kullanmanız gerekir.

#### <a name="review-the-status-of-your-product-licensing"></a>Ürün lisanslarınızın durumunu gözden geçirin 
Bu güncelleştirmeyi yüklemek için etkin bir yazılım güvencesi (SA) sözleşmenize veya eşdeğer abonelik haklarına sahip olmanız gerekir. Siteyi güncelleştirdiğinizde **lisanslama** sayfası, **yazılım güvencesi sona erme tarihini**onaylama seçeneğini sunar.

Bu değer isteğe bağlıdır. Lisans sona erme tarihi için uygun bir anımsatıcı olarak belirtebilirsiniz. Gelecekteki güncelleştirmeleri yüklediğinizde bu tarih görülebilir. Kurulum sırasında veya bir güncelleştirmenin yüklenmesi sırasında daha önce bu değeri belirtmiş olabilirsiniz. Bu değeri Configuration Manager konsolunda de belirtebilirsiniz. **Yönetim** çalışma alanında, **Site yapılandırması**' nı genişletin ve **siteler**' i seçin. Şeritte **Hiyerarşi ayarları** ' na tıklayın ve **lisanslama** sekmesine geçin.

Daha fazla bilgi için bkz. [lisanslama ve dallar](../../understand/learn-more-editions.md).

#### <a name="review-microsoft-net-versions"></a>Microsoft .NET sürümlerini gözden geçirin 
Bir site bu güncelleştirmeyi yüklediğinde, Configuration Manager .NET Framework 4.5.2 otomatik olarak yüklenir. Bu önkoşul zaten yüklü değilse, site onu aşağıdaki site sistemi rollerinden birini barındıran her bir sunucuya yüklenir:

-   Yönetim noktası
-   Hizmet bağlantı noktası
-   Kayıt proxy noktası
-   Kayıt noktası

Bu yükleme, site sistem sunucusunu bir önyükleme bekleme durumuna alabilir ve hataları Configuration Manager bileşeni durum görüntüleyicisine bildirebilir. Ayrıca, sunucu üzerinde .NET uygulamaları, sunucu yeniden başlatılana kadar rastgele hatalarla karşılaşabilir.

Daha fazla bilgi için bkz. [site ve site sistemi önkoşulları](../../plan-design/configs/site-and-site-system-prerequisites.md).

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Windows 10 için Windows ADK sürümünü gözden geçirin
Windows 10 değerlendirme ve dağıtım seti 'nin (ADK) sürümü 1806 Configuration Manager için desteklenmelidir. Desteklenen Windows ADK sürümleri hakkında daha fazla bilgi için bkz. [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Windows ADK 'yi güncelleştirmeniz gerekiyorsa, Configuration Manager güncelleştirmesine başlamadan önce bunu yapın. Bu sıra varsayılan önyükleme görüntülerinin Windows PE 'nin en son sürümüne otomatik olarak güncelleştirilmesini sağlar. Siteyi güncelleştirdikten sonra özel önyükleme görüntülerini el ile güncelleştirin.

Siteyi Windows ADK 'yi güncelleştirmeden önce güncelleştirirseniz, bkz. [dağıtım noktalarını Önyükleme görüntüsüyle güncelleştirme](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Çözümlenmemiş sorunlar için siteyi ve hiyerarşi durumunu gözden geçirin 
Bir siteyi güncelleştirmeden önce site sunucusunun, site veritabanı sunucusunun ve uzak bilgisayarlara yüklü site sistem rollerinin tüm çalışma sorunlarını çözün. Bir site güncelleştirmesi mevcut çalışma sorunları nedeniyle başarısız olabilir.

Daha fazla bilgi için bkz. [uyarıları ve durum sistemini kullanma](use-alerts-and-the-status-system.md).

#### <a name="review-file-and-data-replication-between-sites"></a>Siteler arasında dosya ve veri çoğaltmayı gözden geçirme   
Siteler arasında dosya ve veritabanı çoğaltmasının çalışır durumda ve güncel olduğundan emin olun. Her iki durumda da gecikme veya biriktirme listesi sorunsuz, başarılı bir güncelleştirmeyi engelleyebilir. Veritabanı çoğaltmasında, güncelleştirmeyi başlatmadan önce sorunları çözmeye yardımcı olması için Çoğaltma Bağlantısı Analizcisi’ni kullanabilirsiniz.

Daha fazla bilgi için [Çoğaltma Bağlantısı Çözümleyicisi hakkında](monitor-replication.md#BKMK_RLA)bölümüne bakın.

#### <a name="install-all-applicable-critical-windows-updates"></a>Tüm geçerli kritik Windows güncelleştirmelerini yükler
Configuration Manager için bir güncelleştirme yüklemeden önce, ilgili her site sistemi için kritik işletim sistemi güncelleştirmelerini yüklemelisiniz. Bu sunucular, site sunucusu, site veritabanı sunucusu ve uzak site sistemi rollerini içerir. Yüklediğiniz bir güncelleştirme yeniden başlatma gerektiriyorsa, yükseltmeye başlamadan önce ilgili sunucuları yeniden başlatın.

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Birincil sitelerde yönetim noktaları için veritabanı çoğaltmalarını devre dışı bırak   
Configuration Manager, etkin yönetim noktaları için veritabanı çoğaltması olan bir birincil siteyi başarıyla güncelleştiremiyor. Configuration Manager için bir güncelleştirme yüklemeden önce, veritabanı çoğaltmasını devre dışı bırakın.

Daha fazla bilgi için bkz. [Yönetim noktaları Için veritabanı çoğaltmaları](../deploy/configure/database-replicas-for-management-points.md).

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>SQL Server AlwaysOn kullanılabilirlik gruplarını el ile yük devretmeye ayarla   
Kullanılabilirlik grubu kullanıyorsanız, güncelleştirme yüklemesine başlamadan önce kullanılabilirlik grubunun el ile yük devretmeye ayarlandığından emin olun. Site güncelleştirildikten sonra, yük devretmeyi otomatik olarak geri yükleyebilirsiniz. Daha fazla bilgi için bkz. [site veritabanı Için AlwaysOn SQL Server](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>Her sitede site bakım görevlerini devre dışı bırak
Güncelleştirmeyi yüklemeden önce güncelleştirme işleminin etkin olduğu süre boyunca çalışabilecek tüm site bakım görevlerini devre dışı bırakın. Örneğin, ancak bunlarla sınırlı olmamak için:

-   Site Sunucusunu Yedekle
-   Eski İstemci İşlemlerini Sil
-   Eski Bulma Verilerini Sil

Bir site veritabanı bakım görevi güncelleştirme yüklemesi sırasında çalıştığında güncelleştirme yüklemesi başarısız olabilir. Bir görevi devre dışı bırakmadan önce, güncelleştirme yüklendikten sonra yapılandırmasını geri yükleyebilmek için görevin zamanlamasını kaydedin.

Daha fazla bilgi için bkz [. bakım görevleri](maintenance-tasks.md) ve [bakım görevleri için başvuru](reference-for-maintenance-tasks.md).

#### <a name="temporarily-stop-any-antivirus-software"></a>Tüm virüsten koruma yazılımlarını geçici olarak durdurma 
Bir siteyi güncelleştirmeden önce, Configuration Manager sunucularındaki virüsten koruma yazılımını durdurun. <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>Site veritabanının bir yedeğini oluşturun 
Bir siteyi güncelleştirmeden önce, merkezi yönetim sitesinde ve birincil sitelerde site veritabanını yedekleyin. Bu yedekleme, olağanüstü durum kurtarma için kullanmak üzere başarılı bir yedeğiniz olmasını sağlar.

Daha fazla bilgi için bkz. [yedekleme ve kurtarma](backup-and-recovery.md).

#### <a name="plan-for-client-piloting"></a>İstemci pilot uygulaması için plan   
İstemciyi güncelleştiren bir güncelleştirme yüklediğinizde, bu yeni istemci güncelleştirmesini, tüm etkin istemcilerinizi dağıtmadan ve yükseltibir ön üretim ortamında test edebilirsiniz. Bu seçenekten faydalanmak için, güncelleştirmeyi yüklemeye başlamadan önce sitenizi üretim öncesi için Otomatik yükseltmeleri destekleyecek şekilde yapılandırmanız gerekir.

Daha fazla bilgi için bkz. [istemcileri](../../clients/manage/upgrade/upgrade-clients.md) yükseltme ve [bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme](../../clients/manage/upgrade/test-client-upgrades.md).

#### <a name="plan-to-use-service-windows"></a>Hizmet pencerelerini kullanmayı planlayın   
Site sunucusu güncelleştirmelerinin yüklenebileceği bir dönem tanımlamak için, hizmet pencerelerini kullanın. Hiyerarşinizdeki sitelerin güncelleştirmeyi yüklemesi sırasında denetim sağlamanıza yardımcı olabilirler. Daha fazla bilgi için bkz. [site sunucuları Için hizmet pencereleri](service-windows.md).

#### <a name="review-supported-extensions"></a>Desteklenen uzantıları gözden geçirme
<!--SCCMdocs#587-->
Configuration Manager Microsoft veya Microsoft iş ortaklarından diğer ürünlerle genişletirseniz, bu ürünlerin 1806 sürümünü desteklediğini onaylayın. Bu bilgi için ürün satıcısına danışın. Örneğin, bkz. Microsoft Dağıtım Araç Seti [sürüm notları](../../../mdt/release-notes.md).

#### <a name="run-the-setup-prerequisite-checker"></a>Kurulum önkoşul denetleyicisi 'ni çalıştırın   
Güncelleştirme konsolunda kullanılabilir olarak listelendiğinde **,** güncelleştirmeyi yüklemeden önce Önkoşul denetleyicisini bağımsız olarak çalıştırabilirsiniz. (Güncelleştirmeyi siteye yüklediğinizde, önkoşul denetleyicisi yeniden çalışır.)

Konsolundan bir önkoşul denetimi çalıştırmak için, **Yönetim** çalışma alanına gidin ve **güncelleştirmeler ve bakım**' ı seçin. **Configuration Manager 1806** güncelleştirme paketini seçin ve şeritte **Önkoşul denetimini Çalıştır** ' a tıklayın.

Daha fazla bilgi için, [konsol içi bir güncelleştirmeyi yüklemeden önce](install-in-console-updates.md#bkmk_beforeinstall) **bir güncelleştirmeyi yüklemeden önce Önkoşul denetleyicisini çalıştırma** bölümüne bakın.

> [!IMPORTANT]  
> Önkoşul denetleyicisi çalıştırıldığında, işlem, site bakım görevlerinde kullanılan bazı ürün kaynak dosyalarını güncelleştirir. Bu nedenle, Önkoşul denetleyicisini çalıştırdıktan sonra ancak güncelleştirmeyi yüklemeden önce, bir site bakım görevi gerçekleştirmeniz gerekirse, CD 'den **setupwpf. exe dosyasını** (Configuration Manager Kurulum) çalıştırın. Site sunucusundaki en son klasör.

#### <a name="update-sites"></a>Siteleri Güncelleştir   
Artık hiyerarşiniz için güncelleştirme yüklemesini başlatmaya hazırsınız. Güncelleştirmeyi yükleme hakkında daha fazla bilgi için bkz. [konsol içi güncelleştirmeleri yükleme](install-in-console-updates.md#bkmk_install).

Güncelleştirmeyi normal iş saatleri dışında yüklemeyi planlayabiliriz. İşlemin iş operasyonlarınız üzerinde en az etkiye sahip olacağını belirleme. Güncelleştirmeyi ve eylemlerini yükleme, site bileşenlerini ve site sistem rollerini yeniden yükler.

Daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](updates.md).



## <a name="post-update-checklist"></a>Güncelleştirme sonrası denetim listesi

Site güncelleştirildikten sonra ortak görevleri ve konfigürasyonları gerçekleştirmek için aşağıdaki denetim listesini kullanın.


#### <a name="confirm-version-and-restart-if-necessary"></a>Sürümü onaylayın ve yeniden başlatın (gerekirse)
Her site sunucusu ve site sistemi rolünün 1806 sürümüne güncelleştirildiğinden emin olun. Konsolunda, **Yönetim** çalışma alanındaki **siteler** ve **dağıtım noktaları** düğümlerine **Sürüm** sütununu ekleyin. Gerektiğinde, bir site sistemi rolü otomatik olarak yeni sürüme güncelleştirmek için yeniden yüklenir. 

İlk olarak güncelleştirme başarılı olmayan uzak site sistemlerini yeniden başlatmayı düşünün. Site altyapınızı gözden geçirin ve ilgili site sunucularının ve uzak site sistem sunucularının başarıyla yeniden başlatıldığından emin olun. Genellikle, site sunucuları yalnızca Configuration Manager bir site sistemi rolü için önkoşul olarak .NET yüklediğinde yeniden başlatılır.


#### <a name="confirm-site-to-site-replication-is-active"></a>Siteden siteye çoğaltmanın etkin olduğunu onaylayın
Configuration Manager konsolunda, durumu görüntülemek ve çoğaltmanın etkin olduğundan emin olmak için aşağıdaki konumlara gidin:  

-   **İzleme** çalışma alanı, **site hiyerarşisi** düğümü  

-   **İzleme** çalışma alanı, **veritabanı çoğaltma** düğümü  

Daha fazla bilgi için aşağıdaki makalelere bakın:  

- [İzleme hiyerarşisi](monitor-hierarchy.md)
- [Çoğaltmayı izleme](monitor-replication.md)
- [Çoğaltma Bağlantısı Çözümleyicisi hakkında](monitor-replication.md#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Configuration Manager konsollarını güncelleştirme
Tüm uzaktan Configuration Manager konsollarını aynı sürüme güncelleştirin. Şu durumlarda konsolu güncelleştirmeniz istenir:  

-   Konsolunu açarsınız.  

-   Konsolda yeni bir düğüme gidebilirsiniz.  


#### <a name="reconfigure-database-replicas-for-management-points"></a>Yönetim noktaları için veritabanı çoğaltmalarını yeniden yapılandırın
Birincil bir siteyi güncelleştirdikten sonra, siteyi güncelleştirmeden önce kaldırdığınız yönetim noktaları için veritabanı çoğaltmasını yeniden yapılandırın. Daha fazla bilgi için bkz. [Yönetim noktaları Için veritabanı çoğaltmaları](../deploy/configure/database-replicas-for-management-points.md).  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Devre dışı bırakılmış tüm bakım görevlerini yeniden yapılandırın
Güncelleştirmeyi yüklemeden önce bir sitede veritabanı [bakım görevlerini](maintenance-tasks.md) devre dışı bırakırsanız, bu görevleri yeniden yapılandırın. Güncelleştirmeden önce yerinde olan ayarları kullanın.  


#### <a name="update-clients"></a>İstemcileri Güncelleştir
Özellikle güncelleştirmeyi yüklemeden önce istemci pilot 'yı yapılandırdıysanız, oluşturduğunuz plana göre istemcileri güncelleştirin. Daha fazla bilgi için bkz. [Windows bilgisayarları için istemcileri yükseltme](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  


#### <a name="third-party-extensions"></a>Üçüncü taraf uzantıları
Configuration Manager için herhangi bir uzantı kullanıyorsanız, Configuration Manager sürüm 1806 ' i desteklemek için bunları en son sürüme güncelleştirin. 


#### <a name="update-custom-boot-images-and-media"></a>Özel önyükleme görüntülerini ve medyayı güncelleştirme
<!--SCCMDocs issue 775-->

Varsayılan veya özel bir önyükleme görüntüsü olup olmadığı, kullandığınız herhangi bir önyükleme görüntüsü için **dağıtım noktalarını güncelleştir** eylemini kullanın. Bu eylem, istemcilerin en son sürümü kullanmasını sağlar. Windows ADK 'nin yeni bir sürümü olmasa bile, Configuration Manager istemci bileşenleri bir güncelleştirmeyle değişebilir. Önyükleme görüntülerini ve medyayı güncelleştirmemeniz durumunda, görev sırası dağıtımları cihazlarda başarısız olabilir. 

Siteyi güncelleştirdiğinizde Configuration Manager *varsayılan* önyükleme görüntülerini otomatik olarak güncelleştirir. Güncelleştirilmiş içeriği otomatik olarak dağıtım noktalarına dağıtır. Bu içeriği ağınız genelinde dağıtmaya hazırsanız, belirli önyükleme görüntülerinde **dağıtım noktalarını güncelleştir** eylemini kullanın. 

Siteyi güncelleştirdikten sonra, *özel* önyükleme görüntülerini el ile güncelleştirin. Bu eylem, gerekirse önyükleme görüntüsünü en son istemci bileşenleriyle güncelleştirir, isteğe bağlı olarak geçerli Windows PE sürümü ile yeniden yükler ve içeriği dağıtım noktalarına yeniden dağıtır. 

Daha fazla bilgi için bkz. [dağıtım noktalarını Önyükleme görüntüsüyle güncelleştirme](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image). 
