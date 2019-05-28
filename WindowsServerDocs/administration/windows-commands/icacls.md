---
title: icacls
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 403edfcc-328a-479d-b641-80c290ccf73e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: 2639b8bb913bcd604a7c79015545006a23e1d0f2
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222955"
---
# <a name="icacls"></a>icacls



指定されたファイルの随意アクセス制御リスト (DACL) を表示または変更し、保存した DACL を指定したディレクトリ内のファイルに適用します。

このコマンドを使用する方法の例については、[例](#examples)を参照してください。

## <a name="syntax"></a>構文

```
icacls <FileName> [/grant[:r] <Sid>:<Perm>[...]] [/deny <Sid>:<Perm>[...]] [/remove[:g|:d]] <Sid>[...]] [/t] [/c] [/l] [/q] [/setintegritylevel <Level>:<Policy>[...]]
icacls <Directory> [/substitute <SidOld> <SidNew> [...]] [/restore <ACLfile> [/c] [/l] [/q]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<FileName>|Dacl を表示する対象のファイルを指定します。|
|\<ディレクトリ >|Dacl を表示するディレクトリを指定します。|
|/t|現在のディレクトリとそのサブディレクトリ内には、指定したすべてのファイルの操作を実行します。|
|/c|任意のファイルのエラーに関係なく、操作を続けます。 エラー メッセージが引き続き表示されます。|
|/l|宛先とシンボリック リンクの操作を実行します。|
|/q|成功メッセージを抑制します。|
|[保存/ \<ACLfile > [/t] [/c] [/l] [/q]|一致するすべてのファイルの Dacl を格納*ACLfile*を後で使用できる **/復元**します。|
|[/setowner\<ユーザー名 > [/t] [/c] [/l] [/q]|指定したユーザーに一致するすべてのファイルの所有者を変更します。|
|[/findSID \<Sid> [/t] [/c] [/l] [/q]]|指定したセキュリティ識別子 (SID) を明示的に言及 DACL が含まれているすべての一致するファイルを検索します。|
|[/verify [/t] [/c] [/l] [/q]]|長さ (アクセス制御エントリ) の ACE のカウントを使用した一貫性のない、標準でないまたは Acl ですべてのファイルを検索します。|
|[/reset [/t] [/c] [/l] [/q]]|既定値の置換の Acl には、すべての一致するファイルの Acl が継承されます。|
|[許可]、[: r] \<Sid >:<Perm>[...]|許可は、ユーザーのアクセス権を指定します。 アクセス許可は、以前に許可されている明示的なアクセス許可を置き換えます。</br>せず **: r**、アクセス許可が以前に許可したアクセス許可を明示的に追加します。|
|[拒否/ \<Sid >:<Perm>[...]|指定したユーザーのアクセス権を明示的に拒否されます。 明示的に拒否 ACE が記載されているアクセス許可の追加され、任意の明示的な許可で同じ権限が削除されます。|
|[/remove[:g\|:d]] \<Sid>[...]] [/t] [/c] [/l] [/q]|DACL から指定された SID のすべての出現を削除します。</br>**: g** sid を指定した権限の付与のすべての出現を削除します。</br>**: d**指定された SID を拒否された権限のすべての出現を削除します。|
|[/setintegritylevel [(CI)(OI)]\<レベル >:<Policy>[...]|一致するすべてのファイルに、整合性の ACE を明示的に追加します。 *レベル*として指定されます。</br>-   **L**[ow]</br>-   **M**[edium]</br>-   **H**[igh]</br>整合性 ACE の継承オプションでは、前に、レベルの場合があり、ディレクトリにのみ適用されます。|
|[置換]、\<SidOld > <SidNew> [...]|既存の SID が置き換えられます (*SidOld*) 新しい SID を持つ (*SidNew*)。 必要があります、*ディレクトリ*パラメーター。|
|復元/\<ACLfile > [/c] [/l] [/q]|保存した Dacl を適用*ACLfile*指定されたディレクトリ内のファイルにします。 必要があります、*ディレクトリ*パラメーター。|
|/inheritancelevel:[e\|d\|r]|継承レベルを設定します。 <br>  **e** -enheritance 有効 <br>**d** - 継承を無効にし、Ace のコピー <br>**r** -継承された Ace をすべて削除します

## <a name="remarks"></a>注釈

-   Sid は、数値またはフレンドリ名のいずれかの形式があります。 数値の形式を使用する場合は、ワイルドカード文字を接辞 **&#42;** SID の先頭にします。
-   **icacls**として ACE エントリの正規の順序が保持されます。  
    -   明示的な拒否
    -   明示的な許可
    -   継承された拒否
    -   継承された許可
-   *Perm*形式は次のいずれかで指定できるアクセス許可マスクです。  
    -   シンプルな権限のシーケンス。

        **F** (フル アクセス)

        **M** (変更のアクセス)

        **RX** (読み取りし、実行アクセス権)

        **R** (読み取り専用アクセス)

        **W** (書き込み専用アクセス)
    -   特定の権限のかっこで囲まれたコンマ区切りの一覧:

        **D** (削除)

        **RC** (コントロールを読み取り)

        **WDAC** (DAC 書き込み)

        **WO** (所有者の書き込み)

        **S** (同期)

        **AS** (システムのセキュリティ アクセス)

        **MA** (最大)

        **GR** (汎用読み取り)

        **GW** (汎用書き込み)

        **GE** (汎用の実行)

        **GA** (すべてジェネリック)

        **RD** (読み取りと一覧表示のデータ ディレクトリ)

        **WD** (書き込みファイルのデータ/追加)

        **AD** (追加データ/追加のサブディレクトリ)

        **市外**(拡張属性の読み取り)

        **WEA** (拡張属性の書き込み)

        **X** (実行/スキャン)

        **DC** (子を削除)

        **RA** (属性の読み取り)

        **WA** (属性の書き込み)
-   継承の権限のいずれかの可能性があります前に*Perm*フォーム、およびそれらがディレクトリにのみ適用されます。

    **(OI)** : オブジェクトの継承

    **(CI)** : コンテナーの継承

    **(IO)** : 継承のみ

    **(NP 受信)** : 伝搬しません継承

## <a name="examples"></a>例

すべてのファイルに対する Dacl を C:\Windows ディレクトリと ACLFile ファイルには、そのサブディレクトリ内に保存するには、次のように入力します。
```
icacls c:\windows\* /save aclfile /t
```
C:\Windows ディレクトリとそのサブディレクトリ内に存在する ACLFile 内のすべてのファイルに対して Dacl を復元するには、次のように入力します。
```
icacls c:\windows\ /restore aclfile
```
ユーザーに"Test1"という名前のファイルに User1 の削除と DAC の書き込みアクセス許可を与えるには、次のように入力します。
```
icacls test1 /grant User1:(d,wdac)
```
「Test2.」をという名前のファイル、SID S-1-1-0 削除および DAC の書き込みのアクセス許可によって定義されたユーザーに付与するには、次のように入力します。
```
icacls test2 /grant *S-1-1-0:(d,wdac)
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
