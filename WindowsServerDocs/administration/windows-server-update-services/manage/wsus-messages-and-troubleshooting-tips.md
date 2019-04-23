---
title: WSUS メッセージとトラブルシューティングのヒント
description: Windows Server Update Service (WSUS) のトピックでは、WSUS のメッセージを使用したトラブルシューティング
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f6317f7-bfe0-42d9-87ce-d8f038c728ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc24893b1a227501959002ea2d81c62813855d4a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883633"
---
# <a name="wsus-messages-and-troubleshooting-tips"></a>WSUS メッセージとトラブルシューティングのヒント

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックには、次の WSUS メッセージに関する情報が含まれています。

-   「コンピューターが状態を報告していません」

-   "メッセージ ID 6703 - WSUS 同期に失敗しました"

-   "エラー 0x80070643:インストール中に致命的なエラー"

-   "一部のサービスは実行されていません。 次のサービス [...] を確認するには"

## <a name="computer-has-not-reported-status"></a>コンピューターが状態を報告していません
このメッセージは、WSUS クライアント コンピューターを現在の更新状態を示すために WSUS サーバーに情報を送信しないと、WSUS コンソールで生成されます。 この問題は通常、WSUS サーバーではなく、WSUS クライアント コンピューターで発生します。

最も一般的な理由は次のとおりです。

-   コンピューターには、ネットワーク接続が切断されました。
    -   ネットワーク ケーブルが接続されていません。
    -   間のネットワーク ケーブルの障害があります。
    -   コンピューターには、問題のあるネットワーク アダプターがあります。
    -   コンピューターが接続するネットワーク ポートが無効になりました。
    -   ワイヤレスのアダプターが関連付けられ、企業のワイヤレス アクセス ポイントに接続することではありません。
-   コンピューターがオフになります。 (それはシャット ダウンされましたまたはスリープまたは休止状態モードでは)。

## <a name="message-id-6703---wsus-synchronization-failed"></a>メッセージ ID 6703 - WSUS の同期に失敗しました
> メッセージ: HTTP ステータス 503 で要求が失敗しました。サービスを使用できません。

> ソース:Microsoft.UpdateServices.Administration.AdminProxy.createUpdateServer します。

WSUS サーバーの更新サービスを開こうとすると、次のエラーが表示されます。

> エラー:接続エラー

> WSUS サーバーに接続しようとしたときにエラーが発生しました。 このエラーは、さまざまな理由から発生することができます。 問題が解決しない場合は、ネットワーク管理者に問い合わせてください。 [リセット] をクリックして、サーバーに再度接続するサーバーのノード。

上記のほか、WSUS 管理 web サイトの URL にアクセスを試みる (つまり、 http://CM12CAS:8530)エラーで失敗します。

> HTTP エラー 503。 サービスをご利用いただけません

このような状況で最も一般的な原因は、IIS の WsusPool アプリケーション プールが停止状態であります。

また、アプリケーション プールのプライベート メモリ制限 (KB) では、1843200 サポート技術情報の既定値に設定されます可能性があります。 この問題が発生した場合は、4 gb (4000000 KB) のプライベート メモリ制限を増やすし、アプリケーション プールを再起動します。 プライベート メモリの制限、WsusPool アプリケーション プールを選択し、[アプリケーション プールの編集の詳細設定] をクリックします。 4 GB (4000000 KB) には、プライベート メモリの制限に設定されます。 アプリケーション プールが再起動したら、SMS_WSUS_SYNC_MANAGER コンポーネントのステータス、wcm.log およびエラーの wsyncmgr.log を監視します。 環境に応じて (8000000 KB) の 8 GB 以上のプライベート メモリ制限を増やす必要ありますに注意してください。

詳細については、次を参照してください。[ConfigMgr 2012 で WSUS の同期は、HTTP 503 エラーで失敗します。](http://blogs.technet.com/b/sus/archive/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors.aspx)

## <a name="error-0x80070643-fatal-error-during-installation"></a>エラー 0x80070643:インストール中に致命的なエラー
WSUS セットアップでは、インストールを実行するのに Microsoft SQL Server を使用します。 WSUS セットアップを実行しているユーザーに SQL server システム管理者のアクセス許可があるないために、この問題が発生します。

この問題を解決するには、ユーザー アカウントまたは SQL Server でのグループ アカウントにシステム管理者のアクセス許可を付与し、WSUS セットアップを再度実行します。

## <a name="some-services-are-not-running-check-the-following-services"></a>一部のサービスが実行されていません。 次のサービスを確認します。

- **Selfupdate:** 参照してください[自動更新する必要があります更新](https://technet.microsoft.com/library/cc708554(v=ws.10).aspx)Selfupdate サービスのトラブルシューティングに関する情報。

- **WSSUService.exe:** このサービスには、同期が容易になります。 同期に問題がある場合は、クリックして WSUSService.exe をアクセス**開始**をポイントして、**管理ツール**、**サービス**を検索し**Windows Server Update Service**サービスの一覧にします。 次の操作を行います。
    
    -   このサービスが実行されていることを確認します。 をクリックして**開始**が停止している場合または**再起動**サービスを更新します。
    
    -   イベント ビューアーを使用して、確認、**アプリケーション**、**み**y、および**システム**イベント ログに問題を示す可能性があるイベントがあるかどうかを参照してください。
    
    -   問題を示す可能性があるイベントがあるかどうかにある SoftwareDistribution.log を確認することもできます。

- **Web servicesSQL サービス:** Web サービスは、IIS でホストされます。 実行されていない場合は、IIS が実行中 (または開始) のことを確認します。 試すこともできます」と入力して、Web サービスをリセットする**iisreset**コマンド プロンプトでします。

- **SQL サービス:** Selfupdate サービスを除くすべてのサービスでは、SQL サービスが実行されていることが必要です。 SQL 接続の問題を示すログ ファイルのいずれかの場合は、まず、SQL サービスを確認します。 SQL サービスにアクセスするには、クリックして**開始**、 をポイント**管理ツール**、 をクリックして**サービス**、次のいずれかの確認。
    
    -   **MSSQLSERver** (WMSDE と MSDE を使用する場合または SQL Server を使用し、インスタンス名の既定のインスタンス名を使用している場合など)
    
    -   **MSSQL$ WSUS** (かどうかは SQL Server データベースを使用して、データベース インスタンス"WSUS"をという名前が)
    
    サービスを右クリックし、をクリックし、**開始**サービスが実行されていない場合または**再起動**が実行されている場合、サービスを更新します。
