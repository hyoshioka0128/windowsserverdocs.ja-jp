---
title: AD フォレストの回復-DC でコンピューターアカウントをリセットする
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adds
ms.openlocfilehash: 320d02f789b8dda771b648b0aa9a58f545f3358b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368869"
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>AD フォレストの回復-DC でコンピューターアカウントをリセットする

>適用先:Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

 DC のコンピューターアカウントのパスワードをリセットするには、次の手順に従います。 
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>ドメインコントローラーのコンピューターアカウントのパスワードをリセットするには  

1. コマンド プロンプトで次のコマンドを入力し、Enter キーを押します。  

   ```
   netdom help resetpwd  
   ```
  
2. 次の例のように、Netdom コマンドラインツールを使用してコンピューターアカウントのパスワードをリセットするために、このコマンドで提供される構文を使用します。  

   ```
   netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
   ```  
  
    ここで、*ドメインコントローラー名*は、回復しているローカル DC です。 
  
   > [!NOTE]
   > このコマンドは2回実行する必要があります。
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
