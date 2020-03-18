---
title: Öğretici - Intune’a cihaz kaydetmek için Autopilot kullanma
titleSuffix: Microsoft Intune
description: Bu öğreticide Intune'a cihaz kaydetmek için Windows Autopilot’ı ayarlayacaksınız.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/19/2018
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
Customer intent: As an Intune admin, I want to set up Windows Autopilot so that users can enroll in Intune.
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c4c6660138df0c05975b1fc6b093c41600c0547
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79327030"
---
# <a name="tutorial-use-autopilot-to-enroll-windows-devices-in-intune"></a>Öğretici - Intune’a cihaz kaydetmek için Windows Autopilot kullanma

Windows Autopilot, cihaz kaydını basitleştirir. Microsoft Intune ve Autopilot ile özel işletim sistemi görüntüleri oluşturmanıza, bu görüntüleri cihazlara uygulamanıza ve bunların bakımını yapmanıza gerek kalmadan son kullanıcılarınıza yeni cihazlar verebilirsiniz.

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:
> [!div class="checklist"]
> * Intune’a cihaz ekleme
> * Bir Autopilot cihaz grubu oluşturma
> * Bir Autopilot dağıtım profili oluşturma
> * Autopilot dağıtım profilini cihaz grubuna atama
> * Kullanıcılara Windows cihazlar dağıtma

Intune aboneliğiniz yoksa [ücretsiz deneme hesabı için kaydolun](../fundamentals/free-trial-sign-up.md).

Autopilot faydalarına, senaryolarına ve önkoşullarına genel bir bakış için bkz. [Windows Autopilot’a genel bakış](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot).


## <a name="prerequisites"></a>Önkoşullar
- [Windows otomatik kaydını ayarlama](quickstart-setup-auto-enrollment.md)
- [Azure Active Directory Premium aboneliği](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->


## <a name="add-devices"></a>Cihazları ekleme

Windows Autopilot’ı ayarlamanın ilk adımı, Windows cihazları Intune’a eklemektir. Tek yapmanız gereken, bir CSV dosyası oluşturmak ve bunu Intune’a aktarmaktır.

1. Herhangi bir metin düzenleyicide Windows cihazları belirleyen, virgülle ayrılmış değerler (CSV) listesi oluşturun. Şu biçimi kullanın:
    
    *seri numarası*, *Windows-ürün kimliği*, *Donanım karması*, *isteğe bağlı-Grup-etiketi*
    
    İlk üç öğe gereklidir, ancak Grup etiketi (daha önce bilinen "Order ID") isteğe bağlıdır.

2. CSV dosyasını kaydedin.

3. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar** > **Windows** > **cihazları** ' nı ( **Windows Autopilot dağıtım > programı** ' nın altında **içeri aktar**' ı seçin.

    ![Windows Autopilot cihazlarının ekran görüntüsü](./media/enrollment-autopilot/autopilot-import-device.png)

4. **Windows Autopilot cihazlar ekle** altında kaydettiğiniz CSV dosyasına göz atın.

    ![Windows Autopilot cihazları ekleme ekran görüntüsü](./media/tutorial-use-autopilot-enroll-devices/autopilot-import-device2.png)

5. Cihaz bilgilerini içeri aktarmayı başlatmak için **İçeri Aktar**'ı seçin. İçeri aktarma birkaç dakika sürebilir.

4. İçeri aktarma işlemi tamamlandıktan sonra **windows > Windows** **kayıt** > **cihazları** > **cihazlar** ' ı ( **Windows Autopilot dağıtım > programı** ' nın altında **Eşitle**) seçin. Eşitlemenin devam ettiğini gösteren bir ileti görüntülenir. Kaç tane cihaz eşitlediğinize bağlı olarak işlemin tamamlanması birkaç dakikayı bulabilir.

5. Yeni cihazları görmek için görüntüyü yenileyin.

## <a name="create-an-autopilot-device-group"></a>Bir Autopilot cihaz grubu oluşturma

Daha sonra bir cihaz grubu oluşturacak ve az önce yüklediğiniz Autopilot cihazları buraya koyacaksınız.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **gruplar** > **Yeni Grup**' u seçin.
2. **Gruplar** dikey penceresinde:
    1. **Grup türü** olarak **Güvenlik**’i seçin.
    2. **Grup adı** olarak *Autopilot Grubu* yazın. **Grup açıklaması** olarak *Autopilot cihazlar için test grubu* yazın.
    3. **Üyelik türü** olarak **Atanan**’ı seçin.
3. **Grup** dikey penceresinde **Üyeler**’i seçin ve Autopilot cihazları gruba ekleyin. Henüz kaydedilmemiş Autopilot cihazları, adın cihaz seri numarası olduğu cihazlardır.
4. **Oluştur**’u seçin.  

## <a name="create-an-autopilot-deployment-profile"></a>Bir Autopilot dağıtım profili oluşturma

Bir cihaz grubu oluşturduktan sonra, Autopilot cihazları yapılandırabilmek için bir dağıtım profili oluşturmalısınız.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde, **Windows** > **windows kayıt** > **dağıtım profilleri** > **Profil oluştur** > **cihazlar** ' ı seçin.
2. **Temel bilgiler** sayfasında, **ad**için *Autopilot profilini*girin. **Açıklama** olarak *Autopilot cihazlar için test profili* yazın.
3. **Tüm hedeflenen cihazları Autopilot’a dönüştür** ayarını **Evet** olarak seçin. Bu ayar, listedeki tüm cihazların Autopilot dağıtım hizmetine kaydolmasını sağlar. Kaydın işlenmesi için 48 saat kadar bekleyin.
4. **İleri**'yi seçin.
5. **Kullanıma hazır deneyim (OOBE)** sayfasında, **dağıtım modu**için **Kullanıcı odaklı**' ı seçin. Bu profile sahip cihazlar, cihazı kaydeden kullanıcı ile ilişkilidir. Cihazı kaydetmek için kullanıcı kimlik bilgileri gerekir.
6. **Azure AD’ye farklı katıl** kutusunda **Azure AD katılımlı**’yı seçin.
7. Aşağıdaki seçenekleri yapılandırın ve diğer ayarları varsayılan olarak bırakın:
    - **Son Kullanıcı Lisans Sözleşmesi (EULA)** : **Gizle**
    - **Gizlilik ayarları**: **Göster**
    - **Kullanıcı hesabı türü**: **Standart**
8. **İleri**'yi seçin.
9. **Atamalar** sayfasında, **ata**için **Seçili gruplar** ' ı seçin.
10. **Dahil edilecek grupları seç**' i seçin, **Autopilot grubu**' nu seçin.
11. **İleri**'yi seçin.
12. Profili oluşturmak için **gözden geçir + oluştur** sayfasında **Oluştur** ' u seçin.

## <a name="distribute-devices-to-users"></a>Cihazları kullanıcılara dağıtma

Artık kullanıcılara Windows cihazları dağıtabilirsiniz. Kullanıcılar ilk oturum açtığında, Autopilot sistemi cihazları otomatik olarak kaydedecek ve yapılandıracaktır. 

## <a name="clean-up-resources"></a>Kaynakları temizleme

Artık Autopilot cihazlarını kullanmak istemiyorsanız, bunları silebilirsiniz.

1. Cihazlar Intune’a kayıtlıysa önce bunları [Azure Active Directory portalından silmeniz](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal) gerekir.

2. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **Windows > ** **Windows kayıt** > **cihazlar** > **cihazlar** ' ı ( **Windows Autopilot dağıtım programı**altında) seçin.

3. Silmek istediğiniz cihazları seçin ve **Sil**' i seçin.

4. **Evet**'i seçerek silme işlemini onaylayın. Silme işlemi birkaç dakika sürebilir.

## <a name="next-steps"></a>Sonraki adımlar

Windows Autopilot için kullanılabilir diğer seçenekler hakkında daha fazla bilgi edinebilirsiniz.

> [!div class="nextstepaction"]
> [Ayrıntılı Autopilot kaydı makalesi](enrollment-autopilot.md)


