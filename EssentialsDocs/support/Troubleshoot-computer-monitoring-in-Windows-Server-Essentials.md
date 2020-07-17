---
title: Windows Server Essentials でのコンピューターの監視のトラブルシューティング
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: f1e6b377-4a24-4d28-9b25-05910914826b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5e2c8706c29e63a74d637e4a2c072d0ffa0a56d5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852205"
---
# <a name="troubleshoot-computer-monitoring-in-windows-server-essentials"></a>Windows Server Essentials でのコンピューターの監視のトラブルシューティング

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このトピックでは、Windows Server Essentials のアラートビューアーおよび電子メール通知を使用して、コンピューターの正常性状態を監視するときに発生する問題のトラブルシューティングについて説明します。  
  
> [!NOTE]
>  Windows Server Essentials コミュニティの最新のトラブルシューティング情報については、 [Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)を参照することをお勧めします。 Windows Server Essentials フォーラムは、ヘルプを検索したり、質問したりするために最適な場所です。  
  
##  <a name="troubleshooting-email-notifications-for-alerts"></a><a name="BKMK_TS"></a>アラートの電子メール通知のトラブルシューティング  
 ここではアラート用の電子メール通知を使用する場合に発生する可能性のあるさまざまな問題を示します。  
  
### <a name="cannot-send-the-test-email-for-the-alert"></a>アラート用のテスト電子メールを送信できない  
 **問題**"アラートのテスト電子メールを送信できません" というエラーメッセージが表示されます。  
  
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
    >  ProgramData フォルダーを表示するには、隠しファイルを表示させる必要があります。 ProgramData フォルダーが表示されない場合は、リボンの **[表示]** タブの **[表示/非]** 表示 グループで、 **[非表示の項目]** ボックスを選択します。  
  
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
