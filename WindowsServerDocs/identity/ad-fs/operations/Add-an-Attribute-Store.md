---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: 属性ストアを追加する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b197268de3c5335e30c2a24a74c5a7b01224b500
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859695"
---
# <a name="add-an-attribute-store"></a>属性ストアを追加する


Active Directory フェデレーションサービス (AD FS) \(AD FS\) によって保護されているリソースへのアクセスを必要とするユーザーアカウントとコンピューターアカウントは、Active Directory Domain Services \(AD DS\)などの属性ストアに格納されます。 要求発行エンジンは、属性ストアを使用して、要求を発行するために必要なデータを収集します。 その後、属性ストアからのデータが要求として投影されます。  
  
属性ストアをフェデレーションサービスに追加するには、次の手順を実行します。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-an-attribute-store"></a>属性ストアを追加するには  
  
1.  **AD FS 管理**を開きます。  
  
2.  **[アクション]** で **[属性ストアの追加]** をクリックします。  

![属性ストアの追加](media/Add-an-Attribute-Store/addstore1.PNG)
  
3. **[属性ストアの追加]** ダイアログボックスで、追加する属性ストアの次のプロパティを構成します。  
  
   -   **[表示名]** に、属性ストアを識別するために使用する名前を入力します。  
  
   -   **[属性ストアの種類]** で、サポートされている属性ストアの種類として、 **Active Directory**、 **LDAP**、または**SQL**のいずれかを選択します。  
  
   -   **[接続文字列]** で、ライトウェイトディレクトリアクセスプロトコル \(LDAP\) ストア、または構造化照会言語 \(SQL\) ストアのいずれかを選択した場合は、属性ストアへの接続を確立するために使用した文字列を入力します。 Active Directory の属性ストアの場合、接続文字列は必要ありません。このため、このフィールドは無効になっています。  
  
       > [!NOTE]  
       > AD FS の既定の設定では、Active Directory 属性ストアが自動的に作成されます。  
 
![属性ストアの追加](media/Add-an-Attribute-Store/addstore2.PNG) 

4. **[OK]** をクリックすると、  
  
## <a name="additional-references"></a>その他の参照情報  

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
  
[属性ストアの役割](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
