---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: SAML 2.0 との相互運用性の向上
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4f55eaacec8ee0eb41e1980f1aa15c6256f8b979
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818733"
---
# <a name="improved-interoperability-with-saml-20"></a>SAML 2.0 との相互運用性の向上

>適用先:Windows Server 2016

  
Windows Server 2016 での AD FS には、複数のエンティティが格納されたメタデータに基づく信頼をインポートするためのサポートを含むその他の SAML プロトコルのサポートが含まれています。  これにより、confederations InCommon フェデレーションと eGov 2.0 標準に準拠している他の実装などに参加する AD FS を構成することができます。   
  
新しい機能は、証明書利用者または要求プロバイダー信頼のグループに基づいています。 各グループは、1 つまたは複数の EntityDescriptor 要素を含むように、2.0 プロファイル、eGov で指定された EntitiesDescriptor (< md:EntitiesDescriptor >) 要素です。  グループは共通の承認規則を持ち、その他のすべてのプロパティは、個々 の信頼オブジェクトのように変更できます。  
  
信頼グループが AD FS にインポートすると AD FS は、メタデータ ドキュメントに基づくグループとして、信頼関係を自動的に更新します。  
  
これらのシナリオを有効にすることは、その追加および削除 AdfsClaimsProviderTrustsGroup AdfsRelyingPartyTrustsGroup オブジェクトの新しい PowerShell コマンドレットを使用して同じくらい簡単です。 これ行う次の例に示すように、メタデータ URL またはファイルを使用します。  
  
さらに、AD FS 2016 SAML のコア仕様、3.4.1.2 セクションで説明されている、スコープのパラメーターをサポートしています。 この要素は、1 つ指定するパーティが証明書利用者または他の id プロバイダー、認証要求を使用します。  
  
## <a name="examples"></a>例  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>参考資料  
  
EGov 2.0 プロファイルが見つかります[ここです。](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
SAML のコア仕様を参照して[ここです。](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


