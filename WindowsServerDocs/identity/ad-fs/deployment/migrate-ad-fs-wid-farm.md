---
title: AD FS 2.0 フェデレーション サーバーの WID ファームを移行します。
description: Windows Server 2012 への AD FS 2.0 サーバー WID ファームの移行に関する情報を提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c85a02ae6a71cf31fd172ec012a14cd81c126e16
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445653"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID ファームを移行します。  
このドキュメントは、広告の移行に関する詳細な情報を提供します FS 2.0 Windows Internal Database (WID) ファームを Windows Server 2012。

## <a name="migrate-an-ad-fs-wid-farm"></a>AD FS WID ファームを移行します。
WID ファームを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  すべてのノード (サーバー) で、WID ファームを確認し、実行手順では、 [WID ファームの移行の準備](prepare-to-migrate-a-wid-farm.md)します。  
  
2.  プライマリ ノード以外をロード バランサーから削除します。  
  
3.  このサーバーから Windows Server 2008 R2 または Windows Server 2012 への Windows Server 2008 上のオペレーティング システムのアップグレードします。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 元の AD FS 構成を作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。  
  
4. このサーバーで元の AD FS 構成を作成します。  
  
元の AD FS 構成を作成するには、 **AD FS フェデレーション サーバー構成ウィザード** を使用して、フェデレーション サーバーを WID ファームに追加します。 詳細については、「 [Add a Federation Server to a Federation Server Farm](add-a-federation-server-to-a-federation-server-farm.md)」を参照してください。  
  
> [!NOTE]
> **AD FS フェデレーション サーバー構成ウィザード** の **[プライマリ フェデレーション サーバーとサービス アカウントの指定]** ページが表示されたら、WID ファームのプライマリ フェデレーション サーバーの名前を入力し、AD FS の移行の準備を行っているときに記録したサービス アカウント情報を必ず入力してください。 詳細については、次を参照してください。 [to Migrate the AD FS 2.0 フェデレーション サーバーを準備](prepare-to-migrate-a-wid-farm.md)します。 
>  
> 表示されたら、**フェデレーション サービス名の指定**で、準備 WID ファームの移行」で記録したのと同じ SSL 証明書を選択してください ページで、 [Prepare to Migrate the AD FS 2.0 の Federation Server](prepare-to-migrate-a-wid-farm.md).  
  
5. このサーバーで AD FS Web ページを更新します。 移行の準備中、カスタマイズされた AD FS web ページをバックアップしている場合は、バックアップ データを使用して、AD FS web ページで既定で作成された既定値を上書きする必要があります、 **%systemdrive%\inetpub\adfs\ls**ディレクトリWindows Server 2012 で AD FS 構成の結果。  
  
6. ロード バランサーに Windows Server 2012 にアップグレードしたサーバーを追加します。  
  
7. WID ファームのその他のセカンダリ サーバーについて、手順 1. ～ 6. を繰り返します。  
  
8. アップグレードされたセカンダリ サーバーの 1 つを WID ファームでプライマリ サーバーに昇格します。 そのためには、Windows PowerShell を開き、 `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`コマンドを実行します。  
  
9. WID ファームの元のプライマリ サーバーをロード バランサーから削除します。  
  
10. Windows PowerShell を使用して、WID ファームの元のプライマリ サーバーをセカンダリ サーバーに降格します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、 `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`コマンドを実行し、元のプライマリ サーバーをセカンダリ サーバーに降格します。  
  
11. Windows Server 2012 から Windows Server 2008 R2 または Windows Server 2008、WID ファームのこの最後のノード (サーバー) 上のオペレーティング システムのアップグレードします。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 元の AD FS 構成を手動で作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。  
  
12. WID ファームのこの最後のノード (サーバー) で元の AD FS 構成を作成します。  
  
元の AD FS 構成を作成するには、 **AD FS フェデレーション サーバー構成ウィザード** を使用して、フェデレーション サーバーを WID ファームに追加します。 詳細については、「 [Add a Federation Server to a Federation Server Farm](add-a-federation-server-to-a-federation-server-farm.md)」を参照してください。  
  
> [!NOTE]
> **AD FS フェデレーション サーバー構成ウィザード** の **[プライマリ フェデレーション サーバーとサービス アカウントの指定]** ページが表示されたら、AD FS の移行の準備を行っているときに記録したサービス アカウント情報を入力してください。 詳細については、次を参照してください。 [to Migrate the AD FS 2.0 フェデレーション サーバーを準備](prepare-to-migrate-a-wid-farm.md)します。 
>  
> 表示されたら、**フェデレーション サービス名の指定**で記録したのと同じ SSL 証明書を選択してください ページで、 [to Migrate the AD FS 2.0 フェデレーション サーバーを準備](prepare-to-migrate-a-wid-farm.md)します。  
  
13. WID ファームのこの最後のサーバーで AD FS Web ページを更新します。 移行の準備中、カスタマイズされた AD FS web ページをバックアップしている場合は、バックアップ データを使用して、AD FS web ページで既定で作成された既定値を上書きする、 **%systemdrive%\inetpub\adfs\ls**の結果としてディレクトリWindows Server 2012 で AD FS の構成。  
  
14. ロード バランサーに Windows Server 2012 にアップグレードした WID ファームのこの最後のサーバーを追加します。  
  
15. カスタム属性ストアなど、その他の AD FS カスタマイズを復元します。  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)