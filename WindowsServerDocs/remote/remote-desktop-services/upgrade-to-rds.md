---
title: リモート デスクトップ サービスの展開を Windows Server 2016 にアップグレードする
description: この記事では、既存のリモート デスクトップ サービスの展開を Windows Server 2016 にアップグレードする方法について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 29648db89b61a9d22aad6d5aa814cfe7f425a970
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403874"
---
# <a name="upgrading-your-remote-desktop-services-deployments-to-windows-server-2016"></a>リモート デスクトップ サービスの展開を Windows Server 2016 にアップグレードする

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 役割がインストールされたサポート対象オペレーティング システムのアップグレード
Windows Server 2016 へのアップグレードがサポートされるのは、Windows Server 2012 R2 および Windows Server 2016 からのみです。

## <a name="flow-for-deployment-upgrades"></a>展開アップグレードのフロー
ダウンタイムを最小限に抑えるために、次の手順に従うことをお勧めします。

1. **RD 接続ブローカー サーバー**を最初にアップグレードするようにします。 展開にアクティブ/アクティブ セットアップがある場合は、展開から 1 つのサーバーを除くすべてのサーバーを削除し、インプレース アップグレードを実行します。 その他の RD 接続ブローカー サーバー上でオフラインでアップグレードを実行してから、それらを展開に追加し直します。 RD 接続ブローカー サーバーのアップグレード中は、展開を使用できません。

   > [!NOTE] 
   > RD 接続ブローカー サーバーをアップグレードする必要があります。 Windows Server 2016 サーバーとの混合展開では、Windows Server 2012 R2 RD 接続ブローカー サーバーはサポートされません。 RD 接続ブローカー サーバーが Windows Server 2016 を実行している場合、展開内のその他のサーバーがまだ Windows Server 2012 R2 を実行していても、展開は機能します。

2. RD セッション ホスト サーバーをアップグレードする前に、**RD ライセンス サーバー**をアップグレードするようにします。
   > [!NOTE] 
   > Windows Server 2012 および 2012 R2 RD ライセンス サーバーは、Windows Server 2016 の展開環境でも動作しますが、Windows Server 2012 R2 以前の CAL のみを処理できます。 これらは Windows Server 2016 CAL を使用できません。 RD ライセンス サーバーの詳細については、「[License your RDS deployment with client access licenses (CALs) (クライアント アクセス ライセンス (CAL) を使用して RDS 展開にライセンスを付与する)](rds-client-access-license.md)」を参照してください。

3. **RD セッション ホスト サーバー**は次にアップグレードできます。 アップグレード中のダウンタイムを回避するために、管理者はアップグレードするサーバーを以下の 2 つの手順で分割することができます。 アップグレード後はすべてが機能します。 アップグレードするには、[リモート デスクトップ セッション ホスト サーバーの Windows Server 2016 へのアップグレード](upgrade-to-rdsh.md)に関するページで説明されている手順を使用します。

4. **RD 仮想化ホスト サーバー**は次にアップグレードできます。 アップグレードするには、[リモート デスクトップ仮想ホスト サーバーの Windows Server 2016 へのアップグレード](upgrade-to-rdvh.md)に関するページで説明されている手順を使用します。

5. **RD Web アクセス サーバー**はいつでもアップグレードできます。
   > [!NOTE]
   > RD Web をアップグレードすると、IIS のプロパティ (すべての構成ファイルなど) がリセットされることがあります。 変更を失わないように、IIS の RD Web サイトに対して行ったカスタマイズのメモまたはコピーを作成します。

   > [!NOTE] 
   > Windows Server 2012 および 2012 R2 RD Web アクセス サーバーは、Windows Server 2016 の展開と連携します。

6. **RD ゲートウェイ サーバー**はいつでもアップグレードできます。
   > [!NOTE]
   > Windows Server 2016 にはネットワーク アクセス保護 (NAP) ポリシーが含まれていません。これらは削除する必要があります。 正しいポリシーを削除する最も簡単な方法は、アップグレード ウィザードを実行することです。 削除する必要がある NAP ポリシーがある場合、アップグレードがブロックされ、特定のポリシーを含むテキスト ファイルがデスクトップ上に作成されます。 NAP ポリシーを管理するには、ネットワーク ポリシー サーバー ツールを開きます。 それらを削除した後、セットアップ ツールの **[更新]** をクリックしてアップグレード プロセスを続行します。 

   > [!NOTE] 
   > Windows Server 2012 および 2012 R2 RD ゲートウェイ サーバーは、Windows Server 2016 の展開と連携します。

## <a name="vdi-deployment--supported-guest-os-upgrade"></a>VDI 展開 - サポートされているゲスト OS のアップグレード
管理者には、VM コレクションのアップグレードに次のオプションがあります。

### <a name="upgrade-managed-shared-vm-collections"></a>マネージド共有 VM コレクションのアップグレード 
管理者は、目的の OS バージョンを使って VM テンプレートを作成し、それを使用してプール内のすべての VM にパッチを適用する必要があります。 

次のパッチ適用シナリオをサポートします。
- Windows 7 SP1 は、Windows 8 または Windows 8.1 にパッチを適用できます。
- Windows 8 は Windows 8.1 にパッチを適用できます。
- Windows 8.1 は Windows 10 にパッチを適用できます。

### <a name="upgrade-unmanaged-shared-vm-collections"></a>アンマネージド共有 VM コレクションのアップグレード 
エンド ユーザーは自分のパーソナル デスクトップをアップグレードできません。 管理者がこのアップグレードを実行する必要があります。 正確な手順はまだ決定されていません。