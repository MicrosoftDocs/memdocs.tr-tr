---
title: iOS cihazınızı Intune’dan kaldırma | Microsoft Docs
description: iOS cihazını Intune’dan nasıl kaldıracağınız açıklanır
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/02/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 28914db1-3e62-45f5-9632-b0d2a808a44d
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 872fb91a4fd684c546fa19a159eb30baca78c05d
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881627"
---
# <a name="remove-your-ios-device-from-intune"></a>iOS cihazınızı Intune’dan kaldırma

iOS cihazınızı Intune’dan kaldırdığınızda, cihazınız artık şirket kaynaklarına erişemez ve Intune tarafından yönetilmez.


## <a name="removing-the-device-from-my-devices"></a>Cihazı Cihazlarım’dan kaldırma

Cihazınızı Intune’dan kaldırmak için aşağıdaki adımları kullanın veya bu videoyu izleyin:


1. Şirket Portalı uygulamasında **Cihazlar**’a dokunun ve kaydını kaldırmak istediğiniz cihazı seçin. Yalnızca bir cihazınız varsa **Cihazlar**’a dokunduğunuzda doğrudan cihaz ayrıntıları ekranına gidersiniz.

2. **YENİDEN ADLANDIR**’ın yanındaki üç nokta işaretine ve **Cihaz Kaldır** > **Kaldır** seçeneklerine dokunun.  

    |![Şirket Portalı uygulaması Cihazlar ekranının kullanıcı Kaldır’a tıkladıktan sonra çıkan seçeneklerini gösteren ekran görüntüsü. “Cihazı Kaldır” düğmesi, “Fabrika Sıfırlaması” düğmesi ve “İptal Et” düğmesini gösterir.](./media/cp_ios_unenroll_after_1804_001.png)|

    |![Şirket Portalı uygulaması Cihazlar ekranının kullanıcı Cihaz Kaldır düğmesine tıkladıktan sonra çıkan seçenekleri gösteren ekran görüntüsü. Kırmızı renkle vurgulanmış “Kaldır” düğmesi ve mavi renkle vurgulanmış “Daha Fazla Bilgi” ve “İptal Et” düğmelerini gösterir.](./media/cp_ios_unenroll_after_1804_002.png)|


    Cihazınızı Intune’dan kaldırdığınızda şunlar olur:

    - Cihazınız artık Şirket Portalı görünmeyecek.

    - Artık Şirket Portalı uygulama yükleyemezsiniz.

    - Cihazı eklediğinizde değiştirilen tüm ayarlar (örneğin, kamerayı devre dışı bırakma veya belirli bir parola uzunluğu gerekliliği) artık geçerliliğini kaybeder.

    - Dosya paylaşımları veya dahili web siteleri gibi şirket kaynaklarına erişemeyebilirsiniz.

    - Artık cihazınızda şirket uygulamalarını ve şirket verilerini kullanamazsınız.

    - Artık Wi-Fi veya bir sanal özel ağ (VPN) kullanarak şirket ağınıza bağlanamayabilirsiniz.

    - Şirket e-posta profilleri cihazdan kaldırılır.

    - Yalnızca e-posta için yapılandırılan cihazlar artık Şirket Portalı uygulamasında veya web sitesinde gösterilmez.

    - Uygulamalar kaldırılır. Şirket uygulama verileri kaldırılır.

## <a name="removing-data-collected-by-the-company-portal-app"></a>Şirket Portalı uygulaması tarafından toplanan verileri kaldırma

Şirket Portalı’nın cihazınızda yerel verileri depoladığı üç yer vardır.

- **Bilgi günlükleri**: Uygulamanın ne kadar süre açık kaldığı veya kilitlenip kilitlenmediği gibi Microsoft tarafından toplanan standart uygulama verileri, cihazı Şirket Portalı’ndan kaldırdığınızda otomatik olarak silinir.

- **Apple analiz**: Apple tarafından toplanan standart uygulama kilitlenme etkinlik verileri. Bu bilgiler, yalnızca cihazınızı fabrika ayarlarına sıfırlarsanız kaldırılabilir. Bu, cihazınızdaki tüm kişisel bilgileri silecektir. Bunu yapmak için **Ayarlar**  >  **genel**  >  **sıfırlama**  >  **tüm içeriği ve ayarları sil**' i açın.

- **Anahtarlık**: Cihazınız, parolalarınız ve diğer oturum açma bilgilerinizi Anahtarlığınızda depolar. Microsoft uygulamaları, Microsoft Outlook ve Microsoft Authenticator dahil cihazınızdaki Microsoft tarafından geliştirilmiş tüm uygulamalar arasında oturum açma bilgilerinizi paylaşır. Apple analiz gibi bu bilgiler, yalnızca cihazınızı fabrika ayarlarına sıfırlarsanız kaldırılabilir. Bu, cihazınızdaki tüm kişisel bilgileri silecektir. Bunu yapmak için **Ayarlar**  >  **genel**  >  **sıfırlama**  >  **tüm içeriği ve ayarları sil**' i açın.


Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.
