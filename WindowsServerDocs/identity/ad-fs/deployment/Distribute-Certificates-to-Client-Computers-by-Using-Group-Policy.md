---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: グループポリシーを使用してクライアントコンピューターに証明書を配布する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 35b543a7a249130d1fd66a0d86424b5bcb0b8d96
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962896"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>グループポリシーを使用してクライアントコンピューターに証明書を配布する


次の手順を使用すると、 \( \) \( \) グループポリシーを使用して、アカウントフェデレーションサーバー、リソースフェデレーションサーバー、および Web サーバーの信頼されたルートにチェーンされている適切な Secure Sockets Layer SSL 証明書または同等の証明書を、アカウントパートナーフォレスト内の各クライアントコンピューターにプッシュダウンできます。

**Domain Admins** **Enterprise Admins** \( この手順を実行するには、Domain admins または Enterprise admins のメンバーシップ、またはそれと同等の Active Directory Domain Services AD DS \) が最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.microsoft.com fwlink?」を参照して \/ \/ ください。LinkId \= 83477 \) 。

### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>グループポリシーを使用してクライアントコンピューターに証明書を配布するには

1.  アカウントパートナー組織のフォレスト内のドメインコントローラーで、**グループポリシー管理**スナップインを開始し \- ます。

2.  既存のグループポリシーオブジェクト GPO を検索 \( \) するか、証明書設定を含む新しい gpo を作成します。 GPO が、 \( \) 適切なユーザーアカウントとコンピューターアカウントが存在するドメイン、サイト、または組織単位の OU に関連付けられていることを確認します。

3.  \-GPO を右クリックし、[**編集**] をクリックします。

4.  コンソールツリーで、[**コンピューターの構成ポリシー] [Windows 設定] [セキュリティ設定] [ \\ \\ \\ \\ 公開キーのポリシー**] を開き、[ \- **信頼されたルート証明機関**] を右クリックして、[**インポート**] をクリックします。

5.  [**証明書のインポートウィザードの開始**] ページで、[**次へ**] をクリックします。

6.  [**インポートするファイル**] ページで、適切な証明書ファイルへのパス ( \( 例 \\ \\ fs1 \\ c $ \\ fs1 .Cer) を入力 \) し、[**次へ**] をクリックします。

7.  [**証明書ストア**] ページで、[**証明書をすべて次のストアに配置する**] をクリックし、[**次へ**] をクリックします。

8.  [**証明書のインポートウィザードの完了**] ページで、入力した情報が正しいことを確認し、[**完了**] をクリックします。

9. 手順 2. ~ 6. を繰り返して、ファーム内の各フェデレーションサーバーに証明書を追加します。
