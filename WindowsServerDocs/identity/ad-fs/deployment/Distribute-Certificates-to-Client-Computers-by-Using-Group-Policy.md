---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: グループポリシーを使用してクライアントコンピューターに証明書を配布する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c0e1ab21faa42789bee20c7b8945284aba068310
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855445"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>グループポリシーを使用してクライアントコンピューターに証明書を配布する


次の手順を使用して、\) を使用して、アカウントフェデレーションサーバー、リソースフェデレーションサーバー、および Web サーバーのアカウントフェデレーションサーバー、リソースフェデレーションサーバー、および Web サーバーの信頼されたルートグループポリシーにチェーンされている適切な Secure Sockets Layer \(SSL\) 証明書 \(または同等の証明書をプッシュダウンすることができます。  
  
この手順を実行するには、 **Domain admins**または**Enterprise admins**のメンバーシップ、またはそれと同等の Active Directory Domain Services \(AD DS\) が最低限必要です。  適切なアカウントとグループメンバーシップの使用に関する詳細については、\(http:\/\/go.microsoft.com\/fwlink\/? [」を参照](https://go.microsoft.com/fwlink/?LinkId=83477)してください。LinkId\=83477\)。   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>グループポリシーを使用してクライアントコンピューターに証明書を配布するには  
  
1.  アカウントパートナー組織のフォレスト内のドメインコントローラーで、**グループポリシー管理**スナップ\-を開始します。  
  
2.  既存のグループポリシーオブジェクト \(GPO\) を検索するか、証明書の設定を含む新しい GPO を作成します。 GPO がドメイン、サイト、または組織単位 \(OU\) に関連付けられていることを確認します。これは、適切なユーザーアカウントとコンピューターアカウントが存在する場所です。  
  
3.  GPO を右\-クリックし、 **[編集]** をクリックします。  
  
4.  コンソールツリーで、[コンピューターの構成]、[Windows の\\設定]、[セキュリティの\\設定]、 **[公開キーのポリシー]** の順に開き、 **[信頼されたルート証明機関]** を右\-クリックして **[インポート]** をクリックし\\\\ます。  
  
5.  **[証明書のインポートウィザードの開始]** ページで、 **[次へ]** をクリックします。  
  
6.  **[インポートするファイル]** ページで、適切な証明書ファイルへのパスを入力します。たとえば、\\\\fs1\\c $\\fs1 .cer\)\(、 **[次へ]** をクリックします。  
  
7.  **[証明書ストア]** ページで、 **[証明書をすべて次のストアに配置する]** をクリックし、 **[次へ]** をクリックします。  
  
8.  **[証明書のインポートウィザードの完了]** ページで、入力した情報が正しいことを確認し、 **[完了]** をクリックします。  
  
9. 手順 2. ~ 6. を繰り返して、ファーム内の各フェデレーションサーバーに証明書を追加します。  
