---
ms.assetid: e5945bae-4a33-487c-a019-92a69db8cf6c
title: Windows Server 2016 でドライブのファームウェアを更新する
ms.prod: windows-server-threshold
ms.author: toklima
ms.manager: dmoss
ms.technology: storage-spaces
ms.topic: article
author: toklima
ms.date: 10/04/2016
ms.openlocfilehash: 50291bd4da05d9c2736c84443b444b9a43f46344
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884783"
---
# <a name="updating-drive-firmware-in-windows-server-2016"></a>Windows Server 2016 でドライブのファームウェアを更新する
>適用対象:Windows 10、Windows Server (半期チャネル)、Windows Server 2016

従来、ドライブのファームウェア更新は、ダウンタイムが発生する可能性があり、面倒な作業でした。記憶域スペースと Windows Server、Windows 10 バージョン 1703 以降を改善しているのはそのためです。 新しいファームウェアの更新メカニズムをサポートするハード ドライブが Windows に含まれている場合、運用環境のドライブでもダウンタイムなしでドライブのファームウェアを更新できます。 ただし、運用環境のドライブのファームウェアを更新する場合、この強力な新機能を使用しながらリスクを最小限に抑える方法について、ここで説明するヒントを必ずご覧ください。

  > [!Warning]
  > ファームウェアの更新は危険な可能性があるメンテナンス操作なので、必ず新しいファームウェア イメージを徹底してテストした後で適用する必要があります。 サポートされないハードウェアの新しいファームウェアは、信頼性と安定性に悪影響を及ぼし、さらにはデータを損失する可能性もあります。 管理者は、更新プログラムに付属するリリース ノートを読み、影響と適用可能性を判断する必要があります。

## <a name="drive-compatibility"></a>ドライブの互換性

Windows Server を使用してドライブのファームウェアを更新するには、サポートされるドライブが必要です。 デバイスの共通の動作を確保するため、マイクロソフトではまず、SAS、SATA、NVMe デバイスに対応する新しい (Windows 10 と Windows Server 2016 用の) オプションのハードウェア ラボ キット (HLK) について要件を定義しました。 この要件では、新しい Windows ネイティブ PowerShell コマンドレットを使用してファームウェアを更新するために、SATA、SAS、NVMe デバイスがサポートする必要があるコマンドの概要を示します。 この要件をサポートするために、ベンダー製品が適切なコマンドをサポート、今後のリビジョンで実装できるかどうかを検証する新しい HLK テストがあります。 

お使いのハードウェアが、Windows によるドライブのファームウェア更新をサポートしているかどうかについては、ソリューション ベンダーに問い合わせてください。
次に、多様な要件のリンクを示します。

-   SATA:[Device.Storage.Hd.Sata](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/device-storage#devicestoragehdsata) -、 **[場合実装\]ファームウェアのダウンロードとアクティブ化**セクション
    
-   SAS:[Device.Storage.Hd.Sas](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/device-storage#devicestoragehdsas) -、 **[場合実装\]ファームウェアのダウンロードとアクティブ化**セクション

-   NVMe:[Device.Storage.ControllerDrive.NVMe](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/device-storage#devicestoragecontrollerdrivenvme) - セクション**5.7**と**5.8**します。

## <a name="powershell-cmdlets"></a>PowerShell コマンドレット

Windows に次の 2 つのコマンドレットが追加されました。

-   Get-StorageFirmwareInformation
-   Update-StorageFirmware

1 つ目のコマンドレットは、デバイスの機能、ファームウェア イメージ、リビジョンに関する詳細情報を返します。 この場合、コンピューターには 1 つのファームウェア スロットがある 1 台の SATA SSD のみが搭載されています。 次に例を示します。

   ```powershell
   Get-PhysicalDisk | Get-StorageFirmwareInformation

   SupportsUpdate        : True
   NumberOfSlots         : 1
   ActiveSlotNumber      : 0
   SlotNumber            : {0}
   IsSlotWritable        : {True}
   FirmwareVersionInSlot : {J3E16101}
   ```

SAS デバイスは常に “SupportsUpdate” を “True” とレポートすることに注意してください。これは、これらのコマンドのサポートをデバイスに明示的にクエリする方法がないためです。

ドライブが新しいファームウェアの更新メカニズムをサポートしている場合、管理者は、2 つ目の Update-StorageFirmware で、イメージ ファイルを使用してドライブのファームウェアを更新することができます。 このイメージ ファイルは、OEM またはドライブ ベンダーから直接入手する必要があります。

  > [!Note]
  > 運用環境のハードウェアを更新する前に、ラボ設定で運用環境と同じハードウェアに対してそのファームウェア イメージをテストします。

ドライブでは、まず新しいファームウェア イメージが内部ステージング領域に読み込まれます。 通常、この処理中も I/O は継続されます。 イメージはダウンロード後にアクティブ化されます。 この処理の間、内部のリセットが発生するので、ドライブは I/O コマンドに応答しなくなります。 つまり、アクティブ化中にこのドライブはデータを提供しません。 このドライブ上のデータにアクセスするアプリケーションは、ファームウェアのアクティブ化が完了するまで応答を待つことになります。 このコマンドレットの実行例を以下に示します。

   ```powershell 
   $pd | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.enc -SlotNumber 0
   $pd | Get-StorageFirmwareInformation

   SupportsUpdate        : True
   NumberOfSlots         : 1
   ActiveSlotNumber      : 0
   SlotNumber            : {0}
   IsSlotWritable        : {True}
   FirmwareVersionInSlot : {J3E160@3}
   ```

一般的に、ドライブが新しいファームウェア イメージをアクティブ化するときに、ドライブは I/O 要求を完了しません。 ドライブがアクティブ化するまでにかかる時間は、ドライブの設計と更新するファームウェアの種類によって変わります。 更新にかかる実測時間は 5 秒未満から 30 秒超でした。

このドライブは、次のように、5.8 秒以内でファームウェアの更新を完了しました。

```powershell 
Measure-Command {$pd | Update-StorageFirmware -ImagePath C:\\Firmware\\J3E16101.enc -SlotNumber 0}

 Days : 0
 Hours : 0
 Minutes : 0
 Seconds : 5
 Milliseconds : 791
 Ticks : 57913910
 TotalDays : 6.70299884259259E-05
 TotalHours : 0.00160871972222222
 TotalMinutes : 0.0965231833333333
 TotalSeconds : 5.791391
 TotalMilliseconds : 5791.391
 ```

## <a name="updating-drives-in-production"></a>運用環境のドライブを更新する

運用環境にサーバーを展開する前に、お使いのソリューション (記憶域エンクロージャ、ドライブ、サーバー) を販売し、サポートしているハードウェア ベンダーまたは OEM から推奨されるファームウェアにドライブのファームウェアを更新することを強くお勧めします。

運用環境へのサーバーの展開後は、サーバーに対する変更を実際に対応できる範囲に抑えることをお勧めします。 ただし、ドライブに非常に重要なファームウェアの更新プログラムがあるとソリューション ベンダーからアドバイスされることがあります。 このような場合、ドライブのファームウェアの更新プログラムを適用する前に、推奨される手順を次に示します。

1. ファームウェアのリリース ノートを読み、実際の環境に影響をもたらす可能性がある問題に更新プログラムが対処していること、実際の環境に悪影響を及ぼす可能性がある既知の問題がファームウェアに含まれていないことを確認します。

2. ラボに同じドライブを搭載したサーバーにファームウェアをインストールし (そのドライブに複数のリビジョンがある場合はリビジョンも同じにします)、新しいファームウェアで負荷をかけてドライブをテストします。 合成負荷テストの実行については、「[Windows Server で合成ワークロードを使用した記憶域スペースのパフォーマンスのテスト](https://technet.microsoft.com/library/dn894707.aspx)」を参照してください。

## <a name="automated-firmware-updates-with-storage-spaces-direct"></a>記憶域スペース ダイレクトでの自動ファームウェア更新

Windows Server 2016 には、記憶域スペース ダイレクト展開 (Microsoft Azure Stack ソリューションを含む) 向けのヘルス サービスが含まれています。 ヘルス サービスの主な目的は、ハードウェア展開の監視と管理を容易にすることです。 管理機能の一部として、ワークロードをオフラインにしたり、ダウンタイムを発生させたりせずに、ドライブのファームウェアをクラスター全体にロールアウトする機能があります。 この機能はポリシーに基づいて動作し、管理者が制御できます。

ヘルス サービスを使用してクラスター全体にファームウェアをロールアウトする作業は、以下の手順で簡単に実行できます。

-   記憶域スペース ダイレクト クラスターに追加する HDD ドライブと SSD ドライブを決め、Windows によるファームウェアの更新をドライブがサポートしているかどうかを確認します
-   サポートされるコンポーネントの XML ファイルに追加するドライブの一覧を作成します
-   サポートされるコンポーネントの XML に、そのドライブの目的のファームウェア バージョンを指定します (ファームウェア イメージの場所のパスを含めます)
-   XML ファイルをクラスター DB にアップロードします

この時点で、ヘルス サービスは XML を検査して解析し、目的のファームウェア バージョンが展開されていないドライブを特定します。 次に、影響を受けるドライブから (ノードごとに) I/O をリダイレクトし、ドライブ上のファームウェアを更新します。 記憶域スペース ダイレクト クラスターは、複数のサーバー ノードにデータを分散させることで、回復性を実現します。ヘルス サービスによって、ドライブを更新する価値があるノード全体を分離できます。 ノードが更新されると、記憶域スペースの修復が開始され、すべてのデータのコピーが相互に同期を保った状態でクラスターに戻されてから、次のノードに進みます。 ファームウェアのロール アウト中に、記憶域スペースの処理が "デグレード" モードに移行することが予想されます。そしてそれは通常のことです。

新しいファームウェア イメージの安定したロールアウトと十分な検証時間を確保するために、複数のサーバーを更新する間隔は長く設定されています。 既定で、ヘルス サービスは、2 を更新する前に 7 日間を待機<sup>nd</sup>サーバー。 以降のサーバー (3<sup>rd</sup>、4<sup>th</sup>,...)、1 日の遅延時間で更新します。 管理者がファームウェアを不安定、または望ましくないと判断した場合、いつでもヘルス サービスで以降のロールアウトを停止できます。 ファームウェアが検証済みで、迅速なロールアウトが望ましい場合、これらの既定値を日単位から時間単位や分単位に変更できます。

次に、一般的な記憶域スペース ダイレクト クラスター向けのサポートされるコンポーネントの XML 例を示します。

```xml
 <Components>
     <Disks>
        <Disk>
            <Manufacturer>Contoso</Manufacturer>
            <Model>XYZ9000</Model>
            <AllowedFirmware>
              <Version>2.0</Version>
              <Version>2.1>/Version>
              <Version>2.2</Version>
            </AllowedFirmware>
            <TargetFirmware>
              <Version>2.2</Version>
              <BinaryPath>\\path\to\image.bin</BinaryPath>
            </TargetFirmware>
        </Disk>
        ...
        ...
    </Disks>
 </Components>
```

この記憶域スペース ダイレクト クラスターで新しいファームウェアのロールアウトを開始するには、.xml をクラスター DB にアップロードします。

```powershell
$SpacesDirect = Get-StorageSubSystem Clus*

$CurrentDoc = $SpacesDirect | Get-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document"

$CurrentDoc.Value | Out-File <Path>
```

Visual Studio Code、メモ帳など、好みのエディターでファイルを編集し、保存します。

```powershell
$NewDoc = Get-Content <Path> | Out-String

$SpacesDirect | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $NewDoc
```

アクションでヘルス サービスを参照し、ロールアウト メカニズムの詳細についてには場合があるこのビデオを参照してください。 https://channel9.msdn.com/Blogs/windowsserver/Update-Drive-Firmware-Without-Downtime-in-Storage-Spaces-Direct

## <a name="frequently-asked-questions"></a>よく寄せられる質問

「[ドライブのファームウェア更新のトラブルシューティング](troubleshoot-firmware-update.md)」もご覧ください。

### <a name="will-this-work-on-any-storage-device"></a>この方法は任意の記憶域デバイスで使用できますか

ファームウェアに正しいコマンドが実装されている記憶域デバイスで使用できます。 ドライブのファームウェアが (SATA/NVMe の) 正しいコマンドを実際にサポートしているかどうかは、Get-StorageFirmwareInformation コマンドレットを実行して確認できます。また、ベンダーと OEM は HLK テストを使用してこの動作をテストできます。

### <a name="after-i-update-a-sata-drive-it-reports-to-no-longer-support-the-update-mechanism-is-something-wrong-with-the-drive"></a>SATA ドライブを更新すると、その更新メカニズムはサポートされなくなったとレポートされます。 ドライブに何か問題があるのでしょうか

いいえ。新しいファームウェアのインストール後に更新ができなくなった場合を除き、ドライブに問題はありません。 これは、キャッシュされたバージョンのドライブの機能が正しくないという既知の問題です。 “Update-StorageProviderCache -DiscoveryLevel Full” を実行すると、ドライブの機能が再列挙され、キャッシュされたコピーが更新されます。 回避策として、上記のコマンドを 1 回実行してから、ファームウェアの更新を開始するか、スペース ダイレクト クラスターでロールアウトを完了することをお勧めします。

### <a name="can-i-update-firmware-on-my-san-through-this-mechanism"></a>このメカニズムで SAN のファームウェアを更新できますか
いいえ。通常、SAN には、メンテナンス操作用に独自のユーティリティとインターフェイスがあります。 この新しいメカニズムは、SATA、SAS、NVMe デバイスなど、直接接続されている記憶域向けです。

### <a name="from-where-do-i-get-the-firmware-image"></a>ファームウェア イメージはどこで入手できますか

ファームウェアは、常にお使いの OEM、ソリューション、ベンダー、またはドライブ ベンダーから直接に入手し、他の入手先からはダウンロードしないでください。 Windows には、ドライブにイメージを取得するメカニズムがありますが、イメージの整合性を検証する機能はありません。

### <a name="will-this-work-on-clustered-drives"></a>この方法はクラスター化されたドライブで使用できますか

このコマンドレットは、クラスター化されたドライブ上でも動作しますが、ヘルス サービスの調整によって実行中のワークロードに対する I/O の影響を軽減することに留意してください。 クラスター化されたドライブに対してコマンドレットを直接使用すると、I/O が遅延する可能性があります。 一般的に、基になるドライブに対するワークロードがないか、最小限の場合に、ドライブのファームウェア更新を行うことがベスト プラクティスです。

### <a name="what-happens-when-i-update-firmware-on-storage-spaces"></a>記憶域スペースのファームウェアを更新すると、どうなりますか

記憶域スペース ダイレクトにヘルス サービスを展開した Windows Server 2016 の場合、ドライブが Windows Server によるファームウェアの更新をサポートしていれば、ワークロードをオフラインすることなく、この操作を実行できます。

### <a name="what-happens-if-the-update-fails"></a>更新が失敗すると、どうなりますか

更新プログラムがさまざまな理由で失敗する可能性、それらの一部は。1)、ドライブは、Windows がファームウェアを更新するための正しいコマンドをサポートしていません。 この場合、新しいファームウェア イメージはアクティブ化されず、ドライブの動作には引き続き古いイメージが使用されます。 2) イメージをそのドライブにダウンロードできないか、ドライブに適用できません (バージョンの不一致、破損したイメージなど)。 この場合、ドライブはアクティブ化コマンドに失敗します。 この場合も、ドライブの動作には引き続き古いイメージが使用されます。

ファームウェアの更新後にドライブがまったく応答しない場合、ドライブ ファームウェア自体のバグが発生している可能性があります。 ラボ環境ですべてのファームウェア更新プログラムをテストしてから、運用環境に展開してください。 唯一の解決策はドライブの交換のみの可能性があります。

詳しくは、「[ドライブのファームウェア更新のトラブルシューティング](troubleshoot-firmware-update.md)」をご覧ください。

### <a name="how-do-i-stop-an-in-progress-firmware-roll-out"></a>進行中のファームウェアのロールアウトを停止するにはどうすればよいですか

PowerShell の次のコマンドレットでロールアウトを無効にします。
```powershell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled" -Value false
```

### <a name="i-am-seeing-an-access-denied-or-path-not-found-error-during-roll-out-how-do-i-fix-this"></a>ロールアウト中にアクセス拒否エラーや、パスが見つからないエラーが発生します。解決方法を教えてください

更新に使用するファームウェア イメージにすべてのクラスター ノードからアクセスできるようにします。 最も簡単な方法は、クラスター共有ボリュームに配置することです。
