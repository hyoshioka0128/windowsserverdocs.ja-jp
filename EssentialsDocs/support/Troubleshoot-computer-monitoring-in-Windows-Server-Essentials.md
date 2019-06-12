---
title: Windows Server Essentials でのコンピューターの監視のトラブルシューティング
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1e6b377-4a24-4d28-9b25-05910914826b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1adf8ae2dd8763d0bc5a514609bb2470de6acde4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436069"
---
# <a name="troubleshoot-computer-monitoring-in-windows-server-essentials"></a>Windows Server Essentials でのコンピューターの監視のトラブルシューティング

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このトピックでは、アラート ビューアーおよび Windows Server Essentials での電子メール通知を介したコンピューターの正常性状態の監視中に発生する問題のトラブルシューティングを提供します。  
  
> [!NOTE]
>  Windows Server Essentials コミュニティの最新のトラブルシューティング情報について、お勧めしますをご覧ください、 [Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)します。 Windows Server Essentials フォーラムは、ヘルプを検索したり、質問したりするために最適な場所です。  
  
##  <a name="BKMK_TS"></a> アラートの電子メール通知のトラブルシューティング  
 ここではアラート用の電子メール通知を使用する場合に発生する可能性のあるさまざまな問題を示します。  
  
### <a name="cannot-send-the-test-email-for-the-alert"></a>アラート用のテスト電子メールを送信できない  
 **問題**エラーが発生するメッセージが表示されたら、アラート用のテスト電子メールを送信できません。  
  
 **原因** : このエラーは、アラート通知の設定の次のいずれかの問題が原因で発生する可能性があります。  
  
- SMTP サーバー名またはポート番号が正しくありません。  
  
- SMTP サーバーに 1 つの Sockets Layer (SSL) 接続が必要であると誤って指定されています。  
  
- SMTP サーバーで認証を必要とし、正しくない資格情報が入力されました。  
  
  **解決策**: 電子メール通知設定のエラーを修正します。  
  
##### <a name="to-identify-issues-in-your-email-notification-settings"></a>電子メール通知設定の問題を識別するには  
  
-   正しい SMTP サーバー名、ポート番号、および SSL の使用状況をインターネット サービス プロバイダー (ISP) に尋ねます。  
  
-   サーバーの次の場所で、アラートの電子メール通知について、ログ ファイルを確認します。  
  
     %ProgramData%\Microsoft\Windows Server\Logs\SharedServiceHost-AlertServiceConfig.log  
  
    > [!TIP]
    >  ProgramData フォルダーを表示するには、隠しファイルを表示させる必要があります。 リボンの ProgramData フォルダーが表示されないかどうか**ビュー** ] タブで、**表示/非表示**グループで、[、**アイテムを非表示**テキスト ボックス。  
  
##### <a name="to-update-your-email-notification-setup-for-alerts"></a>アラートの電子メール通知のセットアップを更新するには  
  
1.  ダッシュボードで、右上隅の任意のアラート アイコンをクリックして、アラート ビューアーを開きます。  
  
2.  アラート ビューアーの下部の **[アラートの電子メール通知のセットアップ]** をクリックします。  
  
3.  **[アラートの電子メール通知のセットアップ]** ダイアログ ボックスで、 **[有効化]** をクリックします。  
  
4.  **[SMTP 設定]** ダイアログ ボックスで、SMTP 設定を更新し、 **[OK]** をクリックします。  
  
5.  更新された設定をテストするには、 **[適用して電子メールを送信]** をクリックします。  
  
6.  テスト電子メールが成功したことを確認したら、 **[OK]** をクリックして、更新された設定を保存します。  
  
### <a name="test-email-notification-does-not-list-any-alerts"></a>テスト電子メール通知にすべてのアラートが表示されない  
 **問題** : アラート ビューアーにアラートが表示されている場合でも、アラートのテスト電子メール通知にすべてのアラートが表示されません。  
  
 **解決策** : アラート ビューアーで報告されるすべてのアラートで電子メール通知が生成されるとは限りません。 正常性定義ファイル内で、電子メール通知として報告するように構成されているアラートだけが、指定された電子メールの受信者に電子メールとして送信されます。  
  
 **[適用して電子メールを送信]** をクリックすると、一般に、正常性アラートが表示されていないサンプル電子メール通知を受信します。 ただし、このテスト プロセス中に、電子メール通知を送信するように構成された正常性アラートが識別された場合、そのアラートがテスト電子メールに記載されます。  
  
### <a name="active-alerts-are-displayed-for-an-uninstalled-application"></a>アンインストールされたアプリケーションについてのアクティブなアラートが表示される  
 **問題**: アプリケーションとその正常性定義ファイルがアンインストールされていても、そのアプリケーションについてのアクティブなアラートが表示されます。  
  
 **解決策**: アンインストールされたアプリケーションのアクティブなアラートを手動で削除する必要があります。 アラートを削除するには、次の手順に従います。  
  
##### <a name="to-delete-an-alert-from-the-server-by-using-the-dashboard"></a>ダッシュボードを使用して、サーバーからアラートを削除するには  
  
1.  サーバーからダッシュボードを開きます。  
  
2.  ナビゲーション ウィンドウで、表示されているいずれかのアラート アイコン (警告、注意、または情報) をクリックします。 これにより、アラート ビューアーが起動します。  
  
3.  アラート ビューアーで、削除するアラートを右クリックし、 **[このアラートを削除する]** をクリックします。
