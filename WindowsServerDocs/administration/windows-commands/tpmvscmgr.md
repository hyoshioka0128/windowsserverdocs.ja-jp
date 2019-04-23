---
title: tpmvscmgr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f6cfc15b7c089c9b6ad4d9a267b951373e63a63a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888593"
---
# <a name="tpmvscmgr"></a>tpmvscmgr



Tpmvscmgr コマンド ライン ツールにより、管理者の資格情報を持つユーザーを作成し、コンピューターに TPM 仮想スマート カードを削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
Tpmvscmgr create [/name] [/AdminKey DEFAULT | PROMPT | RANDOM] [/PIN DEFAULT | PROMPT] [/PUK DEFAULT | PROMPT] [/generate] [/machine] [/?]
```
```
Tpmvscmgr destroy [/instance <instance ID>] [/?]
```

### <a name="parameters-for-create-command"></a>Create コマンドのパラメーター

Create コマンドは、ユーザーのシステム上の新しい仮想スマート カードを設定します。 削除が必要な場合は、新しく作成した後で参照カードのインスタンス ID を返します。 インスタンスの ID の形式が**ROOT\SMARTCARDREADER\000n**場所**n** 0 から開始し、新しい仮想スマート カードを作成するたびに 1 ずつ増加します。

|パラメーター|説明|
|---------|-----------|
|/name|必須。 新しい仮想スマート カードの名前を示します。|
|/AdminKey|ユーザーが PIN を忘れた場合、カードの PIN をリセットするために使用する目的の管理者キーを示します。</br>**既定**010203040506070801020304050607080102030405060708 の既定値を指定します。</br>**プロンプト**管理者キーの値を入力するように求めます。</br>**ランダムな**しないユーザーに返されるカードの管理者キーのランダムな設定になります。 これは、スマート カード管理ツールを使用して管理しやすいできない可能性があるカードを作成します。 ランダムに生成されると、48 の 16 進数の文字として管理者キーを入力する必要があります。|
|/PIN|目的のユーザー暗証番号 (pin) の値を示します。</br>**既定**既定 12345678 の暗証番号 (pin) を指定します。</br>**プロンプト**コマンドラインで PIN を入力するように求めます。 PIN は 8 文字以上である必要があり、数字、文字、および特殊文字を含めることができます。|
|/PUK|目的の PIN ロック解除キー (PUK) 値を示します。 PUK 値は 8 文字以上である必要があり、数字、文字、および特殊文字を含めることができます。 パラメーターを省略した場合は、PUK せず、カードが作成されます。</br>**既定**PUK 12345678 の既定値を指定します。</br>**プロンプト**PUK コマンドラインを入力するユーザーにメッセージが表示されます。|
|生成/|仮想スマート カードの関数に必要なストレージでファイルを生成します。 場合、生成/パラメーターを省略すると、このファイル システムなしのカードを作成するのと同じです。 ファイル システムがない、カードは、スマート カード管理システムなど Microsoft Configuration Manager でのみ管理できます。|
|/machine|仮想スマート カードを作成するときに、リモート コンピューターの名前を指定することができます。 これは、ドメイン環境のみで使用でき、DCOM に依存します。 別のコンピューターに仮想スマート カードの作成に成功するコマンド、このコマンドを実行しているユーザーは、リモート コンピューター上のローカルの administrators グループのメンバーである必要があります。|
|/?|このコマンドのヘルプを表示します。|

### <a name="parameters-for-destroy-command"></a>Destroy コマンドのパラメーター

Destroy コマンドは、ユーザーのコンピューターから安全に仮想スマート カードを削除します。

> [!WARNING]
> 仮想スマート カードが削除されると、回復できません。

|パラメーター|説明|
|---------|-----------|
|/instance|削除する仮想スマート カードのインスタンス ID を指定します。 インスタンス Id は、カードの作成時に、Tpmvscmgr.exe によって出力として生成されました。 /Instance パラメーターは、Destroy コマンドの必須フィールドです。|
|/?|このコマンドのヘルプを表示します。|

## <a name="remarks"></a>注釈

メンバーシップ、**管理者**はこのコマンドのすべてのパラメーターの実行に必要な最小のターゲット コンピューターのグループ (または同等)。

英数字の入力では、完全な 127 文字の ASCII セットは許可されています。

## <a name="BKMK_Examples"></a>例

次のコマンドは、別のコンピューターから起動されたスマート カードの管理ツールによって後で管理されている仮想スマート カードを作成する方法を示します。
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey DEFAULT /PIN PROMPT
```
または、既定の管理者キーを使用する代わりに、コマンドラインで、管理者キーを作成できます。 次のコマンドは、管理者キーを作成する方法を示します。
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey PROMPT /PIN PROMPT
```
次のコマンドでは、証明書の登録に使用できるアンマネージ仮想スマート カードを作成します。
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey RANDOM /PIN PROMPT /generate
```
次のコマンドはランダム化された管理者キーを使用して仮想スマート カードを作成します。 キーは自動的に作成 cardis 後破棄されます。 つまり、ユーザーは PIN を忘れた場合または PIN を変更する必要がある、カードを削除し、もう一度作成するユーザーが必要です。 カードを削除するには、ユーザーは、次のコマンドを実行できます。
```
tpmvscmgr.exe destroy /instance <instance ID> 
```
場所\<インスタンス ID > は、値は出力画面に、ユーザーには、カードが作成されたとき。 具体的には、最初のカードを作成して、インスタンス ID は ROOT\SMARTCARDREADER\0000 します。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)