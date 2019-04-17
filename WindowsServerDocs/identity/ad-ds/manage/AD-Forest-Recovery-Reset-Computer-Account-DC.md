---
title: "AD フォレストの回復 - DC でコンピューター アカウントをリセットします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adfs
ms.openlocfilehash: 588510a27f56abb4497b2f80fa0281a858a7e8eb
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>AD フォレストの回復 - DC でコンピューター アカウントをリセットします。 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 DC のコンピューター アカウントのパスワードをリセットするのにには、次の手順を使用します。  
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>ドメイン コントローラーのコンピューター アカウントのパスワードをリセットするには  
  
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    netdom help resetpwd  
    ```  
  
2.  このコマンドは、たとえば、コンピューター アカウントのパスワードをリセットする Netdom コマンド ライン ツールを使用するための構文を使用します。  
  
    ```  
    netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
    ```  
  
     ここで*ドメイン コントローラー名*回復しているローカルの dc です。  
  
    > [!NOTE]
    >  このコマンドは、2 回実行する必要があります。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
