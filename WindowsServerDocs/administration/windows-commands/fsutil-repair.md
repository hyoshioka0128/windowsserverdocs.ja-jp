---
title: fsutil repair
description: Fsutil repair コマンドの参照記事。これは、NTFS 自己修復修復操作を管理および監視します。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 700e1f713d503565321ab29f5384d74382c64f21
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931203"
---
# <a name="fsutil-repair"></a>fsutil repair

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

NTFS 自己修復修復操作を管理および監視します。 自己修復 NTFS は、NTFS ファイルシステムの破損を修復しようとしますが、 **Chkdsk.exe**を実行する必要はありません。 詳細については、「[自己修復 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))」を参照してください。

## <a name="syntax"></a>構文

```
fsutil repair [enumerate] <volumepath> [<logname>]
fsutil repair [initiate] <volumepath> <filereference>
fsutil repair [query] <volumepath>
fsutil repair [set] <volumepath> <flags>
fsutil repair [wait][<waittype>] <volumepath>

```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ual | ボリュームの破損ログのエントリを列挙します。 |
| `<logname>` | には、ボリューム内の確認済みの `$corrupt` 破損のセット、またはボリューム内の一連の検証されていない破損のセットを指定でき `$verify` ます。 |
| 化 | NTFS 自己復旧を開始します。 |
| `<filereference>` | NTFS ボリューム固有のファイル ID (ファイル参照番号) を指定します。 ファイル参照には、ファイルのセグメント番号が含まれます。 |
| query | NTFS ボリュームの自己復旧状態を照会します。 |
| set | ボリュームの自己復旧状態を設定します。 |
| `<flags>` | ボリュームの自己復旧状態を設定するときに使用する修復方法を指定します。<p>このパラメーターは、次の3つの値に設定できます。<ul><li>**0x01** -一般的な修復を有効にします。</li><li>**0x09** -修復せずにデータ損失の可能性について警告します。</li><li>**0x00** -NTFS 自己修復修復操作を無効にします。</li></ul> |
| state | システムまたは特定のボリュームの破損状態を照会します。 |
| wait | 修復が完了するまで待機します。 NTFS が修復を実行しているボリュームで問題を検出した場合、このオプションを選択すると、システムは修復が完了するまで待機して、保留中のスクリプトを実行することができます。 |
| `[waittype {0|1}]` | 現在の修復が完了するまで待機するか、すべての修復が完了するまで待機するかを指定します。 *Waittype*パラメーターには、次の値を設定できます。<ul><li>**0** -すべての修復が完了するまで待機します。 (既定値)</li><li>**1** -現在の修復が完了するまで待機します。</li></ul> |

### <a name="examples"></a>例

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [自己復旧型の NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))
