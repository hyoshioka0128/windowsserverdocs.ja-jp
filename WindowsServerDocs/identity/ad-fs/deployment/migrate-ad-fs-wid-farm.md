---
title: AD FS 2.0 フェデレーションサーバー WID ファームの移行
description: AD FS 2.0 server WID ファームを Windows Server 2012 に移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 89da3de4bc626e12a1fc34752841f2de1afb5322
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408241"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID ファームの移行  
このドキュメントでは、AD FS 2.0 Windows Internal Database (WID) ファームを Windows Server 2012 に移行する方法について詳しく説明します。

## <a name="migrate-an-ad-fs-wid-farm"></a>AD FS WID ファームの移行
WID ファームを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  WID ファーム内のすべてのノード (サーバー) について、「 [wid ファームの移行の準備](prepare-to-migrate-a-wid-farm.md)」の手順を確認して実行します。  
  
2.  プライマリ ノード以外をロード バランサーから削除します。  
  
3.  このサーバーのオペレーティングシステムを windows Server 2008 R2 または Windows Server 2008 から Windows Server 2012 にアップグレードします。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 代わりに、Windows Server 2012 AD FS サーバーロールがインストールされますが、構成されていません。 元の AD FS 構成を作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。  
  
4. このサーバーで元の AD FS 構成を作成します。  
  
元の AD FS 構成を作成するには、 **AD FS フェデレーション サーバー構成ウィザード** を使用して、フェデレーション サーバーを WID ファームに追加します。 詳細については、「 [Add a Federation Server to a Federation Server Farm](add-a-federation-server-to-a-federation-server-farm.md)」を参照してください。  
  
> [!NOTE]
> **AD FS フェデレーション サーバー構成ウィザード** の **[プライマリ フェデレーション サーバーとサービス アカウントの指定]** ページが表示されたら、WID ファームのプライマリ フェデレーション サーバーの名前を入力し、AD FS の移行の準備を行っているときに記録したサービス アカウント情報を必ず入力してください。 詳細については、次を参照してください。 [to Migrate the AD FS 2.0 フェデレーション サーバーを準備](prepare-to-migrate-a-wid-farm.md)します。 
>  
> 表示されたら、**フェデレーション サービス名の指定**で、準備 WID ファームの移行」で記録したのと同じ SSL 証明書を選択してください ページで、 [to Migrate the AD FS 2.0 フェデレーション サーバーを準備](prepare-to-migrate-a-wid-farm.md).  
  
5. このサーバーで AD FS Web ページを更新します。 移行の準備中にカスタマイズされた AD FS web ページをバックアップした場合は、Windows Server 2012 の AD FS 構成の結果として **%systemdrive%\inetpub\adfs\ls**ディレクトリに既定で作成された既定の AD FS web ページを、バックアップデータを使用して上書きする必要があります。  
  
6. Windows Server 2012 にアップグレードしたばかりのサーバーをロードバランサーに追加します。  
  
7. WID ファームのその他のセカンダリ サーバーについて、手順 1. ～ 6. を繰り返します。  
  
8. アップグレードされたセカンダリ サーバーの 1 つを WID ファームでプライマリ サーバーに昇格します。 そのためには、Windows PowerShell を開き、 `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`コマンドを実行します。  
  
9. WID ファームの元のプライマリ サーバーをロード バランサーから削除します。  
  
10. Windows PowerShell を使用して、WID ファームの元のプライマリ サーバーをセカンダリ サーバーに降格します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、 `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`コマンドを実行し、元のプライマリ サーバーをセカンダリ サーバーに降格します。  
  
11. WID ファームのこの最後のノード (サーバー) にあるオペレーティングシステムを Windows Server 2008 R2 または Windows Server 2008 から Windows Server 2012 にアップグレードします。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 代わりに、Windows Server 2012 AD FS サーバーロールがインストールされますが、構成されていません。 元の AD FS 構成を手動で作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。  
  
12. WID ファームのこの最後のノード (サーバー) で元の AD FS 構成を作成します。  
  
元の AD FS 構成を作成するには、 **AD FS フェデレーション サーバー構成ウィザード** を使用して、フェデレーション サーバーを WID ファームに追加します。 詳細については、「 [Add a Federation Server to a Federation Server Farm](add-a-federation-server-to-a-federation-server-farm.md)」を参照してください。  
  
> [!NOTE]
> **AD FS フェデレーション サーバー構成ウィザード** の **[プライマリ フェデレーション サーバーとサービス アカウントの指定]** ページが表示されたら、AD FS の移行の準備を行っているときに記録したサービス アカウント情報を入力してください。 詳細については、次を参照してください。 [to Migrate the AD FS 2.0 フェデレーション サーバーを準備](prepare-to-migrate-a-wid-farm.md)します。 
>  
> 表示されたら、**フェデレーション サービス名の指定**で記録したのと同じ SSL 証明書を選択してください ページで、 [to Migrate the AD FS 2.0 フェデレーション サーバーを準備](prepare-to-migrate-a-wid-farm.md)します。  
  
13. WID ファームのこの最後のサーバーで AD FS Web ページを更新します。 移行の準備中にカスタマイズされた AD FS web ページをバックアップした場合は、Windows Server 2012 の AD FS 構成の結果として **%systemdrive%\inetpub\adfs\ls**ディレクトリに既定で作成された既定の AD FS web ページを、バックアップデータを使用して上書きします。  
  
14. Windows Server 2012 にアップグレードした WID ファームの最後のサーバーをロードバランサーに追加します。  
  
15. カスタム属性ストアなど、その他の AD FS カスタマイズを復元します。  
  
## <a name="next-steps"></a>次のステップ
 [AD FS 2.0 フェデレーションサーバー  の移行の準備](prepare-to-migrate-ad-fs-fed-server.md)  
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバー  を移行します](migrate-the-ad-fs-fed-server.md)。  
 [AD FS 2.0 フェデレーションサーバープロキシ  を移行します](migrate-the-ad-fs-2-fed-server-proxy.md)。  
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)