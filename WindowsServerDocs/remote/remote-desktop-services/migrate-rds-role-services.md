---
title: リモート デスクトップ サービスの展開を Windows Server 2016 に移行する
description: この記事では、新しい Windows Server 2016 サーバーに、リモート デスクトップ サービスの展開を移行する方法について説明します。
ms.author: chrimo
ms.date: 11/01/2016
ms.topic: article
ms.assetid: 9b1fa833-4325-48a8-bf34-46265f40c001
author: christianmontoya
manager: scottman
ms.openlocfilehash: 62c2cc99277b3cf74f6bde5be59b69569c27a31b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961816"
---
# <a name="migrate-your-remote-desktop-services-deployment-to-windows-server-2016"></a>リモート デスクトップ サービスの展開を Windows Server 2016 に移行する

Windows Server 2012 R2 でリモート デスクトップ サービスを実行中の場合は、Azure SQL や記憶域スペース ダイレクトのサポートなどの新機能を活用するために Windows Server 2016 に移動できます。

リモート デスクトップ サービスの展開の移行は、Windows Server 2016 を実行している移行元サーバーから Windows Server 2016 を実行している移行先サーバーへ移行する場合にサポートされます。 つまり、Windows Server 2012 R2 の RDS から Windows Server 2016 への直接的なインプレース移行はできません。 代わりに、RDS のほとんどのコンポーネントは、まず Windows Server 2016 にアップグレードしてからデータとライセンスを移行します。 直接移行が可能なコンポーネントは、RD Web、RD ゲートウェイ、およびライセンス サーバーのみです。

アップグレード プロセスと要件の詳細については、「[リモート デスクトップ サービスの展開を Windows Server 2016 にアップグレードする](./upgrade-to-rds.md)」を参照してください。

次の手順を使用して、リモート デスクトップ サービスの展開を移行します。

- [RD 接続ブローカー サーバーを移行する](#migrate-rdconnection-broker-servers)

- [セッション コレクションを移行する](#migrate-session-collections)

- [仮想デスクトップ コレクションを移行する](#migrate-virtual-desktop-collections)

- [RD Web アクセス サーバーを移行する](#migrate-rdweb-access-servers)

- [RD ゲートウェイ サーバーを移行する](#migrate-rdgateway-servers)

- [RD ライセンス サーバーを移行する](#migrate-rdgateway-servers)

- [証明書を移行する](#migrate-certificates)

## <a name="migrate-rdconnection-broker-servers"></a>RD 接続ブローカー サーバーを移行する

これは移行のために最初に行う最も重要な手順で、Windows Server 2016 を実行している移行先サーバーに RD 接続ブローカーを移行します。

> [!IMPORTANT]
> リモート デスクトップ接続ブローカー (RD 接続ブローカー) 移行元サーバーは、高可用性によって移行がサポートされるように構成する必要があります。 詳細については、[リモート デスクトップ接続ブローカー クラスターの展開](./rds-connection-broker-cluster.md)に関する記事を参照してください。

1. 高可用性の設定で複数の RD 接続ブローカー サーバーを扱う場合は、現在アクティブなサーバーを除くすべての RD 接続ブローカー サーバーを削除します。

2. 展開内に残っている RD 接続ブローカー サーバーを Windows Server 2016 に[アップグレード](./upgrade-to-rds.md)します。

3. Windows Server 2016 RD 接続ブローカー サーバーを高可用性展開に追加します。

> [!NOTE]
> Windows Server 2016 と Windows Server 2012 R2 が混在する高可用性の構成は、RD 接続ブローカー サーバーではサポートされません。
> Windows Server 2016 を実行している RD 接続ブローカーは、Windows Server 2012 R2 を実行している RD セッション ホスト サーバーを使用したセッション コレクションにサービスを提供できます。また、Windows Server 2012 R2 を実行している RD 仮想化ホスト サーバーを使用した仮想デスクトップ コレクションにサービスを提供できます。

## <a name="migrate-session-collections"></a>セッション コレクションを移行する

Windows Server 2012 R2 のセッション コレクションを Windows Server 2016 のセッション コレクションに移行するには、以下の手順を実行します。

> [!IMPORTANT]
> セッション コレクションの移行は、前の手順「[RD 接続ブローカー サーバーを移行する](#migrate-rdconnection-broker-servers)」が正常に完了した場合にのみ実行してください。

1. Windows Server 2012 R2 から Windows Server 2016 に[セッション コレクションをアップグレード](./upgrade-to-rdsh.md)します。

2. セッション コレクションに、Windows Server 2016 を実行している新しい RD セッション ホスト サーバーを追加します。

3. RD セッション ホスト サーバーのすべてのセッションからサインアウトし、セッション コレクションから移行を必要とするサーバーを削除します。

   > [!NOTE]
   > UVHD テンプレート (UVHD-template.vhdx) がセッション コレクションで有効になっており、ファイル サーバーが新しいサーバーに移行されている場合は、新しいパスを使用して、[ユーザー プロファイル ディスク:場所] コレクション プロパティを更新します。 ユーザー プロファイル ディスクを利用するための新しい場所の相対パスは、移行元サーバーでの相対パスと同じになっている必要があります。
   >
   > Windows Server 2012 R2 と Windows Server 2016 を実行しているサーバーが混在する RD セッション ホスト サーバーのセッション コレクションはサポートされていません。

## <a name="migrate-virtual-desktop-collections"></a>仮想デスクトップ コレクションを移行する

Windows Server 2012 R2 を実行している移行元サーバーから Windows Server 2016 を実行している移行先サーバーに仮想デスクトップ コレクションを移行するには、以下の手順を実行します。

> [!IMPORTANT]
> 前の手順「[RD 接続ブローカー サーバーを移行する](#migrate-rdconnection-broker-servers)」が正常に完了した場合にのみ、仮想デスクトップ コレクションを移行してください。

1. Windows Server 2012 R2 を実行しているサーバーから Windows Server 2016 に[仮想デスクトップ コレクションをアップグレード](./upgrade-to-rdvh.md)します。

2. 仮想デスクトップ コレクションに、新しい Windows Server 2016 RD 仮想化ホスト サーバーを追加します。

3. RD 仮想化ホスト サーバーで実行されている、現在の仮想デスクトップ コレクション内にあるすべての仮想マシンを、新しいサーバーに移行します。

4. 移行元サーバーの仮想デスクトップ コレクションから、移行したすべての RD 仮想化ホスト サーバーを削除します。

> [!NOTE]
> UVHD テンプレート (UVHD-template.vhdx) がセッション コレクションで有効になっており、ファイル サーバーが新しいサーバーに移行されている場合は、新しいパスを使用して、[ユーザー プロファイル ディスク:場所] コレクション プロパティを更新します。 ユーザー プロファイル ディスクを利用するための新しい場所の相対パスは、移行元サーバーでの相対パスと同じになっている必要があります。
>
> Windows Server 2012 R2 と Windows Server 2016 を実行しているサーバーが混在する RD 仮想化ホスト サーバーの仮想デスクトップ コレクションはサポートされていません。

## <a name="migrate-rdweb-access-servers"></a>RD Web アクセス サーバーを移行する

RD Web アクセス サーバーを移行するには、次の手順に従います。

- Windows Server 2016 を実行している移行先サーバーを、リモート デスクトップ サービスの展開に参加させ、RD Web の役割をインストールします

- [IIS Web 配置ツール](https://www.iis.net/)を使用して、RD Web の Web サイト設定を、現在の RD Web アクセス サーバーから Windows Server 2016 を実行している移行先サーバーに移行します。

- Windows Server 2016 を実行している移行先サーバーに、[証明書を移行](#migrate-certificates)します。

- リモート デスクトップ サービスの展開から移行元サーバーを削除します。

## <a name="migrate-rdgateway-servers"></a>RD ゲートウェイ サーバーを移行する

RD ゲートウェイ サーバーを移行するには、次の手順に従います。

- Windows Server 2016 を実行している移行先サーバーを、リモート デスクトップ サービスの展開に参加させ、RD ゲートウェイの役割をインストールします

- [IIS Web 配置ツール](https://www.iis.net/)を使用して、RD ゲートウェイのエンドポイント設定を、現在の RD ゲートウェイ サーバーから Windows Server 2016 を実行している移行先サーバーに移行します。

- Windows Server 2016 を実行している移行先サーバーに、[証明書を移行](#migrate-certificates)します。

- リモート デスクトップ サービスの展開から移行元サーバーを削除します。

## <a name="migrate-rdlicensing-servers"></a>RD ライセンス サーバーを移行する

Windows Server 2012 または Windows Server 2012 R2 を実行している移行元サーバーから Windows Server 2016 を実行している移行先サーバーに RD ライセンス サーバーを移行するには、以下の手順を実行します。

1. 移行元サーバーから移行先サーバーに、[リモート デスクトップ サービス クライアント アクセス ライセンス (RDS CAL) を移行](migrate-rds-cals.md)します。

2. (通常、最初の RD 接続ブローカー サーバーで実行される) リモート デスクトップ管理サーバー上の **[サーバー マネージャー]** の **[展開プロパティ]** を編集して、Windows Server 2016 を実行している新しい RD ライセンス サーバーのみを含めるようにします。

3. 元の RD ライセンス サーバーを非アクティブ化します。**リモート デスクトップ ライセンス マネージャー** で、適切なサーバーを右クリックし、 **[Advanced]\(詳細\)** にポインターを合わせて **[サーバーの非アクティブ化]** を選択し、ウィザードの手順に従います。

4. リモート デスクトップ ライセンス マネージャーの **[サーバー マネージャー]** で、移行元の RD ライセンス サーバーを展開から削除します。

## <a name="migrate-certificates"></a>証明書を移行する

証明書を正しく移行するには、証明書を実際に移行するプロセスと、リモート デスクトップ サービスの展開プロパティで証明書情報を更新するプロセスの両方が必要です。

証明書の一般的な移行には、次の手順が含まれます。

- 証明書を秘密キーと共に PFX ファイルにエクスポートします。

- 証明書を PFX ファイルからインポートします。

適切な証明書を移行した後、サーバー マネージャーまたは PowerShell で、リモート デスクトップ サービスの展開のために必要な次の証明書を更新します。

- RD 接続ブローカー - シングル サインオン

- RD 接続ブローカー - RDP ファイルの公開

- RD ゲートウェイ - HTTPS 接続

- RD Web アクセス - HTTPS 接続および RemoteApp とデスクトップ接続のサブスクリプション
