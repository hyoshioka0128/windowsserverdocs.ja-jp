---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: "グループ ポリシーを使用してクライアント コンピューターに証明書を配布します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d3a7e05e4d16565b17b69de254e353df749bbc3a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>グループ ポリシーを使用してクライアント コンピューターに証明書を配布します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


次の手順を使用するには、プッシュ ダウン適切な Secure Sockets Layer \(SSL\) 証明書を \ (またはそれと同等の証明書を信頼された使いますチェーン化された) アカウント フェデレーション サーバーで、リソース フェデレーション サーバーと Web サーバーのグループ ポリシーを使用して、アカウント パートナー フォレスト内の各クライアント コンピューターにします。  
  
メンバーシップ**Domain Admins**または**Enterprise Admins**、または Active Directory ドメイン サービスに相当するもので \(AD DS\) がこの手順を完了するために必要な最小値。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)\ (http:///\/go.microsoft.com\/fwlink\/ですか?LinkId\ = 83477\)。   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>グループ ポリシーを使用してクライアント コンピューターに証明書を配布するには  
  
1.  アカウント パートナー組織のフォレスト内のドメイン コント ローラーでは、開始、**グループ ポリシーの管理**スナップインです。  
  
2.  既存のグループ ポリシー オブジェクト \(GPO\) を見つけるか、証明書の設定を含む新しい GPO を作成します。 GPO がドメイン、サイト、または組織単位に関連付けられていることを確認、適切なユーザー アカウントとコンピューター アカウントが存在する \(OU\) します。  
  
3.  クリックして、GPO を右クリック**編集**します。  
  
4.  コンソール ツリーで、開く**コンピューター Configuration\\Policies\\Windows Settings\\Security Settings\\Public キーのポリシー**、右クリック**信頼されたルート証明機関**、] をクリックし、**インポート**します。  
  
5.  **証明書のインポート ウィザードへようこそ**] ページで [**次**します。  
  
6.  **インポートするファイル**] ページで、適切な証明書ファイルへのパスを入力 \ (たとえば、\\\fs1\\c$\\fs1.cer\)] をクリックし、**[次へ]**します。  
  
7.  **証明書ストア**] ページで [**すべての証明書を次のストアに配置**、] をクリックし、**[次へ]**します。  
  
8.  **証明書のインポート ウィザードの完了**] ページで入力した情報が正確であることを確認してをクリックして**完了**します。  
  
9. 手順 2 ~ 6 をフェデレーション サーバー ファーム内の各追加の証明書を追加する.  
