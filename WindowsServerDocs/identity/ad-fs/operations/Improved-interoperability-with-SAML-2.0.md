---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: "SAML 2.0 との相互運用性"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4f55eaacec8ee0eb41e1980f1aa15c6256f8b979
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="improved-interoperability-with-saml-20"></a>SAML 2.0 との相互運用性

>Windows Server 2016 の適用対象:

  
Windows Server 2016 での AD FS には、メタデータを含む複数のエンティティに基づく信頼をインポートするためのサポートを含む追加の SAML プロトコルのサポートが含まれています。  これにより、AD FS confederations InCommon フェデレーションおよび eGov 2.0 標準に準拠しているその他の実装などへの参加を構成することができます。   
  
新しい機能は、証明書利用者の要求プロバイダー信頼グループに基づいています。 各グループは、1 つまたは複数の EntityDescriptor 要素を含むように、eGov で 2.0 のプロファイルに指定された EntitiesDescriptor (< md:EntitiesDescriptor >) 要素です。  グループに共通の承認規則があるし、個々 の信頼オブジェクトと同様に、その他のすべてのプロパティを変更できます。  
  
信頼グループは、AD FS にインポートされてと AD FS はメタデータ ドキュメントに基づくグループとしての信頼関係を自動的に更新します。  
  
これらのシナリオを有効にするとは、オブジェクトを使用して新しい PowerShell コマンドレットを追加および削除 AdfsClaimsProviderTrustsGroup AdfsRelyingPartyTrustsGroup と同じくらい簡単です。 これを行うメタデータ URL またはファイルを使用して次の例に示すようにします。  
  
また、AD FS 2016 では、SAML コア仕様、3.4.1.2] セクションで説明するようにスコープ パラメーターのサポートがあります。 この要素は、証明書利用者のパーティがいずれかを指定するか、認証用の複数の id プロバイダーの要求を使用します。  
  
## <a name="examples"></a>例  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>参照  
  
EGov 2.0 プロファイルはあります[次のとおりです。](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
SAML コア仕様を参照して[次のとおりです。](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


