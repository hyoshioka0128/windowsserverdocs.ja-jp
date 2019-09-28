---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: コンピューターをドメインに参加させる
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 9f6d657397cb07d081a229135e3e6c97c7191164
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408347"
---
# <a name="join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させる

Active Directory フェデレーションサービス (AD FS) @no__t の AD FS @ no__t を機能させるには、フェデレーションサーバーとして機能する各コンピューターがドメインに参加している必要があります。 フェデレーションサーバープロキシはドメインに参加することができますが、これは必須ではありません。  
  
Web サーバーがクレーム @ no__t 対応アプリケーションのみをホストしている場合は、Web サーバーをドメインに参加させる必要はありません。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させるには  
  
1.  **開始**画面で「**コントロール パネルの** し、ENTER キーを押します。  
  
2.  **[システムとセキュリティ]** に移動し、 **[システム]** をクリックします。  
  
3.  **[コンピューター名、ドメインおよびワークグループの設定]** で **[設定の変更]** をクリックします。  
  
4.  **[コンピューター名]** タブで、 **[変更]** をクリックします。  
  
5.  次 **[のメンバー]** で **[ドメイン]** をクリックし、このコンピューターを参加させるドメインの名前を入力して、[ **OK]** をクリックします。  
  
6.  **[OK]** をクリックし、コンピューターを再起動します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

