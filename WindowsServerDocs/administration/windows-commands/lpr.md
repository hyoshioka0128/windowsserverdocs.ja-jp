---
title: lpr
description: Lpr コマンドの参照記事。印刷用の準備として、ラインプリンタデーモン (LPD) サービスを実行しているコンピューターまたはプリンターの共有デバイスにファイルを送信します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afc8790b-8b52-45c4-acdf-be0ffa9da534
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ea40ef71da7804f01c963049f07e1f6b5395354
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927114"
---
# <a name="lpr"></a>lpr

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

印刷の準備として、ラインプリンタデーモン (LPD) サービスを実行しているコンピューターまたはプリンターの共有デバイスにファイルを送信します。

## <a name="syntax"></a>構文

```
lpr [-S <servername>] -P <printername> [-C <bannercontent>] [-J <jobname>] [-o | -o l] [-x] [-d] <filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -S`<servername>` | (名前または IP アドレスを使用して) LPD 印刷キューをホストするコンピューターまたはプリンターの共有デバイスが、表示する状態であることを指定します。  このパラメーターは必須であり、大文字にする必要があります。 |
| -P`<printername> `| 表示するステータスを持つ印刷キューのプリンタを (名前で) 指定します。 プリンターの名前を検索するには、[**プリンター** ] フォルダーを開きます。 このパラメーターは必須であり、大文字にする必要があります。 |
| -C`<bannercontent>` | 印刷ジョブのバナーページに印刷するコンテンツを指定します。 このパラメーターを指定しない場合、印刷ジョブが送信されたコンピューターの名前がバナーページに表示されます。 このパラメーターは大文字にする必要があります。 |
| -J`<jobname>` | バナーページに印刷される印刷ジョブの名前を指定します。 このパラメーターを含めない場合は、印刷するファイルの名前がバナーページに表示されます。 このパラメーターは大文字にする必要があります。 |
| `[-o | -o l]` | 印刷するファイルの種類を指定します。 パラメーター **-o**は、テキストファイルを印刷することを指定します。 パラメーター **-o l**は、バイナリファイル (たとえば PostScript ファイル) を出力することを指定します。 |
| -d | データファイルをコントロールファイルの前に送信する必要があることを指定します。 プリンターでデータファイルを最初に送信する必要がある場合は、このパラメーターを使用します。 詳細については、プリンターのドキュメントを参照してください。 |
| -X | **Lpr**コマンドが、4.1. 4_u1 までのリリースでは、Sun Microsystems オペレーティングシステム (SunOS と呼ばれます) と互換性がある必要があることを指定します。 |
| `<filename>` | 印刷するファイルを (名前で) 指定します。 このパラメーターは必須です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

*Document.txt*テキストファイルを*10.0.0.45*の LPD ホスト上の*Laserprinter1*プリンターキューに出力するには、次のように入力します。

```
lpr -S 10.0.0.45 -P Laserprinter1 -o Document.txt
```

Laserprinter1 Adobe PostScript ファイルを*10.0.0.45*の LPD ホスト上の*Laserprinter1*プリンターキューに*PostScript_file*出力するには、次のように入力します。

```
lpr -S 10.0.0.45 -P Laserprinter1 -o l PostScript_file.ps
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)
