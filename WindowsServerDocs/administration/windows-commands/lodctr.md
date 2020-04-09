---
title: lodctr
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 33c14970a669d24f1cc803003e8530712311c564
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840955"
---
# <a name="lodctr"></a>lodctr

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

を使用すると、パフォーマンスカウンターの名前とレジストリ設定をファイルに登録または保存し、信頼されたサービスを指定できます。
## <a name="syntax"></a>構文
```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```
#### <a name="parameters"></a>パラメーター

|    パラメーター     |                                                                                                                                         説明                                                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <filename>    |                                                                                          パフォーマンスカウンターの名前の設定と、初期化ファイルのファイル名で指定された説明テキストを登録します。                                                                                          |
|  /s:<filename>   |                                                                                                       パフォーマンスカウンターのレジストリ設定と説明テキストをファイル <filename>に保存します。                                                                                                       |
|        /r        |                                現在のレジストリ設定およびレジストリに関連するキャッシュされたパフォーマンスファイルから、カウンターのレジストリ設定を復元し、テキストを説明します。<p>このオプションは、Windows Server 2003 オペレーティングシステムでのみ使用できます。                                |
|  /r:<filename>   | パフォーマンスカウンターのレジストリ設定を復元し、ファイル <filename>からテキストを説明します。 **警告:** **lodctr/r**コマンドを使用すると、すべてのパフォーマンスカウンターのレジストリ設定と説明テキストが上書きされ、指定されたファイルで定義されている構成に置き換えられます。 |
| /t:<servicename> |                                                                                                                       サービス <servicename> が信頼されていることを示します。                                                                                                                       |
|        /?        |                                                                                                                             コマンド プロンプトでヘルプを表示します。                                                                                                                             |

## <a name="remarks"></a>コメント
入力する情報にスペースが含まれる場合は、テキストを囲む引用符を使用して (たとえば、 <filename>)。
## <a name="examples"></a><a name=BKMK_Examples></a>例
現在のパフォーマンスレジストリ設定とカウンターの説明テキストを file **perf 作成 1**に保存するには、次の手順を実行します。
```
lodctr /s:perf backup1.txt
```
## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

