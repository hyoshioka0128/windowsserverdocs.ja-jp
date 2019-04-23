---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: 属性ストアを追加する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 11baba5bfdb699f120a506feb8361db21d26cff1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837863"
---
# <a name="add-an-attribute-store"></a>属性ストアを追加する

>適用先:Windows Server 2016、Windows Server 2012 R2

ユーザー アカウントとコンピューター アカウントを Active Directory フェデレーション サービスによって保護されているリソースへのアクセスを必要とする\(AD FS\)は、Active Directory Domain Services などの属性ストアに格納されている\(AD DS\). 要求発行エンジンでは、属性ストアを使用して、要求を発行するために必要なデータを収集します。 属性ストアからデータを要求として投影されます。  
  
次の手順を使用して、属性ストアをフェデレーション サービスに追加することができます。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-an-attribute-store"></a>属性ストアを追加するには  
  
1.  開いている**AD FS 管理**します。  
  
2.  **アクション**クリックして**属性ストアを追加**します。  

![属性ストアを追加します。](media/Add-an-Attribute-Store/addstore1.PNG)
  
3.  **属性ストアを追加** ダイアログ ボックスで、属性ストアに追加するは、次のプロパティを構成します。  
  
    -   **表示名**、属性ストアを識別するために使用する名前を入力します。  
  
    -   **属性ストアの種類**、サポートされている属性ストアの種類を**Active Directory**、 **LDAP**、または**SQL**します。  
  
    -   **接続文字列**か、ライトウェイト ディレクトリ アクセス プロトコルを選択した場合、 \(LDAP\)ストアまたは構造化照会言語\(SQL\)ストア、文字列を入力します属性ストアへの接続を確立するために使用することです。 Active Directory 属性ストアの場合、接続文字列は必要ありません。そのため、このフィールドは無効になります。  
  
        > [!NOTE]  
        > AD FS の既定の設定では、Active Directory 属性ストアが自動的に作成されます。  
 
![属性ストアを追加します。](media/Add-an-Attribute-Store/addstore2.PNG) 

4.  **[OK]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
  
[属性ストアの役割](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
