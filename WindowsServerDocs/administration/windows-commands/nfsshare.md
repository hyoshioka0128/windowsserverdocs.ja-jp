---
title: nfsshare
description: NFS (Network File System) 共有を制御する nfsshare コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 437a2615-335a-442f-9713-d50d5f3983a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4774d5ce929de5e79e2cde78e45b0cd9bdca163c
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721525"
---
# <a name="nfsshare"></a>nfsshare

ネットワークファイルシステム (NFS) 共有を制御します。 パラメーターを指定せずに使用します。このコマンドは、NFS サーバーによってエクスポートされたすべての Network File System (NFS) 共有を表示します。

## <a name="syntax"></a>構文

```
nfsshare <sharename>=<drive:path> [-o <option=value>...]
nfsshare {<sharename> | <drive>:<path> | * } /delete
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| -o anon =`{yes|no}` | 匿名 (マップされていない) ユーザーが共有ディレクトリにアクセスできるかどうかを指定します。 |
| -o rw =`[<host>[:<host>]...]` | *ホスト*によって指定されたホストまたはクライアントグループによる、共有ディレクトリへの読み取り/書き込みアクセスを提供します。 ホスト名とグループ名は、コロン (**:**) で区切る必要があります。 *Host*が指定されていない場合は、すべてのホストとクライアントグループ ( **ro**オプションで指定されたものを除く) が読み取り/書き込みアクセス権を取得します。 どちらの場合、 **ro** も **rw** オプションが設定されている、すべてのクライアントが共有ディレクトリへの読み取り/書き込みアクセス権を持ちます。 |
| -o ro =`[<host>[:<host>]...]` | *ホスト*によって指定されたホストまたはクライアントグループによる、共有ディレクトリへの読み取り専用アクセスを提供します。 ホスト名とグループ名は、コロン (**:**) で区切る必要があります。 *Host*が指定されていない場合、すべてのクライアント ( **rw**オプションで指定されたものを除く) は、読み取り専用アクセスを取得します。 **Ro**オプションが1つ以上のクライアントに対して設定されているにもかかわらず、 **rw**オプションが設定されていない場合、 **ro**オプションで指定されたクライアントだけが共有ディレクトリにアクセスできます。 |
| -o encoding =`{euc-jp|euc-tw|euc-kr|shift-jis|Big5|Ksc5601|Gb2312-80|Ansi)` | NFS 共有で構成する言語エンコードを指定します。 共有で使用できる言語は1つだけです。 この値には、次のいずれかの値を含めることができます。<ul><li>**euc-jp:** 日本語</li><li>**euc-tw:** 中国語</li><li>**韓国:** 韓国語</li><li>**シフト jis:** 日本語</li><li>**Big5:** 中国語</li><li>**Ksc5601:** 韓国語</li><li>**Gb2312-80:** 簡体字中国語</li><li>**Ansi:** ANSI エンコード</li></ul> |
| -o anongid =`<gid>` | 匿名 (マップされていない) ユーザーが*gid*をグループ識別子 (gid) として使用して共有ディレクトリにアクセスすることを指定します。 既定値は **-2**です。 匿名アクセスが無効になっている場合でも、マップされていないユーザーが所有するファイルの所有者をレポートするときに、匿名 GID が使用されます。 |
| -o anonuid =`<uid>` | 匿名 (マップされていない) ユーザーが、 *uid*をユーザー ID (uid) として使用して共有ディレクトリにアクセスすることを指定します。 既定値は **-2**です。 匿名 UID は、匿名アクセスが無効になっている場合でも、マップされていないユーザーが所有するファイルの所有者を報告するときに使用されます。 |
| -o root =`[<host>[:<host>]...]` | *ホスト*によって指定されたホストまたはクライアントグループによって、共有ディレクトリへのルートアクセスを提供します。 ホスト名とグループ名は、コロン (**:**) で区切る必要があります。 *Host*が指定されていない場合、すべてのクライアントがルートアクセスを取得します。 **ルート**オプションが設定されていない場合は、共有ディレクトリへのルートアクセス権を持つクライアントはありません。 |
| /delete | *Sharename*または `<drive>:<path>` が指定されている場合、このパラメーターは指定された共有を削除します。 ワイルドカード (*) が指定されている場合、このパラメーターはすべての NFS 共有を削除します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- 唯一のパラメーターとして*sharename*が指定されている場合、このコマンドは*sharename*によって識別される NFS 共有のプロパティを一覧表示します。

- *Sharename*とが使用されている場合 `<drive>:<path>` 、このコマンドはによって識別されるフォルダーを `<drive>:<path>` *sharename*としてエクスポートします。 **/Delete**オプションを使用すると、指定したフォルダーは NFS クライアントで使用できなくなります。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [サービスがネットワーク ファイル システム コマンドのリファレンス](services-for-network-file-system-command-reference.md)

- [NFS コマンドレットリファレンス](https://docs.microsoft.com/powershell/module/nfs)
