---
title: msdt
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7bec16ab3f716148bb009dd56be475fcd058a897
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868899"
---
# <a name="msdt"></a>msdt



コマンドラインまたは自動化されたスクリプトの一部としてトラブルシューティングパックを起動し、ユーザー入力なしで追加のオプションを有効にします。

## <a name="syntax"></a>構文

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

## <a name="parameters"></a>パラメーター

次の表に、msdt でサポートされているパラメーターとオプションを示します。


|      パラメーター      |                                                                                            説明                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /id \<パッケージ名 > |        実行する診断パッケージを指定します。 利用可能なパッケージの一覧については、このトピックで後述する「利用可能なトラブルシューティングパック」セクションのトラブルシューティングパック ID を参照してください。         |
|  /path \<ディレクトリ (/path)  |                                                                                           diagpkg ファイル                                                                                            |
|   /dci \<パスキー >   |                                        Msdt でパスキーフィールドをプリセットします。 このパラメーターは、サポートプロバイダーがパスキーを指定した場合にのみ使用されます。                                         |
|  /dt \<ディレクトリ >   | 指定されたディレクトリのトラブルシューティングの履歴を表示します。 診断結果は、ユーザーの **%LOCALAPPDATA%\Diagnostics**または **%LOCALAPPDATA%\ElevatedDiagnostics**ディレクトリに格納されます。 |
| /af \<応答ファイル >  |                                               1つ以上の診断対話に対する応答を含む応答ファイルを XML 形式で指定します。                                               |

