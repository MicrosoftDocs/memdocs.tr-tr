---
title: Microsoft Intune cihaz yönetimi özellikleri
description: Intune’un kaydettiğiniz cihazları yönetmenize nasıl yardımcı olabileceğini öğrenmek için bu konuyu okuyun.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/16/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: de83a021343b733816330bc9be94c57a57afd9f1
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989847"
---
# <a name="enrolled-device-management-capabilities-of-microsoft-intune"></a>Microsoft Intune’un kayıtlı cihaz yönetimi özellikleri

Microsoft Intune bir dizi cihazı hizmete *kaydederek* yönetmenize olanak tanır. Bazı cihaz türlerini kendiniz kaydedebilirsiniz veya kullanıcılar *şirket portalı* uygulamasını kullanarak kaydedebilir. Kaydetme, uygulamalara gözatıp yüklemeye izin verir, cihazlarının şirket ilkeleriyle uyumlu olduğundan emin olun ve BT desteğiyle iletişim kurun.

Bu makale, cihazların kaydolduktan sonra elde ettiğiniz yeteneklerin tam bir listesini sağlar.

Yönetim, envanter, uygulama dağıtımı, sağlama ve kullanımdan kaldırma işlemleri Azure portal Intune aracılığıyla gerçekleştirilir.

Kullanıcılar uygulamaları yüklemek, cihazlarını kaydetmek veya kaydı kaldırmak ve BT departmanına ya da yardım masasına başvurmak için şirket portalına erişim kazanır.



## <a name="device-security-and-configuration"></a>Cihaz güvenliği ve yapılandırma

|Özellik|Ayrıntılar|Daha fazla bilgi|
|--------------|-----------|--------------------|
|Yapılandırma ilkeleri<br><br>Özel ilkeler| Kuruluşunuzdaki mobil cihazlarda birçok ayar ve özelliği yönetmenizi sağlar. Örneğin, parola isteyebilir, başarısız oturum açma girişimlerinin sayısını sınırlandırabilir, ekranın kilitlenmesinden önceki süreyi sınırlandırabilir, parola sona erme süresini ayarlayabilir ve daha önce kullanılan parolaların kullanımını engelleyebilirsiniz. Ayrıca cihaz kamerası veya web tarayıcısı gibi donanım ve yazılım özelliklerinin kullanımını da denetleyebilirsiniz.<br><br>Yapılandırma ilkeleri ihtiyaç duyduğunuz ayarları içermiyorsa özel ilkeleri kullanın. İOS/ıpados cihazlarında, Apple Configurator aracından dışarı aktardığınız ayarları içeri aktarabilirsiniz. Diğer cihazlar için Open Mobile Alliance Uniform Resource Identifier (OMA-URI) ayarlarını kullanarak cihazdaki ayarları ve özellikleri yapılandırabilirsiniz.|[Microsoft Intune ilkeleriyle cihazlarınızın ayarlarını ve özelliklerini yönetme](../protect/device-compliance-get-started.md)|
|Uzaktan Temizleme, Uzak Kilit ve Parola Sıfırlama|Bir cihaz kaybolur veya çalınırsa hassas verileri siler. Örneğin, cihazı uzaktan kilitleyebilir, fabrika ayarlarına sıfırlayabilir veya yalnızca kurumsal verileri temizleyebilirsiniz.<br><br>Kullanıcılar cihazlarına erişimi kaybederse geçiş kodlarını sıfırlayabilir, kaybolan veya çalınan cihazları kilitleyebilir ve hatta kaybolan ya da çalınan cihazların verilerini temizleyebilirsiniz.|[Uzaktan kilitleme](../remote-actions/device-remote-lock.md) ve [geçiş kodu sıfırlama](../remote-actions/device-passcode-reset.md) ile cihazlarınızı korumaya yardımcı olma|
|Bilgi noktası modu|Mobil cihazların ekran yakalama ve güç düğmesi gibi belirli özelliklerini kilitlemenizi sağlar. Ayrıca, cihazları belirttiğiniz tek bir uygulamayı çalıştıracak şekilde kısıtlamanıza olanak tanır. |[Microsoft Intune’da iOS yapılandırma ilkesi ayarları](../configuration/device-restrictions-ios.md)|
|AutoPilot sıfırlama|Sıfırlama işlemini uzaktan başlatmak için cihaza bir görev gönderir ve bu işlemi başlatmak için BT personelinin veya diğer yöneticilerin her bir makineyi ziyaret etmesini önler. Bir cihazda Autopilot Reset kullanıldığında, cihazın birincil kullanıcısı kaldırılır. Sıfırlamadan sonra oturum açan bir sonraki Kullanıcı, birincil kullanıcı olarak ayarlanır.|[Uzak Windows Autopilot sıfırlaması](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)|

## <a name="app-management"></a>Uygulama yönetimi

|Özellik|Ayrıntılar|Daha fazla bilgi|
|--------------|-----------|--------------------|
|Uygulama dağıtımı ve yönetimi|Mobil uygulamaları kurulum dosyalarından ve uygulama mağazalarından uygulama dağıtma, uygulama durumunun ayrıntılı bir şekilde izlenmesi ve uygulama kaldırma dahil yaşam döngüsü boyunca yönetmenize yardımcı olmak için çeşitli araçlar sağlar.|[Microsoft Intune'da uygulamaları dağıtma](../apps/apps-deploy.md)|
|Uyumlu ve uyumlu olmayan uygulamalar|Uyumlu uygulamaların (kullanıcıların yüklemesine izin verilen uygulamalar) ve uyumlu olmayan uygulamaların (kullanıcıların yüklemesine izin verilmeyen uygulamalar) listelerini belirtmenizi sağlar.|[Microsoft Intune’da iOS ilke ayarları](../configuration/device-restrictions-ios.md)|
|Mobil uygulama yönetimi|Mobil uygulama yönetimini kullanarak, hem Intune tarafından yönetilen hem de yönetilmeyen tüm cihazlarda uygulamalar için kısıtlamaları yapılandırır. Kopyalama ve yapıştırma, verilerin dış yedeklemesi ve uygulamalar arasında veri aktarımı gibi işlemleri kısıtlayarak şirket verilerinizin güvenliğini artırabilirsiniz.|[Configure and deploy mobile application management policies in the Microsoft Intune console (Microsoft Intune konsolunda mobil uygulama yönetimi ilkelerini yapılandırma ve dağıtma)](../developer/app-wrapper-prepare-android.md)|
|iOS mobil uygulama yapılandırması|, Kullanıcı uygulamayı çalıştırdığında gerekli olabilecek iOS/ıpados uygulamalarına yönelik ayarları sağlamak için mobil uygulama yapılandırma ilkelerini kullanır. Örneğin, uygulama kullanıcının bağlantı noktası numarasını veya oturum açma bilgilerini belirtmesini isteyebilir. Uygulama yapılandırmasını daha kolay hale getirebilirsiniz ve destek çağrılarının sayısını azaltabilirsiniz.|[İOS/ıpados uygulamalarını Microsoft Intune 'de mobil uygulama yapılandırma ilkeleriyle yapılandırma](../apps/app-configuration-policies-use-ios.md)|
|iOS/ıpados mobil uygulama sağlama profilleri|, Süresi dolmak üzere olan iOS/ıpados uygulamalarına sağlama profilleri dağıtmanıza yardımcı olur. |[Uygulamalarınızın süresinin dolmasını engellemek için iOS/ıpados mobil sağlama profili ilkelerini kullanın](../apps/app-provisioning-profile-ios.md)|
|Yönetilen tarayıcı|Cihaz kullanıcılarının ziyaret edebileceği web sitelerini denetlemek için yönetilen tarayıcı profilleri yapılandırır. Ayrıca, yönetilen tarayıcıya mobil uygulama yönetimi ilkeleri de uygulayabilirsiniz.|[Microsoft Intune ile yönetilen tarayıcı ilkelerini kullanarak Internet erişimini yönetme](../apps/app-configuration-managed-browser.md)|
|İş İçin Windows Hello|Parolaları, akıllı kartları ya da sanal akıllı kartları değiştirmek için Windows 10’da şirket içi Active Directory’nin veya Azure Active Directory’nin kullanıldığı alternatif bir oturum açma yöntemi olan İş İçin Windows Hello’yu tümleştirmenize olanak tanır.|[Microsoft Intune ile cihazlarda İş İçin Windows Hello ayarlarını denetleme](../protect/windows-hello.md)|
|Toplu satın alınan uygulamalar|Bir toplu satın alma programı aracılığıyla lisans bilgilerini uygulama mağazasından içeri aktararak, kaç lisans kullandığınızı izleyerek ve sahip olduğunuzdan fazla uygulama kopyası yüklemenizi önleyerek satın aldığınız uygulamaları yönetmenize yardımcı olur.|[Microsoft Intune kullanarak toplu satın alınan uygulamaları yönetme](../apps/vpp-apps.md)|

## <a name="company-resource-access"></a>Şirket kaynak erişimi

|Özellik|Ayrıntılar|Daha fazla bilgi|
|--------------|-----------|--------------------|
|Sertifika profilleri|Wi-Fi, VPN ve e-posta profillerini güvenli hale getirmek ve kimlik doğrulaması yapmak için kullanılabilen güvenli sertifika profilleri ve Basit Sertifika Kaydı Profilleri (SCEP) sertifikaları oluşturur ve dağıtır.|[Microsoft Intune’da sertifika profilleriyle güvenli kaynak erişimi](../protect/certificates-configure.md)|
|Wi-Fi profilleri|Kablosuz ağ ayarlarını kullanıcılarınıza dağıtır. Bu ayarları dağıtarak kurumsal ağa bağlanmak için gereken kullanıcı çabasını en aza indirirsiniz.|[Microsoft Intune’da Wi-Fi bağlantıları](../configuration/wi-fi-settings-configure.md)|
|E-posta profilleri|Kullanıcıların kendi bölümünde herhangi bir kurulum yapması gerekmeden kişisel cihazlarında Şirket e-postasına erişebilmeleri için cihazlara e-posta ayarları oluşturur ve dağıtır.|[Microsoft Intune ile e-posta profillerini kullanarak kurumsal e-postaya erişim yapılandırma](../configuration/email-settings-configure.md)|
|VPN profilleri|VPN ayarlarını kuruluşunuzdaki kullanıcı ve cihazlara dağıtır. Bu ayarları dağıtarak, şirket ağındaki kaynaklara bağlanmak için gereken kullanıcı çabasını en aza indirirsiniz.|[Microsoft Intune’da VPN bağlantıları](../configuration/device-profiles.md#vpn)|
|Koşullu erişim ilkeleri|Intune tarafından yönetilmeyen cihazların Microsoft Exchange e-posta ve SharePoint Online hizmetlerine erişimini yönetir.|[Microsoft Intune ile e-posta ve SharePoint erişimini kısıtlama](../protect/app-based-conditional-access-intune.md)|

## <a name="next-steps"></a>Sonraki adımlar

[Yönetebileceğiniz cihazların listesini görüntüleyin](../remote-actions/device-management.md).
