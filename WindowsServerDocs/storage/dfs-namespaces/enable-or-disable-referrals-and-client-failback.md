---
title: 紹介とクライアント フェールバックを有効または無効にする
description: この記事では、紹介とクライアント フェールバックを有効または無効にする方法について説明します。
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 0336588dcf0c170698c89b32a29952916bd26100
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954759"
---
# <a name="enable-or-disable-referrals-and-client-failback"></a>紹介とクライアント フェールバックを有効または無効にする

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

紹介とは、ユーザーが名前空間のルートにアクセスするか、ターゲットを持つ DFS フォルダーにアクセスしたときに、クライアント コンピューターがドメイン コントローラーまたは名前空間サーバーから受信する、順序付きのサーバーの一覧です。 クライアント コンピューターは、紹介を受信した後、まず一覧の先頭のサーバーにアクセスしようとします。 そのターゲットにアクセスできない場合は、次のターゲットにアクセスしようとします。 サーバーが使用不能になった場合は、そのサーバーの復元後にクライアントが優先サーバーにフェールバックするように構成できます。

次のセクションでは、紹介を有効または無効にする方法とクライアント フェールバックを有効にする方法について説明します。

## <a name="enable-or-disable-referrals"></a>紹介を有効または無効にする

名前空間サーバーまたはフォルダー ターゲットの紹介を無効にすることで、ユーザーがその名前空間サーバーやフォルダー ターゲットに接続しないようにすることができます。 この機能は、メンテナンスを行うために、サーバーを一時的にオフラインにする場合に役立ちます。

-   フォルダー ターゲットへの紹介を有効または無効にするには、次の手順を使います。

    1.  DFS の管理のコンソール ツリーの **[名前空間]** ノードで、ターゲットを含むフォルダーをクリックし、**[詳細]** ウィンドウの **[フォルダー ターゲット]** タブをクリックします。
    2.  フォルダー ターゲットを右クリックし、**[フォルダー ターゲットを無効にする]** または **[フォルダー ターゲットを有効にする]** をクリックします。

-   名前空間サーバーへの紹介を有効または無効にするには、次の手順を使います。

    1.  DFS 管理コンソールツリーで、適切な名前空間を選択し、[**名前空間サーバー** ] タブをクリックします。
    2.  適切な名前空間サーバーを右クリックし、**[名前空間サーバーを無効にする]** または **[名前空間サーバーを有効にする]** をクリックします。


> [!TIP]
> Windows PowerShell を使って紹介を有効または無効にするには、Windows Server 2012 で導入された [Set-DfsnRootTarget –State](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731089(v=ws.11)) または [Set-DfsnServerConfiguration](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731089(v=ws.11)) コマンドレットを使います。

## <a name="enable-client-failback"></a>クライアント フェールバックを有効にする

ターゲットが使用不能になった場合は、そのターゲットの復元後にクライアントがそのターゲットにフェールバックするように構成できます。 フェールバックが機能するには、[DFS 名前空間クライアントの要件のまとめに関するページ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11))に示された要件をクライアント コンピューターが満たしている必要があります。


> [!NOTE]
> Windows PowerShell を使うことで名前空間ルートでクライアント フェールバックを有効にするには、[Set-DfsnRoot](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11)) コマンドレットを使います。 DFS フォルダーでクライアント フェールバックを有効にするには、[Set-DfsnFolder](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11)) コマンドレットを使います。


## <a name="to-enable-client-failback-for-a-namespace-root"></a>名前空間のルートでクライアントのフェールバックを有効にするには

1.  [**スタート**] をクリックし、[**管理ツール**] をポイントして、[**DFS 管理**] をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、名前空間を右クリックし、**[プロパティ]** をクリックします。

3.  **[紹介]** タブで、**[クライアントを優先するターゲットにフェールバックする]** チェック ボックスをオンにします。

ターゲットを持つフォルダーは、名前空間のルートからクライアント フェールバックの設定を継承します。 名前空間のルートでクライアントのフェールバックが無効になっている場合は、次の手順を実行して、ターゲットを持つフォルダーへのクライアントのフェールバックを有効にできます。

## <a name="to-enable-client-failback-for-a-folder-with-targets"></a>ターゲットを持つフォルダーへのクライアントのフェールバックを有効にするには

1.  [**スタート**] をクリックし、[**管理ツール**] をポイントして、[**DFS 管理**] をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、ターゲットを持つフォルダーを右クリックし、**[プロパティ]** をクリックします。

3.  [**紹介**] タブで、[**クライアントを優先するターゲットにフェールバックする**] チェック ボックスをオンにします。

## <a name="additional-references"></a>その他の参照情報

-   [DFS 名前空間を調整する](tuning-dfs-namespaces.md)
-   [DFS 名前空間クライアントの要件を確認する](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11))
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)
