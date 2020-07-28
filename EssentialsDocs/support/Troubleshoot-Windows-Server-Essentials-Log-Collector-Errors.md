---
title: Windows Server Essentials Log Collector エラーのトラブルシューティング
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: fa2e1685-31c0-4d4f-a10a-6c8885dfc493
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 36c8143883667896c3ecdb3aa4b09d3c474537d2
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180298"
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Windows Server Essentials Log Collector エラーのトラブルシューティング

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Log Collector を実行すると、次のエラーのいずれかが発生する可能性があります。 問題を解決するには、関連するエラー用に提供されたガイダンスに従ってください。

> [!NOTE]
> このドキュメントでは、サーバー以外のネットワーク上のコンピューターは、ネットワークコンピューターと呼ばれています。

###  <a name="the-destination-folder-is-not-valid"></a><a name="BKMK_TheDestinationFolderIsNotValid"></a>コピー先フォルダーが有効ではありません
 **原因:** ログ ファイルをコピーしようとしているフォルダーが存在しないか、ファイルを格納するための空き領域が不足している可能性があります。

 **解決策:** 選択したフォルダーが存在して、ファイルを格納するドライブに十分な空き領域があることを確認します。 また、ドライブ上の一時フォルダーにも十分な空き領域があることを確認する必要があります。

###  <a name="a-network-error-has-occurred"></a><a name="BKMK_ANetworkErrorHasOccurred"></a>ネットワークエラーが発生しました
 **原因:** ネットワーク コンピューターまたはサーバーにネットワーク関連の問題がある可能性があります。

 **解決策:** すべてのコンピューターとネットワーク デバイスの電源が入っていて、ネットワークに接続されていることを確認します。 この問題を解決できない場合、ネットワーク管理者にお問い合わせください。

###  <a name="cannot-collect-log-files-for-the-computer"></a><a name="BKMK_CannotCollectLogFiles"></a>コンピューターのログファイルを収集できません
 **原因:** サーバー ウィザードへのコンピューターの接続を使用して、コンピューターがサーバーに正常に接続されていなかったため、Log Collector がコンピューターにインストールされていない可能性があります。

 **解決策:** サーバーへの接続に関する問題を解決する方法の詳細については、「[コンピューターをサーバーに接続](https://go.microsoft.com/fwlink/p/?LinkID=241492)する場合のトラブルシューティング」を参照してください。

 まだコンピューターをサーバーに接続できない場合は、次のようにログ ファイルを USB フラッシュ ドライブに手動でコピーできます。

-   Windows 7、Windows 8、または Windows Multipoint Server を搭載しているクライアント コンピューターの場合、 **%sysdir%\programdata\Microsoft\Windows Server** に配置された [ **Logs**] フォルダーをコピーできます。

###  <a name="you-do-not-have-permission-to-save-the-log-files-to-the-selected-folder"></a><a name="BKMK_YouDoNotHavePermission"></a>選択したフォルダーにログファイルを保存するためのアクセス許可がありません
 **原因:** ログ ファイルを保存するために選択したフォルダーへの書き込みアクセス許可がない可能性があります。

 **解決策:** ログファイルを保存する既定のパスを使用している場合は、共有フォルダー ** \\ \\<ServerName \> \Logs**に対する書き込みアクセス許可があることを確認します。 ネットワーク コンピューターにログを保存している場合、ログ ファイルの保存先に選択したフォルダーに対する書き込みアクセス許可があることを確認します。

###  <a name="the-computer-is-not-configured-properly-to-collect-the-log-files"></a><a name="BKMK_TheComputerIsNotConfiguredProperly"></a>コンピューターがログファイルを収集するように適切に構成されていない
 **原因:** コンピューターが、Log Collector に対して正しく構成されていません。

 **解決策:** Log Collector を再インストールします。 「[Log Collector の再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)」を参照してください。

###  <a name="an-unknown-error-occurred"></a><a name="BKMK_AnUnknownErrorOccurred"></a>不明なエラーが発生しました
 **原因:** 不明。

 **解決策 1:** Log Collector の再度実行します。 エラーがもう一度発生した場合は、接続に問題がないことを確認します。 Log Collector の再インストールを試すこともできます。 「[Log Collector の再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)」を参照してください。 この問題を解決できない場合、ネットワーク管理者にお問い合わせください。

 **解決策 2:** まず、ログ ファイルを保存するフォルダーを開きます。 コンピューター名の ZIP ファイルが生成されている場合は、このエラーを無視してログ ファイルを使用します。 ログ ファイルが生成されていない場合は、Log Collector を再実行します。 エラーがもう一度発生した場合は、接続に問題がないことを確認します。 Log Collector の再インストールを試すこともできます。 「[Log Collector の再インストール](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)」を参照してください。 この問題を解決できない場合、ネットワーク管理者にお問い合わせください。