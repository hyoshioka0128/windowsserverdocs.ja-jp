---
title: ReFS 整合性ストリーム
description: ''
author: gawatu
ms.author: jgerend
manager: dmoss
ms.date: 10/16/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.assetid: 1f1215cd-404f-42f2-b55f-3888294d8a1f
ms.openlocfilehash: 11f0a696fb843f5cd8b4a7ff3318c28d6c1adeb8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871343"
---
# <a name="refs-integrity-streams"></a>ReFS 整合性ストリーム
>適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server (半期チャネル)、Windows 10

整合性ストリームは、チェックサムを使用してデータの整合性を検証および保持する、ReFS のオプション機能です。 ReFS は、常に、メタデータのチェックサムを使用しますが、既定では ReFS はファイル データのチェックサムを生成および検証しません。 整合性ストリームは、ファイル データのチェックサムを利用できるオプションの機能です。 整合性ストリームを有効にすると、データが有効か、破損しているかを ReFS が明確に判別できます。 さらに、ReFS と記憶域スペースの連携によって、破損したメタデータやデータを自動的に修正できます。

## <a name="how-it-works"></a>方法 

整合性ストリームは、個々のファイルやディレクトリまたはボリューム全体について有効にすることができ、整合性ストリームの設定はいつでも切り替えることができます。 さらに、ファイルとディレクトリの整合性ストリームの設定は、その親ディレクトリから継承されます。 

整合性ストリームを有効にすると、ReFS は指定したファイルのメタデータ内にそのファイルのチェックサムを作成して保持します。 このチェックサムによって、ReFS では、データにアクセスする前にデータの整合性を検証できます。 ReFS は、整合性ストリームが有効になっているデータを返す前に、まずそのチェックサムを計算します。

![ファイル データのチェックサムを計算します。](media/compute-checksum.gif)

次に、このチェックサムが、ファイルのメタデータに含まれているチェックサムと比較されます。 チェックサムが一致した場合、データは有効とマークされ、ユーザーに返されます。 チェックサムが一致しない場合、データは破損しています。 ボリュームの回復性によって、ReFS で破損に対応する方法が決定されます。

- ReFS が回復性のないシンプル領域またはベア ドライブにマウントされている場合、ReFS は破損したデータを返さずに、ユーザーにエラーを返します。 
- ReFS が回復性のあるミラー スペースまたはパリティ スペースにマウントされている場合、ReFS は破損の修正を試行します。 
    - 試行が成功した場合、ReFS は修正の書き込みを適用してデータの整合性を復元し、アプリケーションに有効なデータを返します。 アプリケーションでは、破損があったことは認識されません。
    - 試行が失敗した場合、ReFS はエラーを返します。 

ReFS では、すべての破損がシステム イベント ログに記録され、このログに破損が修正されたかどうかが反映されます。 

![是正書き込みデータの整合性を復元します。](media/corrective-write.gif)

## <a name="performance"></a>パフォーマンス 

整合性ストリームによって、システムのデータの整合性は向上しますが、パフォーマンスの低下も招きます。 これには、いくつかの原因が考えられます。
- 整合性ストリームが有効な場合、すべての書き込み操作は Allocate-on-Write 操作になります。 この操作では ReFS が既存のデータの読み取りや変更を行う必要がないため、Read-Modify-Write のボトルネックは回避されますが、ファイル データが頻繁に断片化し、読み取りの遅延が発生します。 
- システムのワークロードと基盤となる記憶域に応じて、チェックサムを計算して検証するためのコンピューティング コストは IO の待機時間の増加を招く可能性があります。 

整合性ストリームを使用すると、パフォーマンスが低下する可能性があるため、パフォーマンスが重要なシステムでは整合性ストリームを無効にしておくことをおすすめします。 

## <a name="integrity-scrubber"></a>整合性スクラブ機能

前述のように、ReFS でデータにアクセスする前に、必ずデータの整合性が自動的に検証されます。 ReFS はまた、アクセス頻度の低いデータを ReFS で検証できるバックグラウンド スクラブ機能も使用します。 このスクラブ機能ではボリュームが定期的にスキャンされ、破損する可能性のある部分が特定されて、破損データの修復が事前にトリガーされます。

  >[!NOTE]
  >データ整合性スクラブ機能で検証できるのは、整合性ストリームが有効なファイルのファイル データのみです。

既定ではスクラブ機能が 4 週間ごとに実行されますが、この間隔は、タスク スケジューラーの [Microsoft]\[Windows]\[データ整合性スキャン ]で構成できます。 

## <a name="examples"></a>例
ファイル データの整合性の設定を監視および変更するには、ReFS は **Get-FileIntegrity** および **Set-FileIntegrity** コマンドレットを使用します。

### <a name="get-fileintegrity"></a>Get-FileIntegrity
ファイル データの整合性ストリームが有効になっているかどうかを確認するには、**Get-FileIntegrity** コマンドレットを使用します。 

```PowerShell
PS C:\> Get-FileIntegrity -FileName 'C:\Docs\TextDocument.txt'
```

**Get-Item** コマンドレットを使用して、指定したディレクトリにあるすべてのファイルの整合性ストリームの設定を取得することもできます。 

```PowerShell
PS C:\> Get-Item -Path 'C:\Docs\*' | Get-FileIntegrity
```

### <a name="set-fileintegrity"></a>Set-FileIntegrity
ファイルのデータの整合性のストリームを有効/無効にするには、**Set-FileIntegrity** コマンドレットを使用します。 

```PowerShell
PS C:\> Set-FileIntegrity -FileName 'H:\Docs\TextDocument.txt' -Enable $True
```

**Get-Item** コマンドレットを使用して、指定したフォルダーにあるすべてのファイルの整合性ストリームの設定項目を設定することもできます。 

```PowerShell
PS C:\> Get-Item -Path 'H\Docs\*' | Set-FileIntegrity -Enable $True 
```

**Set-FileIntegrity** コマンドレットは、ボリュームやディレクトリに対して直接使用することもできます。 

```PowerShell
PS C:\> Set-FileIntegrity H:\ -Enable $True
PS C:\> Set-FileIntegrity H:\Docs -Enable $True
```

## <a name="see-also"></a>関連項目

-   [ReFS の概要](refs-overview.md)
-   [ReFS ブロック複製](block-cloning.md)
-   [記憶域スペース ダイレクトの概要](../storage-spaces/storage-spaces-direct-overview.md)
