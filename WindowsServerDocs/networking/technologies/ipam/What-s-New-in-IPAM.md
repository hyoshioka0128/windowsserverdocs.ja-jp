---
title: IPAM の新機能
description: このトピックでは、Windows Server 2016 で新しく追加または変更された IP アドレス管理 (IPAM) の機能について説明します。
manager: brianlic
ms.topic: get-started-article
ms.assetid: f2f2f1a5-ac2f-41b7-a495-98ad0e2a9b20
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2d30db0228177b80050eaae3e56919245b750a0c
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997342"
---
# <a name="whats-new-in-ipam"></a>IPAM の新機能

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 で新しく追加または変更された IP アドレス管理 (IPAM) の機能について説明します。

IPAM は、エンタープライズまたはクラウドサービスプロバイダー (CSP) ネットワークの IP アドレスと DNS インフラストラクチャに高度なカスタマイズが可能な管理および監視機能を提供します。 IPAM を使用して、動的ホスト構成プロトコル (DHCP) とドメインネームシステム (DNS) を実行しているサーバーの監視、監査、および管理を行うことができます。

## <a name="updates-in-ipam-server"></a><a name="BKMK_IPAM2012R2"></a>IPAM サーバーの更新プログラム
Windows Server 2016 での IPAM の新機能と強化された機能を次に示します。

|機能|新機能か強化された機能か|説明|
|--------------------------|-------------------|---------------|
|[強化された IP アドレス管理](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|強化しました|IPv4/32 および IPv6/128 サブネットの処理や、IP アドレスブロック内の空き IP アドレスのサブネットと範囲の検索などのシナリオでは、IPAM 機能が強化されています。|
|[強化された DNS サービス管理](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|新規|IPAM では、ドメインに参加している Active Directory 統合 DNS サーバーとファイルベースの DNS サーバーの両方について、DNS リソースレコード、条件付きフォワーダー、および DNS ゾーン管理がサポートされています。|
|[統合 DNS、DHCP、IP アドレス (DDI) 管理](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|強化しました|いくつかの新しいエクスペリエンスと統合ライフサイクル管理操作が有効になっています。たとえば、IP アドレスに関連するすべての DNS リソースレコードの視覚化、DNS リソースレコードに基づく IP アドレスの自動インベントリ、DNS と DHCP の両方の操作での IP アドレスのライフサイクル管理などが可能です。|
|[複数の Active Directory フォレストのサポート](#bkmk_ad)|新規|Ipam がインストールされているフォレストと各リモートフォレストの間に双方向の信頼関係がある場合は、IPAM を使用して複数の Active Directory フォレストの DNS および DHCP サーバーを管理できます。|
|[使用率データの消去](#bkmk_purge)|新規|指定した日付よりも古い IP アドレス使用率データを削除することで、IPAM データベースのサイズを減らすことができるようになりました。|
|[Windows PowerShell によるロールベースの Access Control のサポート](#bkmk_ps)|新規|Windows PowerShell を使用して、IPAM オブジェクトのアクセススコープを設定できます。|

### <a name="enhanced-ip-address-management"></a><a name="EIP"></a>強化された IP アドレス管理
次の機能により、IPAM アドレス管理機能が向上します。
>[!NOTE]
>IPAM Windows PowerShell コマンドリファレンスについては、「 [Windows powershell の IP アドレス管理 (ipam) サーバーコマンドレット](/powershell/module/ipamserver/)」を参照してください。

#### <a name="support-for-31-32-and-128-subnets"></a>/31、/32、および/128 サブネットのサポート
Windows Server 2016 の IPAM では、/31、/32、および/128 サブネットがサポートされるようになりました。 たとえば、スイッチ間のポイントツーポイントリンクには、2つのアドレスサブネット (/31 IPv4) が必要になる場合があります。 また、一部のスイッチでは、単一のループバックアドレスが必要になる場合があります (IPv4 の場合は/32、IPv6 の場合は/128)。

#### <a name="find-free-subnets-with-find-ipamfreesubnet"></a>**IpamFreeSubnet を使用してフリーサブネットを検索する**

このコマンドは、割り当てに使用できるサブネット (IP ブロック、プレフィックス長、要求されたサブネットの数) を返します。

使用可能なサブネットの数が要求されたサブネットの数より少ない場合は、使用可能なサブネットが、要求された数よりも少ないことを示す警告と共に返されます。

>[!NOTE]
>この関数は実際にはサブネットを割り当てません。可用性を報告するだけです。 ただし、コマンドレットの出力を**IpamSubnet**コマンドにパイプして、サブネットを作成することができます。

詳細については、「 [IpamFreeSubnet](/powershell/module/ipamserver/Find-IpamFreeSubnet)」を参照してください。

#### <a name="find-free-address-ranges-with-find-ipamfreerange"></a>**IpamFreeRange を使用して、空きアドレス範囲を検索する**

この新しいコマンドは、IP サブネット、範囲で必要なアドレスの数、および要求された範囲の数を指定して、使用可能な IP アドレスの範囲を返します。

コマンドは、要求されたアドレスの数に一致する連続する一連の未割り当ての IP アドレスを検索します。 このプロセスは、要求された範囲の数が見つかるか、使用可能なアドレス範囲が使用できなくなるまで繰り返されます。

> [!NOTE]
> この関数では、実際には範囲が割り当てられず、可用性もレポートされます。 ただし、コマンドレットの出力を**IpamRange**コマンドにパイプして、範囲を作成することができます。

詳細については、「 [IpamFreeRange](/powershell/module/ipamserver/Find-IpamFreeRange)」を参照してください。

### <a name="enhanced-dns-service-management"></a><a name="EDNS"></a>強化された DNS サービス管理
Windows Server 2016 の IPAM では、IPAM が実行されている Active Directory フォレスト内の、ファイルベースのドメインに参加している DNS サーバーの検出がサポートされるようになりました。

さらに、次の DNS 機能が追加されました。

-   Windows Server 2008 以降を実行している DNS サーバーからの DNS ゾーンとリソースレコードのコレクション (DNSSEC に関連するもの以外)。

-   (DNSSEC に関連するものを除く) すべての種類のリソースレコードに対して、プロパティと操作を構成 (作成、変更、および削除) します。

-   プライマリセカンダリゾーンとスタブゾーンを含むすべての種類の DNS ゾーンに対して、プロパティと操作を構成 (作成、変更、削除) します。

-   セカンダリゾーンとスタブゾーンで実行されたタスクは、前方参照ゾーンと逆引き参照ゾーンのどちらであるかに関係なく、トリガーされます。 たとえば、master**からの転送**や、 **master からのゾーンの新しいコピーの転送**などのタスクが該当します。

-   サポートされている DNS 構成 (DNS レコードと DNS ゾーン) のロールベースのアクセス制御。

-   条件付きフォワーダーのコレクションと構成 (作成、削除、編集)。

### <a name="integrated-dns-dhcp-and-ip-address-ddi-management"></a><a name="DDI"></a>統合 DNS、DHCP、IP アドレス (DDI) 管理
Ip アドレスインベントリで IP アドレスを表示する場合、[詳細] ビューには、IP アドレスに関連付けられているすべての DNS リソースレコードを表示するためのオプションがあります。

DNS リソースレコードコレクションの一部として、DNS 逆引き参照ゾーンの PTR レコードが IPAM によって収集されます。 任意の IP アドレス範囲にマップされているすべての逆引き参照ゾーンについて、IPAM は、対応するマップされた IP アドレス範囲内のそのゾーンに属するすべての PTR レコードの IP アドレスレコードを作成します。 IP アドレスが既に存在する場合、PTR レコードはその IP アドレスに関連付けられています。 逆引き参照ゾーンがどの IP アドレスの範囲にもマップされていない場合、IP アドレスは自動的に作成されません。

IPAM を使用して逆引き参照ゾーンに PTR レコードを作成した場合、IP アドレスインベントリは、前述の方法と同じ方法で更新されます。 その後のコレクションでは、IP アドレスが既にシステムに存在しているため、PTR レコードはその IP アドレスに単純にマップされます。

### <a name="multiple-active-directory-forest-support"></a><a name="bkmk_ad"></a>複数の Active Directory フォレストのサポート
Windows Server 2012 R2 では、ipam は、IPAM サーバーと同じ Active Directory フォレストに属している DNS サーバーと DHCP サーバーを検出して管理することができました。 これで、IPAM サーバーがインストールされているフォレストと双方向の信頼関係がある場合に、別の AD フォレストに属する DNS サーバーと DHCP サーバーを管理できるようになりました。 [**サーバー検出の構成**] ダイアログボックスにアクセスして、管理対象の他の信頼されているフォレストからドメインを追加することができます。 サーバーが検出されると、管理エクスペリエンスは、IPAM がインストールされている同じフォレストに属するサーバーと同じになります。

詳細については、「[複数の Active Directory フォレスト内のリソースを管理](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md)する」を参照してください。

### <a name="purge-utilization-data"></a><a name="bkmk_purge"></a>使用率データの消去
使用率データの消去では、古い IP アドレス使用率データを削除して IPAM データベースのサイズを小さくすることができます。 データの削除を実行する場合、日付を指定すると、指定した日付以上のすべてのデータベースエントリが IPAM によって削除されます。

詳細については、「[使用率データの消去](../../technologies/ipam/Purge-Utilization-Data.md)」を参照してください。

### <a name="windows-powershell-support-for-role-based-access-control"></a><a name="bkmk_ps"></a>Windows PowerShell によるロールベースの Access Control のサポート
Windows PowerShell を使用して、ロールベースの Access Control を構成できるようになりました。 Windows PowerShell コマンドを使用して、IPAM の DNS および DHCP オブジェクトを取得し、アクセススコープを変更することができます。 このため、Windows PowerShell スクリプトを作成して、次のオブジェクトにアクセススコープを割り当てることができます。

-   IP アドレス空間

-   IP アドレスブロック

-   IP アドレスサブネット

-   IP アドレス範囲

-   DNS サーバー

-   DNS ゾーン

-   DNS 条件付きフォワーダー

-   DNS リソース レコード

-   DHCP サーバー

-   DHCP スーパースコープ

-   DHCP スコープ

詳細については、「windows powershell での[役割ベースの Access Control の管理](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)」および「windows [Powershell での IP アドレス管理 (IPAM) サーバーコマンドレット](/powershell/module/ipamserver/)」を参照してください。