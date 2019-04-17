---
title: "Windows Server 2016 のヘルス サービス"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 5bc71e71-920e-454f-8195-afebd2a23725
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 834fcfb749e89e4768dce3f229564feea550a432
ms.sourcegitcommit: 30fcae929ce7b611f5d3a5f8fee64b0299272110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2017
---
# <a name="health-service-in-windows-server-2016"></a>Windows Server 2016 のヘルス サービス
> Windows Server 2016 に適用されます。

ヘルス サービスは、日常的な監視、改善する Windows Server 2016 と記憶域スペース ダイレクトを実行するクラスター操作エクスペリエンスの新機能です。

## <a name="prerequisites"></a>前提条件  

ヘルス サービスは既定では、記憶域スペース ダイレクトを有効になっています。 設定または開始には、追加の操作は必要ありません。 記憶域スペース ダイレクトの詳細については、次を参照してください。[記憶域スペース ダイレクトでは、Windows Server 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)します。  

## <a name="reports"></a>レポート

参照してください[ヘルス サービスのレポート](health-service-reports.md)します。

## <a name="faults"></a>障害

参照してください[ヘルス サービス障害](health-service-faults.md)します。

## <a name="actions"></a>アクション

参照してください[ヘルス サービス アクション](health-service-actions.md)します。

## <a name="automation"></a>オートメーション  

このセクションでは、ディスクのライフ サイクルでヘルス サービスで自動化されるワークフローについて説明します。  

### <a name="disk-lifecycle"></a>ディスクのライフ サイクル   

ヘルス サービスは、物理ディスクのライフ サイクルのほぼすべての段階を自動化します。 展開の初期状態が、最適な正常、つまり、すべての物理ディスクが正常に動作してみましょう。  

#### <a name="retirement"></a>サポート終了  

不要になったされると対応する障害が発生したときに、物理ディスクが自動的にリタイアしました。 これにはいくつかのケースがあります。  

-   メディアの障害: 物理ディスクが明確に故障失敗したか破損, と置き換える必要があります。  

-   通信の損失: 物理ディスク接続が失われたために 15 分間にわたってします。  

-   応答不能: 物理ディスクが発生して待機時間または 1 時間以内に複数回 3 5.0 秒以上のします。  

>[!NOTE]
> 接続が一度に多数の物理ディスクを切断するか、またはヘルス サービスでは、ノード全体または記憶域エンクロージャに場合*いない*根本原因である可能性がないために、これらのディスクをインベントリから削除します。  

場合は、使用停止されたディスクは、その他の多数の物理ディスクのキャッシュとして機能していた、これらは自動的に再割り当てする別のキャッシュ ディスクがある場合。 特殊なユーザー操作は必要ありません。  

#### <a name="restoring-resiliency"></a>回復性の復元  

物理ディスクが削除されているヘルス サービスすぐに開始完全回復性を復元する、残りの物理ディスクにデータをコピーします。 これが完了したら、データは完全に保護され、再びフォールト トレラント新たに。  

>[!NOTE]
> このように即時に復元では、残りの物理ディスク間でのための十分な使用可能な容量が必要です。  

#### <a name="blinking-the-indicator-light"></a>インジケーター ライトの点滅  

可能であれば、ヘルス サービスは、使用停止された物理ディスクまたはそのスロットのインジケーター ライトが点滅開始されます。 これは無期限に続きます使用停止されたディスクが交換されるまでです。  

>[!NOTE]
> 場合によっては、ディスクが失敗した機能インジケーター ライトもをこれらの方法でなど、合計停電します。  

#### <a name="physical-replacement"></a>物理的な交換  

可能な場合、使用停止された物理ディスクを置き換える必要があります。 ほとんどの場合、これから成る、ホット スワップでつまり ノードまたはストレージ格納装置の電源を切る必要はありません。 役に立つ場所と一部の情報でのエラーを参照してください。  

#### <a name="verification"></a>検証

代わりのディスクが挿入されると、コンポーネントのサポートされているドキュメントに照らし合わせて検証されます (次のセクションを参照してください)。

#### <a name="pooling"></a>プール  

許可された場合、代替ディスクはその前身のプールに使用できるように自動的に置き換えられます。 この時点では、システムが完全に正常、初期状態に返され、し、障害は表示されなくなります。  

## <a name="supported-components-document"></a>サポートされているコンポーネントのドキュメント  

ヘルス サービスは、管理者またはソリューション ベンダーによって提供されるサポートされているコンポーネント ドキュメントに記憶域スペース ダイレクトで使用されるコンポーネントを制限する強制メカニズムを提供します。 これは、使用できますを誤って使用のサポートされていないハードウェアを防ぐためにするか、他のユーザーによって保証やサポート契約の順守に役立つことがあります。 この機能は、Ssd、Hdd などの物理ディスク デバイスに現在制限と、NVMe ドライブします。 コンポーネントのサポートされているドキュメントは、モデル、製造元 (省略可能)、およびファームウェアのバージョン (オプション) に制限できます。

### <a name="usage"></a>使用状況  

コンポーネントのサポートされているドキュメントは、XML を基にした構文を使用します。 Visual Studio Code など、使い慣れたテキスト エディターを使用することをお勧め (利用可能なを無料で[ここ](http://code.visualstudio.com/)) またはメモ帳を保存して再利用する XML ドキュメントを作成します。

#### <a name="sections"></a>セクションでは

ドキュメントには 2 つの独立したセクション:**ディスク**と**キャッシュ**します。

場合、**ディスク**セクションには、プールに参加表示されているドライブのみを許可します。 一覧にないすべてのドライブは運用環境での使用方法を効果的にこれらをプールに参加したり、されません。 このセクションでは、空のまま場合、任意のドライブをプールに参加する許可されます。

場合、**キャッシュ**セクションには、表示されているドライブのみをキャッシュとして使用されます。 このセクションでは、空のまま、記憶域スペース ダイレクトを試みます推測メディアの種類、バスの種類に基づいています。 たとえば、ソリッド ステート ドライブ (SSD) とハード ディスク ドライブ (HDD) の展開を使用している場合、以前が自動的に選択; キャッシュ用ただし、オール フラッシュを使用して、展開する場合は、ここでキャッシュを使用するには高い耐久性のデバイスを指定する必要があります。

>[!IMPORTANT]
> ドライブが既にプールされて、使用中で、コンポーネントのサポートされているドキュメントはさかのぼって適用されません。  

#### <a name="example"></a>使用例  

```XML
<Components>

  <Disks>
    <Disk>
      <Manufacturer>Contoso</Manufacturer>
      <Model>XYZ9000</Model>
      <AllowedFirmware>
        <Version>2.0</Version>
        <Version>2.1</Version>
        <Version>2.2</Version>
      </AllowedFirmware>
      <TargetFirmware>
        <Version>2.1</Version>
        <BinaryPath>\\path\to\image.bin</BinaryPath>
      </TargetFirmware>
    </Disk>
  </Disks>

  <Cache>
    <Disk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </Disk>
  </Cache>

</Components>

```

複数のドライブを一覧表示、追加するだけ追加**&lt;ディスク&gt;** 、どちらのセクション内のタグ。

記憶域スペース ダイレクトを展開する場合は、この XML を挿入を使用して、 **XML**フラグ。

```PowerShell
Enable-ClusterS2D -XML <MyXML>
```

設定またはコンポーネントのサポートされているドキュメントを変更したら、記憶域スペース ダイレクトが展開されている (つまり、ヘルス サービスが既に実行中) したら、次の PowerShell コマンドレットを使用します。

```PowerShell
$MyXML = Get-Content <\\path\to\file.xml> | Out-String  
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $MyXML  
```

>[!NOTE]
>モデル、製造元、およびファームウェアのバージョンのプロパティと完全に一致を使用して取得した値、 **Get-physicaldisk**コマンドレット。 ベンダーの実装によっては、「常識的な」想定この異なる可能性があります。 たとえば、"Contoso"ではなく、製造元が"Contoso"、かモデルが"Contoso XZY9000"は、空白になります可能性があります。  

次の PowerShell コマンドレットを使用して確認できます。  

```PowerShell
Get-PhysicalDisk | Select Model, Manufacturer, FirmwareVersion  
```

## <a name="settings"></a>設定

参照してください[ヘルス サービスの設定](health-service-settings.md)します。

## <a name="see-also"></a>参照してください。

- [ヘルス サービスをレポートします。](health-service-reports.md)
- [ヘルス サービス障害](health-service-faults.md)
- [ヘルス サービス アクション](health-service-actions.md)
- [ヘルス サービスの設定](health-service-settings.md)
- [Windows Server 2016 での記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)
