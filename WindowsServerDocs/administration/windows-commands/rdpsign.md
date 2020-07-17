---
title: rdpsign
description: Rdpsign コマンドの参照記事。これにより、リモートデスクトッププロトコル (.rdp) ファイルにデジタル署名することができます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4a6fa8ce-3d32-49a5-b056-bcc1a23391f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2aefbc144820d0132bd4993d150dec955e22e01d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931972"
---
# <a name="rdpsign"></a>rdpsign

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ プロトコル (.rdp) ファイルにデジタル署名することできます。

> [!NOTE]
> 最新バージョンの新機能については、「 [Windows Server でのリモートデスクトップサービスの新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))機能」を参照してください。

## <a name="syntax"></a>構文

```
rdpsign /sha1 <hash> [/q | /v |] [/l] <file_name.rdp>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| /sha1`<hash>` | これは、セキュア ハッシュ アルゴリズム 1 (SHA1) ハッシュ、証明書ストアに含まれている署名証明書の拇印を指定します。 Windows Server 2012 R2 以前で使用されています。 |
| /sha256`<hash>` | 証明書ストアに含まれる署名証明書のセキュアハッシュアルゴリズム 256 (SHA256) ハッシュであるサムプリントを指定します。 Windows Server 2016 以降の/sha1 を置き換えます。 |
| /q | 非表示モードです。 コマンドが成功すると、出力なしは、コマンドが失敗した場合は、最小限の出力。 |
| /v | 詳細モード。 すべての警告、メッセージ、および状態を表示します。 |
| /l | 実際には、入力ファイルのいずれかを置き換えることがなく、署名と出力の結果をテストします。 |
| `<file_name.rdp>` | .Rdp ファイルの名前。 完全なファイル名を使用して署名する .rdp ファイル (複数可) を指定する必要があります。 ワイルドカード文字は使用できません。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- SHA1 または SHA256 証明書の拇印は、信頼された .rdp ファイルの発行元を表す必要があります。 証明書の拇印を取得するには、**証明**書スナップインを開き、使用する証明書をダブルクリックします (ローカルコンピューターの証明書ストアまたは個人証明書ストアのいずれか)。次に、[**詳細**] タブをクリックし、**フィールド**の一覧で [**拇印**] をクリックします。

    > [!NOTE]
    > rdpsign.exe ツールで使用するために拇印をコピーする場合は、スペースを削除する必要があります。

- 署名された出力ファイルは、入力ファイルを上書きします。

- 複数のファイルが指定されていて、いずれかの .rdp ファイルの読み取りまたは書き込みができない場合、ツールは次のファイルに進みます。

### <a name="examples"></a>例

*File1*という名前の .rdp ファイルに署名するには、.rdp ファイルを保存したフォルダーに移動し、次のように入力します。

```
rdpsign /sha1 hash file1.rdp
```

> [!NOTE]
> *ハッシュ* 値はスペースを含めないの SHA1 証明書の拇印を表します。

ファイルに実際に署名せずに、.rdp ファイルのデジタル署名が成功するかどうかをテストするには、次のように入力します。

```
rdpsign /sha1 hash /l file1.rdp
```

、 *File1*、 *file2*、および*file3*という名前の複数の .rdp ファイルに署名するには、次のように入力します (ファイル名の間にスペースが含まれます)。

```
rdpsign /sha1 hash file1.rdp file2.rdp file3.rdp
```

## <a name="see-also"></a>関連項目

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
