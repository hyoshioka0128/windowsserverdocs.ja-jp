---
ms.assetid: 13210461-1e92-48a1-91a2-c251957ba256
title: ドライブのファームウェア更新のトラブルシューティング
ms.prod: windows-server
ms.author: toklima
manager: masriniv
ms.technology: storage
ms.topic: article
author: toklima
ms.date: 04/18/2017
ms.openlocfilehash: b62fdfe64ea579f61239dc582c639fb10ec1371c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820885"
---
# <a name="troubleshooting-drive-firmware-updates"></a>ドライブのファームウェア更新のトラブルシューティング

>適用対象: Windows 10、Windows Server (半期チャネル)

Windows 10 バージョン 1703 以降と Windows Server (半期チャネル) には、ファームウェア更新可能 AQ (追加修飾子) によって認定済みの HDD と SSD のファームウエアを PowerShell を介して更新する機能が含まれています。

この機能について詳しくは、以下をご覧ください。

- [Windows Server 2016 でのドライブのファームウェアの更新](update-firmware.md)
- [記憶域スペースダイレクトにダウンタイムを発生させずにドライブのファームウェアを更新する](https://channel9.msdn.com/Blogs/windowsserver/Update-Drive-Firmware-Without-Downtime-in-Storage-Spaces-Direct)

ファームウェア更新では、さまざまな理由によって障害が発生します。 この記事では、高度なトラブルシューティングに役立つ情報を提供します。

  > [!Note]
  > 問題によっては、この記事の情報だけでは、考えられるすべての障害のケースを完全にデバッグできない場合があります。

## <a name="common-issues"></a>一般的な問題
アーキテクチャの観点から見ると、この新しい機能は、Windows ストレージ スタックに実装されている API を PowerShell によって呼び出して使用します。 ストレージ スタックに業界標準のコマンドが正しく実装されるかどうかは、ドライバーとハードウェアに依存します。 そのため、障害が発生する可能性のあるポイントが複数存在します。 その中でもよく見られるのは、以下の問題です。

1.  対象のドライブが、業界標準のコマンドを正しく実装していない (AQ を持っていない)
2.  更新の実行に必要な API が実装されていないか、不具合がある (サード パーティ製ドライバーを使用している場合)
3.  API は機能しているが、ファームウェア自体に問題がある (無効または破損したイメージなど)

以下では、使用するドライバーがマイクロソフト製の場合とサード パーティ製の場合のそれぞれについて、トラブルシューティングの方法を説明します。

## <a name="identifying-inappropriate-hardware"></a>問題のあるハードウェアの特定
デバイスが適切なコマンドのセットをサポートしているかどうかを確認する最も簡単な方法は、単純に PowerShell を起動し、ディスクを表す PhysicalDisk オブジェクトを Get-StorageFirmwareInfo コマンドレットに渡すことです。 以下に例を示します。

```powershell
Get-PhysicalDisk -SerialNumber 15140F55976D | Get-StorageFirmwareInformation
```
以下に出力例を示します。

```
PhysicalDisk          : MSFT_PhysicalDisk (ObjectId = "{1}\\TOKLIMA-DL380\root/Microsoft/Windo...)
SupportsUpdate        : True
NumberOfSlots         : 1
ActiveSlotNumber      : 0
SlotNumber            : {0}
IsSlotWritable        : {True}
FirmwareVersionInSlot : {0013}
```

少なくとも SATA デバイスと NVMe デバイスでは、SupportsUpdate フィールドを確認して、組み込みの PowerShell 機能によってファームウェアを更新できるかどうかを判断できます。

しかし SAS 接続デバイスは、常に SupportsUpdate フィールドを "True" とレポートします。これは、適切なコマンドがサポートされているかどうかを業界標準コマンドを使って照会できないためです。

SAS デバイスが、必要なコマンド セットをサポートしているかどうかを確認するには、以下の 2 つの方法があります。
1.  適切なファームウェア イメージを使って Update-StorageFirmware コマンドレットを実行してみる
2.  Windows Server カタログを参照して、FW 更新プログラム AQ が正常に取得された SAS デバイスを特定します (https://www.windowsservercatalog.com/)

### <a name="remediation-options"></a>考えられる解決方法
テスト対象のデバイスが適切なコマンド セットをサポートしていない場合、必要なコマンド セットを備えた新しいファームウェアの提供についてベンダーに問い合わせるか、「Windows Server Catalogue」を参照して、適切なコマンド セットを実装する調達可能なデバイスを探します。

## <a name="troubleshooting-with-3rd-party-drivers-sas"></a>サードパーティ製ドライバー (SAS) のトラブルシューティング
ハードウェアと最も緊密にやり取りするソフトウェア コンポーネントは、Windows ストレージ スタックのミニポート ドライバーです。 SATA や NVMe などの一部のストレージ プロトコルについて、マイクロソフトは、ネイティブの Windows ドライバーを提供しています。 これらのドライバーでは、さらに詳細なデバッグ情報を取得できます。 ただし、サード パーティのハードウェア ベンダーとソフトウェア ベンダーは、自社のデバイス対応のミニポート ドライバーを自由に作成することができるため、サポートされるデバッグ情報のレベルがベンダーによって異なることがあります。

ミニポート ドライバーに関係なく、ファームウェアのダウンロードで発生した問題を特定し、ストレージ スタックに送信された API をアクティブ化するには、次のイベント ログ チャネルを確認してください。

イベント ビューアー - [アプリケーションとサービス ログ] - [Microsoft] - [Windows] - [StorDiag] - **[Microsoft-Windows-Storage-ClassPnP/Operational]**

このチャネルには、ミニポート ドライバーに送信された Windows API に関する情報と、それに対するミニポート ドライバーからの応答が記録されています。 たとえば、SAS HBA 経由で接続されている SATA デバイスにファームウェアをダウンロードしようとしたが、その SAS HBA に SAS から SATA への必要な変換機能が正しく実装されていない場合は、以下のエラー状態が表示されます。

```powershell
Get-PhysicalDisk -SerialNumber 44GS103UT5EW | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.enc -SlotNumber 0
```
この場合の出力例を以下に示します。

```
Update-StorageFirmware : Failed

Extended information:
A warning or error has been encountered during storage firmware update.
Incorrect function.

Activity ID: {1224482b-2315-4a38-81eb-27bb7de19c00}
At line:1 char:47
+ ... S103UT5EW | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.en ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo          : NotSpecified: (:) [Update-StorageFirmware], CimException
+ FullyQualifiedErrorId : StorageWMI 4,Microsoft.Management.Infrastructure.CimCmdlets.InvokeCimMethodCommand,Update-StorageFirmware
```
    
PowerShell がエラーをスローし、呼び出された関数 (つまり Kernel API) が誤っていたという情報を受信しています。 この情報から、API がサードパーティ製の SAS ミニポート ドライバによって実装されなかったか (この例ではこれが原因です)、API がダウンロード セグメントの不整合などの、他の理由によって失敗したことが考えられます。

```
EventData
DeviceGUID  {132EDB55-6BAC-A3A0-C2D5-203C7551D700}
DeviceNumber    1
Vendor  ATA 
Model   TOSHIBA THNSNJ12
FirmwareVersion 6101
SerialNumber    44GS103UT5EW
DownLevelIrpStatus  0xc0000185
SrbStatus   132
ScsiStatus  2
SenseKey    5
AdditionalSenseCode 36
AdditionalSenseCodeQualifier    0
CdbByteCount    10
CdbBytes    3B0E0000000001000000
NumberOfRetriesDone 0
```

チャネルからの ETW イベント507は、SCSI SRB 要求が失敗したことを示し、SenseKey が "5" (無効な要求) であること、および AdditionalSense 情報が ' 36 ' (CDB の無効なフィールド) であることを示しています。

   > [!Note]
   > この情報は対象のミニポートから直接提供されるため、この情報の精度はミニポート ドライバーの実装と性能に依存します。

ミニポート ドライバーがエラー状態を正確に区別しない場合、1 つのエラー コードが複数のエラー状態を意味することがあります。 たとえば、SAS HBA 経由で SATAデバイスに無効なファームウェア イメージをダウンロードしようとした場合 (通常、デバイスが失敗する) も、同じエラー コードが表示される可能性があります。

複数のプロトコルが混在するために変換が行われる場合 (つまり SATA が SAS の背後にある場合)、SATA デバイスを直接 SATA コントローラーに接続してテストして、問題を切り分けることをお勧めします。

### <a name="remediation-options"></a>考えられる解決方法
サード パーティ製のドライバーが必要な API や変換機能を実装していないことが特定された場合、マイクロソフトが提供する SATA または NVMe の代替ドライバー (それぞれ、StorAHCI.sys と StorNVMe.sys) と交換するか、SAS ドライバーの提供元の OEM または HBA ベンダーに、適切なサポートが組み込まれた新しいバージョンの提供について問い合わせることができます。

## <a name="additional-troubleshooting-with-microsoft-drivers-satanvme"></a>マイクロソフト製ドライバー (SATA/NVMe) の高度なトラブルシューティング
StorAHCI.sys や StorNVMe.sys などの Windows ネイティブ ドライバーがストレージ デバイスで使われている場合、ファームウェアの更新作業中に発生したエラーについて詳細情報を取得できる可能性があります。

ClassPnP 運用チャネルを超えると、StorAHCI と Storahci によって、次の ETW チャネルでデバイスのプロトコル固有のリターンコードがログに記録されます。

イベント ビューアー - [アプリケーションとサービス ログ] - [Microsoft] - [Windows] - [StorDiag] - **[Microsoft-Windows-Storage-StorPort/Diagnose]**

診断ログは既定では表示されませんが、イベント ビューアーで [表示] をクリックし、ドロップダウン メニューの [分析およびデバッグ ログの表示] をオンにすると、アクティブ化されて表示されます。

このような詳細なログ エントリを収集するには、ログを有効にしたうえでファームウェア更新時の障害を再現し、診断ログを保存します。

以下では、ダウンロードしたイメージが無効であったために、SATA デバイスのファームウェア更新が失敗した例を示します (イベント ID: 258)。

``` 
EventData
MiniportName    storahci
MiniportEventId 19
MiniportEventDescription    Firmware Activate Completion
PortNumber  0
Bus 2
Target  0
LUN 0
Irp 0xffff8c84cd45aca0
Srb 0xffffab0024030bc0
Parameter1Name  SrbStatus
Parameter1Value 130
Parameter2Name  ReturnCode
Parameter2Value 0
Parameter3Name  FeaturesReg
Parameter3Value 15
Parameter4Name  SectorCountReg
Parameter4Value 0
Parameter5Name  DriveHeadReg
Parameter5Value 160
Parameter6Name  CommandReg
Parameter6Value 146
Parameter7Name  NULL
Parameter7Value 0
Parameter8Name  NULL
Parameter8Value 0
```

上記のイベントでは、パラメーター値 2 ～ 6 にデバイスの詳細情報が含まれています。 ここで、これらの ATA レジスタ値を検討してみましょう。 Download Microcode コマンドの失敗に関する以下の値は、ATA ACS 仕様を参照して解釈できます。
- リターン コード: 0 (0000 0000) (該当せず - ペイロードが転送されていないため何も意味しません)
- 機能:15 (0000 1111) (ビット1は ' 1 ' に設定され、"abort" を示します)
- SectorCount: 0 (0000 0000) (該当せず)
- DriveHead: 160 (1010 0000) (該当せず - 設定されているのは廃止されたビットのみです)
- コマンド: 146 (1001 0010) (sense データの可用性を示す ' 1 ' に設定されているビット 1)

この情報から、ファームウェア更新操作はデバイスによって中止されたことがわかります。

Windows ネイティブの NVMe ドライバー (StorNVMe.sys) が動作する NVMe デバイスを使用する場合は、このチャネルで同程度のレベルの情報が利用できます。
