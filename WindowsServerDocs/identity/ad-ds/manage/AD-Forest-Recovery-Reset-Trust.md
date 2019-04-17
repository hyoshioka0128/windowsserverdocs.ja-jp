---
title: "AD フォレストの回復 - フル サーバーのバックアップ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adfs
ms.openlocfilehash: 51b53e7348ae00ed2fc63711b9c3297279ebe033
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>信頼関係の 1 つの側での信頼のパスワードをリセットします。  

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 フォレストの回復はセキュリティ侵害に関連している場合は、信頼関係の 1 つの側での信頼のパスワードをリセットする次の手順を使用します。 これには、子と親ドメイン (信頼する側のドメイン) このドメインと別のドメイン (信頼される側のドメイン) の間に明示的な信頼間の暗黙の信頼が含まれます。  
  
 入力方向の信頼 (このドメインが属している側) とも呼ばれる、信頼の信頼する側のドメイン側のみのパスワードをリセットします。 次に、出力方向の信頼とも呼ばれる、信頼の信頼されたドメインにある同じパスワードを使用します。 各 (信頼される側) のドメインの最初の DC を復元する場合は、出力方向の信頼のパスワードをリセットします。  
  
 信頼のパスワードをリセットするにより、ドメイン コントローラーは、そのドメインの外部の正しくない可能性のあるドメイン コントローラーではレプリケートされません。 各ドメインの最初の DC の復元中に同じ信頼のパスワードを設定してこの DC が回復された Dc のそれぞれでレプリケートすることを確認します。 AD DS をインストールすることによって回復される、ドメイン内のそれ以降の Dc は、インストール プロセス中にこれらの新しいパスワードを自動的にレプリケートされます。  
  
## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>信頼関係の 1 つの側での信頼のパスワードをリセットするには  
  
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    netdom experthelp trust  
    ```  
  
2.  このコマンドは、NetDom ツールを使用して、信頼のパスワードをリセットするの構文を使用します。  
  
     たとえば、フォレスト内に 2 つのドメインがある場合: 親と子 — と親ドメインの復元されたドメイン コントローラーでこのコマンドを実行している、次のコマンド構文を使用します。  
  
    ```  
    netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
    ```  
  
     子ドメインで次のコマンドを実行するときは、次のコマンド構文を使用します。  
  
    ```  
    netdom trust child domain name /domain:parent domain name /resetOneSide /password:password /userO:administrator /passwordO:*  
    ```  
  
    > [!NOTE]
    >  **passwordT**信頼の両側に同じ値にする必要があります。 このコマンドを 1 回だけ実行 (とは異なり、**netdom resetpwd**コマンド) に自動的をリセットするため、パスワード 2 回クリックします。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
