---
ms.assetid: a0c6dbfe-d898-496d-9356-825f7fbd90ec
title: fsutil 8dot3name
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 50a8fc9a3de9f7033e82f05d075c07019c84fbfd
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439125"
---
# <a name="fsutil-8dot3name"></a>fsutil 8dot3name

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

クエリまたはを含む短い名前 (8dot3 名) の動作の設定を変更します。

-   クエリの短い名前の動作の現在の設定

-   短い名前が指定したディレクトリ パスから削除された場合に影響を受ける可能性がありますレジストリ キーの指定されたディレクトリ パスをスキャンします。

-   短い名前の動作を制御する設定を変更します。 この設定は、指定されたボリュームまたはボリュームの既定の設定を適用できます。

-   ディレクトリ内のすべてのファイルの短い名前を削除します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil 8dot3name [query] [<VolumePath>]
fsutil 8dot3name [scan] [/s] [/l [<log file>] ] [/v] <DirectoryPath>
fsutil 8dot3name [set] { <DefaultValue> | <VolumePath> {1|0}}
fsutil 8dot3name [strip] [/t] [/s] [/f] [/l [<log file.] ] [/v] <DirectoryPath>
```

## <a name="parameters"></a>パラメーター

|                 パラメーター                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           クエリ [<VolumePath>]            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                           8dot3 短い名前作成の動作の状態をファイル システムに照会します。<br /><br />場合、 *VolumePath*すべてのボリュームの既定の 8dot3name 作成動作設定が表示される、パラメーターとして指定されていません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|           スキャン <DirectoryPath>            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        ファイルが配置されているをスキャンする、指定した*DirectoryPath* 8dot3 の短い名前は、ファイル名から削除された場合に影響を受ける可能性がありますレジストリ キー。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| 設定 { <DefaultValue> &#124; <VolumePath>} | 次のインスタンスで 8dot3 名前作成のファイル システムの動作を変更します。<br /><br /><ul><li>ときに*DefaultValue*が指定されているレジストリ キー、 **HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreationNtfsDisable8dot3NameCreationNtfsDisable8dot3NameCreation**に設定されている、 *DefaultValue*します。<br /><br />    *DefaultValue*次の値を持つことができます。<br /><br /><ul><li>**0**:システム上のすべてのボリュームの 8dot3 名の作成を有効にします。</li><li>**1**:システム上のすべてのボリュームの 8dot3 名の作成を無効にします。</li><li>**2**:8dot3 名の作成は、ボリュームごとに設定します。</li><li>**3**:システム ボリュームを除くすべてのボリュームの 8dot3 名の作成を無効にします。</li></ul></li><li>ときに、 *VolumePath*を指定すると、ディスク フラグ 8dot3name プロパティで指定されたボリュームは、指定されたボリュームの 8dot3 名の作成を有効にする設定 (**0**) またはセットを 8dot3 名の作成を無効にする、ボリュームを指定 (**1**)。<br /><br />    8dot3 名前作成の既定のファイル システム動作は、値に設定する必要があります**2**を有効にしたり、指定されたボリュームの 8dot3 名の作成を無効にする前にします。</li></ul> |
|           ストリップ <DirectoryPath>           |                                                                                                                                                                                                                                                                                                                  8dot3 ファイル名が存在するすべてのファイルを削除します。 指定した*DirectoryPath*します。 8dot3 ファイル名は、すべてのファイルは削除されません場所、 *DirectoryPath*結合ファイルに名は 260 文字以上含まれています。<br /><br />このコマンドは、一覧表示されますが、8dot3 ファイル名が完全に削除したファイルを指定するレジストリ キーを変更しません。<br /><br />ファイルから 8dot3 ファイル名を完全に削除の影響の詳細については、次を参照してください。[解説](Fsutil-8dot3name.md#BKMK_remarks)します。                                                                                                                                                                                                                                                                                                                  |
|               <VolumePath>                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       ドライブ名の後にコロンまたは形式の GUID を指定します**ボリューム {** <em>GUID</em> **}** します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|                    /f                     |                                                                                                                                                                                                                                                                                                   指定するすべてのファイルを指定した*DirectoryPath*が 8dot3 ファイル名削除 8dot3 ファイル名を使用してファイルをポイントするレジストリ キーがある場合でもです。 この場合は、操作は、8dot3 ファイル名を削除しますが、8dot3 ファイル名を使用しているファイルを指す任意のレジストリ キーを変更しません。 **警告:** ディレクトリまたは使用する前にボリュームをバックアップすることをお勧めしますが、 **/f**パラメーター予期しないアプリケーションのエラーになる可能性があるため、アンインストールすることができないなどのプログラムします。                                                                                                                                                                                                                                                                                                    |
|              /l [<log file>]              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                  情報が書き込まれるログ ファイルを指定します。<br /><br />場合、 **/l**パラメーターが指定されていないすべての情報が既定のログ ファイルに書き込まれます。<br /><br />**%temp%\8dot3_removal_log@ (** <em>GMT YYYY MM DD HH、MM-SS</em> **) .log**                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                    /s                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      指定した操作は、指定されたサブディレクトリに適用する必要があります*DirectoryPath*します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|                    /t                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                          テスト モードで 8dot3 ファイル名の削除を実行することを指定します。 8dot3 ファイル名の実際の削除を除くすべての操作が実行されます。 テスト モードを使用すると、どのレジストリ キーは、8dot3 ファイル名を使用するファイルをポイントを検出します。                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                    /v                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       ログ ファイルに書き込まれたすべての情報が、コマンドラインにも表示されることを指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

## <a name="BKMK_remarks"></a>「解説」

-   8dot3 ファイル名を完全に削除して、8dot3 ファイル名をポイントするレジストリ キーを変更しないが、アプリケーションをアンインストールすることができないなどの予期しないアプリケーションが失敗する可能性があります。 まず、ディレクトリまたはボリューム前にバックアップする 8dot3 ファイル名を削除しようとするをお勧めします。

## <a name="BKMK_examples"></a>例
{928842df-5a01-11de-a85c-806e6f6e6963}、GUID で指定されているディスク ボリュームの無効化 8dot3 名の動作を照会するには、次のように入力します。

```
fsutil 8dot3name query Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

使用して、8dot3 名の動作を照会することも、**動作**サブコマンドします。

8dot3 ファイル名を削除する、 *D:\MyData*ディレクトリとログ ファイルとして指定されている情報の書き込み中に、すべてのサブディレクトリ*mylogfile.log*種類。

```
fsutil 8dot3name strip /l mylogfile.log /s d:\MyData
```

### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[fsutil 8dot3name](Fsutil-8dot3name.md)

[fsutil の動作](Fsutil-behavior.md)


