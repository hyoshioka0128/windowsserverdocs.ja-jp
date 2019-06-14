---
title: msdt
description: 'Windows コマンド」のトピック * * *- '
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
ms.openlocfilehash: ba411cf73026afe9990e5c32824e3dc277507891
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437234"
---
# <a name="msdt"></a>msdt



コマンドラインまたは自動化されたスクリプトの一部として、トラブルシューティング パックを呼び出し、ユーザー入力がないその他のオプションを使用します。

## <a name="syntax"></a>構文

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

## <a name="parameters"></a>パラメーター

次の表には、パラメーターと msdt.exe でサポートされるオプションが含まれています。


|      パラメーター      |                                                                                            説明                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /id\<パッケージ名 > |        実行すると、診断パッケージを指定します。 利用可能なパッケージの一覧は、"利用可能なトラブルシューティング パックでしょうか。 でのトラブルシューティング パック ID を参照してください。 このトピックで後述する「します。         |
|  /path\<ディレクトリ  |                                                                                           .diagpkg ファイル                                                                                            |
|   /dci \<passkey>   |                                        Msdt のパスキーのフィールドに設定します。 このパラメーターは、サポート プロバイダーにパスキーが提供されている場合にのみ使用します。                                         |
|  /dt \<directory>   | 指定したディレクトリ内には、トラブルシューティングの履歴を表示します。 ユーザーの診断結果が格納されている **%LOCALAPPDATA%\Diagnostics**または **%LOCALAPPDATA%\ElevatedDiagnostics**ディレクトリ。 |
| /af\<応答ファイル >  |                                               1 つまたは複数の診断操作に応答が含まれている XML 形式で応答ファイルを指定します。                                               |

