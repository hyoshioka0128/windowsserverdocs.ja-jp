---
title: 仮想マシン自動ライセンス認証
TOCTitle: Automatic VM Activation
description: Windows Server 2019、Windows Server 2016、および Windows Server 2012 R2 での Vm をアクティブ化する方法
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822093"
---
# <a name="automatic-virtual-machine-activation"></a>仮想マシン自動ライセンス認証

> 適用対象:Windows Server 2019、Windows Server 半期チャネルでは、Windows Server 2016、Windows Server 2012 R2

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

AVMA には、Windows Server 2019 Datacenter、Windows Server 2016 Datacenter または Windows Server 2012 R2 を実行している Microsoft の仮想化サーバーが必要です。 

別のバージョンのホストをアクティブ化するゲストを次に示します。

|サーバー ホストのバージョン|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|
|-|-|-|-|
|Windows Server 2019|x|X|x|
|Windows Server 2016| |x|x|
|Windows Server 2012 R2| ||x|

アクティブ化 (Datacenter、Standard、または Essentials) のすべてのエディションがこれらに注意してください。

このツールは、他の仮想化サーバー テクノロジと機能しません。

## <a name="how-to-implement-avma"></a>AVMA を実装する方法

1.  Windows Server Datacenter の仮想化サーバーにインストールし、Microsoft HYPER-V Server ロールを構成します。 詳細については、次を参照してください。 [Hyper-v サーバーのインストール](../virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server.md)します。

2.  [仮想マシンを作成する](../virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v.md)し、サポートされているサーバーのオペレーティング システムをインストールします。

3.  仮想マシンに AVMA キーをインストールします。 管理者特権のコマンド プロンプトで、次のコマンドを実行します。
    
    ``` 
    slmgr /ipk <AVMA_key>  
    ```

仮想マシンは、仮想化サーバーに対して自動的にライセンス認証を実行します。


> [!TIP]
> また、Unattend.exe セットアップ ファイルで AVMA キーを使用することもできます。


## <a name="avma-keys"></a>AVMA キー

次の AVMA キーは、Windows Server 2019 で使用できます。

|エディション|   AVMA キー|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B-2D623-4GF74|
|Essentials|    2CTP7-NHT64-BP62M-FV6GG-HFV28|
 
次の AVMA キーは、Windows Server バージョンは 1809 で使用できます。

|エディション|   AVMA キー|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B-2D623-4GF74|

次の AVMA キーは、Windows Server、バージョン 1803 および 1709 で使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|


次の AVMA キーは、Windows Server 2016 で使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|
|Essentials|B4YNW-62DX9-W8V6M-82649-MHBKQ|


Windows Server 2012 R2 では、次の AVMA キーを使用できます。

|エディション|AVMA キー|
|-|-|
|Datacenter|Y4TGP-NPTV9-HTC2H-7MGQ3-DV4TW|
|Standard|DBGBW-NPF86-BJVTX-K3WKJ-MTB6V|
|Essentials|K2XGM-NMBT3-2R6Q8-WF2FK-P36R2|

## <a name="reporting-and-tracking"></a>レポートと追跡

仮想化サーバーのレジストリ (KVP) は、ゲスト オペレーティング システムにリアルタイム追跡データを提供します。 このレジストリ キーは仮想マシンと共に移動するため、ライセンス情報も同様に取得できます。 既定では、KVP は仮想マシンに関する次のような情報を返します。

  - 完全修飾ドメイン名 (Fully qualified domain name)。

  - インストールされているオペレーティング システムとサービス パック

  - プロセッサ アーキテクチャ

  - IPv4 および IPv6 のネットワーク アドレス

  - RDP アドレス

この情報を取得する方法の詳細については、次を参照してください。 [Hyper-v スクリプト。KVP guestintrinsicexchangeitems](http://blogs.msdn.com/b/virtual_pc_guy/archive/2008/11/18/hyper-v-script-looking-at-kvp-guestintrinsicexchangeitems.aspx)します。


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

