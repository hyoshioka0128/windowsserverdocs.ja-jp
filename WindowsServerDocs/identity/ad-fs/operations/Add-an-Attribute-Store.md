---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: "属性ストアを追加します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 11baba5bfdb699f120a506feb8361db21d26cff1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-an-attribute-store"></a>属性ストアを追加します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

ユーザー アカウントと Active Directory フェデレーション サービス \(AD FS\) によって保護されているリソースへのアクセスを必要とするコンピューター アカウントは、Active Directory Domain Services \(AD DS\) などの属性ストアに保存されます。 要求発行エンジンでは、属性ストアを使用して、要求を発行するために必要なデータを収集します。 属性ストアからのデータは、信頼性情報として、投影されます。  
  
フェデレーション サービスに属性ストアを追加するのに、次の手順を使用することができます。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-an-attribute-store"></a>属性ストアを追加するには  
  
1.  開いている**AD FS 管理**します。  
  
2.  下にある**操作**クリックして**属性ストアの追加**します。  

![属性ストアを追加します。](media/Add-an-Attribute-Store/addstore1.PNG)
  
3.  **属性ストアの追加**] ダイアログ ボックスで、追加する属性ストアの次のプロパティを構成します。  
  
    -   **表示名**を使用して、属性ストアを識別する名前を入力します。  
  
    -   **属性ストアの種類**、サポートされている属性ストアの種類を選択するか**Active Directory**、**LDAP**、または**SQL**します。  
  
    -   **接続文字列**Lightweight Directory Access Protocol \(LDAP\) ストアまたは構造化照会言語 \(SQL\) ストアでは、いずれかを選択した場合、属性ストアへの接続を確立するために使用する文字列を入力します。 Active Directory 属性ストアでは、接続文字列は必要ありません。そのため、このフィールドは無効です。  
  
        > [!NOTE]  
        > AD FS は、既定では、Active Directory 属性ストアを自動的に作成します。  
 
![属性ストアを追加します。](media/Add-an-Attribute-Store/addstore2.PNG) 

4.  をクリックして**OK**します。  
  
## <a name="additional-references"></a>その他の参照  

[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md)
  
[属性ストアのロール](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
