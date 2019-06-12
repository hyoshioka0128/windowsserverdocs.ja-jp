---
title: cipher
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78ef795e-0f87-4acd-8d15-192c972c0f41
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d801d6e6286e97319766c879f7289f6191cc7101
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434336"
---
# <a name="cipher"></a>cipher



NTFS ボリュームのディレクトリとファイルの暗号化を表示または変更します。 パラメーターを指定せずに使用されている場合**暗号**現在のディレクトリとすべてのファイルの暗号化の状態が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
cipher [/e | /d | /c] [/s:<Directory>] [/b] [/h] [PathName [...]]
cipher /k
cipher /r:<FileName> [/smartcard]
cipher /u [/n]
cipher /w:<Directory>
cipher /x[:efsfile] [FileName]
cipher /y
cipher /adduser [/certhash:<Hash> | /certfile:<FileName>] [/s:Directory] [/b] [/h] [PathName [...]]
cipher /removeuser /certhash:<Hash> [/s:<Directory>] [/b] [/h] [<PathName> [...]]
cipher /rekey [PathName [...]]
```

## <a name="parameters"></a>パラメーター

|          パラメーター           |                                                                                                                                                   説明                                                                                                                                                    |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              /b               |                                                                                                    エラーが発生した場合を中止します。 既定では、**暗号**は引き続きエラーが発生した場合でも実行されます。                                                                                                    |
|              /c               |                                                                                                                                   暗号化されたファイルの情報を表示します。                                                                                                                                    |
|              /d               |                                                                                                                                   指定したファイルまたはディレクトリの暗号化を解除します。                                                                                                                                   |
|              /e               |                                                                                          指定したファイルまたはディレクトリを暗号化します。 ディレクトリは、後で追加されるファイルが暗号化されるようにマークされます。                                                                                           |
|              /h               |                                                                                                     ファイルを表示と非表示にまたはシステム属性。 既定では、これらのファイルは暗号化または復号化されません。                                                                                                     |
|              /k               |                                                                            暗号化ファイル システム (EFS) ファイルを新しい証明書と使用するためのキーを作成します。 場合、 **/k**パラメーターを指定すると、その他のすべてのパラメーターは無視されます。                                                                            |
|  /r:\<ファイル名 > [/smartcard]  |   EFS 回復エージェントのキーと証明書を生成し、(証明書と秘密キーを含む) .pfx ファイルと .cer ファイル (証明書のみを含む) に書き込みます。 場合 **/smartcard**指定は、回復キーと証明書をスマート カードに書き込むし、.pfx ファイルは生成されません。   |
|        /s:\<ディレクトリ >        |                                                                                                               指定したすべてのサブディレクトリでは、指定の操作を実行します。*ディレクトリ*します。                                                                                                               |
|            /u [/n]            |  ローカル ドライブに暗号化されたすべてのファイルを検索します。 使用されている場合、 **/n**パラメーター、更新は行われません。 使用がない場合 **/n**、 **/u**ユーザーのファイルの暗号化キーまたは回復エージェントの現在のものでは、キーを比較し、変更されている場合は、それらを更新します。 このパラメーターでのみ機能 **/n**します。  |
|        /w:\<ディレクトリ >        | ボリューム全体で使用可能な未使用のディスク領域からデータを削除します。 使用する場合、 **/w**パラメーター、その他のすべてのパラメーターは無視されます。 指定されたディレクトリは、ローカル ボリューム内の任意の場所に配置できます。 ある場合、マウント ポイントまたはディレクトリを指す、別のボリューム データのボリュームが削除されます。 |
|  /x [: efsfile] [\<ファイル名 >]   |                                 指定したファイル名に、EFS 証明書とキーをバックアップします。 使用されている場合 **: efsfile**、 **/x**ファイルの暗号化に使用されたユーザーの証明書をバックアップします。 それ以外の場合、ユーザーの現在の EFS 証明書とキーをバックアップします。                                 |
|              /y               |                                                                                                                      ローカル コンピューターの現在の EFS 証明書サムネイルが表示されます。                                                                                                                      |
|  /adduser [/certhash:\<ハッシュ >  |                                                                                                                                              /certfile:<FileName>]                                                                                                                                               |
|            /rekey             |                                                                                                                 現在構成されている EFS キーを使用する場合は、指定された暗号化されたファイルを更新します。                                                                                                                 |
| /removeuser/certhash:\<ハッシュ > |                                                                                       指定したファイルからユーザーを削除します。 *ハッシュ*提供 **/certhash**を削除する証明書の SHA1 ハッシュをする必要があります。                                                                                       |
|              /?               |                                                                                                                                       コマンド プロンプトにヘルプを表示します。                                                                                                                                       |

## <a name="remarks"></a>注釈

-   親ディレクトリが暗号化されていない場合は、データが変更されるときに、暗号化されたファイルを解読になる。 そのため、ファイルを暗号化する場合、親ディレクトリも暗号化する必要があります。
-   管理者は、ユーザーは、回復エージェントを作成する EFS 回復ポリシーに .cer ファイルの内容を追加し、個々 のファイルを回復する .pfx ファイルをインポートできます。
-   複数のディレクトリ名とワイルドカードを使用することができます。
-   複数のパラメーターの間にスペースを配置する必要があります。

## <a name="BKMK_examples"></a>例

現在のディレクトリ内の各ファイルとサブディレクトリの暗号化の状態を表示するには、次のように入力します。
```
cipher
```
暗号化されたファイルとディレクトリがでマークされた、 **E**します。暗号化されていないファイルとディレクトリがでマークされた、 **U**します。たとえば、現在暗号化されている現在のディレクトリとそのすべての内容にする必要は、次の出力を示します。
```
Listing C:\Users\MainUser\Documents\
New files added to this directory will not be encrypted.
U Private
U hello.doc
U hello.txt
```
前の例で使用されるプライベート ディレクトリでの暗号化を有効にするには、次のように入力します。
```
cipher /e private
```
次の出力が表示されます。
```
Encrypting files in C:\Users\MainUser\Documents\
Private             [OK]
1 file(s) [or directorie(s)] within 1 directorie(s) were encrypted.
```
**暗号**コマンドは、次の出力を表示します。
```
Listing C:\Users\MainUser\Documents\
New files added to this directory will not be encrypted.
E Private
U hello.doc
U hello.txt
```
プライベートのディレクトリがマークされていることに注意してください。 暗号化された状態。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)