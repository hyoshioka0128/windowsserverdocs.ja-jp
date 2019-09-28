---
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
title: Fsutil 修復
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 6e4e285bf8401d628f7e4bcbaeafb0c6defa3ad1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376914"
---
# <a name="fsutil-repair"></a>Fsutil 修復
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

NTFS 自己修復修復操作を管理および監視します。

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
|ual|ボリュームの破損ログのエントリを列挙します。|
|\<volumepath >|ドライブ名の後にコロンが続くボリュームを指定します。|
|\<LogName >|$Corrupt-ボリューム内の確認された破損のセット。<br />$Verify-ボリュームに存在する未確認の破損のセット。|
|化|NTFS 自己復旧を開始します。|
|\<FileReference >|NTFS ボリューム固有のファイル ID (ファイル参照番号) を指定します。 ファイル参照には、ファイルのセグメント番号が含まれます。|
|クエリ (query)|NTFS ボリュームの自己復旧状態を照会します。|
|セット (set)|ボリュームの自己復旧状態を設定します。|
|\<Flags >|ボリュームの自己復旧状態を設定するときに使用する修復方法を指定します。<br /><br />**Flags**パラメーターには、次の3つの値を設定できます。<br /><br />-   **0x01**:一般的な修復を有効にします。<br />-   **0x09**:修復せずにデータ損失の可能性について警告します。<br />-   **0x00**:NTFS 自己修復の修復操作を無効にします。|
|state|システムまたは特定のボリュームの破損状態を照会します。|
|待機|修復が完了するまで待機します。 NTFS が修復を実行しているボリュームで問題を検出した場合、このオプションを選択すると、システムは修復が完了するまで待機して、保留中のスクリプトを実行することができます。|
|[WaitType {0&#124;1}]|現在の修復が完了するまで待機するか、すべての修復が完了するまで待機するかを指定します。 *WaitType*は次の値に設定できます。<br /><br />-   **0**:すべての修復が完了するまで待機します。 (既定値)<br />-   **1**:現在の修復が完了するまで待機します。|

## <a name="remarks"></a>コメント

-   自己修復 NTFS は、NTFS ファイルシステムの破損を修復しようとしますが、 **chkdsk.exe**を実行する必要はありません。 この機能は、Windows Server 2008 で導入されました。 詳細については、「[自己復旧 NTFS](https://go.microsoft.com/fwlink/?LinkID=165401)」を参照してください。

## <a name="BKMK_examples"></a>例

ボリュームの確認済みの破損を列挙するには、次のように入力します。

```
fsutil repair enumerate C: $Corrupt 
```

ドライブ C で自己修復修復を有効にするには、次のように入力します。

```
fsutil repair set c: 1
```

ドライブ C で自己修復修復を無効にするには、次のように入力します。

```
fsutil repair set c: 0
```

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[自己復旧 (NTFS)](https://go.microsoft.com/fwlink/?LinkID=165401)


