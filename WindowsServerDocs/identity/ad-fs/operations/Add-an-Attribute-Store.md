---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: 属性ストアを追加する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0f5c9d3b0f856ab72a16930ddb5c50686d747ecc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358388"
---
# <a name="add-an-attribute-store"></a>属性ストアを追加する


@No__t-0AD FS @ no__t によっ Active Directory フェデレーションサービス (AD FS) て保護されているリソースへのアクセスを必要とするユーザーアカウントとコンピューターアカウントは、Active Directory Domain Services \(AD DS @ no__t のように、属性ストアに格納されます。 要求発行エンジンは、属性ストアを使用して、要求を発行するために必要なデータを収集します。 その後、属性ストアからのデータが要求として投影されます。  
  
属性ストアをフェデレーションサービスに追加するには、次の手順を実行します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-an-attribute-store"></a>属性ストアを追加するには  
  
1.  **AD FS 管理**を開きます。  
  
2.  **[アクション]** で **[属性ストアの追加]** をクリックします。  

![属性ストアの追加](media/Add-an-Attribute-Store/addstore1.PNG)
  
3. **[属性ストアの追加]** ダイアログボックスで、追加する属性ストアの次のプロパティを構成します。  
  
   -   **[表示名]** に、属性ストアを識別するために使用する名前を入力します。  
  
   -   **[属性ストアの種類]** で、サポートされている属性ストアの種類として、 **Active Directory**、 **LDAP**、または**SQL**のいずれかを選択します。  
  
   -   **[接続文字列]** で、ライトウェイトディレクトリアクセスプロトコル \(ldap @ no__t ストアまたは構造化照会言語 \(sql @ no__t ストアのいずれかを選択した場合は、属性への接続を確立するために使用した文字列を入力します。ソース. Active Directory の属性ストアの場合、接続文字列は必要ありません。このため、このフィールドは無効になっています。  
  
       > [!NOTE]  
       > AD FS の既定の設定では、Active Directory 属性ストアが自動的に作成されます。  
 
![属性ストアの追加](media/Add-an-Attribute-Store/addstore2.PNG) 

4. **[OK]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
  
[属性ストアの役割](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
