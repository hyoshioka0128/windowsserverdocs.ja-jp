---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: グループ ポリシーを使用してクライアント コンピューターに証明書を配布します。
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d3a7e05e4d16565b17b69de254e353df749bbc3a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839233"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>グループ ポリシーを使用してクライアント コンピューターに証明書を配布します。

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


次の手順を使用して、適切な Secure Sockets Layer をプッシュできます\(SSL\)証明書\(と同等の信頼されたルートにチェーン化された証明書または\)アカウント フェデレーション サーバーでは、リソース フェデレーション サーバー、およびグループ ポリシーを使用して、アカウント パートナー フォレスト内の各クライアント コンピューターに Web サーバー。  
  
メンバーシップ**Domain Admins**または**Enterprise Admins**、または Active Directory Domain Services での同等\(AD DS\)はこの手順を実行するために必要な最小値。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/でしょうか。LinkId\=83477\)します。   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>グループ ポリシーを使用してクライアント コンピューターに証明書を配布するには  
  
1.  アカウント パートナー組織のフォレストのドメイン コント ローラーで、開始、 **Group Policy Management**スナップ\-でします。  
  
2.  既存のグループ ポリシー オブジェクトを見つける\(GPO\)または証明書の設定を格納する新しい GPO を作成します。 GPO がドメイン、サイト、または組織単位に関連付けられていることを確認\(OU\)適切なユーザーおよびコンピューター アカウントが存在します。  
  
3.  右\-、GPO をクリックし、クリックして**編集**します。  
  
4.  コンソール ツリーで開く**コンピューターの構成\\ポリシー\\Windows 設定\\セキュリティ設定\\公開キーのポリシー**、右\-をクリックします **。信頼されたルート証明機関**、 をクリックし、**インポート**します。  
  
5.  **証明書のインポート ウィザードへようこそ**] ページで [**次**します。  
  
6.  **インポートするファイル**ページで、適切な証明書ファイルへのパスを入力\(など\\ \\fs1\\c$\\fs1.cer\)、順にクリックします**次**します。  
  
7.  **証明書ストア**] ページで [**次のストアに証明書をすべてを配置**、順にクリックします**次**。  
  
8.  **証明書のインポート ウィザードの完了** ページで入力した情報が正確であることを確認してクリックして**完了**します。  
  
9. 手順 2. ~ 6. をフェデレーション サーバー ファーム内の各追加の証明書を追加する.  
