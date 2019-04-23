---
ms.assetid: e5f55f3e-8d2a-4526-8d67-36a539126c22
title: fsutil の階層制御
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: dcb69e4e9c71a723bfd735eb7915472f1232a92b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859253"
---
# <a name="fsutil-tiering"></a>fsutil の階層制御
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

設定してフラグを無効にすると、階層の一覧など、ストレージ層の関数の管理を有効にします。

## <a name="syntax"></a>構文

```
fsutil tiering [clearflags] <volume> <flags>
fsutil tiering [queryflags] <volume>
fsutil tiering [regionlist] <volume>
fsutil tiering [setflags] <volume> <flags>
fsutil tiering [tierlist] <volume>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|clearflags|ボリュームの階層化の動作のフラグを無効にします。|
|\<ボリューム >|ボリュームを指定します。|
|/TrNH|階層型記憶域のボリュームでは、熱の収集を無効にするとします。<br /><br>NTFS や refs などのにのみ適用されます。|
|queryflags|ボリュームの階層化の動作のフラグを照会します。|
|regionlist|ボリュームと、それぞれの記憶域階層の階層化されたリージョンの一覧を表示します。|
|setflags|ボリュームの階層化の動作のフラグを有効にします。|
|tierlist|ボリュームに関連付けられている記憶域 tieres を一覧表示します。|


### <a name="examples"></a>例

C のボリュームにフラグを照会するには、次のように入力します。

```
fsutil tiering clearflags C:
```

C のボリュームにフラグを設定するには、次のように入力します。

```
fsutil tiering setflags C: /TrNH
```

C のボリュームにフラグをクリアするには、次のように入力します。

```
fsutil tiering clearflags C: /TrNH
```

ボリューム C と、各ストレージ層のリージョンを一覧表示するには、次のように入力します。

```
fsutil tiering regionlist C:
```

C のボリュームの階層を一覧表示するには、次のように入力します。

```
fsutil tiering tierlist C:
```



### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

