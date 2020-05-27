---
title: Windows 10 için toplu kayıt
titleSuffix: Microsoft Intune
description: Microsoft Intune için toplu kayıt paketi oluşturma
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/21/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: spshumwa
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ecbde2f6e6a40379cd37a6ddebe09fa9dab8e3b1
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988927"
---
# <a name="bulk-enrollment-for-windows-devices"></a>Windows cihazlar için toplu kayıt

Bir yönetici olarak çok sayıda yeni Windows cihazını Azure Active Directory ve Intune’a dahil edebilirsiniz. Azure AD kiracınıza cihazları toplu kaydetmek için Windows Yapılandırma Tasarımcısı (WCD) uygulaması ile bir sağlama paketi oluşturursunuz. Sağlama paketini şirkete ait cihazlara uygulamak, cihazları Azure AD kiracınıza dahil eder ve Intune yönetimine kaydeder. Paket uygulandıktan sonra, Azure AD kullanıcılarınızın oturum açması için bu size hazırlanın.

Azure AD kullanıcıları, bu cihazlarda standart kullanıcılardır ve atanan Intune ilkelerini ve gerekli uygulamaları alırlar. Windows toplu kayıt kullanılarak Intune'a kaydedilmiş olan Windows cihazları, kullanılabilir uygulamaları yüklemek için Şirket Portalı uygulamasını kullanabilir. 

## <a name="prerequisites-for-windows-devices-bulk-enrollment"></a>Windows cihazları toplu kaydetme önkoşulları

- Windows 10 Creator Update (Build 1709) veya üzeri çalıştıran cihazlar
- [Windows otomatik kayıt](windows-enroll.md#enable-windows-10-automatic-enrollment)

## <a name="create-a-provisioning-package"></a>Sağlama paketi oluşturma

1. Microsoft Mağazası'ndan [Windows Yapılandırma Tasarımcısı (WCD)](https://www.microsoft.com/store/apps/9nblggh4tx22) uygulamasını indirin.
   ![Windows Yapılandırma Tasarımcısı uygulama mağazasının ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-store.png)

2. **Windows Yapılandırma Tasarımcısı** uygulamasını açın ve **Masaüstü cihazları sağla** seçeneğini belirleyin.
   ![Windows Yapılandırma Tasarımcısı uygulamasında Masaüstü cihazları sağla seçeneğini belirlemenin ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-select.png)

3. Aşağıdaki bilgileri belirttiğiniz **Yeni proje** penceresi açılır:
   - **Ad** - Projenizin adı
   - **Proje klasörü** - Projenin kaydetme konumu
   - **Açıklama** - Proje için isteğe bağlı bir açıklama ![Windows Yapılandırma Tasarımcısı uygulamasında ad, proje klasörü ve açıklama belirtilen ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-name.png)

4. Cihazlarınız için benzersiz bir ad girin. Adlar bir seri numarası (%SERIAL%) veya rastgele bir karakter kümesi içerebilir. İsteğe bağlı olarak Windows sürümünü yükseltiyor, cihazı paylaşımlı kullanım için yapılandırıyor ve önceden yüklenmiş yazılımları kaldırıyorsanız bir ürün anahtarı girebilirsiniz.
   
   ![Windows Yapılandırma Tasarımcısı uygulamasında ad ve ürün anahtarı belirtme ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-device.png)

5. İsteğe bağlı olarak, cihazları ilk kez başlattığınızda bağlanacakları Wi-Fi ağını yapılandırabilirsiniz.  Ağ cihazları yapılandırılmadıysa, cihaz ilk başlatıldığında kablolu bir ağ bağlantısı gerekir.
   ![Windows Yapılandırma Tasarımcısı uygulamasında Ağ SSID’si ve Ağ türü seçeneklerini içeren Wi-Fi etkinleştirme ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-network.png)

6. **Azure AD'ye Kaydet**’i seçin, bir **Toplu Belirteç Süre Sonu** tarihi girin ve ardından **Toplu Belirteç Al**’ı seçin.
   ![Windows Yapılandırma Tasarımcısı uygulamasında hesap yönetiminin ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-account.png)

7. Bir toplu belirteç almak için Azure AD kimlik bilgilerinizi sağlayın.
   ![Windows Yapılandırma Tasarımcısı uygulamasında oturum açma ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-cred.png)

8. Bu **hesabı bu cihazda her yerde kullan** sayfasında, **yalnızca bu uygulamayı**seçin.

9. **Toplu Belirteç** başarıyla alındığında **İleri**’ye tıklayın.

10. İsteğe bağlı olarak, **Uygulama ekleyebilir** ve **Sertifika ekleyebilirsiniz**. Bu uygulamalar ve sertifikalar cihazda sağlanır.

11. İsteğe bağlı olarak, sağlama paketinizi parola ile koruyabilirsiniz.  **Oluştur**' a tıklayın.
    ![Windows Yapılandırma Tasarımcısı uygulamasında paket koruması ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-create.png)

## <a name="provision-devices"></a>Cihaz sağlama

1. Uygulamada belirtilen **Proje klasörü** içinde belirtilen konumdaki sağlama paketine erişin.

2. Sağlama paketini cihaza nasıl uygulayacağınızı seçin.  Sağlama paketi bir cihaza aşağıdaki yollardan biriyle uygulanabilir:
   - Sağlama paketini bir USB sürücüye yerleştirin, USB sürücüyü toplu kaydetmek istediğiniz cihaza yerleştirin ve ilk kurulum sırasında uygulayın
   - Sağlama paketini bir ağ klasörüne yerleştirin ve ilk kurulumdan sonra uygulayın

   Sağlama paketi uygulama ile ilgili adım adım yönergeler için bkz. [Sağlama paketi uygulama](https://technet.microsoft.com/itpro/windows/configure/provisioning-apply-package).

3. Paketi uyguladıktan sonra, cihaz bir dakika içinde otomatik olarak yeniden başlatılır.
   ![Windows Yapılandırma Tasarımcısı uygulamasında ad, proje klasörü ve açıklama belirtilen ekran görüntüsü](./media/windows-bulk-enroll/bulk-enroll-add.png)

4. Cihaz yeniden başlatıldığında, Azure Active Directory'ye bağlanır ve Microsoft Intune’a kaydedilir.

## <a name="troubleshooting-windows-bulk-enrollment"></a>Windows toplu kayıt için sorun giderme

### <a name="provisioning-issues"></a>Sağlama sorunları
Sağlama, yeni Windows cihazlarda kullanılmak üzere tasarlanmıştır. Sağlama hataları cihazın silinmesini veya bir önyükleme görüntüsünden kurtarılmasını gerektirebilir. Bu örneklerde sağlama hatalarının bazı nedenleri açıklanır:

- Yerel bir hesap oluşturmayan bir Active Directory etki alanına veya Azure Active Directory kiracısına katılmayı deneyen bir sağlama paketinin, ağ bağlantısı olmaması nedeniyle etki alanına katılma işlemi başarısız olursa cihaza ulaşılamayabilir.
- Sağlama paketi tarafından çalıştırılan betikler, sistem bağlamında çalıştırılır. Betikler cihaz dosya sisteminde ve yapılandırmalarında rastgele değişiklikler yapabilir. Kötü amaçlı veya hatalı bir betik, cihazın yalnızca yeniden görüntü oluşturma veya silinme yollarıyla kurtarılabilecek bir duruma gelmesine neden olabilir.

Olay Görüntüleyicisi içindeki **sağlama-tanılama-sağlayıcı** Yönetim günlüğünde paketinizdeki ayarların başarısını/başarısız olup olmadığını kontrol edebilirsiniz.

### <a name="bulk-enrollment-with-wi-fi"></a>Wi-Fi ile toplu kayıt 

Açık bir ağ kullanmadığınız durumlarda, bağlantıları başlatmak için [cihaz düzeyinde sertifikalar](../protect/certificates-configure.md) kullanmanız gerekir. Toplu kayıtlı cihazlar, ağ erişimi için kullanıcı hedefli sertifikalara kullanamaz. 

### <a name="conditional-access"></a>Koşullu Erişim
Toplu kayıt kullanılarak kaydedilen Windows cihazları için koşullu erişim kullanılamaz.
