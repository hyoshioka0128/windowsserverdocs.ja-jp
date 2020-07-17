---
title: AD フォレストの回復-DC でコンピューターアカウントをリセットする
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adds
ms.openlocfilehash: 80bdf4bd78b1d4cd678ff09dc2e7326a290032dd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823715"
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>AD フォレストの回復-DC でコンピューターアカウントをリセットする

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

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
