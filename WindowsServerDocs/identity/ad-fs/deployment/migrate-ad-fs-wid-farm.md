---
title: AD FS 2.0 フェデレーションサーバー WID ファームの移行
description: AD FS 2.0 server WID ファームを Windows Server 2012 に移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: 8ee9d015b56dfec59e1d13a9ffa51f6297d60787
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962756"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID ファームの移行
このドキュメントでは、AD FS 2.0 Windows Internal Database (WID) ファームを Windows Server 2012 に移行する方法について詳しく説明します。

## <a name="migrate-an-ad-fs-wid-farm"></a>AD FS WID ファームの移行
WID ファームを Windows Server 2012 に移行するには、次の手順を実行します。

1.  WID ファーム内のすべてのノード (サーバー) について、「 [wid ファームの移行の準備](prepare-to-migrate-a-wid-farm.md)」の手順を確認して実行します。

2.  プライマリ ノード以外をロード バランサーから削除します。

3.  このサーバーのオペレーティングシステムを windows Server 2008 R2 または Windows Server 2008 から Windows Server 2012 にアップグレードします。 詳細については、「[Windows Server 2012 のインストール](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11))」を参照してください。

> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 代わりに、Windows Server 2012 AD FS サーバーロールがインストールされますが、構成されていません。 元の AD FS 構成を作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。

4. このサーバーで元の AD FS 構成を作成します。

元の AD FS 構成を作成するには、 **AD FS フェデレーション サーバー構成ウィザード** を使用して、フェデレーション サーバーを WID ファームに追加します。 詳細については、[フェデレーション サーバー ファームへのフェデレーション サーバーの追加に関するページ](add-a-federation-server-to-a-federation-server-farm.md)を参照してください。

> [!NOTE]
> **AD FS フェデレーション サーバー構成ウィザード** の **[プライマリ フェデレーション サーバーとサービス アカウントの指定]** ページが表示されたら、WID ファームのプライマリ フェデレーション サーバーの名前を入力し、AD FS の移行の準備を行っているときに記録したサービス アカウント情報を必ず入力してください。 詳細については、「 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-a-wid-farm.md)」を参照してください。
>
> [**フェデレーションサービス名の指定**] ページが表示されたら、「 [prepare to migrate The AD FS 2.0 Federation Server](prepare-to-migrate-a-wid-farm.md)」の「WID ファームの移行の準備」で記録したものと同じ SSL 証明書を選択してください。

5. このサーバーで AD FS Web ページを更新します。 移行の準備中にカスタマイズされた AD FS web ページをバックアップした場合は、Windows Server 2012 の AD FS 構成の結果として **%systemdrive%\inetpub\adfs\ls**ディレクトリに既定で作成された既定の AD FS web ページを、バックアップデータを使用して上書きする必要があります。

6. Windows Server 2012 にアップグレードしたばかりのサーバーをロードバランサーに追加します。

7. WID ファームのその他のセカンダリ サーバーについて、手順 1. ～ 6. を繰り返します。

8. アップグレードされたセカンダリ サーバーの 1 つを WID ファームでプライマリ サーバーに昇格します。 そのためには、Windows PowerShell を開き、 `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`コマンドを実行します。

9. WID ファームの元のプライマリ サーバーをロード バランサーから削除します。

10. Windows PowerShell を使用して、WID ファームの元のプライマリ サーバーをセカンダリ サーバーに降格します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS cmdlets を Windows PowerShell セッションに追加します。 次に、 `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`コマンドを実行し、元のプライマリ サーバーをセカンダリ サーバーに降格します。

11. WID ファームのこの最後のノード (サーバー) にあるオペレーティングシステムを Windows Server 2008 R2 または Windows Server 2008 から Windows Server 2012 にアップグレードします。 詳細については、「[Windows Server 2012 のインストール](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11))」を参照してください。

> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 代わりに、Windows Server 2012 AD FS サーバーロールがインストールされますが、構成されていません。 元の AD FS 構成を手動で作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。

12. WID ファームのこの最後のノード (サーバー) で元の AD FS 構成を作成します。

元の AD FS 構成を作成するには、 **AD FS フェデレーション サーバー構成ウィザード** を使用して、フェデレーション サーバーを WID ファームに追加します。 詳細については、[フェデレーション サーバー ファームへのフェデレーション サーバーの追加に関するページ](add-a-federation-server-to-a-federation-server-farm.md)を参照してください。

> [!NOTE]
> **AD FS フェデレーション サーバー構成ウィザード** の **[プライマリ フェデレーション サーバーとサービス アカウントの指定]** ページが表示されたら、AD FS の移行の準備を行っているときに記録したサービス アカウント情報を入力してください。 詳細については、「 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-a-wid-farm.md)」を参照してください。
>
> [**フェデレーションサービス名の指定**] ページが表示されたら、 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-a-wid-farm.md)」で記録したものと同じ SSL 証明書を選択してください。

13. WID ファームのこの最後のサーバーで AD FS Web ページを更新します。 移行の準備中にカスタマイズされた AD FS web ページをバックアップした場合は、Windows Server 2012 の AD FS 構成の結果として **%systemdrive%\inetpub\adfs\ls**ディレクトリに既定で作成された既定の AD FS web ページを、バックアップデータを使用して上書きします。

14. Windows Server 2012 にアップグレードした WID ファームの最後のサーバーをロードバランサーに追加します。

15. カスタム属性ストアなど、その他の AD FS カスタマイズを復元します。

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md) [AD FS 2.0 フェデレーションサーバープロキシ](prepare-to-migrate-ad-fs-fed-proxy.md)の移行の準備[AD FS 2.0 フェデレーションサーバー](migrate-the-ad-fs-fed-server.md) [AD FS 2.0 フェデレーションサーバープロキシの](migrate-the-ad-fs-2-fed-server-proxy.md)移行[AD FS 1.1 Web エージェントの](migrate-the-ad-fs-web-agent.md)移行
