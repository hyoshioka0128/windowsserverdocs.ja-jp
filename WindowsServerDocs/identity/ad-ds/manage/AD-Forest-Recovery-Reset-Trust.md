---
title: AD フォレストの回復の完全なサーバーをバックアップします。
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: 455c930a90cd443cf1fe62f436abca88384f79c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865563"
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>信頼関係の 1 つの側での信頼のパスワードをリセットします。  

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

 フォレストの回復はセキュリティ違反に関連付けられている場合は、信頼関係の 1 つの側での信頼のパスワードをリセットする、次の手順を使用します。 これには、子と親ドメインと、このドメイン (信頼されるドメイン) と別のドメイン (信頼されたドメイン) の間の明示的な信頼での暗黙的な信頼関係が含まれます。 
  
 入力方向の信頼 (このドメインが属している側) とも呼ばれる、信頼関係の信頼する側のドメイン側のみのパスワードをリセットします。 次に、出力方向の信頼とも呼ばれる、信頼の信頼されたドメインにあるものと同じパスワードを使用します。 (信頼された) の他のドメインのそれぞれの最初の DC を復元するときに、出力方向の信頼のパスワードをリセットします。 
  
 信頼のパスワードのリセットにより、DC は、そのドメインの外部の不適切な可能性のある Dc ではレプリケートされません。 同じ信頼のパスワードを設定すると、各ドメインの最初の DC を復元するときに、このドメイン コント ローラーが復旧された Dc の各にレプリケートすることを確認します。 AD DS をインストールすることによって回復される、ドメイン内のそれ以降の Dc は、インストール プロセス中にこれらの新しいパスワードを自動的にレプリケートされます。 
  
## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>信頼関係の 1 つの側での信頼のパスワードをリセットするには  
  
1. コマンド プロンプトで次のコマンドを入力し、Enter キーを押します。  

   ```  
   netdom experthelp trust  
   ```  
  
2. このコマンドは、NetDom ツールを使用して、信頼のパスワードをリセットすることの構文を使用します。
   たとえば、フォレスト内の 2 つのドメイン: 親と子: 親ドメインで、復元された DC でこのコマンドを実行しているとは、次のコマンド構文を使用します。  

   ```  
   netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
   ```  

   子ドメインでこのコマンドを実行するときは、次のコマンド構文を使用します。  

   ```  
   netdom trust child domain name /domain:parent domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
   ```  

   > [!NOTE]
   > **passwordT**信頼の両側で値が同じである必要があります。 このコマンドを 1 回だけ実行 (とは異なり、 **netdom resetpwd**コマンド) が自動的にパスワードをリセットします 2 回ためです。 
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
