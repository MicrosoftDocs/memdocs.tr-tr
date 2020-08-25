---
title: Microsoft Intune kullanarak Windows cihazları için kaydı ayarlama
titleSuffix: ''
description: Windows cihazları için kaydı ayarlayın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 48560af1ff31d5660f00e775a2f510b88c08fd9c
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820604"
---
# <a name="set-up-enrollment-for-windows-devices"></a>Windows cihazları için kaydı ayarlama

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Bu makale BT yöneticilerinin kullanıcıları için Windows kaydını kolaylaştırmasına yardımcı olur. [Intune’u kurduğunuzda](../fundamentals/setup-steps.md) kullanıcılar, iş veya okul hesaplarıyla [oturum açarak](https://docs.microsoft.com/mem/intune/user-help/windows-enrollment-company-portal) Windows cihazlarını kaydederler.  

Bir Intune yöneticisi olarak, kayıt sürecini aşağıdaki yollarla basitleştirebilirsiniz:

- [Otomatik kaydı etkinleştirme](#enable-windows-10-automatic-enrollment) (Azure AD Premium gereklidir)
- [CNAME kaydı](#simplify-windows-enrollment-without-azure-ad-premium)
- [Toplu kaydı etkinleştirme](windows-bulk-enroll.md) (Azure AD Premium ve Windows yapılandırma Tasarımcısı gereklidir)

Windows cihaz kaydını nasıl basit hale getirebileceğinizi iki faktör belirler:

- **Azure Active Directory Premium kullanıyor musunuz?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium), Enterprise Mobility + Security ve diğer lisanslama planlarına dahildir.
- **Kullanıcılar hangi Windows istemci sürümlerini kaydedecekler?** <br>Windows 10 cihazları iş veya okul hesabı eklenerek otomatik olarak kaydedilebilir. Önceki sürümlerin Şirket Portalı uygulamasını kullanarak kaydolması gerekir.

||**Azure AD Premium**|**Diğer AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Otomatik kayıt](#enable-windows-10-automatic-enrollment) |Kullanıcı kaydı|
|**Önceki Windows sürümleri**|Kullanıcı kaydı|Kullanıcı kaydı|

Otomatik kayıt kullanabilen kuruluşlar, Windows Yapılandırma Tasarımcısı uygulamasını kullanarak [cihazları toplu kaydetmeyi](windows-bulk-enroll.md) de yapılandırabilirler.

## <a name="device-enrollment-prerequisites"></a>Cihaz kaydı önkoşulları

Yöneticinin yönetim için cihazları Intune 'a kaydedebilmesi için, lisansların yönetici hesabına zaten atanmış olması gerekir. [Cihaz kaydı için lisans atama hakkında bilgi edinin](../fundamentals/licenses-assign.md)

## <a name="multi-user-support"></a>Çok kullanıcı desteği

Intune, her ikisini de içeren cihazlarda birden çok kullanıcıyı destekler:

- Windows 10 Creator 'ın güncelleştirmesini çalıştırma
- Azure Active Directory etki alanına katılmış.

Standart kullanıcılar Azure AD kimlik bilgileriyle oturum açtığında, kullanıcı adlarına atanmış uygulama ve ilkeler alırlar. Yalnızca cihazın [birincil kullanıcısı](../remote-actions/find-primary-user.md) , uygulama yükleme ve cihaz eylemleri gerçekleştirme gibi self servis senaryoları için şirket portalı kullanabilir (kaldırma, sıfırlama). Birincil Kullanıcı atanmamış paylaşılan Windows 10 cihazlarında, Şirket Portalı kullanılabilir uygulamaları yüklemek için yine de kullanılabilir.

[!INCLUDE [AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## <a name="simplify-windows-enrollment-without-azure-ad-premium"></a>Azure AD Premium olmadan Windows kaydını kolaylaştırma
Kaydolmayı basitleştirmek için, kayıt isteklerini Intune sunucularına yönlendiren bir etki alanı adı sunucusu (DNS) diğer adı (CNAME kayıt türü) oluşturun. Aksi takdirde Intune'a bağlanmaya çalışan kullanıcıların kayıt sırasında Intune sunucu adını girmeleri gerekir.

**1. Adım: CNAME oluşturma** (isteğe bağlı)<br>
Şirketinizin etki alanı için CNAME DNS kaynak kayıtları oluşturun. Örneğin, şirketinizin Web sitesi contoso.com ise, DNS 'de EnterpriseEnrollment.contoso.com enterpriseenrollment-s.manage.microsoft.com 'e yönlendiren bir CNAME oluşturursunuz.

CNAME DNS girişlerini oluşturma isteğe bağlı olmakla birlikte, CNAME kayıtları kullanıcılar için kaydolmayı kolaylaştırır. CNAME kaydı bulunamazsa, kullanıcıların MDM sunucu adını (enrollment.manage.microsoft.com) el ile girmesi istenir.

|Tür|Konak adı|Şunu gösterir:|TTL|
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 saat|
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|1 saat|

Şirket birden fazla UPN soneki kullanıyorsa, her etki alanı için bir CNAME oluşturmanız ve bunları EnterpriseEnrollment-s.manage.microsoft.com adresine yönlendirmeniz gerekir. Örneğin Contoso kullanıcıları e-posta/UPN'leri olarak aşağıdaki biçimleri kullanın:

- name@contoso.com
- name@us.contoso.com
- name@eu.contoso.com

Contoso DNS yöneticisinin aşağıdaki CNAME'leri oluşturması gerekir:

|Tür|Konak adı|Şunu gösterir:|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 saat|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 saat|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 saat|

`EnterpriseEnrollment-s.manage.microsoft.com` – E-postanın etki alanı adından etki alanı tanıma ile Intune hizmetine yeniden yönlendirmeyi destekler

DNS kaydındaki değişikliklerin yaygınlaştırılması 72 saat kadar sürebilir. DNS kaydı yayılıncaya kadar DNS değişikliğini Intune'da doğrulayamazsınız.

## <a name="additional-endpoints-are-used-but-no-longer-supported"></a>Ek uç noktalar kullanılıyor ancak artık desteklenmiyor
EnterpriseEnrollment-s.manage.microsoft.com, kayıt için tercih edilen FQDN 'dir. Geçmişte müşteriler tarafından kullanılan ve çalışmaya devam eden iki uç nokta vardır ancak artık desteklenmiyordur. EnterpriseEnrollment.manage.microsoft.com (-s eklentisi olmadan) ve manage.microsoft.com adresleri, otomatik bulma sunucusu için hedef olarak çalışır ancak kullanıcının onay iletisinde Tamam seçeneğine dokunması gerekecektir. EnterpriseEnrollment-s.manage.microsoft.com üzerine geldiğinizde, kullanıcının ek onay adımını yapması gerekmez, bu nedenle önerilen yapılandırmadır

## <a name="alternate-methods-of-redirection-are-not-supported"></a>Alternatif Yönlendirme Yöntemleri Desteklenmez
CNAME yapılandırması haricinde bir yöntem kullanılması desteklenmez. Örneğin enterpriseenrollment.contoso.com/EnrollmentServer/Discovery.svc bağlantısının enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc veya manage.microsoft.com/EnrollmentServer/Discovery.svc is adresine yönlendirilmesi desteklenmez.

**2. Adım: CNAME'i doğrulama** (isteğe bağlı)<br>
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **Windows**  >  **Windows kaydı**  >  **CNAME doğrulaması**' nı seçin.
2. **Etki Alanı** kutusuna şirket Web sitesini girin ve ardından **Test Et**'i seçin.

## <a name="tell-users-how-to-enroll-windows-devices"></a>Kullanıcılara Windows cihazlarını nasıl kaydedeceklerini anlatma
Kullanıcılara Windows cihazlarını nasıl kaydedeceklerini ve cihazları yönetilmeye başladıktan sonra nelerle karşılaşabileceklerini anlatın.

> [!NOTE]
> Windows'un belirli sürümlerinde, son kullanıcıların atadığınız Windows uygulamalarını görüntüleyebilmesi için Şirket Portalı web sitesinde Microsoft Edge üzerinden erişmesi gerekir. Google Chrome, Mozilla Firefox ve Internet Explorer gibi diğer tarayıcılar bu filtreleme türünü desteklemez.

Son kullanıcı kayıt talimatları için bkz. [Windows cihazınızı Intune'a kaydetme](../user-help/windows-enrollment-company-portal.md). Ayrıca kullanıcılara [BT yöneticim cihazımda neleri görebilir?](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) sayfasındaki bilgilere göz atmalarını da söyleyebilirsiniz.

>[!IMPORTANT]
> Otomatik MDM kaydını etkinleştirmediyseniz ancak Azure AD’ye katılmış Windows 10 cihazlarınız varsa, kayıt sonrasında Intune konsolunda iki kayıt görünecektir. Bu, Azure AD 'ye katılmış cihazların **hesaplara**  >  **erişim iş veya okul** hesabına gitmesini ve aynı hesabı kullanarak **bağlanmasını** sağlayarak bunu durdurabilirsiniz. 

Son kullanıcı görevleri hakkında daha fazla bilgi için bkz. [Microsoft Intune’da son kullanıcı deneyimi hakkında kaynaklar](../fundamentals/end-user-educate.md).

## <a name="registration-and-enrollment-cnames"></a>Kayıt ve kayıt CNAMEs
Azure Active Directory, iOS/ıpados, Android ve Windows cihazları için cihaz kaydı için kullandığı farklı bir CNAME 'e sahiptir. Intune koşullu erişimi, cihazların "çalışma alanına katılmış" olarak da kaydedilmesini gerektirir. Koşullu erişim kullanmayı planlıyorsanız, sahip olduğunuz her şirket adı için EnterpriseRegistration CNAME 'i de yapılandırmalısınız.

| Tür | Konak adı | Şunu gösterir: | TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseRegistration. company_domain. com | EnterpriseRegistration.windows.net | 1 saat|

Cihaz kaydı hakkında daha fazla bilgi için bkz [. Azure Portal kullanarak cihaz kimliklerini yönetme](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal)

## <a name="windows-10-auto-enrollment-and-device-registration"></a>Windows 10 otomatik kayıt ve cihaz kaydı

Bu bölüm ABD kamu bulut müşterileri için geçerlidir.

CNAME DNS girişlerini oluşturma isteğe bağlı olmakla birlikte, CNAME kayıtları kullanıcılar için kaydolmayı kolaylaştırır. Kayıt CNAME kaydı bulunamazsa, kullanıcılardan MDM sunucu adını el ile girmesi istenir, enrollment.manage.microsoft.us.

| Tür | Konak adı | Şunu gösterir: | TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseEnrollment.company_domain.com | EnterpriseEnrollment-s.manage.microsoft.us | 1 saat|
|CNAME | EnterpriseRegistration.company_domain.com | EnterpriseRegistration.windows.net | 1 saat |


## <a name="next-steps"></a>Sonraki adımlar

- [Azure'da Inture kullanarak Windows cihazlarını yönetirken dikkat edilmesi gerekenler](../fundamentals/intune-legacy-pc-client.md).
