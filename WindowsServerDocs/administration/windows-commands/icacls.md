---
title: icacls
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 403edfcc-328a-479d-b641-80c290ccf73e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: 59d10b9ed681b7e0af120798dde9f200182d67d3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842265"
---
# <a name="icacls"></a>icacls

指定されたファイルの随意アクセス制御リスト (DACL) を表示または変更し、保存した DACL を指定したディレクトリ内のファイルに適用します。

このコマンドを使用する方法の例については、[例](#examples)を参照してください。

## <a name="syntax"></a>構文

```
icacls <FileName> [/grant[:r] <Sid>:<Perm>[...]] [/deny <Sid>:<Perm>[...]] [/remove[:g|:d]] <Sid>[...]] [/t] [/c] [/l] [/q] [/setintegritylevel <Level>:<Policy>[...]]
icacls <Directory> [/substitute <SidOld> <SidNew> [...]] [/restore <ACLfile> [/c] [/l] [/q]]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ファイル名 >|Dacl を表示するファイルを指定します。|
|\<Directory >|Dacl を表示するディレクトリを指定します。|
|/t|現在のディレクトリとそのサブディレクトリにある、指定されたすべてのファイルに対して操作を実行します。|
|/c|ファイルエラーが発生しても操作を続行します。 エラーメッセージは引き続き表示されます。|
|/l|シンボリックリンクに対して操作を実行します。|
|/q|成功メッセージを表示しません。|
|[\<ACLfile > [/t] [/c] [/l] [/q]]|は、 **/restore**で後で使用するために、一致するすべてのファイルの Dacl を*aclfile*に格納します。|
|[/setowner \<Username > [/t] [/c] [/l] [/q]]|一致するすべてのファイルの所有者を、指定したユーザーに変更します。|
|[/findsid \<Sid > [/t] [/c] [/l] [/q]]|指定されたセキュリティ識別子 (SID) を明示的に示す DACL を含む、一致するすべてのファイルを検索します。|
|[/verify [/t] [/c] [/l] [/q]]|Acl を持つすべてのファイルを検索します。これは、標準ではないか、または ACE (アクセス制御エントリ) のカウントと整合性がありません。|
|[/リセット [/t] [/c] [/l] [/q]]|一致するすべてのファイルについて、Acl を既定の継承された Acl に置き換えます。|
|[/grant [: r] \<Sid >:<Perm>[...]]|指定されたユーザーアクセス権を付与します。 権限は、以前に許可された明示的な権限に代わるものです。</br>**: R**を使用しない場合、以前に許可した明示的なアクセス許可にアクセス許可が追加されます。|
|[/拒否 \<Sid >:<Perm>[...]]|指定されたユーザーアクセス権を明示的に拒否します。 明示的な拒否 ACE は、指定された権限に対して追加され、明示的な許可では同じ権限が削除されます。|
|[/remove [: g\|:d]] \<Sid > [...]]/tスイッチ/l/q|指定された SID のすべての出現箇所を DACL から削除します。</br>**: g**は、指定された SID に対して与えられているすべての権限を削除します。</br>**:d**は、指定された SID に対してすべての拒否された権限を削除します。|
|[/setintegritylevel [(CI) (OI)]\<レベル >:<Policy>[...]]|一致するすべてのファイルに整合性 ACE を明示的に追加します。 *レベル*は次のように指定します。</br>-   **L**[o]</br>-   **M**[edium]</br>-   **H**[igh]</br>整合性 ACE の継承オプションはレベルの前に配置でき、ディレクトリにのみ適用されます。|
|[/代替 \<SidOld > <SidNew> [...]]|既存の SID (*Sidold*) を新しい Sid (*sidold*) に置き換えます。 *Directory*パラメーターが必要です。|
|/restore \<ACLfile > [/c] [/l] [/q]|保存された Dacl を*Aclfile*から指定されたディレクトリ内のファイルに適用します。 *Directory*パラメーターが必要です。|
|/inheritancelevel: [e\|d\|r]|継承レベルを設定します。 <br>  **e** -enheritance を有効にする <br>**d** -継承を無効にして ace をコピーする <br>**r** -継承されたすべての ace を削除します。

## <a name="remarks"></a>コメント

-   Sid は、数字またはフレンドリ名の形式で指定できます。 数値形式を使用する場合、接辞は、ワイルド **&#42;** カード文字を SID の先頭にします。
-   **icacls**は、ACE エントリの正規の順序を次のように保持します。  
    -   明示的な拒否
    -   明示的な許可
    -   継承された拒否
    -   継承された付与
-   *Perm*は、次のいずれかの形式で指定できるアクセス許可マスクです。  
    -   単純な権限のシーケンス:

        **F** (フルアクセス)

        **M** (アクセス権の変更)

        **RX** (読み取りおよび実行アクセス)

        **R** (読み取り専用アクセス)

        **W** (書き込み専用アクセス)
    -   特定の権限のかっこ内のコンマ区切りのリスト:

        **D** (削除)

        **RC** (読み取りコントロール)

        **WDAC** (DAC の書き込み)

        **WO** (書き込み所有者)

        **S** (同期)

        **AS** (アクセスシステムセキュリティ)

        **MA** (最大許容)

        **GR** (汎用読み取り)

        **GW** (汎用書き込み)

        **GE** (汎用実行)

        **GA** (汎用すべて)

        **RD** (データの読み取り/一覧のディレクトリ)

        **WD** (データの書き込み/ファイルの追加)

        **AD** (データの追加/サブディレクトリの追加)

        **動詞**(拡張属性の読み取り)

        **Wea** (拡張属性の書き込み)

        **X** (実行/走査)

        **DC** (子の削除)

        **RA** (属性の読み取り)

        **WA** (属性の書き込み)
-   継承権限は、次*のいずれか*の権限を付与することができます。

    **(OI)** : オブジェクト継承

    **(CI)** : コンテナー継承

    **(IO)** : 継承のみ

    **(NP)** : 継承を伝達しません

## <a name="examples"></a>例

C:\Windows ディレクトリにあるすべてのファイルの Dacl と、そのサブディレクトリを ACLFile ファイルに保存するには、次のように入力します。

```
icacls c:\windows\* /save aclfile /t
```

C:\Windows ディレクトリとそのサブディレクトリに存在する ACLFile 内のすべてのファイルの Dacl を復元するには、次のように入力します。

```
icacls c:\windows\ /restore aclfile
```

ユーザー User1 に対して、Test1 という名前のファイルに対する DAC アクセス許可の削除と書き込みを許可するには、次のように入力します。

```
icacls test1 /grant User1:(d,wdac)
```

SID S-1-1-0 で定義されたユーザーを許可するには、"Test2" という名前のファイルに DAC アクセス許可を削除して、次のように入力します。

```
icacls test2 /grant *S-1-1-0:(d,wdac)
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
