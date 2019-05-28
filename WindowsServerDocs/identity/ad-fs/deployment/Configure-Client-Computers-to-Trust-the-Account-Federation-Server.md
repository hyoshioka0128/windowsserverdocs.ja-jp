---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: アカウント フェデレーション サーバーを信頼するクライアント コンピューターを構成します。
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: e28d050a9aa40c015af16a665e90535cb810b4ff
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192330"
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>アカウント フェデレーション サーバーを信頼するクライアント コンピューターを構成します。

クライアント コンピューターが Active Directory フェデレーション サービスを使用してフェデレーション アプリケーションを正常にアクセスできるように\(AD FS\)ブラウザーの信頼できるように各クライアント コンピューターで Internet Explorer の設定に構成すること最初にする必要がありますアカウント フェデレーション サーバー。 行うことができますこの手動またはグループ ポリシーによって管理好みに応じて、次の手順のいずれかを実行しています。  
  
## <a name="configuring-internet-explorer-settings-manually"></a>Internet Explorer の設定を構成する手動で  
次の手順を使用して、AD FS によるフェデレーションをサポートするために各ユーザーの Internet Explorer の設定を手動で構成することができます。 複数のユーザーは、1 台のコンピューターを使用して場合、により、この手順が複数回完了: ユーザー プロファイルごとに 1 回です。  
  
この手順を実行するには、フェデレーション アプリケーションにアクセスするユーザーとしてログオンします。 これは、プロファイル\-特定の設定。 そのため、手動で特定のコンピューターのプロファイルが存在するのにこの設定を追加することが必要です。  
  
#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>アカウント フェデレーション サーバーを信頼するクライアント コンピューターを手動で構成するには  
  
1.  クライアント コンピューターでは、Internet Explorer を起動します。  
  
2.  **[ツール]** メニューの **[インターネット オプション]** をクリックします。  
  
3.  **セキュリティ**タブをクリックし、**ローカル イントラネット** アイコンをクリック**サイト**します。  
  
4.  をクリックして **詳細設定** 、および**この Web サイトをゾーンに追加**、型の完全なドメイン ネーム システム\(DNS\)アカウント フェデレーション サーバーの名前\(https など:\/\/fs1.fabrikam.com\)、 をクリックし、**追加**します。  
  
5.  **[OK]** を 3 回クリックします。  
  
## <a name="configuring-internet-explorer-settings-by-using-grouppolicy"></a>グループ ポリシーを使用して Internet Explorer の設定を構成します。  
ほとんどの展開では、グループ ポリシーを使用して、各クライアント コンピューターに適切な Internet Explorer の設定をプッシュすることをお勧めします。  
  
メンバーシップ**Domain Admins**または**Enterprise Admins**、または Active Directory Domain Services での同等\(AD DS\)はこの手順を実行するために必要な最小値。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/でしょうか。LinkId\=83477\)します。   
  
#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-grouppolicy"></a>グループ ポリシーを使用して、アカウント フェデレーション サーバーを信頼するクライアント コンピューターを構成するには  
  
1.  アカウント パートナー組織のフォレストのドメイン コント ローラーで、開始、 **Group Policy Management**スナップ\-でします。  
  
2.  適切なグループ ポリシー オブジェクトを見つける\(GPO\)、右\-をクリックし、クリックして**編集**します。  
  
3.  コンソール ツリーで開く**ユーザーの構成\\設定\\Windows 設定\\Internet Explorer のメンテナンス**、順にクリックします**セキュリティ**します。  
  
4.  詳細ウィンドウでダブルクリック\-クリックして**セキュリティ ゾーンおよびコンテンツの規制**します。  
  
5.  **セキュリティ ゾーンとプライバシー**、 をクリックして**現行のセキュリティ ゾーンとプライバシーの設定をインポート**、 をクリックし、**設定の変更**します。  
  
6.  クリックして**ローカル イントラネット**、 をクリックし、**サイト**します。  
  
7.  **この Web サイトをゾーンに追加**、アカウント フェデレーション サーバーの完全な DNS 名を入力\(例: https:\/\/fs1.fabrikam.com\)、 をクリックして**の追加**、 をクリックし、**閉じる**します。  
  
8.  クリックして**OK**グループ ポリシーにこれらの変更を適用する 2 つの時刻。  
  
