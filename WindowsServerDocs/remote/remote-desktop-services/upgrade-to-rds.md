---
title: Windows Server 2016 に、リモート デスクトップ サービスのデプロイをアップグレードします。
description: この記事では、既存のリモート デスクトップ サービスのデプロイを Windows Server 2016 にアップグレードする方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 03/20/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7b1f1f6-57c8-40ab-a235-e36240dcc1f8
author: spatnaik
manager: scottman
notes: https://social.technet.microsoft.com/wiki/contents/articles/22069.remote-desktop-services-upgrade-guidelines-for-windows-server-2012-r2.aspx
ms.openlocfilehash: f683a7d9346494e7f1fb6faf716ca9c90cfef8d3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875753"
---
# <a name="upgrading-your-remote-desktop-services-deployments-to-windows-server-2016"></a>Windows Server 2016 に、リモート デスクトップ サービスのデプロイをアップグレードします。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 役割がインストールされた OS のアップグレードをサポート
Windows Server 2016 へのアップグレードは、Windows Server 2012 R2 および Windows Server 2016 からのみサポートされます。

## <a name="flow-for-deployment-upgrades"></a>デプロイのアップグレードのフロー
ダウン時間を最小限に抑えるためには、次の手順に従うことをお勧めします。

1. **RD 接続ブローカー サーバー**最初にアップグレードする必要があります。 配置にアクティブ/アクティブ セットアップがある場合、すべてが 1 つのサーバーを展開から削除し、インプレース アップグレードを実行します。 残りの RD 接続ブローカー サーバーをオフラインでアップグレードを実行し、再展開に追加します。 RD 接続ブローカー サーバーのアップグレード中には、展開を利用できません。

   > [!NOTE] 
   > RD 接続ブローカー サーバーをアップグレードする必要があります。 Windows Server 2012 R2 RD 接続ブローカー サーバーで混合展開サーバーの Windows Server 2016 では、いないはサポートします。 RD 接続ブローカー サーバーは、Windows Server 2016 を実行するいるとは、展開内のサーバーの残りの部分には、Windows Server 2012 R2 が実行しているが場合でも、配置が機能、なります。

2. **RD ライセンス サーバー** RD セッション ホスト サーバーをアップグレードする前にアップグレードする必要があります。
   > [!NOTE] 
   > Windows Server 2012 および 2012 R2 の RD ライセンス サーバーは、Windows Server 2016 の展開で機能しますから Windows Server 2012 R2 と以前の Cal のみ処理できます。 Windows Server 2016 の Cal を使用できません。 参照してください[RDS デプロイをクライアント アクセス ライセンス (Cal) ライセンス](rds-client-access-license.md)RD ライセンス サーバーの詳細について。

3. **RD セッション ホスト サーバー**次にアップグレードすることができます。 アップグレード中にダウンタイムを回避するために、管理者は、以下のように 2 つの手順でアップグレードするサーバーを分割できます。 アップグレード後に機能すべてになります。 をアップグレードする」に記載の手順を使用して、 [Windows Server 2016 へのリモート デスクトップ セッション ホストのアップグレード サーバー](upgrade-to-rdsh.md)します。

4. **RD 仮想化ホスト サーバー**次にアップグレードすることができます。 をアップグレードする」に記載の手順を使用して、 [Windows Server 2016 へのリモート デスクトップ仮想化ホストのアップグレード サーバー](upgrade-to-rdvh.md)します。

5. **RD Web アクセス サーバー**いつでもアップグレードできます。
   > [!NOTE]
   > RD Web をアップグレードすると、(すべての構成ファイル) などの IIS のプロパティがリセットすることがあります。 変更内容は失われません、ノートまたは IIS の RD Web サイトを実行したカスタマイズのコピーを確認します。

   > [!NOTE] 
   > Windows Server 2012 および 2012 R2 の RD Web アクセス サーバーは、Windows Server 2016 の展開で動作します。

6. **RD ゲートウェイ サーバー**いつでもアップグレードできます。
   > [!NOTE]
   > Windows Server 2016 でネットワーク アクセス保護 (NAP) ポリシーが含まれません: 削除する必要があります。 適切なポリシーを削除する最も簡単な方法のアップグレード ウィザードを実行していることです。 すべての NAP ポリシーを削除する必要がある場合は、アップグレードがブロックし、特定のポリシーを含むデスクトップ上のテキスト ファイルを作成します。 NAP ポリシーを管理するには、ネットワーク ポリシー サーバー ツールを開きます。 をクリックして削除すると、**更新**アップグレード プロセスを続行するセットアップ ツールで。 

   > [!NOTE] 
   > Windows Server 2012 および 2012 R2 RD ゲートウェイ サーバーは、Windows Server 2016 の展開で動作します。

## <a name="vdi-deployment--supported-guest-os-upgrade"></a>VDI 展開 – サポートされているゲスト OS のアップグレード
管理者は、VM のコレクションのアップグレードには、次のオプションが完成します。

### <a name="upgrade-managed-shared-vm-collections"></a>共有の管理対象 VM コレクションをアップグレードします。 
管理者は、目的の OS バージョンの VM テンプレートを作成し、それを使用して、プール内のすべての Vm の修正プログラムを適用する必要があります。 

次の修正プログラム適用シナリオ: サポートされています
- Windows 7 SP1 は Windows 8 または Windows 8.1 にパッチを適用できます。
- Windows 8 は Windows 8.1 にパッチを適用できます。
- Windows 8.1 は Windows 10 にパッチを適用できます。

### <a name="upgrade-unmanaged-shared-vm-collections"></a>管理されていない共有 VM コレクションをアップグレードします。 
エンドユーザーは自分のパーソナル デスクトップをアップグレードできません。 管理者は、アップグレードを実行する必要があります。 正確な手順では、まだを特定します。