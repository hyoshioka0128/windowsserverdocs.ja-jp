---
title: Windows Server Essentials Log Collector エラーのトラブルシューティング
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836663"
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Windows Server Essentials Log Collector エラーのトラブルシューティング

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Log Collector を実行すると、次のエラーのいずれかが発生する可能性があります。 問題を解決するには、関連するエラー用に提供されたガイダンスに従ってください。  
  
> [!NOTE]
>  このドキュメントでは、サーバー以外のネットワーク上のコンピューターがネットワーク コンピューターに呼び出されます。 でしょうか。  
  
###  <a name="BKMK_TheDestinationFolderIsNotValid"></a> コピー先のフォルダーが無効です。  
 **原因:** ログ ファイルをコピーしようとしているフォルダーが存在しないか、ファイルを格納するための空き領域が不足している可能性があります。  
  
 **解決方法:** 選択したフォルダーが存在して、ファイルを格納するドライブに十分な空き領域があることを確認します。 また、ドライブ上の一時フォルダーにも十分な空き領域があることを確認する必要があります。  
  
###  <a name="BKMK_ANetworkErrorHasOccurred"></a> ネットワーク エラーが発生しました  
 **原因:** ネットワーク コンピューターまたはサーバーにネットワーク関連の問題がある可能性があります。  
  
 **解決方法:** すべてのコンピューターとネットワーク デバイスの電源が入っていて、ネットワークに接続されていることを確認します。 この問題を解決できない場合、ネットワーク管理者にお問い合わせください。  
  
###  <a name="BKMK_CannotCollectLogFiles"></a> コンピューターのログ ファイルを収集することはできません。  
 **原因:** サーバー ウィザードへのコンピューターの接続を使用して、コンピューターがサーバーに正常に接続されていなかったため、Log Collector がコンピューターにインストールされていない可能性があります。  
  
 **解決方法:** サーバーに接続に関する問題を解決する方法については、次を参照してください。[コンピューターをサーバーに接続するトラブルシューティング](https://go.microsoft.com/fwlink/p/?LinkID=241492)でしょうか。 (https://go.microsoft.com/fwlink/p/?LinkID=241492) Microsoft web サイト。  
  
 まだコンピューターをサーバーに接続できない場合は、次のようにログ ファイルを USB フラッシュ ドライブに手動でコピーできます。  
  
-   Windows 7、Windows 8、または Windows Multipoint Server を搭載しているクライアント コンピューターの場合、 **%sysdir%\programdata\Microsoft\Windows Server** に配置された **[Logs]** フォルダーをコピーできます。  
  
###  <a name="BKMK_YouDoNotHavePermission"></a> 選択したフォルダーにログ ファイルを保存するアクセス許可がありません。  
 **原因:** ログ ファイルを保存するために選択したフォルダーへの書き込みアクセス許可がない可能性があります。  
  
 **解決方法:** ログ ファイルを保存する既定のパスを使用する場合は、共有フォルダーに対する書き込みアクセス許可があることを確認 **\\ \\< ServerName\>\Logs**します。 ネットワーク コンピューターにログを保存している場合、ログ ファイルの保存先に選択したフォルダーに対する書き込みアクセス許可があることを確認します。  
  
###  <a name="BKMK_TheComputerIsNotConfiguredProperly"></a> ログ ファイルを収集するコンピューターが正しく構成されていません  
 **原因:** コンピューターが、Log Collector に対して正しく構成されていません。  
  
 **解決方法:** Log Collector を再インストールします。 「[Log Collector の再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)」を参照してください。  
  
###  <a name="BKMK_AnUnknownErrorOccurred"></a> 不明なエラーが発生しました  
 **原因:** 不明。  
  
 **解決策 1:** Log Collector の再度実行します。 エラーがもう一度発生した場合は、接続に問題がないことを確認します。 Log Collector の再インストールを試すこともできます。 「[Log Collector の再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)」を参照してください。 この問題を解決できない場合、ネットワーク管理者にお問い合わせください。  
  
 **解決方法 2:** まず、ログ ファイルを保存するフォルダーを開きます。 コンピューター名の ZIP ファイルが生成されている場合は、このエラーを無視してログ ファイルを使用します。 ログ ファイルが生成されていない場合は、Log Collector を再実行します。 エラーがもう一度発生した場合は、接続に問題がないことを確認します。 Log Collector の再インストールを試すこともできます。 「[Log Collector の再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)」を参照してください。 この問題を解決できない場合、ネットワーク管理者にお問い合わせください。