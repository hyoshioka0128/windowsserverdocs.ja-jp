---
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
title: fsutil の修復
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 18c06b1f426105b098a5dc7e992b1e3becd3a4ca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846683"
---
# <a name="fsutil-repair"></a>fsutil の修復
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

管理および NTFS 自己復旧修復操作を監視します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil repair [enumerate] <volumepath> [<LogName>]
fsutil repair [initiate] <VolumePath> <FileReference>
fsutil repair [query] <VolumePath>
fsutil repair [set] <VolumePath> <Flags>
fsutil repair [wait][<WaitType>] <VolumePath>

```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|列挙します。|ボリュームの破損ログのエントリを列挙します。|
|\<volumepath >|コロンの後にドライブ名として、ボリュームを指定します。|
|\<LogName>|$ が壊れています - 一連のボリュームの破損を確認します。<br />$ を確認します - ボリュームで未確認の潜在的な破損のセット。|
|開始|NTFS 自己復旧を開始します。|
|\<FileReference>|NTFS ボリュームに固有のファイル ID (ファイルの参照番号) を指定します。 ファイル参照には、ファイルのセグメント数が含まれています。|
|クエリ (query)|NTFS ボリュームの自動修復の状態を照会します。|
|セット (set)|ボリュームの自動修復の状態を設定します。|
|\<フラグ >|ボリュームの自動修復の状態を設定するときに使用される修復方法を指定します。<br /><br />**フラグ**パラメーターは、3 つの値に設定することができます。<br /><br />-   **0x01**:[全般] の修復を有効にします。<br />-   **0x09**:修復なしのデータ損失の可能性について警告します。<br />-   **0x00**:NTFS 自己復旧修復操作を無効にします。|
|state|指定したボリュームまたはシステムの破損状態を照会します。|
|待機|Repair(s) を完了するまで待機します。 NTFS は、修復を実行するは、ボリューム上の問題を検出しましたが、このオプションは、保留中のスクリプトを実行する前に、修復が完了するまで待機するシステムをできます。|
|[WaitType {0&#124;1}]|現在の修復を完了するか、すべての修復を完了するを待機するを待機するかどうかを示します。 *WaitType*次の値に設定することができます。<br /><br />-   **0**:すべての修復を完了するまで待機します。 (既定値)<br />-   **1**:現在の修復を完了するまで待機します。|

## <a name="remarks"></a>注釈

-   必要とせず、NTFS ファイル システムをオンラインでの破損を修正しようとして NTFS の自己修復**Chkdsk.exe**を実行します。 この機能は、Windows Server 2008 で導入されました。 詳細については、次を参照してください。[自己復旧 NTFS](https://go.microsoft.com/fwlink/?LinkID=165401)します。

## <a name="BKMK_examples"></a>例

ボリュームの確認済みの破損を列挙するには、次のように入力します。

```
fsutil repair enumerate C: $Corrupt 
```

ドライブ C 上の自動修復の修復を有効にするには、次のように入力します。

```
fsutil repair set c: 1
```

ドライブ C 上の自動修復の修復を無効にするには、次のように入力します。

```
fsutil repair set c: 0
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[自己 NTFS の復旧](https://go.microsoft.com/fwlink/?LinkID=165401)


