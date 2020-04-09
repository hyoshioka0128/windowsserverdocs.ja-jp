---
title: msdt
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87c1e4e8cd6d9de036b47de590867a6531d0335a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839255"
---
# <a name="msdt"></a>msdt



コマンドラインまたは自動化されたスクリプトの一部としてトラブルシューティングパックを起動し、ユーザー入力なしで追加のオプションを有効にします。

## <a name="syntax"></a>構文

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

### <a name="parameters"></a>パラメーター

次の表に、msdt でサポートされているパラメーターとオプションを示します。


|      パラメーター      |                                                                                            説明                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /id \<パッケージ名 > |        実行する診断パッケージを指定します。 利用可能なパッケージの一覧については、このトピックで後述する「利用可能なトラブルシューティングパック」セクションのトラブルシューティングパック ID を参照してください。         |
|  /path \<ディレクトリ  |                                                                                           diagpkg ファイル                                                                                            |
|   /dci \<パスキー >   |                                        Msdt でパスキーフィールドをプリセットします。 このパラメーターは、サポートプロバイダーがパスキーを指定した場合にのみ使用されます。                                         |
|  /dt \<directory >   | 指定されたディレクトリのトラブルシューティングの履歴を表示します。 診断結果は、ユーザーの **%LOCALAPPDATA%\Diagnostics**または **%LOCALAPPDATA%\ElevatedDiagnostics**ディレクトリに格納されます。 |
| /af \<応答ファイル >  |                                               1つ以上の診断対話に対する応答を含む応答ファイルを XML 形式で指定します。                                               |

