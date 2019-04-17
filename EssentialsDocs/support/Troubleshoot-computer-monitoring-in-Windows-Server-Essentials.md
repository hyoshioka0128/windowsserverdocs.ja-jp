---
title: "Windows Server Essentials でのコンピューターの監視をトラブルシューティングします。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 72fe309e0e7ce6d7227cce8b7f2c5dbf018eb4a1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-computer-monitoring-in-windows-server-essentials"></a>Windows Server Essentials でのコンピューターの監視をトラブルシューティングします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このトピックでは、アラート ビューアーおよび Windows Server Essentials で電子メール通知を介したコンピューターのヘルス状態の監視中に発生する問題のトラブルシューティングを提供します。  
  
> [!NOTE]
>  Windows Server Essentials コミュニティから最新のトラブルシューティング情報について、ことをお勧めを参照する、[Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)します。 Windows Server Essentials フォーラムは、ヘルプについては、検索するか、質問をお勧めします。  
  
##  <a name="BKMK_TS"></a>アラートの電子メール通知のトラブルシューティング  
 このセクションでは、アラートの電子メール通知を使用する場合に発生する可能性のあるさまざまな問題を示します。  
  
### <a name="cannot-send-the-test-email-for-the-alert"></a>アラート用のテスト電子メールを送信することはできません。  
 **問題**エラーが発生する、というメッセージがアラート用のテスト電子メールを送信できません。  
  
 **原因**アラート通知の設定で、次の問題のいずれかによってこのエラーが発生する可能性があります。  
  
-   正しくない SMTP サーバー名またはポート番号。  
  
-   それが正しく指定されていません、SMTP サーバーが 1 つの Sockets Layer (SSL) 接続が必要であります。  
  
-   SMTP サーバーの認証を必要とし、不適切な資格情報を入力します。  
  
 **解決策**電子メール通知設定で、エラーを修正します。  
  
##### <a name="to-identify-issues-in-your-email-notification-settings"></a>電子メール通知設定で問題を特定するには  
  
-   正しい SMTP サーバー名、ポート番号、および SSL の使用状況、インターネット サービス プロバイダー (ISP) を要求します。  
  
-   サーバーで、この場所に、アラートの電子メール通知のログ ファイルを確認します。  
  
     %ProgramData%\Microsoft\Windows Server\Logs\SharedServiceHost-AlertServiceConfig.log  
  
    > [!TIP]
    >  ProgramData フォルダーを見るには、表示される項目を非が表示する必要があります。 T don s リボンで、ProgramData フォルダーを表示する場合は**ビュー** ] タブで、**表示/非表示**グループで、[、**隠し項目を**テキスト ボックス。  
  
##### <a name="to-update-your-email-notification-setup-for-alerts"></a>アラートの電子メール通知のセットアップを更新するには  
  
1.  ダッシュ ボードを開くには、アラート ビューアー右上隅にある任意のアラート アイコンをクリックします。  
  
2.  アラート ビューアーの下部にある、] をクリックして**アラートの電子メール通知設定**します。  
  
3.  **アラートの電子メール通知設定**ダイアログ ボックスで、をクリックして**を有効にする**します。  
  
4.  **SMTP 設定**] ダイアログ ボックスで、SMTP 設定を更新し、をクリックして**OK**します。  
  
5.  更新された設定をテストする] をクリックして**適用して送信電子メール**します。  
  
6.  テスト電子メールが成功したことを確認したら、クリックして**OK**、更新された設定を保存します。  
  
### <a name="test-email-notification-does-not-list-any-alerts"></a>テスト電子メール通知にすべてのアラートが表示されません。  
 **問題**アラート ビューアーに表示されているアラートがある場合でも、アラートのテスト電子メール通知ですべてのアラートが表示されません。  
  
 **解決策**アラート ビューアーで報告されるすべてのアラートは、電子メール通知を生成します。 正常性定義ファイル内で電子メール通知として報告するように構成されているアラートだけは、指定した電子メールの受信者に電子メールとして送信されます。  
  
 クリックすると**適用して送信電子メール**、正常性アラートが表示されているなしでサンプル電子メール通知を受信する通常します。 ただし、このテスト プロセス中に、電子メール通知を送信するように構成された正常性アラートを識別する場合、アラートはテスト電子メールに含まれています。  
  
### <a name="active-alerts-are-displayed-for-an-uninstalled-application"></a>アンインストールされたアプリケーションのアクティブなアラートが表示されます。  
 **問題**アプリケーションとその正常性定義ファイルがアンインストールされた場合でも、アプリケーションのアクティブなアラートが表示されます。  
  
 **解決策**アンインストールされたアプリケーションのアクティブなアラートを手動で削除する必要があります。 アラートを削除するには、次のします。  
  
##### <a name="to-delete-an-alert-from-the-server-by-using-the-dashboard"></a>ダッシュ ボードを使用して、サーバーからアラートを削除するには  
  
1.  サーバーからダッシュ ボードを開きます。  
  
2.  ナビゲーション ウィンドウで、表示されるアラート アイコン (重大、警告、情報案内のいずれか) をクリックします。 これにより、アラート ビューアーが起動します。  
  
3.  アラート ビューアーで、削除、およびをクリックするアラートを右クリックして**このアラートを削除**します。
