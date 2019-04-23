---
title: AD フォレストの回復 - DC のコンピューター アカウントをリセットします。
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adds
ms.openlocfilehash: 388b460196888d4ca0cd12218972197afb6d49c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852763"
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>AD フォレストの回復 - DC のコンピューター アカウントをリセットします。

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

 DC のコンピューター アカウントのパスワードをリセットするのにには、次の手順を使用します。 
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>ドメイン コント ローラーのコンピューター アカウントのパスワードをリセットするには  

1. コマンド プロンプトで次のコマンドを入力し、Enter キーを押します。  

   ```
   netdom help resetpwd  
   ```
  
2. このコマンドは、Netdom コマンド ライン ツールを使用して、たとえば、コンピューター アカウントのパスワードをリセットすることの構文を使用します。  

   ```
   netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
   ```  
  
    場所*ドメイン コント ローラー名*ローカル dc は、回復中です。 
  
   > [!NOTE]
   > このコマンドは、2 回実行する必要があります。
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
