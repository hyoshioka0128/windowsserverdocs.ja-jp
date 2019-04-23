---
title: AD フォレストの回復 - krbtgt パスワードをリセットします。
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.technology: identity-adds
ms.openlocfilehash: 1ac0dcb9da1d10a417c128cb8498a5d8362d9a9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883743"
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>AD フォレストの回復 - krbtgt パスワードをリセットします。

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

ドメインの krbtgt パスワードをリセットするのにには、次の手順を使用します。 次の手順では、書き込み可能 Dc が読み取り専用ドメイン コント ローラー (Rodc) が適用されます。
  
> [!IMPORTANT]
> オンラインの Rodc をフォレストの回復中に回復する場合、Rodc の krbtgt アカウントを削除しないでください。 RODC の krbtgt アカウントが形式 krbtgt_ 記載*数*します。
>
> DC (passfilt.dll) などのカスタマイズされたパスワード フィルターを使用する場合、krbtgt のパスワードをリセットしようとするとエラーを受信可能性があります。 詳細については、この問題を回避するを参照してくださいマイクロソフト サポート技術情報[記事 2549833](https://support.microsoft.com/kb/2549833) (https://support.microsoft.com/kb/2549833)します。
  
## <a name="to-reset-the-krbtgt-password"></a>Krbtgt パスワードをリセットするには  
  
1. をクリックして**開始**、 をポイント**コントロール パネルの **、 をポイント**管理ツール**、順にクリックします**Active Directory ユーザーとコンピューター**します。
2. クリックして**ビュー**、 をクリックし、**高度な機能**します。
3. コンソール ツリーで ドメインのコンテナーをダブルクリックし、クリックして**ユーザー**します。
4. 詳細ペインで右クリックし、 **krbtgt**ユーザー アカウント、およびクリック**パスワードのリセット**します。
   ![パスワードのリセット](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)
5. **新しいパスワード**、新しいパスワードを入力して、パスワードを再入力**パスワードの確認入力**、 をクリックし、 **OK**。 システムが自動的に、指定したパスワードの独立した強力なパスワードを生成するため、指定したパスワードは大きくありません。
  
> [!NOTE]
> この操作を 2 回行う必要があります。 Krbtgt アカウントのパスワードの履歴は、最新の 2 つのパスワードが含まれています。 つまり、2 つです。 履歴から、古いパスワードを効果的に消去する 2 回パスワードをリセットして方法がない別の DC はレプリケートこの DC で古いパスワードを使用しています。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md) 
