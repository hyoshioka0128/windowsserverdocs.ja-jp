---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: "アカウント フェデレーション サーバーを信頼するクライアント コンピューターを構成します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bdfb086c8177e72c074ac5b5b1a38aac49c4082c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>アカウント フェデレーション サーバーを信頼するクライアント コンピューターを構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

できるように、クライアント コンピューターは、Active Directory フェデレーション サービス \(AD FS\) を使用してフェデレーション アプリケーションを正常にアクセスできる、する必要がありますまず設定を構成する Internet Explorer 各クライアント コンピューターで、ブラウザーは、アカウント フェデレーション サーバーを信頼できるようにします。 行うことができますこれ手動またはグループ ポリシーを使って、管理の基本設定に応じて、次の手順のいずれかの操作を実行することによってします。  
  
## <a name="configuring-internet-explorer-settings-manually"></a>Internet Explorer の設定を構成する手動で  
AD FS でのフェデレーションをサポートするために各ユーザーの Internet Explorer の設定を手動で構成するのに、次の手順を使用することができます。 複数のユーザーは、1 台のコンピューターを使用している場合は、この手順は複数回-ユーザーのプロフィールごとに 1 回です。  
  
この手順を実行するには、フェデレーション アプリケーションにアクセスするユーザーとしてログオンします。 これは、profile\ 固有の設定です。 そのため、手動で特定のコンピュータに存在しているプロファイルごとにこの設定を追加することが必要です。  
  
#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>クライアント コンピューターは、アカウント フェデレーション サーバーの信頼を手動で構成するには  
  
1.  クライアント コンピューターでは、Internet Explorer を起動します。  
  
2.  **ツール**] メニューのをクリックして**インターネット オプション**します。  
  
3.  **セキュリティ**タブをクリックし、**ローカル イントラネット**] アイコンをクリックして**サイト**します。  
  
4.  をクリックして**詳細**、し、[**この Web サイトをゾーンに追加**、アカウント フェデレーション サーバーのドメイン ネーム システム \(DNS\) フル_ネームを入力 \ (たとえば、https:\/\/fs1.fabrikam.com\)] をクリックし、**追加**します。  
  
5.  をクリックして**OK** 3 回です。  
  
## <a name="configuring-internet-explorer-settings-by-using-group-policy"></a>グループ ポリシーを使用して Internet Explorer の設定を構成します。  
ほとんどの展開では、グループ ポリシーを使用して、各クライアント コンピューターに適切な Internet Explorer の設定をプッシュすることをお勧めします。  
  
メンバーシップ**Domain Admins**または**Enterprise Admins**、または Active Directory ドメイン サービスに相当するもので \(AD DS\) がこの手順を完了するために必要な最小値。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)\ (http:///\/go.microsoft.com\/fwlink\/ですか?LinkId\ = 83477\)。   
  
#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-group-policy"></a>グループ ポリシーを使用して、アカウント フェデレーション サーバーを信頼するクライアント コンピューターを構成するには  
  
1.  アカウント パートナー組織のフォレスト内のドメイン コント ローラーでは、開始、**グループ ポリシーの管理**スナップインです。  
  
2.  検索の適切なグループ ポリシー オブジェクト \(GPO\)、右クリックし、クリック**編集**します。  
  
3.  コンソール ツリーで、開く**ユーザー構成 Settings\\Internet Explorer のメンテナンス**、] をクリックし、**セキュリティ**します。  
  
4.  詳細ウィンドウでダブルクリック**セキュリティ ゾーンおよびコンテンツの規制**します。  
  
5.  [**セキュリティ ゾーンとプライバシー**、] をクリックして**現行のセキュリティ ゾーンとプライバシーの設定をインポート**、] をクリックし、**設定の変更**します。  
  
6.  をクリックして**ローカル イントラネット**、] をクリックし、**サイト**します。  
  
7.  **この Web サイトをゾーンに追加**、アカウント フェデレーション サーバーの完全な DNS 名を入力 \ (たとえば、https:\/\/fs1.fabrikam.com\)] をクリックして**追加**、] をクリックし、**閉じる**します。  
  
8.  をクリックして**OK** 2 倍になるグループ ポリシーにこれらの変更を適用します。  
  
