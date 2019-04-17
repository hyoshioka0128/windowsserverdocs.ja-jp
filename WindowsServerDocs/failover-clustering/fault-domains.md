---
ms.assetid: 56fc7f80-9558-467e-a6e9-a04c9abbee33
title: "障害ドメインの認識"
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-failover-clustering
ms.topic: article
author: cosmosdarwin
ms.date: 09/16/2016
ms.openlocfilehash: f5c64bb8f8b7d4b8d13c76c4e94cfcf52ee32c30
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="fault-domain-awareness-in-windows-server-2016"></a>Windows Server 2016 での障害ドメインの認識

> 適用対象: Windows Server 2016

フェールオーバー クラスタ リングにより、複数のサーバーが連携して高可用性を提供、または言い換えれば、ノードのフォールト トレランスを提供します。 今日の企業は、インフラストラクチャからさらに高い可用性を要求します。 クラウドのようなアップタイムを達成するため、シャーシの障害、ラックの停止、または自然災害など、発生するもほとんどをから保護する必要があります。 その理由は Windows Server 2016 のフェールオーバー クラスタ リングが導入されていますシャーシ、ラック、およびサイトのフォールト トレランスもします。

障害ドメインとフォールト トレランス、密接に関連する概念です。 障害ドメインとは、単一障害点を共有するハードウェア コンポーネントのセットです。 フォールト トレラントに特定のレベルにするには、そのレベルで複数の障害ドメインが必要です。 たとえば、ラックに、サーバーと、データのフォールト トレラント必要があります分散複数のラック。

このショート ビデオでは、Windows Server 2016 での障害ドメインの概要が表示されます。  
[![Windows Server 2016 での障害ドメインの概要を見るには、この画像をクリックします。](media/Fault-Domains-in-Windows-Server-2016/Part-1-Fault-Domains-Overview.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-1-Overview)

## <a name="benefits"></a>特典
- **記憶域スペース ダイレクトを含む、記憶域スペースでは、障害ドメインを使用して、データの安全性を最大化します。**  
    記憶域スペースの回復性は、分散、ソフトウェア定義の RAID と概念的には同じです。 すべてのデータの複数のコピーは同期状態が維持、ハードウェアが失敗した場合、1 つのコピーが失われた、回復性を復元する他のユーザーに再びコピーされます。 最善の回復性を実現するには、別個の障害ドメインのコピーを保管してください。

- **[ヘルス サービス](health-service-overview.md)使用フォールト ドメインをより役立つアラートを提供します。**  
    各障害ドメインは、後続のアラートに自動的に含まれている、場所のメタデータと関連付けることができます。 これらの記述子は、運用や保守の担当者を支援し、ハードウェアを明確にすることによってエラーを削減できます。  

- **ストレッチ クラスタ リング、記憶域のアフィニティの障害ドメインが使用します。** ストレッチ クラスタ リングでは、一般的なクラスターへの参加の遠隔地のサーバーを許可します。 最適なパフォーマンスをアプリケーションまたは仮想マシンをその記憶域を提供するものに近くにあるサーバーで実行してください。 障害ドメインの認識は、この記憶域のアフィニティを使用できます。   

## <a name="levels-of-fault-domains"></a>障害ドメインのレベル  
障害ドメインのサイト、ラック、シャーシ、およびノードの 4 つの標準的なレベルがあります。 ノードが自動的に検出されました。追加の各レベルはオプションです。 たとえば、展開でブレード サーバーを使用しない場合、シャーシ レベル可能性があります合理的でないします。  

![障害ドメインのさまざまなレベルの図](media/Fault-Domains-in-Windows-Server-2016/levels-of-fault-domains.png)

## <a name="usage"></a>使用状況  
PowerShell または XML マークアップを使用すると、障害ドメインを指定します。 どちらの方法も同等でありフル機能を提供します。

>[!IMPORTANT]
> 可能であれば、記憶域スペース ダイレクトを有効にする前に、障害ドメインを指定します。 これにより、シャーシまたはラックのフォールト トレランスのため、プール、層、および回復性や列の数などの設定を準備する自動構成できます。 プールとボリュームが作成されたら、データが遡及的に移動されません変更に応じて障害ドメイン トポロジします。 シャーシまたはラック間で記憶域スペース ダイレクトを有効にした後のノードを移動するにはまずを削除するノードとそのドライブを使用して、プールから`Remove-ClusterNode -CleanUpDisks`します。

### <a name="defining-fault-domains-with-powershell"></a>PowerShell による障害ドメインを定義します。
Windows Server 2016 には、障害ドメインを使用する、次のコマンドレットが導入されています。
* `Get-ClusterFaultDomain`
* `Set-ClusterFaultDomain`
* `New-ClusterFaultDomain` 
* `Remove-ClusterFaultDomain`

このショート ビデオでは、これらのコマンドレットの使用法を示します。
[![クラスター障害ドメインのコマンドレットの使用状況に関する短いビデオを視聴するには、この画像をクリックします。](media/Fault-Domains-in-Windows-Server-2016/Part-2-Using-PowerShell.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-2-Using-PowerShell)

使用`Get-ClusterFaultDomain`を現在の障害ドメイン トポロジを確認します。 これには、クラスターに加えて、シャーシ、ラック、または作成したサイト内のすべてのノードが一覧表示します。 などのパラメーターを使用してフィルター処理することができます**-種類**または**-名前**、これらは必須ではありませんが、します。

```PowerShell
Get-ClusterFaultDomain
Get-ClusterFaultDomain -Type Rack
Get-ClusterFaultDomain -Name "server01.contoso.com"
```

使用`New-ClusterFaultDomain`を新しいシャーシ、ラック、またはサイトを作成します。 `-Type`と`-Name`必須のパラメーターです。 値`-Type`は`Chassis`、`Rack`、および`Site`します。 `-Name`任意の文字列を指定できます。 (の`Node`名前、種類の障害ドメインはセットと、実際のノード名を自動的にする必要があります)。

```PowerShell
New-ClusterFaultDomain -Type Chassis -Name "Chassis 007"
New-ClusterFaultDomain -Type Rack -Name "Rack A"
New-ClusterFaultDomain -Type Site -Name "Shanghai"
```

> [!IMPORTANT]  
> Windows Server では、ことはできず、作成された障害ドメインが、実際の物理的な世界で何もに対応しているは検証されません。 (この聞こえるかもしれませんが、明らかにを理解することが重要です。)現実の世界で、すべてのノードが 1 つのラックを場合、作成し、2 つ`-Type Rack`ソフトウェアでの障害ドメインではラックのフォールト トレランスが魔法提供しません。 これらのコマンドレットを使用して作成するトポロジ、ハードウェアの実際の配置を一致することを確認する責任があります。

使用`Set-ClusterFaultDomain`別に 1 つの障害ドメインを移動します。 条項「親」と「子」は、この入れ子の関係を説明するよく使用されます。 `-Name`と`-Parent`必須のパラメーターです。 `-Name`、; 移動する障害ドメインの名前を指定`-Parent`、移行先の名前を指定します。 複数の障害ドメインを一度に移動するには、その名前を一覧表示します。

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent "Rack A"
Set-ClusterFaultDomain -Name "Rack A", "Rack B", "Rack C", "Rack D" -Parent "Shanghai"
```

> [!IMPORTANT]  
> 障害ドメインを移動するときにその子も一緒に移動します。 上記の例では、後者とは別にする必要はありません、上海サイトに移動する Rack A が server01.contoso.com の親である場合は、– は既にあるため、現実世界の存在、同様にされています。

出力に親子関係を確認できます`Get-ClusterFaultDomain`で、`ParentName`と`ChildrenNames`列です。

使用することも`Set-ClusterFaultDomain`障害ドメインの他の特定のプロパティを変更します。 たとえば、することができますオプション`-Location`または`-Description`任意の障害ドメインのメタデータ。 指定した場合は、ハードウェアのヘルス サービスからアラートにこの情報に含まれています。 使用してフォールト ドメインを変更することも、`-NewName`パラメーター。 名前を変更しない`Node`障害ドメインを入力します。

```PowerShell
Set-ClusterFaultDomain -Name "Rack A" -Location "Building 34, Room 4010"
Set-ClusterFaultDomain -Type Node -Description "Contoso XYZ Server"
Set-ClusterFaultDomain -Name "Shanghai" -NewName "China Region"
```

使用`Remove-ClusterFaultDomain`シャーシ、ラック、または作成したサイトを削除します。 `-Name`パラメーターは必須です。 できません子を含む障害ドメインを削除する-最初に、削除する、子かを使用して外部に移動`Set-ClusterFaultDomain`します。 その他のすべての障害ドメインの外部での障害ドメインを移動するに次のように設定します。その`-Parent`を空の文字列 ("")。 削除することはできません`Node`障害ドメインを入力します。 複数の障害ドメインを一度に削除するのには、その名前を一覧表示します。

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent ""
Remove-ClusterFaultDomain -Name "Rack A"
```

### <a name="defining-fault-domains-with-xml-markup"></a>XML マークアップによる障害ドメインの定義
XML を基にした構文を使用して、障害ドメインを指定できます。 Visual Studio Code など、使い慣れたテキスト エディターを使用することをお勧め (利用可能なを無料で*[ここ](https://code.visualstudio.com/)*) またはメモ帳を保存して再利用する XML ドキュメントを作成します。  

このショート ビデオでは、障害ドメインを指定する XML マークアップの使用法を示します。

[![CXML を使用して、障害ドメインを指定する方法を示す短いビデオを視聴するには、このイメージをクリックして](media/Fault-Domains-in-Windows-Server-2016/Part-3-Using-XML-Markup.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-3-Using-XML)

PowerShell では、次のコマンドレットを実行します:`Get-ClusterFaultDomainXML`します。 これは、XML として、クラスターの現在の障害のドメインの詳細を返します。 これが反映すべて検出`<Node>`を開く、閉じるでラップされた、`<Topology>`タグ。  

この出力をファイルに保存するのには、次を実行します。  

```PowerShell
Get-ClusterFaultDomainXML | Out-File <Path>  
```

ファイルを開いて、および追加`<Site>`、`<Rack>`、および`<Chassis>`タグをサイト、ラック、およびシャーシにこれらのノードを分散する方法を指定します。 すべてのタグは、一意によって識別されなければならず**名**します。 ノードの場合、既定で設定されたノードの名前を維持する必要があります。  

> [!IMPORTANT]  
> 推移的なサイトに従う必要があります、その他のすべてのタグは省略可能ですが、&gt;ラック&gt;シャーシ&gt;Node の階層と正しく閉じられる必要があります。  
名前に加えて、自由形式`Location="..."`と`Description="..."`記述子を任意のタグに追加することができます。  

#### <a name="example-two-sites-one-rack-each"></a>例: 2 つのサイトを 1 つのラック  

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

このガイドでは、2 つの例が、`<Site>`、`<Rack>`、`<Chassis>`、および`<Node>`タグを混在し、展開の物理トポロジを反映するように多くの追加方法に一致することができます物する可能性があります。 これらの例では、これらのタグの柔軟性とを明確にするための自由形式の location 記述子の値を示しています。ご利用ください。  

### <a name="optional-location-and-description-metadata"></a>省略可能: の場所と説明のメタデータ

オプションを提供する**場所**または**説明**任意の障害ドメインのメタデータ。 指定した場合は、ハードウェアのヘルス サービスからアラートにこの情報に含まれています。 このショート ビデオでは、このような記述子を追加する価値について説明します。

[![Cクリックすると、障害ドメインに location 記述子を追加する値を示す短いビデオを参照してください](media/Fault-Domains-in-Windows-Server-2016/part-4-location-description.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-4-Location-Description)

## <a name="see-also"></a>参照してください。  
-   [Windows Server 2016](../get-started/windows-server-2016.md)  
-   [Windows Server 2016 での記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md) 
