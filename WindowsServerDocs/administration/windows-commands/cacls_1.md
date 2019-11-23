---
title: cacls
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04b60bd852abdb55059efb96aec4c290361d6a74
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379948"
---
# <a name="cacls"></a>cacls

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたファイルの随意アクセス制御リスト (DACL) を表示または変更します。  
## <a name="syntax"></a>構文  
```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```  
### <a name="parameters"></a>パラメーター  

|        パラメーター        |                                                                                            説明                                                                                             |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      \<filename\>       |                                                                            必須。 指定されたファイルの Acl を表示します。                                                                             |
|           /t            |                                                          現在のディレクトリとすべてのサブディレクトリ内の指定されたファイルの Acl を変更します。                                                          |
|           /m            |                                                                          ディレクトリにマウントされているボリュームの Acl を変更します。                                                                           |
|           /l            |                                                                        シンボリックリンク自体とターゲットを操作します。                                                                         |
|         /s: sddl         |                                       SDDL 文字列で指定されている Acl を置き換えます ( **/e**、 **/g**、 **/r**、 **/p**、 **/d**では無効です)。                                        |
|           /e            |                                                                                 ACL を置き換えるのではなく、編集します。                                                                                  |
|           /c            |                                                                                 アクセス拒否エラーを続行します。                                                                                  |
|    /g user:\<の perm\>     |   指定されたユーザーアクセス権を付与します。<br /><br />アクセス許可の有効な値:<br /><br />-n-なし<br />-r-読み取り<br />-w-書き込み<br />-c-変更 (書き込み)<br />-f-フルコントロール   |
|      /r ユーザー [...]      |                                                                  指定されたユーザーのアクセス権を取り消します ( **/e**でのみ有効)。                                                                   |
| [/p ユーザー:\<perm\> [...] | 指定されたユーザーのアクセス権を置き換えます。<br /><br />アクセス許可の有効な値:<br /><br />-n-なし<br />-r-読み取り<br />-w-書き込み<br />-c-変更 (書き込み)<br />-f-フルコントロール |
|     [/d ユーザー [...]      |                                                                                    指定されたユーザーアクセスを拒否します。                                                                                     |
|           /?            |                                                                                コマンド プロンプトにヘルプを表示します。                                                                                |

## <a name="remarks"></a>注釈  
- このコマンドは廃止されました。 代わりに[icacls](icacls.md)を使用してください。  
- 結果を解釈するには、次の表を使用します。  


  |      出力       |                アクセス制御エントリ (ACE) はに適用されます                |
  |-------------------|---------------------------------------------------------------------|
  |        OI         |               オブジェクト継承。 このフォルダーとファイル。                |
  |        CI         |           コンテナーの継承。 このフォルダーとサブフォルダー。            |
  |        IO         | 継承のみ。 ACE は、現在のファイルまたはディレクトリには適用されません。 |
  | 出力メッセージがありません |                          このフォルダーのみです。                          |
  |     OI項目      |                 このフォルダー、サブフォルダー、およびファイル。                 |
  |   OI項目IO    |                     サブフォルダーとファイルのみ。                      |
  |     項目IO      |                          サブフォルダーのみです。                           |
  |     OIIO      |                             ファイルのみ。                             |


- ワイルドカード ( **?** と **\\\*** ) を指定して、複数のファイルを指定します。  
- 複数のユーザーを指定できます。  

#### <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)   
-   [icacls](icacls.md)  
