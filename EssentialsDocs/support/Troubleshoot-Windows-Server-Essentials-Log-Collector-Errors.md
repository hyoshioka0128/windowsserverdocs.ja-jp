---
title: "Windows Server Essentials Log Collector エラーをトラブルシューティングします。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa2e1685-31c0-4d4f-a10a-6c8885dfc493
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e92236c8e5d956b50f657ebcbe1a942b5841fded
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Windows Server Essentials Log Collector エラーをトラブルシューティングします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Log Collector を実行すると、次のエラーのいずれかが発生する可能性があります。 問題を解決するには、関連するエラーの原因として提供されているガイダンスに従います。  
  
> [!NOTE]
>  このドキュメントでは、サーバー以外のネットワーク上のコンピューターがネットワーク コンピューターに呼び出されますですか?。  
  
###  <a name="BKMK_TheDestinationFolderIsNotValid"></a>インストール先のフォルダが正しくありません。  
 **原因:**ログ ファイルをコピーしようはフォルダーが存在しないか、ファイルを保持するのに十分な領域がない可能性があります。  
  
 **解決策:**選択したフォルダーが存在して、こと十分な空き領域が利用可能なファイルのドライブに確認します。 ドライブ上の一時フォルダーに残っている十分な空き領域があることを確認する必要があります。  
  
###  <a name="BKMK_ANetworkErrorHasOccurred"></a>ネットワーク エラーが発生しました  
 **原因:**ネットワーク コンピューターまたはサーバーにネットワーク関連の問題がある可能性があります。  
  
 **解決策:**ネットワークに接続されていること、すべてのコンピューターとネットワーク デバイスの電源が入っていることを確認します。 場合は、問題を解決できない場合は、担当者に問い合わせて、ネットワーク管理者に問い合わせてください。  
  
###  <a name="BKMK_CannotCollectLogFiles"></a>コンピューターのログ ファイルを収集することはできません。  
 **原因:**、コンピューターが正常にサーバー ウィザードへのコンピューターの接続を使用してサーバーに接続されているために、Log Collector をコンピューターにインストールしない可能性があります。  
  
 **解決策:**方法については、サーバーに接続に関する問題を解決するのには、次を参照してください[コンピューターをサーバーに接続するトラブルシューティング](https://go.microsoft.com/fwlink/p/?LinkID=241492)ですか?。 (https://go.microsoft.com/fwlink/p/?LinkID=241492)、Microsoft Web サイトにします。  
  
 コンピューターをサーバーに接続できない場合は、し、ことができます、ログ ファイル手動でコピーする USB フラッシュ ドライブに次のように。  
  
-   Windows 7、Windows 8、または Windows Multipoint Server を実行しているクライアント コンピューターでコピーすることができます、**ログ**フォルダーにある**%sysdir%\programdata\Microsoft\Windows Server**します。  
  
###  <a name="BKMK_YouDoNotHavePermission"></a>選択したフォルダーにログ ファイルを保存するためのアクセス許可がないです。  
 **原因:**ログ ファイルの保存用に選択したフォルダーに書き込みアクセス許可がないです。  
  
 **解決策:**ログ ファイルの保存を既定のパスを使用している場合は、共有フォルダーに対する書き込みアクセス許可があることを確認**\\\ < ServerName\ > \Logs**します。 ネットワーク コンピューターでログを保存している場合は、ログ ファイルを保存するために選択したフォルダーに対する書き込みアクセス許可があることを確認します。  
  
###  <a name="BKMK_TheComputerIsNotConfiguredProperly"></a>ログ ファイルを収集するコンピューターが正しく構成されていません。  
 **原因:**コンピューターが、Log Collector に対して正しく構成されていないがします。  
  
 **解決策:** Log Collector を再インストールします。 参照してください[Log Collector を再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)します。  
  
###  <a name="BKMK_AnUnknownErrorOccurred"></a>不明なエラーが発生しました  
 **原因:**不明です。  
  
 **解決策 1:** Log Collector の再度実行します。 エラーが再び発生する場合は、接続の問題がないことを確認します。 Log Collector を再インストールしようとすることができます。 参照してください[Log Collector を再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)します。 場合は、問題を解決できない場合は、担当者に問い合わせて、ネットワーク管理者に問い合わせてください。  
  
 **解決策 2:**まず、ログ ファイルが保存されているフォルダーを開きます。 コンピューター名の zip ファイルが既に生成された場合、このエラーを無視し、代わりに、ログ ファイルを使用します。 生成されたログ ファイルが存在しない場合は、Log Collector を再実行します。 エラーが再び発生する場合は、接続の問題がないことを確認します。 Log Collector を再インストールしようとすることができます。 参照してください[Log Collector を再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)します。 場合は、問題を解決できない場合は、担当者に問い合わせて、ネットワーク管理者に問い合わせてください。