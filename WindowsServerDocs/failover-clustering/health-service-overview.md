---
title: Windows Server の正常性サービス
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 5bc71e71-920e-454f-8195-afebd2a23725
author: cosmosdarwin
ms.date: 02/09/2018
ms.openlocfilehash: 5afb64dcf0c59697ed55d7cf51ef1bc36e7e0e36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863813"
---
# <a name="health-service-in-windows-server"></a>Windows Server の正常性サービス

> 適用対象: Windows Server 2016

ヘルス サービスは、日常的な監視を強化する Windows Server 2016 で記憶域スペース ダイレクトを実行するクラスターの運用エクスペリエンスの新しい機能です。

## <a name="prerequisites"></a>前提条件  

既定では、ヘルス サービスは記憶域スペース ダイレクトで有効になっています。 ヘルス サービスを設定または開始するために、他の操作は必要ありません。 記憶域スペース ダイレクトの詳細については、次を参照してください。 [Storage Spaces Direct in Windows Server 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)します。  

## <a name="reports"></a>レポート

参照してください[ヘルス サービスのレポート](health-service-reports.md)します。

## <a name="faults"></a>障害

参照してください[ヘルス サービスのエラー](health-service-faults.md)します。

## <a name="actions"></a>Actions

参照してください[ヘルス サービス アクション](health-service-actions.md)します。

## <a name="automation"></a>自動化  

このセクションでは、ディスクのライフサイクルにおいて、ヘルス サービスで自動化されるワークフローについて説明します。  

### <a name="disk-lifecycle"></a>ディスクのライフサイクル   

ヘルス サービスは、物理ディスクのライフサイクルのほぼすべての段階を自動化します。 たとえば、展開の初期状態が完璧に正常、つまりすべての物理ディスクが正常に動作しているとします。  

#### <a name="retirement"></a>使用停止  

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

可能な場合は、使用停止された物理ディスクを置き換える必要があります。 ほとんどの場合、ホット スワップから成る - つまり、ノードまたは記憶域エンクロージャの電源を切る必要はありません。 場所および部分の情報については「障害」を参照してください。  

#### <a name="verification"></a>検証

代わりのディスクが挿入されると、コンポーネントのサポートされているドキュメントに照らし合わせて検証されます (次のセクションを参照してください)。

#### <a name="pooling"></a>プーリング  

許可された場合、代替ディスクはその前身のプールに自動で置き換えられ、使用できるようになります。 この時点で、システムは完全に正常な初期状態に戻り、障害は表示されなくなります。  

## <a name="supported-components-document"></a>サポートされているコンポーネントのドキュメント  

ヘルス サービスは、管理者またはソリューション ベンダーによって提供されるサポートのコンポーネント ドキュメントに、記憶域スペース ダイレクトで使用されるコンポーネントを制限する強制メカニズムを提供します。 このメカニズムにより、サポートされていないハードウェアが誤って使用されるのを防ぐことができるため、保証やサポート契約の順守に役立ちます。 この機能は Ssd、Hdd などの物理ディスク デバイスに限定されていて、NVMe ドライブします。 コンポーネントのサポートされているドキュメントは、モデル、製造元 (省略可能)、およびファームウェアのバージョン (省略可能) に制限できます。

### <a name="usage"></a>使用方法  

コンポーネントのサポートされているドキュメントは、XML を基にした構文を使用します。 無料など、使い慣れたテキスト エディターを使用することをお勧めします。 [Visual Studio Code](http://code.visualstudio.com/)やメモ帳を保存および再利用できる XML ドキュメントを作成します。

#### <a name="sections"></a>セクション

ドキュメントが 2 つの独立したセクション:`Disks`と`Cache`します。

場合、`Disks`セクションは、提供された、ドライブのみが一覧表示 (として`Disk`) プールに参加することができます。 すべての一覧にないドライブは事実上、運用環境での使用、プールに参加できません。 このセクションが空のままである場合は、プールに参加する任意のドライブが許可されます。

場合、`Cache`セクションは、提供された、ドライブのみが一覧表示 (として`CacheDisk`) のキャッシュに使用されます。 このセクションが空のまま、記憶域スペース ダイレクトしよう[推測では、メディアの種類とバスの種類に基づいて](../storage/storage-spaces/understand-the-cache.md#cache-drives-are-selected-automatically)します。 ここで一覧表示される必要がありますにも表示される`Disks`します。

>[!IMPORTANT]
> ドライブが既にプールに、使用中、コンポーネントのサポートされているドキュメントは過去にさかのぼって適用されません。  

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

複数のドライブを一覧表示、追加`<Disk>`または`<CacheDisk>`タグ。

記憶域スペース ダイレクトを展開するときは、この XML を挿入を使用して、`-XML`パラメーター。

```PowerShell
$MyXML = Get-Content <Filepath> | Out-String  
Enable-ClusterS2D -XML $MyXML
```

設定または記憶域スペース ダイレクトをデプロイした後に、コンポーネントのサポートされているドキュメントを変更します。

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

## <a name="settings"></a>設定

参照してください[ヘルス サービスの設定](health-service-settings.md)します。

## <a name="see-also"></a>関連項目

- [ヘルス サービスをレポートします。](health-service-reports.md)
- [ヘルス サービスの障害](health-service-faults.md)
- [ヘルス サービスの動作](health-service-actions.md)
- [ヘルス サービスの設定](health-service-settings.md)
- [Windows Server 2016 での記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)
