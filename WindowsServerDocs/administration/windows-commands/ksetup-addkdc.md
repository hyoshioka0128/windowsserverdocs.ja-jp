---
title: ksetup addkdc
description: Ksetup addkdc コマンドのリファレンストピック。指定された Kerberos 領域のキー配布センター (KDC) アドレスを広告します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e51279166bf60196d12f877506d3228b78c4a711
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818092"
---
# <a name="ksetup-addkdc"></a>ksetup addkdc

指定された Kerberos 領域のキー配布センター (KDC) アドレスを追加します。

マッピングは**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains**の下のレジストリに格納され、新しい領域設定を使用する前にコンピューターを再起動する必要があります。

> [!NOTE]
> Kerberos 領域構成データを複数のコンピューターに展開するには、**セキュリティ構成テンプレート**スナップインとポリシー配布を個々のコンピューターで明示的に使用する必要があります。 このコマンドを使用することはできません。

## <a name="syntax"></a>構文

```
ksetup /addkdc <realmname> [<KDCname>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<realmname>` | CORP など、大文字の DNS 名を指定します。CONTOSO.COM。 この値は、 **ksetup**の実行時に既定の領域としても表示され、他の KDC を追加する領域です。 |
| `<KDCname>` | 大文字と小文字を区別しない、完全修飾ドメイン名 (mitkdc.contoso.com など) を指定します。 KDC 名を省略した場合、DNS は Kdc を検索します。 |

### <a name="examples"></a>例

Windows 以外の KDC サーバーと、ワークステーションで使用する領域を構成するには、次のように入力します。

```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

前の例と同じコンピューターでローカルコンピューターアカウントのパスワードを% に設定 p@sswrd1 し、コンピューターを再起動するには、次のように入力します。

```
ksetup /setcomputerpassword p@sswrd1%
```

コンピューターの既定の領域名を確認するには、次のように入力します。

```
ksetup
```
レジストリを調べて、マッピングが意図したとおりに発生したことを確認してください。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup setcomputerpassword コマンド](ksetup-setcomputerpassword.md)
