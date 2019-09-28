---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: SAML 2.0 との相互運用性の向上
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d72636d77fe3240caab66dcab8657225d291bec6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407547"
---
# <a name="improved-interoperability-with-saml-20"></a>SAML 2.0 との相互運用性の向上



  
Windows Server 2016 の AD FS には、複数のエンティティを含むメタデータに基づいて信頼をインポートするためのサポートなど、追加の SAML プロトコルサポートが含まれています。  これにより、InCommon フェデレーションや、eGov 2.0 標準に準拠するその他の実装など、confederations に参加するように AD FS を構成することができます。   
  
新しい機能は、証明書利用者または要求プロバイダー信頼のグループに基づいています。 各グループは、eGov 2.0 プロファイルで指定された EntitiesDescriptor (< md: EntitiesDescriptor >) 要素で、1つまたは複数の EntityDescriptor 要素を含みます。  グループには一般的な承認規則があり、その他のすべてのプロパティは、個々の信頼オブジェクトと同様に変更できます。  
  
信頼グループが AD FS にインポートされると、AD FS によって、メタデータドキュメントに基づいて信頼がグループとして自動的に更新されます。  
  
これらのシナリオを有効にすることは、AdfsClaimsProviderTrustsGroup オブジェクトと AdfsRelyingPartyTrustsGroup オブジェクトを追加および削除する新しい PowerShell コマンドレットを使用するのと同じように簡単です。 これを行うには、次の例に示すように、メタデータ URL またはファイルを使用します。  
  
さらに、AD FS 2016 では、「SAML コア仕様」セクション3.4.1.2 で説明されているように、スコープパラメーターがサポートされています。 この要素により、証明書利用者は認証要求に1つ以上の id プロバイダーを指定できます。  
  
## <a name="examples"></a>使用例  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>リファレンス  
  
EGov 2.0 プロファイルについては、こちらを参照[してください。](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
SAML コア仕様については、こちらを参照[してください。](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


