---
title: tpmvscmgr
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b2c8ff4-5c5d-446d-99e7-4daa1b36a163
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0051750f557786b0a564ec20a32089e089898cc0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385660"
---
# <a name="tpmvscmgr"></a>tpmvscmgr



Tpmvscmgr コマンドラインツールを使用すると、管理者の資格情報を持つユーザーは、コンピューター上で TPM 仮想スマートカードを作成および削除できます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
Tpmvscmgr create [/name] [/AdminKey DEFAULT | PROMPT | RANDOM] [/PIN DEFAULT | PROMPT] [/PUK DEFAULT | PROMPT] [/generate] [/machine] [/?]
```
```
Tpmvscmgr destroy [/instance <instance ID>] [/?]
```

### <a name="parameters-for-create-command"></a>Create コマンドのパラメーター

Create コマンドは、ユーザーのシステムに新しい仮想スマートカードを設定します。 削除が必要な場合、後で参照するために新しく作成されたカードのインスタンス ID を返します。 インスタンス ID は、 **ROOT\SMARTCARDREADER\000n**の形式になります。 **n**は0から始まり、新しい仮想スマートカードを作成するたびに1ずつ増加します。

|パラメーター|説明|
|---------|-----------|
|/name|必須。 新しい仮想スマートカードの名前を示します。|
|/Adminkey|ユーザーが PIN を忘れた場合にカードの PIN をリセットするために使用できる、必要な管理者キーを示します。</br>**既定**010203040506070801020304050607080102030405060708の既定値を指定します。</br>**プロンプト**管理者キーの値を入力するようにユーザーに求めます。</br>**ランダム**結果として、ユーザーに返されないカードの管理者キーがランダムに設定されます。 これにより、スマートカード管理ツールを使用して管理できないカードが作成されます。 ランダムに生成された場合、管理者キーは48の16進数文字で入力する必要があります。|
|/ピン|必要なユーザー PIN の値を示します。</br>**既定**12345678の既定の PIN を指定します。</br>**プロンプト**コマンドラインで PIN を入力するようにユーザーに求めます。 PIN は8文字以上にする必要があり、数字、文字、および特殊文字を含めることができます。|
|/PUK|必要な PIN のロック解除キー (PUK) の値を示します。 PUK 値は、8文字以上で、数字、文字、および特殊文字を含めることができます。 パラメーターを省略した場合は、PUK を使用せずにカードが作成されます。</br>**既定**12345678の既定の PUK を指定します。</br>**プロンプト**コマンドラインで PUK を入力するようにユーザーに求めます。|
|/生成|では、仮想スマートカードが機能するために必要なファイルがストレージに生成されます。 /Generate パラメーターを省略した場合は、このファイルシステムを使用せずにカードを作成することと同じです。 ファイルシステムのないカードは、Microsoft Configuration Manager などのスマートカード管理システムでのみ管理できます。|
|/machine|仮想スマートカードを作成できるリモートコンピューターの名前を指定できます。 これはドメイン環境でのみ使用でき、DCOM に依存します。 別のコンピューターで仮想スマートカードを作成するコマンドを正常に実行するには、このコマンドを実行するユーザーが、リモートコンピューターのローカル管理者グループのメンバーである必要があります。|
|/?|このコマンドのヘルプを表示します。|

### <a name="parameters-for-destroy-command"></a>Destroy コマンドのパラメーター

[破棄] コマンドを実行すると、ユーザーのコンピューターから仮想スマートカードが安全に削除されます。

> [!WARNING]
> 削除された仮想スマートカードは回復できません。

|パラメーター|説明|
|---------|-----------|
|/インスタンス|削除する仮想スマートカードのインスタンス ID を指定します。 InstanceID は、カードが作成されたときに Tpmvscmgr によって出力として生成されました。 /インスタンスパラメーターは、Destroy コマンドの必須フィールドです。|
|/?|このコマンドのヘルプを表示します。|

## <a name="remarks"></a>コメント

このコマンドのすべてのパラメーターを実行するには、ターゲットコンピューター上の**Administrators**グループ (またはそれと同等) のメンバーシップが最低限必要です。

英数字入力の場合、127文字の完全な ASCII セットが許可されます。

## <a name="BKMK_Examples"></a>例

次のコマンドは、別のコンピューターから起動するスマートカード管理ツールによって後で管理できる仮想スマートカードを作成する方法を示しています。
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey DEFAULT /PIN PROMPT
```
または、既定の管理者キーを使用する代わりに、コマンドラインで管理者キーを作成することもできます。 次のコマンドは、管理者キーを作成する方法を示しています。
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey PROMPT /PIN PROMPT
```
次のコマンドは、証明書の登録に使用できる管理されていない仮想スマートカードを作成します。
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey RANDOM /PIN PROMPT /generate
```
次のコマンドは、ランダム化された管理者キーを使用して仮想スマートカードを作成します。 キーは、cardis 作成された後に自動的に破棄されます。 これは、ユーザーが PIN を忘れた場合、または PIN を変更したい場合、ユーザーはカードを削除して再度作成する必要があることを意味します。 カードを削除するには、ユーザーは次のコマンドを実行します。
```
tpmvscmgr.exe destroy /instance <instance ID> 
```
ここ\<で、インスタンス ID > は、ユーザーがカードを作成したときに画面に出力される値です。 具体的には、最初に作成されたカードのインスタンス ID は ROOT\SMARTCARDREADER\0000. です。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)