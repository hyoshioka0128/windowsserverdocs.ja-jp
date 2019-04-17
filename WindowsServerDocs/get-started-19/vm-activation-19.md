---
title: 仮想マシンの自動ライセンス認証
TOCTitle: Automatic VM Activation
description: Windows Server 2019、Windows Server 2016 および Windows Server 2012 R2 で Vm をアクティブ化する方法
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: 62873140c8e114ba537dc4fd3ff7c44868c33243
ms.sourcegitcommit: ca5c80bdb903b282e292488172a7cc92546574c0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2018
ms.locfileid: "4375489"
---
# 仮想マシンの自動ライセンス認証

> 適用対象: Windows Server 2019 では、Windows Server 半期チャネルでは、Windows Server 2016、Windows Server 2012 R2

自動仮想マシンのアクティブ化 (AVMA) は、支援、製品使用権とマイクロソフト ソフトウェア ライセンス条項に従って、Windows の製品が使用されていることを確認するために、証明メカニズムとして機能します。

AVMA を使用して、切断された環境であっても各個々 の仮想マシンのプロダクト キーを管理することがなく、適切にアクティブ化された Windows server 仮想マシンをインストールできます。 AVMA では、ライセンスの仮想化のサーバーに仮想マシンのライセンス認証をバインドし、起動時には、仮想マシンをアクティブ化します。 AVMA では、仮想マシンのライセンスの状態の履歴データの使用状況に関するリアルタイム レポートも提供します。 レポートや追跡データは仮想化のサーバーで利用できます。

## 実際の適用例

ボリューム ライセンスまたは OEM ライセンスを使用して有効化される仮想化のサーバーでは、AVMA は、いくつかの利点を提供します。

サーバーのデータ センターのマネージャーは、以下を実行するのに AVMA を使用できます。

  - リモートの場所で仮想マシンのライセンス認証します。

  - 仮想マシンまたはインターネット接続がない場合のライセンス認証します。

  - 仮想化されたシステム上のすべてのアクセス権を必要とせず、仮想化のサーバーから仮想マシンの使用状況とライセンスを追跡します。

プロダクト キーを管理して読み取りをサーバーにシールがありません。 仮想マシンがライセンス認証され、仮想化のサーバーの配列に移行しているときでも、作業を継続します。

サービス プロバイダー ライセンス契約 (SPLA) パートナーおよびその他のホスティング プロバイダーはテナントとプロダクト キーを共有したり、ライセンス認証をテナントの仮想マシンにアクセスする必要はありません。 仮想マシンのライセンス認証は、AVMA を使用すると、テナントに透過的です。 ホスティング プロバイダーをライセンス準拠を確認し、クライアントの使用状況の履歴を追跡する server ログを使用できます。

## システム要件

AVMA には、Windows Server 2019 Datacenter、Windows Server 2016 Datacenter、または Windows Server 2012 R2 を実行している Microsoft 仮想化のサーバーが必要です。 

異なるバージョンのホストをアクティブ化するゲストを以下に示します。

|サーバーのホストのバージョン|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|
|-|-|-|-|
|Windows Server 2019|○|○|○|
|Windows Server 2016| |○|○|
|Windows Server 2012 R2| ||○|

アクティブ化 (Datacenter、Standard、または Essentials) のすべてのエディションがこれらに注意してください。

このツールは、他のサーバーの仮想化テクノロジとは機能しません。

## AVMA を実装する方法

1.  Windows Server Datacenter 仮想化のサーバーでは、インストールし、Microsoft HYPER-V サーバーの役割を構成します。 詳細については、 [HYPER-V サーバーのインストール](../virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server.md)を参照してください。

2.  インストールがサポートされているサーバー オペレーティング システムと[仮想マシンを作成](../virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v.md)します。

3.  仮想マシンで AVMA キーをインストールします。 管理者特権のコマンド プロンプトから次のコマンドを実行します。
    
    ``` 
    slmgr /ipk <AVMA_key>  
    ```

仮想マシンには、仮想化のサーバーに対してライセンスがアクティブに自動的になります。


> [!TIP]
> Unattend.exe セットアップ ファイルで AVMA キーを採用することもできます。


## AVMA キー

次の AVMA キーは、Windows Server 2019 で使用できます。

|エディション|   AVMA キー|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|標準|  TNK62 RXVTB-4P47B-2 次元の 623 4GF74|
|基本情報|    2CTP7-NHT64-BP62M-FV6GG-HFV28|
 
次の AVMA キーは、Windows Server バージョン 1809 で使用できます。

|エディション|   AVMA キー|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|標準|  TNK62 RXVTB-4P47B-2 次元の 623 4GF74|

次の AVMA キーは、Windows Server バージョン 1803 と 1709 で使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|標準|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|


次の AVMA キーは、Windows Server 2016 で使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|標準|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|
|基本情報|B4YNW-62DX9-W8V6M-82649-MHBKQ|


次の AVMA キーは、Windows Server 2012 R2 で使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|Y4TGP-NPTV9-HTC2H-7MGQ3-DV4TW|
|標準|DBGBW-NPF86-BJVTX-K3WKJ-MTB6V|
|基本情報|K2XGM-NMBT3-2R6Q8-WF2FK-P36R2|

## レポートや追跡

仮想化のサーバーのレジストリ (KVP) は、ゲスト オペレーティング システムのリアルタイムの追跡データを提供します。 レジストリ キーは、仮想マシンに移動したとき、ために、ライセンス情報を取得できます。 既定では、KVP は以下を含む、仮想マシンに関する情報を返します。

  - 完全修飾ドメイン名

  - オペレーティング システムとサービス パックがインストールされています。

  - プロセッサ アーキテクチャ

  - IPv4 と IPv6 のネットワーク アドレス

  - RDP アドレス

この情報を取得する方法について詳しくは、以下を参照してください。 [Hyper-v スクリプト: KVP GuestIntrinsicExchangeItems を見ている](http://blogs.msdn.com/b/virtual_pc_guy/archive/2008/11/18/hyper-v-script-looking-at-kvp-guestintrinsicexchangeitems.aspx)します。


> [!NOTE]
> KVP データが保護されていません。 変更できるし、変更を監視されていません。



> [!IMPORTANT]
> 別のプロダクト キー (製品版、OEM、またはボリューム ライセンス キー) を使って AVMA キーが置き換えられる場合、KVP データを削除する必要があります。


AVMA 要求に関する歴史的データは、仮想化のサーバー (イベント Id 12310) のログ ファイルに利用できます。

AVMA のライセンス認証プロセスは透明であるために、エラー メッセージは表示されません。 ただし、次のイベントは、仮想マシン (イベント Id 12309) 上のログ ファイルに取り込まれます。

|通知|説明|
|-|-|
|AVMA の成功|仮想マシンがアクティブ化します。|
|無効なホスト|仮想化のサーバーは、応答性の高いではありません。 これは、サーバーがサポートされているバージョンの Windows を実行されていないときに発生します。|
|無効なデータ|通常、この結果、仮想化のサーバーと破損、暗号化、またはデータの不一致により多くの場合、仮想マシン間の通信でエラーが発生からします。|
|ライセンス認証が拒否されました|仮想化のサーバーには、AVMA ID が一致しないために、ゲスト オペレーティング システムがアクティブにできませんでした。|

