---
title: IPAM の新機能
description: このトピックでは、Windows Server 2016 で追加または変更している IP アドレス管理 (IPAM) 機能について説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f2f2f1a5-ac2f-41b7-a495-98ad0e2a9b20
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 04838cba63805d20ba31629ed9c8e95290046320
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624678"
---
# <a name="whats-new-in-ipam"></a>IPAM の新機能

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、Windows Server 2016 で追加または変更している IP アドレス管理 (IPAM) 機能について説明します。  
  
IPAM では、エンタープライズまたはクラウド サービス プロバイダー (CSP) ネットワーク上の IP アドレスと DNS インフラストラクチャの高度にカスタマイズ可能な管理および監視機能を提供します。 監視、監査、および IPAM を使用して、動的ホスト構成プロトコル (DHCP) およびドメイン ネーム システム (DNS) を実行しているサーバーを管理できます。  
  
## <a name="BKMK_IPAM2012R2"></a>IPAM サーバーでの更新  
Windows Server 2016 での IPAM の新機能と更新機能を次に示します。  
  
|機能|新機能か強化された機能か|説明|  
|--------------------------|-------------------|---------------|  
|[IP アドレス管理の強化](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|強化された機能|処理の/32 の IPv4 および IPv6/128 サブネットと IP アドレス ブロックで空き IP アドレスのサブネットと範囲の検索などのシナリオは、IPAM 機能が向上しました。|  
|[DNS サービス管理の強化](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|新規|IPAM では、両方のドメインに参加している Active Directory に統合された、ファイルに格納された DNS サーバー、DNS リソース レコード、条件付きフォワーダー、および DNS ゾーンの管理をサポートしています。|  
|[統合の DNS、DHCP、および IP アドレス (DDI) の管理](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|強化された機能|いくつかの新しいエクスペリエンスし統合型ライフ サイクル管理の操作が有効になっているなど、すべての DNS リソースを視覚化する IP に関連するレコード アドレス、IP アドレスの DNS リソース レコードと IP アドレスのライフ サイクル管理に基づく自動インベントリDNS と DHCP の両方の操作。|  
|[複数の Active Directory フォレストのサポート](#bkmk_ad)|新規|IPAM を使用して、IPAM がインストールされているフォレストおよび各リモート フォレストの間に双方向信頼関係がある場合に、複数の Active Directory フォレストの DNS および DHCP サーバーを管理することができます。|  
|[使用率データを消去します。](#bkmk_purge)|新規|指定した日付より古い IP アドレスの使用率データを削除することで、IPAM データベースのサイズを減らすことができます。|  
|[ロールベースのアクセス制御用 Windows PowerShell のサポート](#bkmk_ps)|新規|Windows PowerShell を使用して、IPAM オブジェクトにアクセス スコープを設定することができます。|  
  
### <a name="EIP"></a>IP アドレス管理の強化  
次の機能には、IPAM のアドレスの管理機能が向上します。  
>[!NOTE]
>IPAM の Windows PowerShell コマンドのリファレンスを参照してください。 [Windows PowerShell を使用した IP アドレス管理 (IPAM) サーバー コマンドレット](https://docs.microsoft.com/en-us/powershell/module/ipamserver/)します。  
  
#### <a name="support-for-31-32-and-128-subnets"></a>31、/32、および/128 サポート サブネット  
ここで 31、/32、および/128 をサポートするサブネットの Windows Server 2016 での IPAM します。 たとえば、2 つのアドレスのサブネット (/31 IPv4) のスイッチ間でのポイント ツー ポイント リンクに必要な場合があります。 一部のスイッチが 1 つのループバック アドレスにも、必要があります (/32 ipv4、IPv6 の/128)。  
  
#### <a name="find-free-subnets-with-find-ipamfreesubnet"></a>**検索 IpamFreeSubnet で無料のサブネットを検索します。**  
  
このコマンドは、割り当て、使用可能なサブネットを返します。 指定された IP ブロック、プレフィックス長、および要求されたサブネットの数。   
  
利用可能なサブネットの数が要求されたサブネットの数よりも小さい場合は、利用可能なサブネットが使用可能な数は、要求された数よりも小さいことを示す警告返されます。  
  
>[!NOTE]
>この関数は実際には、サブネットを割り当てられません、その可用性を報告するだけです。 コマンドレットの出力をパイプするただし、**追加 IpamSubnet**サブネットを作成するコマンド。  
  
詳細については、次を参照してください。[検索 IpamFreeSubnet](https://docs.microsoft.com/en-us/powershell/module/ipamserver/Find-IpamFreeSubnet)します。  
  
#### <a name="find-free-address-ranges-with-find-ipamfreerange"></a>**検索 IpamFreeRange で無料のアドレス範囲を検索します。**  
  
この新しいコマンドを返します。 使用可能な IP アドレスの範囲、IP サブネット、範囲のために必要なアドレスの数、および要求された範囲の数を指定します。   
  
コマンドは、連続する一連の要求されたアドレスの数に一致する未割り当ての IP アドレスを検索します。 要求された範囲の数が見つかるか、使用可能なアドレスの範囲がなくなるまでまで、プロセスが繰り返されます。  
  
> [!NOTE]
> この関数は実際には、範囲を割り当てられません、その可用性を報告するだけです。 コマンドレットの出力をパイプするただし、**追加 IpamRange**範囲を作成するコマンド。  
  
詳細については、次を参照してください。[検索 IpamFreeRange](https://docs.microsoft.com/en-us/powershell/module/ipamserver/Find-IpamFreeRange)します。  
  
### <a name="EDNS"></a>DNS サービス管理の強化  
Windows Server 2016 での IPAM で、IPAM が実行されている Active Directory フォレストでドメインに参加している、ファイル ベースの DNS サーバーの検出できるようになりました。  
  
さらに、次の DNS 機能が追加されました。  
  
-   DNS ゾーンとリソースは、Windows Server 2008 またはそれ以降を実行している DNS サーバーから (DNSSEC に関連するもの) 以外のコレクションを記録します。  
  
-   構成 (作成、変更、および削除) プロパティとリソース レコード (DNSSEC に関連するもの) 以外のすべての型に対する演算。  
  
-   構成 (作成、変更、削除) プロパティとプライマリ セカンダリ、およびスタブ ゾーンを含む DNS ゾーンのすべての型に対する演算)。  
  
-   トリガー セカンダリでのタスクと、スタブ ゾーンに関係なく前方または逆引き参照ゾーンされる場合。 たとえば、タスクなど**マスタから転送**または**マスターからゾーンの新しいコピーを転送**します。  
  
-   サポートされている DNS の構成 (DNS レコードと DNS ゾーン) のロール ベース アクセス制御。  
  
-   条件付きフォワーダのコレクションと構成 (作成、削除、編集)。  
  
### <a name="DDI"></a>統合の DNS、DHCP、および IP アドレス (DDI) の管理  
IP アドレスを IP アドレスのインベントリを表示すると、IP アドレスに関連付けられているすべての DNS リソース レコードを表示する詳細ビューでオプションがあります。  
  
DNS リソース レコードのコレクションの一部としては、IPAM は、DNS の逆引き参照ゾーンの PTR レコードを収集します。 IPAM ではすべて、逆引き参照ゾーンに対して任意の IP アドレス範囲にマップされますが、対応するマップされた IP アドレスの範囲でそのゾーンに属するすべての PTR レコードの IP アドレス レコードを作成します。 IP アドレスが既に存在する場合、PTR レコードは IP アドレスに関連付けられているだけです。 逆引き参照ゾーンは、任意の IP アドレス範囲にマップされていない場合、IP アドレスは自動的に作成されません。  
  
IPAM を使用して、逆引き参照ゾーンで PTR レコードが作成されると、前述のように、同じ方法で、IP アドレス インベントリが更新されます。 後続の収集中に IP アドレスは、システムでは、既に存在しているので PTR レコードは単にマップされますその IP アドレスを持つ。  
  
### <a name="bkmk_ad"></a>複数の Active Directory フォレストのサポート  
Windows Server 2012 r2、IPAM は検出し、IPAM サーバーと同じ Active Directory フォレストに属する DNS および DHCP サーバーを管理することができました。 これで、IPAM サーバーがインストールされているフォレストと双方向信頼関係がある場合は、別の AD フォレストに属する DNS および DHCP サーバーを管理できます。 移動することができます、**サーバー検出の構成** ダイアログ ボックスし、他のドメインが管理するフォレストを信頼されたを追加します。 サーバーが検出されると、管理エクスペリエンスでは、IPAM がインストールされている同じフォレストに属しているサーバーの場合と同様です。  
  
詳細については、次を参照してください[複数の Active Directory フォレスト内のリソースの管理。](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md)  
  
### <a name="bkmk_purge"></a>使用率データを消去します。  
使用率データを消去古い IP アドレスの使用率データを削除して、IPAM データベースのサイズを縮小することができます。 データの削除を実行する日付を指定して IPAM よりも古いすべてのデータベース エントリを削除します。 または指定した日付と等しい。   
  
詳細については、次を参照してください。[使用率データの消去](../../technologies/ipam/Purge-Utilization-Data.md)します。  
  
### <a name="bkmk_ps"></a>ロールベースのアクセス制御用 Windows PowerShell のサポート  
Windows PowerShell を使用して、ロールベースのアクセス制御を構成することができますようになりました。 IPAM での DNS および DHCP のオブジェクトを取得し、アクセス スコープを変更するのには、Windows PowerShell コマンドを使用できます。 このため、次のオブジェクトにアクセス スコープを割り当てる Windows PowerShell スクリプトを記述できます。  
  
-   IP アドレス空間  
  
-   IP アドレス ブロック  
  
-   IP アドレス サブネット  
  
-   IP アドレスの範囲  
  
-   DNS サーバー  
  
-   DNS ゾーン  
  
-   DNS 条件付けフォワーダー  
  
-   DNS リソース レコード  
  
-   DHCP サーバー  
  
-   DHCP スーパースコープ  
  
-   DHCP スコープ  
  
詳細については、次を参照してください。[ロール ベース アクセス制御の管理 Windows PowerShell を使用した](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)と[Windows PowerShell を使用した IP アドレス管理 (IPAM) サーバー コマンドレット](https://docs.microsoft.com/en-us/powershell/module/ipamserver/)します。  

