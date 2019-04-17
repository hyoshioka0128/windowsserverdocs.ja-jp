---
title: IPAM の新機能
description: このトピックでは、Windows Server 2016 で追加または変更されている IP アドレス管理 (IPAM) 機能について説明します。
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
ms.openlocfilehash: b90cd1ab223e38cbf5933b58a594b32d5e3d4858
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-ipam"></a>IPAM の新機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 で追加または変更されている IP アドレス管理 (IPAM) 機能について説明します。  
  
IPAM では、Enterprise、またはクラウド サービス プロバイダー (CSP) ネットワークの IP アドレスと DNS インフラストラクチャに高度にカスタマイズ可能な管理および監視機能を提供します。 監視、監査、および IPAM を使用して、動的ホスト構成プロトコル (DHCP) およびドメイン ネーム システム (DNS) を実行しているサーバーを管理できます。  
  
## <a name="BKMK_IPAM2012R2"></a>IPAM サーバーに更新プログラム  
Windows Server 2016 での IPAM の新機能と更新機能を次に示します。  
  
|機能/|新しい、または改良されて|説明|  
|--------------------------|-------------------|---------------|  
|[IP アドレス管理の強化](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|向上しました|IPv4/32、IPv6 場合は/128 のサブネットを処理し、IP アドレス ブロックでの空き IP アドレスのサブネットと範囲の検索などのシナリオは、IPAM 機能が向上しました。|  
|[DNS サービス管理の強化](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|新機能|IPAM では、両方のドメインに参加している Active Directory 統合され、ファイルに格納された DNS サーバーの DNS リソース レコード、条件付きフォワーダは、および DNS ゾーンの管理をサポートします。|  
|[統合の DNS、DHCP、および IP アドレス (DDI) の管理](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|向上しました|いくつか新しいエクスペリエンスとの統合のライフ サイクル管理、IP アドレスに関連するすべての DNS リソース レコードを視覚化するなどの操作が有効には、DNS リソース レコードと DNS と DHCP の両方の IP アドレスのライフ サイクル管理に基づいて IP アドレスのインベントリに自動化されています。|  
|[複数の Active Directory フォレストのサポート](#bkmk_ad)|新機能|IPAM を使用して、IPAM がインストールされているフォレストおよび各リモートのフォレストの間に双方向信頼関係がある場合は、複数の Active Directory フォレストの DNS および DHCP サーバーを管理することができます。|  
|[使用率データを削除します。](#bkmk_purge)|新機能|指定した日付より古い IP アドレスの使用率データを削除して、IPAM データベースのサイズを減らすことができますようになりました。|  
|[Role Based Access Control 用 Windows PowerShell のサポート](#bkmk_ps)|新機能|Windows PowerShell を使用して、IPAM オブジェクトにアクセス スコープを設定することができます。|  
  
### <a name="EIP"></a>IP アドレス管理の強化  
次の機能には、IPAM のアドレスの管理機能が向上します。  
>[!NOTE]
>IPAM の Windows PowerShell コマンドのリファレンスを参照してください。 [Windows PowerShell の IP アドレス管理 (IPAM) サーバー コマンドレット](https://technet.microsoft.com/library/jj553807.aspx)します。  
  
#### <a name="support-for-31-32-and-128-subnets"></a>/31、/32、および場合は/128 サポート サブネット  
今すぐサポート/31、/32、および場合は/128 サブネットの Windows Server 2016 での IPAM のします。 たとえば、次の 2 つのアドレスのサブネット (/31 IPv4) のスイッチ間 point-to-point リンクに必要な場合があります。 また、一部のスイッチが 1 つのループバック アドレスを必要可能性があります (/32 ipv4、IPv6 の場合は/128)。  
  
#### **<a name="find-free-subnets-with-find-ipamfreesubnet"></a>検索 IpamFreeSubnet による無料のサブネットを検索します。**  
  
このコマンドは返しますサブネットの割り当てに使用可能な IP ブロック、プレフィックスの長さ、および要求されたサブネットの数を指定します。   
  
利用可能なサブネットの数が要求されたサブネットの数より少ない場合は、利用可能なサブネットが利用可能な番号が要求された数よりも少ないリソースであることを示す警告で返されます。  
  
>[!NOTE]
>この関数は実際に割り当てることができません、サブネット、可用性を報告するだけです。 ただし、コマンドレットの出力をパイプすることができます、**追加 IpamSubnet**サブネットを作成するコマンドです。  
  
詳細については、次を参照してください。[検索 IpamFreeSubnet](https://technet.microsoft.com/library/mt712782.aspx)します。  
  
#### **<a name="find-free-address-ranges-with-find-ipamfreerange"></a>検索 IpamFreeRange で無料のアドレスの範囲を検索します。**  
  
この新しいコマンドを返します利用可能な IP アドレスの範囲、IP サブネット、範囲のために必要なアドレスの数と要求された範囲の数を指定します。   
  
要求されたアドレスの数に一致する未割り当ての IP アドレスの継続的な一連のコマンドを検索します。 要求された範囲の数が見つかると、または使用可能なアドレスの範囲は利用できなくなるまでになるまでのプロセスが繰り返されます。  
  
> [!NOTE]
> この関数は実際に割り当てることができません、範囲、可用性を報告するだけです。 ただし、コマンドレットの出力をパイプすることができます、**追加 IpamRange**範囲を作成するコマンドです。  
  
詳細については、次を参照してください。[検索 IpamFreeRange](https://technet.microsoft.com/library/mt712772.aspx)します。  
  
### <a name="EDNS"></a>DNS サービス管理の強化  
Windows Server 2016 での IPAM で、IPAM が実行されている Active Directory フォレストのドメインに参加している、ファイル ベースの DNS サーバーの検出できるようになりました。  
  
さらに、次の DNS の機能が追加されました。  
  
-   DNS ゾーンとリソースは、Windows Server 2008 以降を実行している DNS サーバーから (DNSSEC に関連するもの) 以外のコレクションを記録します。  
  
-   構成 (作成、変更、および削除) プロパティとすべての種類 (以外にも、DNSSEC 関連) リソース レコードの操作します。  
  
-   構成 (作成、変更、削除) プロパティとすべての種類の DNS ゾーンのプライマリ セカンダリ、およびスタブ ゾーンを含む operations)。  
  
-   トリガーされたセカンダリのタスクとスタブ ゾーン、かに関係なく前方または逆引き参照ゾーンされる場合。 たとえば、タスクなど**マスタから転送**または**ゾーンの新しいコピーをマスタから転送**します。  
  
-   サポートされている DNS の構成 (DNS レコードと DNS ゾーン) の役割に基づいたアクセス制御します。  
  
-   条件付きフォワーダのコレクションと構成 (作成、削除、編集)。  
  
### <a name="DDI"></a>統合の DNS、DHCP、および IP アドレス (DDI) の管理  
IP アドレス インベントリで IP アドレスを表示するときに、IP アドレスに関連付けられているすべての DNS リソース レコードを表示する、詳細ビューのオプションがあります。  
  
として一部 DNS リソース レコード コレクションには、IPAM は、DNS 逆引き参照ゾーンの PTR レコードを収集します。 すべての逆引き参照ゾーンは任意の IP アドレス範囲にマップされる、IPAM は、対応する割り当てられた IP アドレスの範囲でそのゾーンに属するすべての PTR レコードの IP アドレス レコードを作成します。 IP アドレスが既に存在する場合、PTR レコードはその IP アドレスに単に関連付けられます。 逆引き参照ゾーンが任意の IP アドレス範囲にマップされていない場合、IP アドレスは自動的に作成されません。  
  
IPAM を使用して、逆引き参照ゾーンの PTR レコードが作成されると、上記のようと同じ方法で、IP アドレス インベントリが更新されます。 後続の収集時に、IP アドレスが、システムに既に存在するため、PTR レコード単にマップされますその IP アドレスを持つ。  
  
### <a name="bkmk_ad"></a>複数の Active Directory フォレストのサポート  
Windows Server 2012 R2 では、IPAM を検出および IPAM サーバーと同じ Active Directory フォレストに属する DNS および DHCP サーバーを管理できませんでした。 IPAM サーバーがインストールされているフォレストと双方向信頼関係がある場合は、別の AD フォレストに属する DNS および DHCP サーバーを管理できます。 移動することができます、**サーバー検出の構成**] ダイアログ ボックスにしてから、その他のドメインに信頼を管理するフォレストを追加します。 サーバーが検出後管理エクスペリエンスは、IPAM がインストールされている同じフォレストに属しているサーバーに対しても同じです。  
  
詳細については、次を参照してください[複数の Active Directory フォレスト内のリソースの管理。](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md)  
  
### <a name="bkmk_purge"></a>使用率データを削除します。  
使用率データの削除では、古い IP アドレスの使用率データの削除で IPAM データベース サイズを小さくことができます。 データの削除を実行する日付を指定して IPAM がよりも古いすべてのデータベースのエントリを削除または、日付を入力します。   
  
詳細については、次を参照してください。[使用率データの消去](../../technologies/ipam/Purge-Utilization-Data.md)します。  
  
### <a name="bkmk_ps"></a>Role Based Access Control 用 Windows PowerShell のサポート  
Windows PowerShell を使用して、役割ベースのアクセス制御を構成するようになりましたことができます。 IPAM 内の DNS および DHCP のオブジェクトを取得し、アクセス スコープを変更する Windows PowerShell コマンドを使用することができます。 このため、次のオブジェクトにアクセス スコープを割り当てるに Windows PowerShell スクリプトを記述できます。  
  
-   IP アドレス空間  
  
-   IP アドレス ブロック  
  
-   IP アドレス サブネット  
  
-   IP アドレスの範囲  
  
-   DNS サーバー  
  
-   DNS ゾーン  
  
-   DNS 条件付きフォワーダ  
  
-   DNS リソース レコード  
  
-   DHCP サーバー  
  
-   DHCP スーパースコープ  
  
-   DHCP スコープ  
  
詳細については、次を参照してください。[管理 Role Based Access Control Windows PowerShell を使用した](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)と[Windows PowerShell の IP アドレス管理 (IPAM) サーバー コマンドレット](https://technet.microsoft.com/library/jj553807.aspx)します。  

