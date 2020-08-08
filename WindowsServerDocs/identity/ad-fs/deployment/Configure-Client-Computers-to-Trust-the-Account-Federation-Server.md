---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを構成する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 31a878460b94dadcb01578a45c21d270e1560391
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938454"
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを構成する

クライアントコンピューターが Active Directory フェデレーションサービス (AD FS) AD FS を使用してフェデレーションアプリケーションに正常にアクセスできるようにするには \( \) 、まず、各クライアントコンピューターで Internet Explorer の設定を構成して、ブラウザーがアカウントフェデレーションサーバーを信頼するようにする必要があります。 この操作は、管理者の設定に応じて、次のいずれかの手順を実行して、手動またはグループポリシーによって行うことができます。

## <a name="configuring-internet-explorer-settings-manually"></a>Internet Explorer の設定を手動で構成する
次の手順に従って、AD FS を通じてフェデレーションをサポートするように、各ユーザーの Internet Explorer 設定を手動で構成することができます。 複数のユーザーが1台のコンピューターを使用する場合は、ユーザープロファイルごとに1回、この手順を複数回実行します。

この手順を実行するには、フェデレーションアプリケーションにアクセスするユーザーとしてログオンします。 これはプロファイル \- 固有の設定です。 そのため、特定のコンピューターに存在する各プロファイルについて、この設定を手動で追加する必要があります。

#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを手動で構成するには

1.  クライアントコンピューターで、Internet Explorer を起動します。

2.  **[ツール]** メニューの **[インターネット オプション]** をクリックします。

3.  [**セキュリティ**] タブで、[**ローカルイントラネット**] アイコンをクリックし、[**サイト**] をクリックします。

4.  [**詳細設定**] をクリックし、[**この Web サイトをゾーンに追加する**] で、アカウントフェデレーションサーバーの完全なドメインネームシステム \( DNS \) 名 ( \( 例: https: Fs1.fabrikam.com) を入力し、 \/ \/ \) [**追加**] をクリックします。

5.  [**OK**] を 3 回クリックします。

## <a name="configuring-internet-explorer-settings-by-using-grouppolicy"></a>グループポリシーを使用した Internet Explorer の設定の構成
ほとんどの展開では、グループポリシーを使用して、各クライアントコンピューターに適切な Internet Explorer の設定をプッシュすることをお勧めします。

**Domain Admins** **Enterprise Admins** \( この手順を実行するには、Domain admins または Enterprise admins のメンバーシップ、またはそれと同等の Active Directory Domain Services AD DS \) が最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.microsoft.com fwlink?」を参照して \/ \/ ください。LinkId \= 83477 \) 。

#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-grouppolicy"></a>グループポリシーを使用して、アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを構成するには

1.  アカウントパートナー組織のフォレスト内のドメインコントローラーで、**グループポリシー管理**スナップインを開始し \- ます。

2.  適切なグループポリシーオブジェクト \( GPO を見つけて \) 右クリックし、[ \- **編集**] をクリックします。

3.  コンソールツリーで、[ユーザーの構成設定] [Windows の設定] [ ** \\ \\ \\ Internet Explorer のメンテナンス**] の順に開き、[**セキュリティ**] をクリックします。

4.  詳細ウィンドウで、 \- [**セキュリティゾーンおよびコンテンツの規制**] をダブルクリックします。

5.  [**セキュリティゾーンとプライバシー**] で、[**現在のセキュリティゾーンとプライバシーの設定をインポートする**] をクリックし、[**設定の変更**] をクリックします。

6.  [**ローカルイントラネット**] をクリックし、[**サイト**] をクリックします。

7.  [**この Web サイトをゾーンに追加する**] で、アカウントフェデレーションサーバーの完全な DNS 名 ( \( 例: https: fs1.fabrikam.com) を入力し、 \/ \/ \) [**追加**] をクリックして、[**閉じる**] をクリックします。

8.  [ **OK** ] を2回クリックして、これらの変更をグループポリシーに適用します。

