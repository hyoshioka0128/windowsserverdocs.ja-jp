---
title: "Krbtgt パスワードのリセット - AD フォレストの回復"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.technology: identity-adfs
ms.openlocfilehash: 445fa18503e26d04e20a61cfe652424f78631abe
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>Krbtgt パスワードのリセット - AD フォレストの回復 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 ドメインの krbtgt パスワードをリセットするのにには、次の手順を使用します。 次の手順では、書き込み可能な Dc を読み取り専用ドメイン コントローラー (Rodc) が適用されます。  
  
> [!IMPORTANT]
>  フォレストの回復時にオンラインに Rodc を回復する場合、Rodc の krbtgt アカウントを削除しないでください。 RODC の krbtgt アカウントが形式 krbtgt_ で表示されている*数*します。  
>   
>  DC で (passfilt.dll) などのカスタム パスワード フィルターを使用する場合、krbtgt パスワードをリセットしようとするときにエラーを受け取る場合があります。 詳細については、この問題を回避するを参照してくださいマイクロソフト サポート技術情報[記事 2549833](https://support.microsoft.com/kb/2549833) (https://support.microsoft.com/kb/2549833)。  
  
## <a name="to-reset-the-krbtgt-password"></a>Krbtgt パスワードをリセットするには  
  
1.  をクリックして**開始**、] をポイント**コントロール パネルの [**、] をポイント**管理ツール**、] をクリックし、**Active Directory ユーザーとコンピューター**します。  
2.  2.  をクリックして**ビュー**、] をクリックし、**高度な機能**します。  
3.  コンソール ツリーで、[ドメイン コンテナーをダブルクリックし、クリックして**ユーザー**します。  
4.  詳細ウィンドウで右クリックし、**krbtgt**ユーザー アカウント、およびクリック**パスワードのリセット**します。  
![[パスワードをリセットします。](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)
5.  **新しいパスワード**、新しいパスワードを入力して、パスワードを再入力**パスワードの確認入力**、] をクリックし、**OK**します。 指定したパスワードは、システムには、指定したパスワードを自動的に独立した強力なパスワードが生成するため、大きな違いはありません。  
  
    > [!NOTE]
    >  2 回クリック操作を実行する必要があります。 Krbtgt アカウントのパスワードの履歴は 2 つ、2 つの最も最近使用したパスワードが含まれています。 2 回効果的にオフにする、古いパスワード履歴からパスワードをリセットするには、によって方法がないように別の DC はレプリケートこの DC と、古いパスワードを使用しています。  
 
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md) 
  
