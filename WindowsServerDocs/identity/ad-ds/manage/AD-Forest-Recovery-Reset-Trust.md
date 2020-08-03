---
title: AD フォレストの回復-信頼できるパスワードのリセット
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: 66b0e772a1d656551811f4f9ded0a8d80627e485
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519009"
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>信頼の1側での信頼されたパスワードのリセット

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

 フォレストの回復がセキュリティ侵害に関連している場合は、次の手順を使用して、信頼の一方の側で信頼されたパスワードをリセットします。 これには、子ドメインと親ドメイン間の暗黙的な信頼と、このドメイン (信頼する側のドメイン) と別のドメイン (信頼される側のドメイン) との間の明示的な信頼が含まれます。

 信頼の信頼する側のドメイン側 (このドメインが属する側) でのみパスワードをリセットします。 次に、信頼されているドメイン側 (出力方向の信頼とも呼ばれます) で同じパスワードを使用します。 他の (信頼されている) ドメインのそれぞれで最初の DC を復元するときに、出力方向の信頼のパスワードをリセットします。

 信頼のパスワードをリセットすると、DC がドメインの外部に存在する可能性のある Dc にレプリケートされなくなります。 各ドメインの最初の DC を復元するときに同じ信頼のパスワードを設定することにより、この DC が復旧された各 Dc と確実にレプリケートされるようになります。 AD DS のインストールによって回復されるドメイン内の後続の Dc は、インストールプロセス中にこれらの新しいパスワードを自動的にレプリケートします。

## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>信頼の一方の側で信頼のパスワードをリセットするには

1. コマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

   ```
   netdom experthelp trust
   ```

2. このコマンドによって提供される構文を使用して、NetDom ツールを使用して信頼のパスワードをリセットします。
   たとえば、フォレスト内に親と子の2つのドメインがあり、親ドメインの復元された DC でこのコマンドを実行している場合は、次のコマンド構文を使用します。

   ```
   netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*
   ```

   子ドメインでこのコマンドを実行する場合は、次のコマンド構文を使用します。

   ```
   netdom trust child domain name /domain:parent domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*
   ```

   > [!NOTE]
   > **Passwordt**は、信頼の両側で同じ値にする必要があります。 このコマンドは、パスワードを2回自動的にリセットするため、( **netdom resetpwd**コマンドとは異なり) 1 回だけ実行します。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
