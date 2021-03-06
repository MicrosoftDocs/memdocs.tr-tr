---
title: Hızlı Başlangıç - Intune'da otomatik kayıt ayarlama
description: Hızlı Başlangıç - Intune'da Windows 10 cihazları için otomatik kayıt ayarlayın.
services: microsoft-intune
author: ErikjeMS
manager: dougeby
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 01/17/2020
ms.author: erikje
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 599a5f6e6e355a37e909182fc14a07d489f45558
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86872044"
---
# <a name="quickstart-set-up-automatic-enrollment-for-windows-10-devices"></a>Hızlı Başlangıç: Windows 10 cihazları için otomatik kayıt ayarlama

Bu hızlı başlangıçta Microsoft Intune'u, belirli kullanıcılar Windows 10 cihazlarında oturum açtığında bu cihazları otomatik kaydetmeye ayarlayacaksınız.

Intune aboneliğiniz yoksa [ücretsiz deneme hesabı için kaydolun](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Önkoşullar

- Microsoft Intune Abonelik- [ücretsiz deneme hesabı için kaydolun](../fundamentals/free-trial-sign-up.md).
- Bu hızlı başlangıcı tamamlamak için önce [bir kullanıcı oluşturun](../fundamentals/quickstart-create-user.md) ve [bir grup oluşturun](../fundamentals/quickstart-create-group.md).

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Microsoft uç nokta yöneticisinde Intune 'da oturum açma

[Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) genel yönetici veya Intune Yöneticisi olarak oturum açın. Intune Deneme aboneliği oluşturduysanız aboneliği oluşturduğunuz hesap Genel yönetici rolüne sahip olur.

## <a name="set-up-windows-10-automatic-enrollment"></a>Windows 10 otomatik kaydını ayarlama

Bu örnekte kurumsal ve kendi cihazını getir türü cihazların otomatik kaydolabilmesi için MDM kaydını kullanacaksınız. Ücretsiz bir Azure Active Directory Premium aboneliğine kaydolacaksınız.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **tüm hizmetler**  >  **M365 Azure Active Directory**  >  **Azure Active Directory**  >  **Mobility (MDM ve MAM)** öğesini seçin.
2. **Bu özelliği kullanmak için ücretsiz bir Premium deneme sürümü edinin** seçeneğini belirleyin. Bu seçeneğin belirlenmesi, Azure Active Directory ücretsiz Premium deneme sürümü kullanılarak otomatik kayıt yapılmasına imkan verir. 

    ![Azure Active Directory ücretsiz Premium deneme sürümünü seçin](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-01.png)

3. **Enterprise Mobility + Security E5** ücretsiz deneme seçeneğine tıklayın. 
4. Ücretsiz **deneme**sürümünü  >  **etkinleştirme** ücretsiz deneme sürümünü etkinleştirin.

    ![Enterprise Mobility + Security E5 ücretsiz deneme sürümünü seçin](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-02.png)

    > [!NOTE]
    > Etkinleştirilmesi bir dakika sürebilir. 

3. Intune 'U yapılandırmak için **Microsoft Intune** ' ı seçin. 

    ![Listeden Microsoft Intune’u seçin](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-03.png)

4. Çalışanlarınızın Windows cihazlarındaki kurumsal verileri yönetmek için MDM otomatik kaydı kullanmak üzere **MDM kullanıcı kapsamı** olarak **Bazıları**’nı seçin. MDM otomatik kaydı, AAD’ye katılmış cihazlar ve kendi cihazını getir senaryoları için yapılandırılır.

    ![Yapılandırma listesinden “Bazıları”nı seçin](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-04.png)

5. **Grup Seç**  >  **contoso sınayıcıları**  >  atanan grup olarak**Seç** ' e tıklayın.

    ![Kaydedilecek grubu seçin](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-05.png)

6. İş gücünüzün cihazlarında verileri yönetmek için **MAM Kullanıcıları kapsamı**’nı **Bazıları** olarak belirleyin.

    ![Kaydedilecek grubu seçin](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-06.png)

7. **Grup Seç**  >  **contoso sınayıcıları**  >  atanan grup olarak**Seç ' i** seçin. 
8. Geri kalan yapılandırma değerleri için varsayılan değerleri kullanabilirsiniz.
9. **Kaydet**'i seçin.

## <a name="clean-up-resources"></a>Kaynakları temizleme

Intune otomatik kaydını yeniden yapılandırmak için [Windows cihazları için kayıt ayarlama](windows-enroll.md)'ya bakın.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta Windows 10 cihazları için otomatik kaydı ayarlamayı öğrendiniz. Cihaz kaydı hakkında daha fazla bilgi için bkz. [Cihaz kaydı nedir?](device-enrollment.md)

Bu Intune hızlı başlangıç serisini takip etmek için bir sonraki hızlı başlangıca ilerleyin.

> [!div class="nextstepaction"]
> [Hızlı Başlangıç: Windows 10 cihazınızı kaydetme](quickstart-enroll-windows-device.md)
