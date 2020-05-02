---
title: msdt
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5d31b1b5a73d975aec08d675aaff04ee29c7d3c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723870"
---
# <a name="msdt"></a>msdt



コマンドラインまたは自動化されたスクリプトの一部としてトラブルシューティングパックを起動し、ユーザー入力なしで追加のオプションを有効にします。

## <a name="syntax"></a>構文

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

### <a name="parameters"></a>パラメーター

次の表に、msdt でサポートされているパラメーターとオプションを示します。


|      パラメーター      |                                                                                            [説明]                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /id \<パッケージ名> |        実行する診断パッケージを指定します。 利用可能なパッケージの一覧については、このトピックで後述する「利用可能なトラブルシューティングパック」セクションのトラブルシューティングパック ID を参照してください。         |
|  /path \<ディレクトリ (/path)  |                                                                                           diagpkg ファイル                                                                                            |
|   /dci \<パスキー>   |                                        Msdt でパスキーフィールドをプリセットします。 このパラメーターは、サポートプロバイダーがパスキーを指定した場合にのみ使用されます。                                         |
|  /dt \<ディレクトリ>   | 指定されたディレクトリのトラブルシューティングの履歴を表示します。 診断結果は、ユーザーの **%LOCALAPPDATA%\Diagnostics**または **%LOCALAPPDATA%\ElevatedDiagnostics**ディレクトリに格納されます。 |
| /af \<応答ファイル>  |                                               1つ以上の診断対話に対する応答を含む応答ファイルを XML 形式で指定します。                                               |

