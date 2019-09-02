---
title: 仮想マシンの自動ライセンス認証
TOCTitle: Automatic VM Activation
description: Windows Server 2019、Windows Server 2016、および Windows Server 2012 R2 で VM のライセンス認証を行う方法
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
ms.openlocfilehash: 18e20433050371dc02782fb8630a885e53ae31ad
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63688702"
---
# <a name="automatic-virtual-machine-activation"></a>仮想マシンの自動ライセンス認証

> 適用対象:Windows Server 2019、Windows Server 半期チャネル、Windows Server 2016、Windows Server 2012 R2

仮想マシンの自動ライセンス認証 (AVMA) は、購入証明メカニズムとして機能し、Windows 製品が製品使用権利およびマイクロソフト ソフトウェア ライセンス条項に従って使用されていることを保証します。

AVMA では、適切にライセンス認証されている Windows サーバーに仮想マシンをインストールできます。各仮想マシンのプロダクト キーを管理する必要はありません。インターネットに接続されていない環境でも同様です。 AVMA は仮想マシンのライセンス認証をライセンスを付与する仮想化サーバーにバインドし、起動時に仮想マシンをアクティブにします。 また AVMA では、仮想マシンの使用状況に関するリアルタイムのレポートや仮想マシンのライセンス状態に関する履歴データも提供されます。 レポートの作成やデータの追跡は仮想化サーバーで行うことができます。

## <a name="practical-applications"></a>実際の適用例

ボリューム ライセンスまたは OEM ライセンスを使用してライセンス認証されている仮想化サーバー上で、AVMA にはいくつかの利点があります。

サーバー データセンター管理者は、AVMA を使用して次の操作を実行できます。

  - 遠隔地にある仮想マシンをライセンス認証する

  - インターネット接続の有無にかかわらず仮想マシンをライセンス認証する

  - 仮想化されたシステムにアクセスする権限をまったく必要とせずに、仮想マシンの使用状況とライセンス状態を仮想化サーバーから追跡する

サーバー上で管理するプロダクト キーも表示するステッカーもありません。 仮想マシンが仮想化サーバーのアレイ間で移行された場合でも、その仮想マシンはライセンス認証され、引き続き動作します。

Service Provider License Agreement (SPLA) パートナーやその他のホスティング プロバイダーは、テナントとプロダクト キーを共有したり、テナントの仮想マシンにライセンス認証のためにアクセスしたりする必要はありません。 AVMA を使用しているとき、仮想マシンのライセンス認証はテナントに対して透過的に行われます。 ホスティング プロバイダーはサーバーのログを使用して、ライセンスの準拠を確認し、クライアントの使用履歴を追跡できます。

## <a name="system-requirements"></a>システム要件

AVMA には、Windows Server 2019 Datacenter、Windows Server 2016 Datacenter、または Windows Server 2012 R2 を実行している Microsoft の仮想化サーバーが必要です。 

以下に、異なるバージョンのホストでライセンス認証を行えるゲストを示します。

|サーバー ホストのバージョン|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|
|-|-|-|-|
|Windows Server 2019|X|X|X|
|Windows Server 2016| |X|X|
|Windows Server 2012 R2| ||X|

これらはすべてのエディション (Datacenter、Standard、または Essentials) のライセンス認証を行うことに注意してください。

このツールは、他の仮想化サーバー テクノロジでは機能しません。

## <a name="how-to-implement-avma"></a>AVMA を実装する方法

1.  Windows Server Datacenter の仮想化サーバーで、Microsoft Hyper-V Server の役割をインストールして構成します。 詳細については、[Hyper-V Server のインストール](../virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server.md)に関するページを参照してください。

2.  [仮想マシンを作成](../virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v.md)し、そこに、サポートされているサーバー オペレーティング システムをインストールします。

3.  仮想マシンに AVMA キーをインストールします。 管理者特権のコマンド プロンプトで、次のコマンドを実行します。
    
    ``` 
    slmgr /ipk <AVMA_key>  
    ```

仮想マシンは、仮想化サーバーに対して自動的にライセンス認証を実行します。


> [!TIP]
> また、Unattend.exe セットアップ ファイルで AVMA キーを使用することもできます。


## <a name="avma-keys"></a>AVMA キー

Windows Server 2019 には以下の AVMA キーを使用できます。

|エディション|   AVMA キー|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|標準|  TNK62-RXVTB-4P47B-2D623-4GF74|
|Essentials|    2CTP7-NHT64-BP62M-FV6GG-HFV28|
 
Windows Server バージョン 1809 には以下の AVMA キーを使用できます。

|エディション|   AVMA キー|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|標準|  TNK62-RXVTB-4P47B-2D623-4GF74|

Windows Server バージョン 1803 および 1709 には以下の AVMA キーを使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|標準|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|


Windows Server 2016 には以下の AVMA キーを使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|標準|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|
|Essentials|B4YNW-62DX9-W8V6M-82649-MHBKQ|


Windows Server 2012 R2 では、次の AVMA キーを使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|Y4TGP-NPTV9-HTC2H-7MGQ3-DV4TW|
|標準|DBGBW-NPF86-BJVTX-K3WKJ-MTB6V|
|Essentials|K2XGM-NMBT3-2R6Q8-WF2FK-P36R2|

## <a name="reporting-and-tracking"></a>レポートと追跡

仮想化サーバーのレジストリ (KVP) は、ゲスト オペレーティング システムにリアルタイム追跡データを提供します。 このレジストリ キーは仮想マシンと共に移動するため、ライセンス情報も同様に取得できます。 既定では、KVP は仮想マシンに関する次のような情報を返します。

  - 完全修飾ドメイン名 (Fully qualified domain name)。

  - インストールされているオペレーティング システムとサービス パック

  - プロセッサ アーキテクチャ

  - IPv4 および IPv6 のネットワーク アドレス

  - RDP アドレス

この情報を取得する方法について詳しくは、[Hyper-V スクリプトでのKVP GuestIntrinsicExchangeItems の参照](http://blogs.msdn.com/b/virtual_pc_guy/archive/2008/11/18/hyper-v-script-looking-at-kvp-guestintrinsicexchangeitems.aspx)に関するページを参照してください。


> [!NOTE]
> KVP のデータはセキュリティで保護されません。 変更が可能であり、変更内容も監視されません。



> [!IMPORTANT]
> AVMA キーが別のプロダクト キー (リテール、OEM、またはボリューム ライセンス キー) に置き換えられた場合、KVP のデータは削除してください。


AVMA の要求に関する履歴データは、仮想化サーバー上のログ ファイル (EventID 12310) にあります。

AVMA のライセンス認証は透過的であるため、エラー メッセージは表示されません。 ただし、次のイベントは、仮想マシン上のログ ファイル (EventID 12309) に記録されます。

|通知|説明|
|-|-|
|AVMA Success|仮想マシンがライセンス認証されました。|
|Invalid Host|仮想化サーバーが応答していません。 この問題は、サーバーがサポートされているバージョンの Windows を実行していない場合に生じることがあります。|
|Invalid Data|これは通常、破損、暗号化、またはデータの不一致によって、仮想化サーバーと仮想マシンとの通信にエラーが発生したことが原因です。|
|Activation Denied|AVMA ID が一致しないため、仮想化サーバーはゲスト オペレーティング システムのライセンス認証を行うことができませんでした。|

