---
title: Windows Server でのヘルスサービス
manager: eldenc
ms.author: cosdar
ms.topic: article
ms.assetid: 5bc71e71-920e-454f-8195-afebd2a23725
author: cosmosdarwin
ms.date: 02/09/2018
ms.openlocfilehash: 69bf8d66fdd3e7fac4066791d0521173484a894f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953418"
---
# <a name="health-service-in-windows-server"></a>Windows Server でのヘルスサービス

> 適用先:Windows Server 2019、Windows Server 2016

ヘルスサービスは、Windows Server 2016 の新機能であり、記憶域スペースダイレクトを実行しているクラスターの日常的な監視と操作エクスペリエンスを向上させます。

## <a name="prerequisites"></a>前提条件

既定では、ヘルス サービスは記憶域スペース ダイレクトで有効になっています。 ヘルス サービスを設定または開始するために、他の操作は必要ありません。 記憶域スペースダイレクトの詳細については、「 [Windows Server 2016 の記憶域スペースダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)」を参照してください。

## <a name="reports"></a>Reports

「[ヘルスサービスレポート](health-service-reports.md)」を参照してください。

## <a name="faults"></a>障害

「[ヘルスサービスのエラー](health-service-faults.md)」を参照してください。

## <a name="actions"></a>アクション

「[ヘルスサービスアクション](health-service-actions.md)」を参照してください。

## <a name="automation"></a>オートメーション

このセクションでは、ディスクのライフサイクルにおいて、ヘルス サービスで自動化されるワークフローについて説明します。

### <a name="disk-lifecycle"></a>ディスクのライフサイクル

ヘルス サービスは、物理ディスクのライフサイクルのほぼすべての段階を自動化します。 たとえば、展開の初期状態が完璧に正常、つまりすべての物理ディスクが正常に動作しているとします。

#### <a name="retirement"></a>廃止

物理ディスクは、使用不可能になったとき、および関連する障害が発生したときに自動的に使用停止されます。 いくつかのケースを次に示します。

-   メディアの障害: 物理ディスクは明確に故障したか破損しており、交換する必要があります。

-   通信の損失: 物理ディスクは 15 分間以上連続して接続を失っています。

-   応答不能: 物理ディスクで 5.0 秒以上の待機時間が 1 時間以内に 3 回以上発生しています。

>[!NOTE]
> 一度に多数の物理ディスク、1 つのノード全体、またはストレージ格納装置の接続が失われた場合、こうしたディスクが根本原因である可能性は低いため、ヘルス サービスではこれらのディスクを使用停止*しません*。

使用停止されたディスクが他の多くの物理ディスクのキャッシュとして機能していた場合、これらの物理ディスクは別のキャッシュ ディスクに自動的に再割り当てされます (利用可能なキャッシュ ディスクがある場合)。 ユーザーの操作は特に必要ありません。

#### <a name="restoring-resiliency"></a>回復性の復元

物理ディスクが使用停止されると、完全な回復性を復元するため、ヘルス サービスはすぐにそのディスクのデータを残りの物理ディスクにコピーし始めます。 コピーが完了すると、データは完全に保護され、再びフォールト トレラントになります。

>[!NOTE]
> このように即時に復元を行うには、残りの物理ディスクに利用可能な容量が十分にある必要があります。

#### <a name="blinking-the-indicator-light"></a>インジケーターのライトの点滅

可能な場合、ヘルス サービスは、使用停止された物理ディスクまたはそのスロットのインジケーター ライトを点滅させます。 この点滅は、使用停止されたディスクが交換されるまで無期限に続きます。

>[!NOTE]
> 場合によっては、インジケーター ライトも機能しない状態でディスクに障害が生じることがあります (完全な電源喪失など)。

#### <a name="physical-replacement"></a>物理的な交換

可能な場合は、使用停止された物理ディスクを置き換える必要があります。 多くの場合、これはホットスワップで構成されています。つまり、ノードまたは記憶域エンクロージャの電源をオフにする必要はありません。 場所および部分の情報については「障害」を参照してください。

#### <a name="verification"></a>検証

交換ディスクが挿入されると、サポートされているコンポーネントドキュメントに対して検証されます (次のセクションを参照)。

#### <a name="pooling"></a>Pooling

許可された場合、代替ディスクはその前身のプールに自動で置き換えられ、使用できるようになります。 この時点で、システムは完全に正常な初期状態に戻り、障害は表示されなくなります。

## <a name="supported-components-document"></a>サポートされているコンポーネントドキュメント

ヘルスサービスには、記憶域スペースダイレクトによって使用されるコンポーネントを、管理者またはソリューションベンダーから提供されるサポートされているコンポーネントドキュメントに限定するための実施メカニズムが用意されています。 このメカニズムにより、サポートされていないハードウェアが誤って使用されるのを防ぐことができるため、保証やサポート契約の順守に役立ちます。 現在、この機能は、Ssd、Hdd、NVMe ドライブを含む物理ディスクデバイスに限定されています。 サポートされているコンポーネントドキュメントでは、モデル、製造元 (オプション)、およびファームウェアのバージョン (オプション) を制限できます。

### <a name="usage"></a>使用方法

サポートされているコンポーネントドキュメントでは、XML による構文を使用します。 無料の[Visual Studio Code](https://code.visualstudio.com/)やメモ帳などの任意のテキストエディターを使用して、保存して再利用できる XML ドキュメントを作成することをお勧めします。

#### <a name="sections"></a>セクション

ドキュメントには、とという2つの独立したセクションがあり `Disks` `Cache` ます。

セクションが指定されている場合、に表示され `Disks` ているドライブ (as `Disk` ) のみがプールに参加できます。 一覧にないドライブはプールに参加できないため、運用環境での使用が実質的に妨げられます。 このセクションを空のままにすると、すべてのドライブがプールに参加できるようになります。

セクションが指定されている場合は、表示され `Cache` ているドライブ (as `CacheDisk` ) だけがキャッシュに使用されます。 このセクションを空のままにした場合、記憶域スペースダイレクト[メディアの種類とバスの種類に基づいて推測](../storage/storage-spaces/understand-the-cache.md#cache-drives-are-selected-automatically)が試行されます。 ここに表示されているドライブは、にも表示され `Disks` ます。

>[!IMPORTANT]
> サポートされているコンポーネントのドキュメントは、既にプールおよび使用されているドライブには、遡及的には適用されません。

#### <a name="example"></a>例

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
        <BinaryPath>C:\ClusterStorage\path\to\image.bin</BinaryPath>
      </TargetFirmware>
    </Disk>
    <Disk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </Disk>
  </Disks>

  <Cache>
    <CacheDisk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </CacheDisk>
  </Cache>

</Components>

```

複数のドライブを一覧表示するに `<Disk>` は、またはタグを追加するだけです `<CacheDisk>` 。

記憶域スペースダイレクトを配置するときにこの XML を挿入するには、パラメーターを使用し `-XML` ます。

```PowerShell
$MyXML = Get-Content <Filepath> | Out-String
Enable-ClusterS2D -XML $MyXML
```

記憶域スペースダイレクトが展開された後に、サポートされているコンポーネントドキュメントを設定または変更するには:

```PowerShell
$MyXML = Get-Content <Filepath> | Out-String
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $MyXML
```

>[!NOTE]
>モデル、製造元、およびファームウェアのバージョンのプロパティは、**Get-PhysicalDisk** コマンドレットで取得される値と完全に一致する必要があります。 こうしたプロパティは、ベンダーの実装によっては、ユーザーの "常識的な" 想定とは異なる可能性があります。 たとえば、製造元は "Contoso" ではなく "CONTOSO-LTD" である場合や、製造元は空白でモデルが "Contoso XZY9000" となっている場合があります。

次の PowerShell コマンドレットを使用して確認できます。

```PowerShell
Get-PhysicalDisk | Select Model, Manufacturer, FirmwareVersion
```

## <a name="settings"></a>Settings

[ヘルスサービス設定](health-service-settings.md)を参照してください。

## <a name="additional-references"></a>その他の参照情報

- [レポートのヘルスサービス](health-service-reports.md)
- [ヘルスサービスエラー](health-service-faults.md)
- [ヘルスサービスアクション](health-service-actions.md)
- [ヘルスサービスの設定](health-service-settings.md)
- [Windows Server 2016 での記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)
