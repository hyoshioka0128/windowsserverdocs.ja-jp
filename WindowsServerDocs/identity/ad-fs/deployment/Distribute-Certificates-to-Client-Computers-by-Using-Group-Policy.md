---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: グループポリシーを使用してクライアントコンピューターに証明書を配布する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1d9692bc099174f15b77e792087f4c7055bf85d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359622"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>グループポリシーを使用してクライアントコンピューターに証明書を配布する


次の手順を使用して、適切な Secure Sockets Layer \(SSL @ no__t 証明書 \(、またはアカウントフェデレーションサーバー、リソースフェデレーションサーバー、およびの信頼されたルート @ no__t にチェーンされている同等の証明書をプッシュダウンすることができます。グループポリシーを使用して、アカウントパートナーフォレスト内の各クライアントコンピューターへの Web サーバー。  
  
この手順を実行するには、 **Domain admins**または**Enterprise admins**のメンバーシップ、またはそれと同等の Active Directory Domain Services \(ad DS @ no__t が最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/?」を参照してください。LinkId\=83477\)。   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>グループポリシーを使用してクライアントコンピューターに証明書を配布するには  
  
1.  アカウントパートナー組織のフォレスト内のドメインコントローラーで、**グループポリシー管理**スナップ @ no__t-1 を開始します。  
  
2.  既存のグループポリシーオブジェクト \(GPO @ no__t を検索するか、証明書の設定を含む新しい GPO を作成します。 GPO がドメイン、サイト、または組織単位に関連付けられていることを確認します。その際、適切なユーザーアカウントとコンピューターアカウントが存在する、\(OU @ no__t-1 を指定します。  
  
3.  右 @ no__t をクリックし、GPO をクリックして、 **[編集]** をクリックします。  
  
4.  コンソールツリーで、**コンピューターの構成 @ no__t-1Policies @ no__t-2Windows の設定 @ no__t-3Security settings @ no__t-4 公開キーのポリシー**を右クリックし、**信頼されたルート証明機関** をクリックして、インポート をクリックします。.  
  
5.  **[証明書のインポートウィザードの開始]** ページで、 **[次へ]** をクリックします。  
  
6.  **[インポートするファイル]** ページで、適切な証明書 @no__t ファイルへのパスを入力します。たとえば、\\ @ no__t-3fs1 @ no__t-4c $ \\fs1 .cer @ no__t を入力し、 **[次へ]** をクリックします。  
  
7.  **[証明書ストア]** ページで、 **[証明書をすべて次のストアに配置する]** をクリックし、 **[次へ]** をクリックします。  
  
8.  **[証明書のインポートウィザードの完了]** ページで、入力した情報が正しいことを確認し、 **[完了]** をクリックします。  
  
9. 手順 2. ~ 6. を繰り返して、ファーム内の各フェデレーションサーバーに証明書を追加します。  
