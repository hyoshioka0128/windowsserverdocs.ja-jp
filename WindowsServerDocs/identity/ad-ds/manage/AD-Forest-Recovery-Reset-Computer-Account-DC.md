---
title: AD フォレストの回復-DC でコンピューターアカウントをリセットする
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.openlocfilehash: 3d779e989c4414629c9a7414adf41c96525368c4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969839"
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
