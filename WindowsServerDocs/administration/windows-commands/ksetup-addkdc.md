---
title: ksetup:addkdc
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d3e0d38bdec11618561ee4acaa32ffdd06695fab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868533"
---
# <a name="ksetupaddkdc"></a>ksetup:addkdc



Kerberos 領域を特定のキー配布センター (KDC) アドレスを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addkdc <RealmName> [<KDCName>] 
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName>|CORP. などの大文字の DNS 名と領域名が指定されています。CONTOSO.COM、およびこれが既定の領域として一覧表示と**ksetup**が実行します。 その他の KDC を追加しようとしているこの領域になります。|
|\<KDCName>|KDC 名 mitkdc.microsoft.com などの大文字と小文字の完全修飾ドメイン名で表されます。 KDC 名を省略すると、DNS は Kdc に配置します。|

## <a name="remarks"></a>注釈

これらのマッピングが下のレジストリに格納されている**HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**します。 に複数のコンピューターを Kerberos 領域の構成データを配置するには、代わりにセキュリティの構成テンプレート スナップインとポリシー配布を使用**ksetup**個別のコンピューターに明示的にします。

新しい領域の設定が使用する前に、コンピューターを再起動する必要があります。

コンピューターの既定の領域名を確認します。 または、意図したとおりにこのコマンドが成功したことを確認するには、実行**ksetup**コマンド プロンプトで、追加の KDC に対する出力を確認します。

## <a name="BKMK_Examples"></a>例

Windows 以外の KDC サーバーとワークステーションを使用する必要がある領域を構成します。
```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```
Ksetup ツールを実行ローカル コンピューター アカウントのパスワードを設定する前のコマンドのように、同じコンピューターのコマンド ライン"p@sswrd1%? です。 コンピューターを再起動します。
```
Ksetup /setcomputerpassword p@sswrd1%
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)