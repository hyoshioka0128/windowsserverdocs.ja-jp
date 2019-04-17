---
title: "AD FS 2.0 フェデレーション サーバーの WID ファームを移行します。"
description: "Windows Server 2012 への AD FS 2.0 サーバー WID ファームの移行に関する情報を提供します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dbef7d07041a1fd32656c95947d5202b566c068a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID ファームを移行します。  
このドキュメントでは、広告を移行する方法の詳細について FS 2.0 Windows Internal Database (WID) ファームを Windows Server 2012 です。

## <a name="migrate-an-ad-fs-wid-farm"></a>AD FS WID ファームを移行します。
WID ファームを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  すべてのノード (サーバー) に WID ファームを確認し、手順を実行[WID ファームの移行の準備](prepare-to-migrate-a-wid-farm.md)します。  
  
2.  どのプライマリ ノード以外をロード バランサーから削除します。  
  
3.  このサーバーから Windows Server 2008 R2 または Windows Server 2012 への Windows Server 2008 上のオペレーティング システムのアップグレードします。 詳細については、次を参照してください。[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)します。  
  
> [!IMPORTANT]
>  オペレーティング システムのアップグレードの結果、このサーバーの AD FS 構成が失われたと AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 元の AD FS 構成を作成し、フェデレーション サーバーの移行を完了する他の AD FS 設定を復元する必要があります。  
  
4.  このサーバーで元の AD FS 構成を作成します。  
  
使用して、元の AD FS 構成を作成することができます、**AD FS フェデレーション サーバー構成ウィザード**WID ファームにフェデレーション サーバーを追加します。 詳細については、次を参照してください。[フェデレーション サーバー ファームにフェデレーション サーバーを追加](add-a-federation-server-to-a-federation-server-farm.md)します。  
  
> [!NOTE]
> 達すると、**プライマリ フェデレーション サーバーとサービス アカウントを指定**] ページで、**AD FS フェデレーション サーバー構成ウィザード**を WID ファームのプライマリ フェデレーション サーバーの名前を入力して、AD FS の移行の準備中に記録したサービス アカウント情報を入力してください。 詳細については、次を参照してください。[移行、AD FS 2.0 フェデレーション サーバーの準備](prepare-to-migrate-a-wid-farm.md)します。 
>  
> 達すると、**フェデレーション サービス名の指定**の準備」WID ファームの移行」で記録したのと同じ SSL 証明書を選択してください] ページで、[移行、AD FS 2.0 フェデレーション サーバーの準備](prepare-to-migrate-a-wid-farm.md)します。  
  
5.  このサーバー上で、AD FS Web ページを更新します。 既定では既定で作成された AD FS Web ページを上書きする、バックアップ データを使用する必要がある、移行の準備中、カスタマイズされた AD FS Web ページをバックアップした場合、**%systemdrive%\inetpub\adfs\ls**ディレクトリに Windows Server 2012 で AD FS 構成の結果。  
  
6.  ロード バランサーに Windows Server 2012 にアップグレードしたサーバーを追加します。  
  
7.  WID ファームの残りのセカンダリ サーバーを手順 1. ~ 6. を繰り返します。  
  
8.  WID ファームのプライマリ サーバーにアップグレードされたセカンダリ サーバーのいずれかの販売を促進します。 これを行うには、Windows PowerShell を開き、次のコマンドを実行します。`PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`します。  
  
9. WID ファームの元のプライマリ サーバーをロード バランサーから削除します。  
  
10. WID ファームを Windows PowerShell を使用して、セカンダリ サーバーで元のプライマリ サーバーを降格します。 Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 セカンダリ サーバーにする元のプライマリ サーバーを降格する、次のコマンドを実行します。`PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`します。  
  
11. Windows Server 2012 から Windows Server 2008 R2 または Windows Server 2008、WID ファームのこの最後のノード (サーバー) 上のオペレーティング システムのアップグレードします。 詳細については、次を参照してください。[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)します。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードする場合の結果、このサーバーの AD FS 構成が失われたと AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 手動で元の AD FS 構成を作成して、フェデレーション サーバーの移行を完了する他の AD FS 設定を復元する必要があります。  
  
12. この最後のノード (サーバー) に WID ファームの元の AD FS 構成を作成します。  
  
使用して、元の AD FS 構成を作成することができます、**AD FS フェデレーション サーバー構成ウィザード**WID ファームにフェデレーション サーバーを追加します。 詳細については、次を参照してください。[フェデレーション サーバー ファームにフェデレーション サーバーを追加](add-a-federation-server-to-a-federation-server-farm.md)します。  
  
> [!NOTE]
> 達すると、**プライマリ フェデレーション サーバーとサービス アカウントを指定**] ページで、**AD FS フェデレーション サーバー構成ウィザード**、AD FS の移行の準備中に記録したサービス アカウント情報を入力します。 詳細については、次を参照してください。[移行、AD FS 2.0 フェデレーション サーバーの準備](prepare-to-migrate-a-wid-farm.md)します。 
>  
> 達すると、**フェデレーション サービス名の指定**で記録したのと同じ SSL 証明書を選択してください] ページで、[移行、AD FS 2.0 フェデレーション サーバーの準備](prepare-to-migrate-a-wid-farm.md)します。  
  
13. WID ファームのこの最後のサーバーで、AD FS Web ページを更新します。 移行の準備中、カスタマイズされた AD FS Web ページをバックアップした場合は、既定では既定で作成された AD FS Web ページを上書きする、バックアップ データを使用して、**%systemdrive%\inetpub\adfs\ls**ディレクトリに Windows Server 2012 で AD FS 構成の結果。  
  
14. ロード バランサーに Windows Server 2012 にアップグレードした WID ファームのこの最後のサーバーを追加します。  
  
15. カスタム属性ストアなどその他の AD FS カスタマイズを復元します。  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)