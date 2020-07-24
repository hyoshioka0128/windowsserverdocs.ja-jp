---
title: nfsstat
description: Nfsstat コマンドの参照記事。ネットワークファイルシステム (NFS) とリモートプロシージャコール (RPC) の呼び出しに関する統計情報を表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da7a9768-44bd-404b-97ee-c388d00dc395
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0eb2836b15c24dc946953c0c82c4b3586971c5bc
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956734"
---
# <a name="nfsstat"></a>nfsstat

ネットワークファイルシステム (NFS) とリモートプロシージャコール (RPC) の呼び出しに関する統計情報を表示するコマンドラインユーティリティ。 パラメーターを指定せずに使用します。このコマンドは、すべての統計データをリセットせずに表示します。

## <a name="syntax"></a>構文

```
nfsstat [-c][-s][-n][-r][-z][-m]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -c | クライアントによって送信および拒否されたクライアント側 NFS および RPC および NFS 呼び出しのみが表示されます。 NFS または RPC の情報のみを表示するには、このフラグを **-n**または **-r**パラメーターと組み合わせます。 |
| -S | サーバー側の NFS およびサーバーによって拒否された RPC および NFS の呼び出しのみを表示します。 NFS または RPC の情報のみを表示するには、このフラグを **-n**または **-r**パラメーターと組み合わせます。 |
| -M | マウントオプション、システム内部のマウントフラグ、およびその他のマウント情報によって設定されたマウントフラグに関する情報を表示します。 |
| -n | クライアントとサーバーの両方の NFS 情報を表示します。 NFS クライアントまたはサーバーの情報のみを表示するには、このフラグと **-c**または **-s**パラメーターを組み合わせます。 |
| -r | クライアントとサーバーの両方の RPC 情報を表示します。 RPC クライアントまたはサーバーの情報のみを表示するには、このフラグと **-c**または **-s**パラメーターを組み合わせます。 |
| -Z | 呼び出しの統計をリセットします。 このフラグはルートユーザーのみが使用でき、他のパラメーターと組み合わせて表示後に特定の統計のセットをリセットできます。 |

### <a name="examples"></a>例

クライアントによって送信および拒否された RPC および NFS 呼び出しの数に関する情報を表示するには、次のように入力します。

```
nfsstat -c
```

クライアントの NFS 呼び出しに関連する情報を表示して印刷するには、次のように入力します。

```
nfsstat -cn
```

クライアントとサーバーの両方の RPC 呼び出しに関連する情報を表示するには、次のように入力します。

```
nfsstat -r
```

サーバーによって受信および拒否された RPC および NFS 呼び出しの数に関する情報を表示するには、次のように入力します。

```
nfsstat -s
```

クライアントとサーバーのすべての呼び出しに関連する情報をゼロにリセットするには、次のように入力します。

```
nfsstat -z
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [サービスがネットワーク ファイル システム コマンドのリファレンス](services-for-network-file-system-command-reference.md)

- [NFS コマンドレットリファレンス](/powershell/module/nfs)
