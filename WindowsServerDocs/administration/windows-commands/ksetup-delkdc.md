---
title: ksetup:delkdc
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e2fa065ca60338b04cc8718e199805cc494c908
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814563"
---
# <a name="ksetupdelkdc"></a>ksetup:delkdc



Kerberos 領域の名前をキー配布センター (KDC) のインスタンスを削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delkdc <RealmName> <KDCName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName>|CORP. などの大文字の DNS 名と領域名が指定されています。CONTOSO.COM、およびこれが既定の領域として一覧表示と**ksetup**が実行します。 その他の KDC を削除しようとして、この領域になります。|
|\<KDCName>|KDC 名 mitkdc.contoso.com などの大文字、完全修飾ドメイン名で表されます。|

## <a name="remarks"></a>注釈

これらのマッピングがレジストリに格納されている**HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**します。 領域の構成データを複数のコンピューターから削除するには、代わりにセキュリティの構成テンプレート スナップインとポリシー配布を使用**ksetup**個別のコンピューターに明示的にします。

Windows 2000 Server Service Pack 1 (SP1) 以前のバージョンとを実行するコンピューターで変更された領域の設定の構成が使用する前に、コンピューターを再起動する必要があります。

コンピューターの既定の領域名を確認します。 または、意図したとおりにこのコマンドが成功したことを確認するには、実行**ksetup**コマンド プロンプトで、一覧で、削除された、KDC が存在しないことを確認します。

## <a name="BKMK_Examples"></a>例

Windows の領域と非 Windows 領域の間のリンクを削除する必要がありますので、このコンピューターのセキュリティ要件が変更されました。 最初に、関連付けを削除し、既存の関連付けの出力を確認します。
```
ksetup
```
次のコマンドを使用して関連付けを削除します。
```
Ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)