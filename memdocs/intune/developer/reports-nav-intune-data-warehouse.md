---
title: Intune Veri Ambarı API’si
titleSuffix: Microsoft Intune
description: Kuruluşunuzun mobil ortamı hakkında öngörü sağlayan raporlar derlemek için Intune Veri Ambarı API’sini kullanabilirsiniz.
keywords: Intune Veri Ambarı
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 701D6CE9-43F6-4A29-8E84-E2B59931C635
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: d55e683d1e0d64eb24f9b9225cd58ff261de6389
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988539"
---
# <a name="microsoft-intune-data-warehouse-api"></a>Microsoft Intune veri ambarı API 'SI

Intune Veri Ambarı API’si, Intune verilerinizin makine tarafından okunabilir bir biçimine erişmenize ve bu verileri sık kullandığınız analiz aracında kullanmanıza olanak tanır. Kurumsal mobil ortamınızla ilgili öngörüler sağlayan raporlar oluşturmak için bu API’yi kullanabilirsiniz. API, aşağıdakiler için standart desenler izleyen OData protokolünü kullanır:

- İstek ve yanıt üst bilgileri
- Durum kodları
- HTTP yöntemleri
- URL kuralları
- Medya türleri
- Yük biçimleri
- Sorgu seçenekleri

Bir OASIS (Organization for the Advancement of Structured Information Standards) standardı olan OData (Açık Veri Protokolü), bu RESTful API’leri oluşturmaya ve kullanmaya yönelik en iyi yöntemleri tanımlar. Intune Veri Ambarı, OData 4.0 sürümünü kullanır.

Bu başvuru bölümünde, uç noktalar, desteklenen HTTP yöntemleri, dönüş yükü biçimleri ve Intune Veri Ambarı veri modelinin belgeleri genel hatlarıyla özetlenir.

> [!Important]  
> Beta sürümünü kullanarak Veri Ambarı’nın en son işlevlerini deneyebilirsiniz. Beta sürümünü kullanabilmeniz için URL’nizin `api-version=beta` sorgu parametresini içermesi gerekir. Özellikler, desteklenen bir hizmet olarak herkesin kullanımına açılmadan önce beta sürümünde sunulur. Intune yeni özellikler ekledikçe beta sürümünün davranışında ve veri anlaşmalarında değişiklikler olabilir. Beta sürümüne bağımlı herhangi bir özel kod veya raporlama araçları, devam eden güncelleştirmelerle birlikte kesilebilir. <!--If you experience problems with the beta service, follow [link to feedback process]() to report the issue or provide feedback.-->

## <a name="odata-custom-client"></a>OData özel istemcisi

Intune Veri Ambarı veri modeline, RESTful uç noktaları yoluyla erişebilirsiniz. Verilerinize erişim kazanmak için istemcinizin OAuth 2.0 kullanarak Azure Active Directory’de (Azure AD) yetkilendirilmesi gerekir. Önce Azure’da bir web uygulaması ve istemci uygulaması ayarlar ve istemciye izinler verirsiniz. Yerel istemciniz yetkilendirilir ve daha sonra Veri Ambarı uç noktaları ile iletişime geçebilir.

Daha fazla bilgi için bkz [. Rest istemcisi Ile veri AMBARı API 'sinden veri edinme](reports-proc-data-rest.md)

> [!Note]  
> Kod örnekleri için GitHub’da [GitHub Intune Veri Ambarı deposuna](https://github.com/Microsoft/Intune-Data-Warehouse) erişebilirsiniz.

## <a name="interacting-with-the-api"></a>API ile etkileşim kurma

API, Azure AD ile yetkilendirme gerektirir. Azure AD, OAuth 2.0 kullanır. Yetkilendirmenin ardından, HTTP GET fiili kullanarak ve kullanıma sunulan varlık koleksiyonları ile bağlantı kurarak API’den veri alabilirsiniz. Ayrıntılar için şu başlıkları inceleyin:

- [Yetkilendirme](reports-api-url.md#authorization)
- [API URL Yapısı](reports-api-url.md#api-url-structure)

## <a name="intune-data-warehouse-data-model"></a>Intune Veri Ambarı veri modeli

OData, istemcilerin herhangi bir veri kaynağı tarafından kullanıma sunulan bilgilere erişmesine olanak tanıyan soyut bir veri modeli ve bir protokol tanımlar. Veri modeli belgeleri konusunda, ad alanları, varlıklar ve Intune Veri Ambarı veri modelindeki dönüş nesneleri açıklanır. Daha fazla bilgi için bkz. [Veri Ambarı Veri Modeli](reports-ref-data-model.md).

## <a name="next-steps"></a>Sonraki adımlar

[Azure AD için Kimlik Doğrulaması Senaryoları](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) makalesini okuyarak Azure AD ile çalışma hakkında daha fazla bilgi edinin.

[odata.org](https://www.odata.org)’da OData kaynaklarını bulabilirsiniz.
  
OData Sürüm 4.0 standardını gözden geçirin: [OData Sürüm 4.0] (https://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html)  
