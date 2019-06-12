---
title: Windows Server 2016 へのリモート デスクトップ サービス展開を移行します。
description: この記事では、Windows Server 2016 の新しいサーバーに、リモート デスクトップ サービス展開を移行する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
msreviewer: ''
nams.suite: ''
nams.technology: remote-desktop-services
ms.author: chrimo
ms.date: 11/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b1fa833-4325-48a8-bf34-46265f40c001
author: christianmontoya
manager: scottman
ms.openlocfilehash: 0e4736f753fc0ad2ece6135de84d481eecb8b7a1
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812589"
---
# <a name="migrate-your-remote-desktop-services-deployment-to-windows-server-2016"></a>Windows Server 2016 へのリモート デスクトップ サービス展開を移行します。

Windows Server 2012 R2 のリモート デスクトップ サービスを実行中の場合は、Azure SQL と記憶域スペース ダイレクトのサポートなどの新機能を活用するために Windows Server 2016 に移動できます。

Windows Server 2016 を実行している移行先サーバーへの Windows Server 2016 を実行している移行元サーバーからリモート デスクトップ サービス展開の移行がサポートされています。 つまり、Windows Server 2016 を Windows Server 2012 R2 で RDS から直接のインプレース移行ではありません。 代わりに、RDS のコンポーネントのほとんどは、まず Windows Server 2016 にアップグレードし、データとライセンスを移行します。 直接の移行で唯一のコンポーネントは、RD Web、RD ゲートウェイ、およびライセンス サーバーは。

アップグレード プロセスと要件の詳細については、次を参照してください。 [、リモート デスクトップ サービス展開を Windows Server 2016 にアップグレードする](upgrade-to-rds-2016.md)します。

リモート デスクトップ サービス デプロイを移行するのにには、次の手順を使用します。

- [RD 接続ブローカー サーバーを移行します。](#migrate-rdconnection-broker-servers)

- [セッション コレクションを移行します。](#migrate-session-collections)

- [仮想デスクトップ コレクションを移行します。](#migrate-virtual-desktop-collections)

- [RD Web アクセス サーバーを移行します。](#migrate-rdweb-access-servers)

- [RD ゲートウェイ サーバーを移行します。](#migrate-rdgateway-servers)

- [RD ライセンス サーバーを移行します。](#migrate-rdgateway-servers)

- [証明書を移行します。](#migrate-certificates)

## <a name="migrate-rdconnection-broker-servers"></a>RD 接続ブローカー サーバーを移行します。

これは、移行の最初に行う最も重要な手順: Windows Server 2016 を実行している移行先サーバーに RD 接続ブローカーを移行します。

> [!IMPORTANT]
> 移行をサポートする高可用性のため、リモート デスクトップ接続ブローカー (RD 接続ブローカー) 移行元サーバーを構成する必要があります。 詳細については、次を参照してください。[リモート デスクトップ接続ブローカーのクラスターのデプロイ](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)します。

1. 高可用性の設定で複数の RD 接続ブローカー サーバーを扱う場合は、現在アクティブなサーバーを除くすべての RD 接続ブローカー サーバーを削除します。

2. [アップグレード](upgrade-to-rds-2016.md)Windows Server 2016 へのデプロイで残っている RD 接続ブローカー サーバー。

3. 高可用性の展開には、Windows Server 2016 の RD 接続ブローカー サーバーを追加します。

> [!NOTE] 
> RD 接続ブローカー サーバーでは、Windows Server 2016 および Windows Server 2012 R2 での混在する高可用性構成はサポートされていません。 Windows Server 2016 を実行している RD 接続ブローカーは、Windows Server 2012 R2 を実行している RD セッション ホスト サーバーのセッション コレクションを利用でき、Windows Server 2012 R2 を実行している RD 仮想化ホスト サーバーと仮想デスクトップ コレクションも利用できます。

## <a name="migrate-session-collections"></a>セッション コレクションを移行する

Windows Server 2016 でのセッション コレクションに Windows Server 2012 R2 でのセッション コレクションを移行する手順に従います。

> [!IMPORTANT]
> 前の手順を正常に完了した後にのみ、セッション コレクションを移行[移行 RD 接続ブローカー サーバー](#migrate-rdconnection-broker-servers)します。

1. [セッション コレクションをアップグレード](Upgrade-to-RDSH-2016.md)から Windows Server 2016 を Windows Server 2012 R2。

2. セッション コレクションに Windows Server 2016 を実行している新しい RD セッション ホスト サーバーを追加します。

3. RD セッション ホスト サーバーのすべてのセッションからサインアウトし、セッション コレクションから移行を必要とするサーバーを削除します。

   > [!NOTE]
   > UVHD テンプレート (uvhd-template.vhdx) がセッション コレクションで有効になっている、ファイル サーバーが新しいサーバーに移行されている場合は、ユーザー プロファイル ディスクを更新します。場所のコレクション プロパティを新しいパスです。 ユーザー プロファイル ディスクを利用するための新しい場所の相対パスは、移行元サーバーでの相対パスと同じになっている必要があります。
   >
   > Windows Server 2012 R2 および Windows Server 2016 を実行しているサーバーが混在している RD セッション ホスト サーバーのセッション コレクションはサポートされていません。

## <a name="migrate-virtual-desktop-collections"></a>仮想デスクトップ コレクションを移行する

Windows Server 2016 を実行している移行先サーバーに Windows Server 2012 R2 を実行している移行元サーバーから仮想デスクトップ コレクションを移行する手順に従います。

> [!IMPORTANT]
> 前の手順を正常に完了した場合にのみ仮想デスクトップ コレクションを移行[移行 RD 接続ブローカー サーバー](#migrate-rdconnection-broker-servers)します。

1. [仮想デスクトップ コレクションのアップグレード](Upgrade-to-RDVH-2016.md)サーバーから Windows Server 2016 を Windows Server 2012 R2 を実行します。

2. 仮想デスクトップ コレクションに新しい Windows Server 2016 の RD 仮想化ホスト サーバーを追加します。

3. RD 仮想化ホスト サーバーで実行されている、現在の仮想デスクトップ コレクション内にあるすべての仮想マシンを、新しいサーバーに移行します。

4. 移行元サーバーの仮想デスクトップ コレクションから、移行したすべての RD 仮想化ホスト サーバーを削除します。

> [!NOTE]
> UVHD テンプレート (uvhd-template.vhdx) がセッション コレクションで有効になっている、ファイル サーバーが新しいサーバーに移行されている場合は、ユーザー プロファイル ディスクを更新します。場所のコレクション プロパティを新しいパスです。 ユーザー プロファイル ディスクを利用するための新しい場所の相対パスは、移行元サーバーでの相対パスと同じになっている必要があります。
>
> Windows Server 2012 R2 および Windows Server 2016 を実行しているサーバーが混在している RD 仮想化ホスト サーバーの仮想デスクトップ コレクションはサポートされていません。

## <a name="migrate-rdweb-access-servers"></a>RD Web アクセス サーバーを移行する

RD Web アクセス サーバーを移行するこれらの手順に従います。

- リモート デスクトップ サービス展開を Windows Server 2016 を実行している移行先サーバーを参加させるし、RD Web ロールのインストール

- 使用[IIS Web 配置ツール](https://www.iis.net/)RD Web web サイトの設定を現在の RD Web アクセス サーバーから Windows Server 2016 を実行している移行先サーバーに移行します。

- [証明書を移行](#migrate-certificates)移行先サーバーに Windows Server 2016 を実行します。

- リモート デスクトップ サービス展開から移行元サーバーを削除します。

## <a name="migrate-rdgateway-servers"></a>RD ゲートウェイ サーバーを移行する

RD ゲートウェイ サーバーを移行するこれらの手順に従います。

- リモート デスクトップ サービス展開を Windows Server 2016 を実行している移行先サーバーを参加させるし、RD ゲートウェイの役割のインストール

- 使用[IIS Web 配置ツール](https://www.iis.net/)現在の RD ゲートウェイ サーバーから Windows Server 2016 を実行している移行先サーバーに RD ゲートウェイ エンドポイントの設定を移行します。

- [証明書を移行](#migrate-certificates)移行先サーバーに Windows Server 2016 を実行します。

- リモート デスクトップ サービス展開から移行元サーバーを削除します。

## <a name="migrate-rdlicensing-servers"></a>RD ライセンス サーバーを移行する

Windows Server 2016 を実行している移行先サーバーに Windows Server 2012 または Windows Server 2012 R2 を実行している移行元サーバーから RD ライセンス サーバーを移行する手順に従います。

1. [リモート デスクトップ サービス クライアント アクセス ライセンス (RDS Cal) を移行](migrate-rds-cals.md)移行先サーバーに移行元サーバーからです。

2. 編集、**配置プロパティ**で**サーバー マネージャー** (最初の RD 接続ブローカー サーバーで通常実行される) をリモート デスクトップの管理サーバー上にのみ、新しい RD ライセンスを含めるWindows Server 2016 を実行しているサーバー。

3. 元の RD ライセンス サーバーを非アクティブ化します。**リモート デスクトップ ライセンス マネージャー**、適切なサーバーを右クリックし、ポインターを合わせる**詳細**を選択する**サーバーの非アクティブ化**、ウィザードの手順に従います.

4. 展開から移行元の RD ライセンス サーバーを削除**サーバー マネージャー**リモート デスクトップの管理サーバーにします。

## <a name="migrate-certificates"></a>証明書を移行する

成功した証明書の移行には、両方実際のプロセスの証明書を移行して、リモート デスクトップ サービスの展開プロパティで証明書情報の更新が必要です。

一般的な証明書の移行には、次の手順が含まれています。

- 秘密キーと共に PFX ファイルに証明書をエクスポートします。

- 証明書を PFX ファイルからインポートします。

適切な証明書を移行した後、サーバー マネージャーまたは PowerShell でリモート デスクトップ サービス展開の次の必要な証明書を更新します。

- RD 接続ブローカー - シングル サインオン

- RD 接続ブローカー - RDP ファイルの公開

- RD ゲートウェイの HTTPS 接続

- RD Web アクセスの HTTPS 接続および RemoteApp とデスクトップ接続のサブスクリプション
