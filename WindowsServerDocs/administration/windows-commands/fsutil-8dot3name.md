---
title: fsutil 8dot3name
description: Fsutil 8dot3name コマンドのリファレンストピックでは、短い名前 (8dot3 名) の動作の設定を照会または変更します。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: a0c6dbfe-d898-496d-9356-825f7fbd90ec
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 02977a33c21560fd2078f0f596f312f4ab4bc408
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436057"
---
# <a name="fsutil-8dot3name"></a>fsutil 8dot3name

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

次のような短い名前 (8dot3 名) の動作の設定を照会または変更します。

- 短い名前の動作の現在の設定を照会しています。

- 指定されたディレクトリパスから短い名前が削除された場合に影響を受ける可能性のあるレジストリキーの指定されたディレクトリパスをスキャンしています。

- 短い名前の動作を制御する設定を変更します。 この設定は、指定したボリュームまたは既定のボリューム設定に適用できます。

- ディレクトリ内のすべてのファイルの短い名前を削除します。

> [!IMPORTANT]
> 8dot3 ファイル名を完全に削除し、8dot3 ファイル名をポイントするレジストリキーを変更しないと、アプリケーションをアンインストールできないなど、予期しないアプリケーションエラーが発生する可能性があります。 8dot3 ファイル名を削除する前に、まずディレクトリまたはボリュームをバックアップすることをお勧めします。

## <a name="syntax"></a>構文

```
fsutil 8dot3name [query] [<volumepath>]
fsutil 8dot3name [scan] [/s] [/l [<log file>] ] [/v] <directorypath>
fsutil 8dot3name [set] { <defaultvalue> | <volumepath> {1|0}}
fsutil 8dot3name [strip] [/t] [/s] [/f] [/l [<log file.] ] [/v] <directorypath>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 照会`[<volumepath>]` | ファイルシステムに対して8dot3 短い名前の作成動作の状態を照会します。<p>*Volumepath*がパラメーターとして指定されていない場合は、すべてのボリュームに対して既定の8dot3name 作成動作設定が表示されます。 |
| 取り込む`<directorypath>` | 8dot3 短い名前がファイル名から削除された場合に影響を受ける可能性があるレジストリキーについて、指定した*directorypath*にあるファイルをスキャンします。 |
| 一連`<defaultvalue> | <volumepath>}` | 次のインスタンスで8dot3 名を作成するときのファイルシステムの動作を変更します。<ul><li>*Defaultvalue*を指定すると、レジストリキー **HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreationNtfsDisable8dot3NameCreationNtfsDisable8dot3NameCreation**が*defaultvalue*に設定されます。<p>*DefaultValue*には、次の値を指定できます。<ul><li>**0**: システム上のすべてのボリュームに対して8dot3 名の作成を有効にします。</li><li>**1**: システム上のすべてのボリュームに対して8dot3 名の作成を無効にします。</li><li>**2**: 8dot3 名の作成をボリュームごとに設定します。</li><li>**3**: システムボリュームを除くすべてのボリュームに対して8dot3 名の作成を無効にします。</li></ul><li>*Volumepath*を指定すると、ディスクフラグ8dot3name プロパティに指定されたボリュームが、指定されたボリューム (**0**) に対して8dot3 名の作成を有効にするように設定されるか、指定されたボリューム (**1**) で8dot3 名の作成を無効にするように設定されます。<p>指定されたボリュームに対して8dot3 名の作成を有効または無効にするには、8dot3 名の作成の既定のファイルシステムの動作を値**2**に設定する必要があります。</li></ul> |
| 帯状`<directorypath>` | 指定した*directorypath*にあるすべてのファイルの8dot3 ファイル名を削除します。 *Directorypath*のファイル名が260文字を超える場合、8dot3 ファイル名は削除されません。<p>このコマンドは、8dot3 ファイル名が完全に削除されたファイルを指すレジストリキーを一覧表示しますが、変更しません。 |
| `<volumepath>` | ドライブ名の後にコロン、または形式の GUID を指定し `volume{GUID}` ます。 |
| /f | 8dot3 ファイル名を使用してファイルを指すレジストリキーがある場合でも、指定した*directorypath*にあるすべてのファイルに8dot3 ファイル名が削除されるように指定します。 この場合、この操作によって8dot3 ファイル名が削除されますが、8dot3 ファイル名を使用しているファイルを指すレジストリキーは変更されません。 **警告:****/F**パラメーターを使用する前に、ディレクトリまたはボリュームをバックアップすることをお勧めします。これは、プログラムをアンインストールできないなど、予期しないアプリケーションエラーが発生する可能性があるためです。 |
| /l`[<log file>]` | 情報を書き込むログファイルを指定します。<p>**/L**パラメーターが指定されていない場合は、すべての情報が既定のログファイル (.log * *) に書き込まれ `%temp%\8dot3_removal_log@(GMT YYYY-MM-DD HH-MM-SS)` ます。 |
| /s | 指定した*directorypath*のサブディレクトリに操作を適用する必要があることを指定します。 |
| /t | 8dot3 ファイル名の削除をテストモードで実行するように指定します。 8dot3 ファイル名の実際の削除を除くすべての操作が実行されます。 テストモードを使用すると、8dot3 ファイル名を使用するファイルを指すレジストリキーを見つけることができます。 |
| /v | ログファイルに書き込まれたすべての情報がコマンドラインにも表示されることを指定します。 |

### <a name="examples"></a>例

GUID で指定されたディスクボリュームの8dot3 名の無効化動作を照会するには、次のように入力します。 {92884 2df-5a01-11e6f6e6963},、次のように入力します。

```
fsutil 8dot3name query volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

また、 **behavior**サブコマンドを使用して、8dot3 名の動作を照会することもできます。

*D:\MyData*ディレクトリとすべてのサブディレクトリにある8dot3 ファイル名を削除するには、次のように入力します。ログファイルには、 *mylogfile .log*として指定します。

```
fsutil 8dot3name strip /l mylogfile.log /s d:\MyData
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [fsutil behavior](fsutil-behavior.md)
