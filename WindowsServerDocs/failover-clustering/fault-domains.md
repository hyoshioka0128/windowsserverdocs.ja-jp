---
ms.assetid: 56fc7f80-9558-467e-a6e9-a04c9abbee33
title: フォールト ドメインの認識
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-failover-clustering
ms.topic: article
author: cosmosdarwin
ms.date: 09/16/2016
ms.openlocfilehash: 18b7a932cc8a22c356fde89baa316c0532ebc374
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476001"
---
# <a name="fault-domain-awareness"></a>フォールト ドメインの認識

> 適用対象:Windows Server 2019 と Windows Server 2016

フェールオーバー クラスタリングでは、複数のサーバーが連携して高可用性 (言い換えれば、ノードのフォールト トレランス) を実現できます。 今日の企業が、インフラストラクチャからさらに高い可用性を要求します。 クラウドのようなアップタイムを達成するには、シャーシの障害、ラックの停止、自然災害など、発生する可能性が極めて低い事態であっても対策を講じる必要があります。 その理由はシャーシ、ラック、およびサイトのフォールト トレランスも導入された Windows Server 2016 のフェールオーバー クラスタ リングします。

## <a name="fault-domain-awareness"></a>フォールト ドメインの認識

障害ドメインとフォールト トレランスは、密接に関連する概念です。 障害ドメインとは、単一障害点を共有するハードウェア コンポーネントのセットです。 特定のレベルのフォールト トレランスを実現するには、そのレベルに複数の障害ドメインが必要です。 たとえば、ラックのフォールト トレランスを実現するには、サーバーとデータが複数のラックに分散されている必要があります。

この短いビデオでは、Windows Server 2016 での障害ドメインの概要を示します。  
[![Windows Server 2016 での障害ドメインの概要を見るには、この画像をクリックします。](media/Fault-Domains-in-Windows-Server-2016/Part-1-Fault-Domains-Overview.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-1-Overview)

### <a name="fault-domain-awareness-in-windows-server-2019"></a>Windows Server 2019 の障害ドメインの認識

障害ドメインの認識は Windows Server 2019 で使用できますが、既定で無効にし、Windows レジストリを使用して有効にする必要があります。

Windows Server 2019 の障害ドメインの認識を有効にするには、Windows レジストリに移動し、(Get クラスター) を設定します。レジストリ キーを AutoAssignNodeSite を 1 にします。

```Registry
    (Get-Cluster).AutoAssignNodeSite=1
```

Windows 2019 の障害ドメインの認識を無効にするには、Windows レジストリに移動し、(Get クラスター) を設定します。AutoAssignNodeSite のレジストリ キーを 0 にします。

```Registry
    (Get-Cluster).AutoAssignNodeSite=0
```

## <a name="benefits"></a>利点
- **記憶域スペースを含む記憶域スペース ダイレクトでは、障害ドメインを使用して、データの安全性を最大化します。**  
    記憶域スペースの回復性は、分散型の、ソフトウェアで定義される RAID と概念的に似ています。 すべてのデータの複数コピーは、同期されて保持されます。ハードウェアで障害が発生して、1 つのコピーが失われると、回復性を復元するために、他のコピーが再びコピーされます。 回復性を最適化するには、別個の障害ドメイン内にコピーが保持される必要があります。

- **[ヘルス サービス](health-service-overview.md)使用の障害より役立つアラートを提供するドメイン。**  
    各障害ドメインを場所のメタデータと関連付けることができます。これは後続のアラートに自動的に含まれるようになります。 これらの記述子は、運用や保守の担当者の役に立ちます。これらの記述子でハードウェアを明確にすることにより、エラーを減らすこともできます。  

- **ストレッチ クラスタ リング、ストレージ関連の障害ドメインが使用されます。** ストレッチ クラスタリングにより、遠隔地のサーバーを一般的なクラスターに参加させることができます。 最高のパフォーマンスのためには、記憶域を提供するサーバーの近くにあるサーバーでアプリケーションまたは仮想マシンを実行する必要があります。 障害ドメインの認識は、この記憶域のアフィニティを使用できます。   

## <a name="levels-of-fault-domains"></a>障害ドメインのレベル  
障害ドメインには、サイト、ラック、シャーシ、ノードという 4 つの標準的なレベルがあります。 ノードは自動的に検出されます。追加の各レベルはオプションです。 たとえば、展開でブレード サーバーを使用しない場合、シャーシ レベルは合理的でない可能性があります。  

![障害ドメインのさまざまなレベルの図](media/Fault-Domains-in-Windows-Server-2016/levels-of-fault-domains.png)

## <a name="usage"></a>使用方法  
PowerShell または XML マークアップを使用すると、障害ドメインを指定します。 どちらの方法も同等であり、完全な機能が提供されます。

>[!IMPORTANT]
> 障害ドメインを指定してから、可能であれば、記憶域スペース ダイレクトを有効にします。 これにより、シャーシまたはラックのフォールト トレランスのためにプール、階層、および設定 (回復性や列の数など) を準備する自動構成が可能になります。 プールとボリュームが作成された後に、障害ドメイン トポロジの変化に応じてデータが遡及的に移動することはありません。 記憶域スペース ダイレクトを有効にした後に、シャーシ間やラック間でノードを移動するには、`Remove-ClusterNode -CleanUpDisks` を使用して、最初にノードとそのドライブをプールから削除する必要があります。

### <a name="defining-fault-domains-with-powershell"></a>PowerShell を使用した障害ドメインの定義
Windows Server 2016 には、障害ドメインを使用する次のコマンドレットが導入されています。
* `Get-ClusterFaultDomain`
* `Set-ClusterFaultDomain`
* `New-ClusterFaultDomain` 
* `Remove-ClusterFaultDomain`

このショート ビデオでは、これらのコマンドレットの使用法を説明します。
[![クラスターの障害ドメインのコマンドレットの使用状況に関する短いビデオを視聴するには、この画像をクリックします。](media/Fault-Domains-in-Windows-Server-2016/Part-2-Using-PowerShell.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-2-Using-PowerShell)

使用`Get-ClusterFaultDomain`を現在の障害ドメイン トポロジを確認します。 これにより、クラスター内のすべてのノードと、作成したシャーシ、ラック、またはサイトが一覧表示されます。 **-Type** や **-Name** といったパラメーターを使用して、フィルター処理できます。ただし、これらのパラメーターは必須ではありません。

```PowerShell
Get-ClusterFaultDomain
Get-ClusterFaultDomain -Type Rack
Get-ClusterFaultDomain -Name "server01.contoso.com"
```

使用`New-ClusterFaultDomain`新しいシャーシ、ラック、またはサイトを作成します。 `-Type`と`-Name`パラメーターが必要です。 使用可能な値を`-Type`は`Chassis`、 `Rack`、および`Site`します。 `-Name`任意の文字列を使用することができます。 (の`Node`名前、種類の障害ドメインはセットとして、実際のノード名を自動的にする必要があります)。

```PowerShell
New-ClusterFaultDomain -Type Chassis -Name "Chassis 007"
New-ClusterFaultDomain -Type Rack -Name "Rack A"
New-ClusterFaultDomain -Type Site -Name "Shanghai"
```

> [!IMPORTANT]  
> Windows Server では、ことはできず、作成するすべての障害ドメインが実際の物理的な世界では何もに対応していることを確認しません。 (当然のことが理解することが重要)。現実の世界で 1 つのラックにすべてのノードが含まれる場合に、ソフトウェアで 2 つの `-Type Rack` 障害ドメインを作成しても、ラックのフォールト トレランスが魔法のように実現することはありません。 上記のコマンドレットを使用して、ハードウェアの実際の配置と一致するトポロジを作成する必要があります。

使用`Set-ClusterFaultDomain`別に 1 つの障害ドメインを移動します。 "親" と "子" という用語は、この入れ子の関係を説明するのに一般的に使用されます。 `-Name`と`-Parent`パラメーターが必要です。 `-Name`、移動する障害ドメインの名前を指定`-Parent`、変換先の名前を指定します。 複数の障害ドメインを一度に移動するには、それらの名前を列記します。

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent "Rack A"
Set-ClusterFaultDomain -Name "Rack A", "Rack B", "Rack C", "Rack D" -Parent "Shanghai"
```

> [!IMPORTANT]  
> 障害ドメインが移動するときは、その子も一緒に移動します。 上記の例で、Rack A が server01.contoso.com の親である場合、server01.contoso.com は、現実の世界と同様に、親 (Rack A) の移動先 (Shanghai サイト) にすでに存在するため、別途 Shanghai サイトに移動する必要はありません。

出力に親子関係を確認できます`Get-ClusterFaultDomain`の`ParentName`と`ChildrenNames`列。

使用することも`Set-ClusterFaultDomain`障害ドメインの他の特定のプロパティを変更します。 たとえば、行うことができます省略可能な`-Location`または`-Description`障害ドメインのメタデータ。 この情報を指定すると、ヘルス サービスからのハードウェアのアラートにこの情報が含まれるようになります。 使用して、障害ドメインの名前を変更することもできます、`-NewName`パラメーター。 名前を変更しない`Node`障害ドメインを入力します。

```PowerShell
Set-ClusterFaultDomain -Name "Rack A" -Location "Building 34, Room 4010"
Set-ClusterFaultDomain -Type Node -Description "Contoso XYZ Server"
Set-ClusterFaultDomain -Name "Shanghai" -NewName "China Region"
```

使用`Remove-ClusterFaultDomain`シャーシ、ラック、または作成したサイトを削除します。 `-Name` パラメーターは必須です。 できませんの子を含む障害ドメインの削除 – 最初に、削除する子かを使用して外部に移動`Set-ClusterFaultDomain`します。 その他のすべての障害ドメインの外部での障害ドメインを移動するに次のように設定します。 その`-Parent`を空の文字列 ("")。 削除することはできません`Node`障害ドメインを入力します。 複数の障害ドメインを一度に削除するには、それらの名前を列記します。

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent ""
Remove-ClusterFaultDomain -Name "Rack A"
```

### <a name="defining-fault-domains-with-xml-markup"></a>XML マークアップによる障害ドメインの定義
XML を基にした構文を使用して、障害ドメインを指定できます。 Visual Studio Code ( *[こちら](https://code.visualstudio.com/)* から無料で入手できます) やメモ帳など、使い慣れたテキスト エディターを使用して、保存して再利用できる XML ドキュメントを作成することをお勧めします。  

このショート ビデオでは、障害ドメインを指定するための XML マークアップの使用法を説明します。

[![XML を使用して、障害ドメインを指定する方法に関する簡単なビデオを視聴するには、この画像をクリックします。](media/Fault-Domains-in-Windows-Server-2016/Part-3-Using-XML-Markup.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-3-Using-XML)

PowerShell では、次のコマンドレットを実行します:`Get-ClusterFaultDomainXML`します。 これにより、クラスターの現在の障害ドメインの詳細が XML として返されます。 これを反映してすべて検出`<Node>`を開いたり閉じたりでラップされた、`<Topology>`タグ。  

次のコマンドレットを実行して、この出力をファイルに保存します。  

```PowerShell
Get-ClusterFaultDomainXML | Out-File <Path>  
```

ファイルを開くし、追加`<Site>`、 `<Rack>`、および`<Chassis>`サイト、ラック、シャーシにわたってこれらのノードを分散する方法を指定するタグ。 すべてのタグは、一意の **Name** で識別される必要があります。 ノードについては、既定で設定された名前をそのまま保持する必要があります。  

> [!IMPORTANT]  
> すべての追加タグはオプションですが、推移的な Site &gt; Rack &gt; Chassis &gt; Node の階層に従って、適切に閉じられる必要があります。  
自由形式の名前だけでなく`Location="..."`と`Description="..."`記述子は、任意のタグに追加できます。  

#### <a name="example-two-sites-one-rack-each"></a>以下に例を示します。2 つのサイトでは、1 つのラック  

```XML
<Topology>  
  <Site Name="SEA" Location="Contoso HQ, 123 Example St, Room 4010, Seattle">  
    <Rack Name="A01" Location="Aisle A, Rack 01">  
      <Node Name="Server01" Location="Rack Unit 33" />  
      <Node Name="Server02" Location="Rack Unit 35" />  
      <Node Name="Server03" Location="Rack Unit 37" />  
    </Rack>  
  </Site>  
  <Site Name="NYC" Location="Regional Datacenter, 456 Example Ave, New York City">  
    <Rack Name="B07" Location="Aisle B, Rack 07">  
      <Node Name="Server04" Location="Rack Unit 20" />  
      <Node Name="Server05" Location="Rack Unit 22" />  
      <Node Name="Server06" Location="Rack Unit 24" />  
    </Rack>  
  </Site>  
</Topology> 
``` 

#### <a name="example-two-chassis-blade-servers"></a>例: 2 つのシャーシ、ブレード サーバー  
```XML
<Topology>  
  <Rack Name="A01" Location="Contoso HQ, Room 4010, Aisle A, Rack 01">  
    <Chassis Name="Chassis01" Location="Rack Unit 2 (Upper)" >  
      <Node Name="Server01" Location="Left" />  
      <Node Name="Server02" Location="Right" />  
    </Chassis>  
    <Chassis Name="Chassis02" Location="Rack Unit 6 (Lower)" >  
      <Node Name="Server03" Location="Left" />  
      <Node Name="Server04" Location="Right" />  
    </Chassis>  
  </Rack>  
</Topology>  
```

新しい障害ドメインの詳細を設定するには、XML を保存し、PowerShell で、次を実行します。  

```PowerShell
$xml = Get-Content <Path> | Out-String  
Set-ClusterFaultDomainXML -XML $xml
```

このガイドは 2 つの例を表示しますが、 `<Site>`、 `<Rack>`、 `<Chassis>`、および`<Node>`タグの混在し、展開の物理トポロジを反映するようにその他多くの方法で照合できますは。 上記の例は、これらのタグの柔軟性と、タグを明確にするための自由形式の Location 記述子の価値を説明しています。  

### <a name="optional-location-and-description-metadata"></a>省略可能: メタデータの場所および説明

オプションを指定する**場所**または**説明**障害ドメインのメタデータ。 この情報を指定すると、ヘルス サービスからのハードウェアのアラートにこの情報が含まれるようになります。 この短いビデオでは、このような記述子の追加の値を示します。

[![クリックすると、障害ドメインに location 記述子を追加する値を示す短いビデオを参照してください。](media/Fault-Domains-in-Windows-Server-2016/part-4-location-description.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-4-Location-Description)

## <a name="see-also"></a>関連項目  
- [Windows Server 2019 の概要](https://docs.microsoft.com/windows-server/get-started-19/get-started-19)  
- [Windows Server 2016 を概要します。](https://docs.microsoft.com/windows-server/get-started/server-basics)  
-   [記憶域スペース ダイレクトの概要](../storage/storage-spaces/storage-spaces-direct-overview.md) 
