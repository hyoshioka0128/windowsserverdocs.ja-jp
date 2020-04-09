---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: コンピューターをドメインに参加させる
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 174f585f3e156fc8e068b9300fc90a20a67869cf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855355"
---
# <a name="join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させる

Active Directory フェデレーションサービス (AD FS) \(\) AD FS を機能させるには、フェデレーションサーバーとして機能する各コンピューターがドメインに参加している必要があります。 フェデレーションサーバープロキシはドメインに参加することができますが、これは必須ではありません。  
  
Web サーバーが要求\-対応アプリケーションのみをホストしている場合は、Web サーバーをドメインに参加させる必要はありません。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させるには  
  
1.  **[スタート]** 画面で「**コントロールパネル**」と入力し、enter キーを押します。  
  
2.  **[システムとセキュリティ]** に移動し、 **[システム]** をクリックします。  
  
3.  **[コンピューター名、ドメインおよびワークグループの設定]** の **[設定の変更]** をクリックします。  
  
4.  **[コンピューター名]** タブで **[変更]** をクリックします。  
  
5.  次 **[のメンバー]** で **[ドメイン]** をクリックし、このコンピューターを参加させるドメインの名前を入力して、[ **OK]** をクリックします。  
  
6.  **[OK]** をクリックし、コンピューターを再起動します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

