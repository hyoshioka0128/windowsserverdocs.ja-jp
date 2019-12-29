---
title: lpr
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afc8790b-8b52-45c4-acdf-be0ffa9da534 jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e853933e368f181866963fdcbc1eca5b84bb8c09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374159"
---
# <a name="lpr"></a>lpr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

印刷の準備として、ラインプリンタデーモン (LPD) サービスを実行しているコンピューターまたはプリンターの共有デバイスにファイルを送信します。  

## <a name="syntax"></a>構文  
```  
lpr [-S <ServerName>] -P <printerName> [-C <BannerContent>] [-J <JobName>] [-o | "-o l"] [-x] [-d] <filename>  
```  
## <a name="parameters"></a>パラメーター  

|     パラメーター      |                                                                                                           説明                                                                                                           |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  -S <ServerName>   |                                    (名前または IP アドレスを使用して) LPD 印刷キューをホストするコンピューターまたはプリンターの共有デバイスが、表示する状態であることを指定します。 必須。                                    |
|  -P <printerName>  |                                                              表示するステータスを持つ印刷キューのプリンタを (名前で) 指定します。 必須。                                                              |
| -C <BannerContent> |                印刷ジョブのバナーページに印刷するコンテンツを指定します。 このパラメーターを指定しない場合、印刷ジョブが送信されたコンピューターの名前がバナーページに表示されます。                 |
|    -J <JobName>    |                           バナーページに印刷される印刷ジョブの名前を指定します。 このパラメーターを含めない場合は、印刷するファイルの名前がバナーページに表示されます。                            |
| [-o&#124; "-o l"]  | 印刷するファイルの種類を指定します。 パラメーター **-o**は、テキストファイルを印刷することを指定します。 パラメーター **"-o l"** は、バイナリファイル (PostScript ファイルなど) を出力することを指定します。 |
|         -d         |              データファイルをコントロールファイルの前に送信する必要があることを指定します。 プリンターでデータファイルを最初に送信する必要がある場合は、このパラメーターを使用します。 詳細については、プリンターのドキュメントを参照してください。               |
|         -x         |                               **Lpr**コマンドが、4.1.4 _u1 までのリリースでは、Sun Microsystems オペレーティングシステム (SunOS と呼ばれます) と互換性がある必要があることを指定します。                                |
|     <FileName>     |                                                                                      印刷するファイルを (名前で) 指定します。 必須。                                                                                      |
|         /?         |                                                                                              コマンド プロンプトにヘルプを表示します。                                                                                               |

## <a name="remarks"></a>コメント  
- プリンターの名前を検索するには、[プリンター] フォルダーを開きます。  
- **-S**、 **-P**、 **-C**、および **-J**パラメーターは大文字と小文字が区別され、大文字で入力する必要があります。  
  ## <a name="BKMK_examples"></a>例  
  この例では、10.0.0.45 にある LPD ホストの Laserprinter1 プリンターキューに "test.txt" テキストファイルを出力する方法を示します。  
  ```  
  lpr -S 10.0.0.45 -P Laserprinter1 -o Document.txt  
  ```  
  この例では、"PostScript_file" Adobe PostScript ファイルを、10.0.0.45 にある LPD ホストの Laserprinter1 プリンターキューに出力する方法を示します。  
  ```  
  lpr -S 10.0.0.45 -P Laserprinter1 "-o l" PostScript_file.ps  
  ```  

#### <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
-   [印刷コマンドのリファレンス](print-command-reference.md)  
