---
title: Scwcmd 変換
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a6a6e37c2c2a362f3aa0aeadef615ff5065713f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843813"
---
# <a name="scwcmd-transform"></a>Scwcmd: transform

> 適用先:Windows Server 2012 R2、Windows Server 2012

新しいグループ ポリシー オブジェクト (GPO) で Active Directory ドメイン サービス セキュリティ構成ウィザード (SCW) を使用して、生成されたセキュリティ ポリシー ファイルを変換します。 変換の処理には、実行されるサーバー上のすべての設定は変わりません。 変換の操作が完了した後、管理者は、サーバーにポリシーを展開する目的の Ou に GPO をリンクする必要があります。

変換操作を完了するには、ドメイン管理者の資格情報が必要です。

> [!IMPORTANT]
> インターネット インフォメーション サービス (IIS) セキュリティ ポリシー設定は、グループ ポリシーを使用して展開できません。</br>> アプリケーションの一覧表示を承認する必要がありますいないを配置することをサーバーに Windows ファイアウォール サービスの開始を自動的にサーバーが最後とされない限り、ファイアウォール ポリシーを開始します。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
scwcmd transform /p:<Policyfile.xml> /g:<GPODisplayName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/p:\<Policyfile.xml>|適用される .xml ポリシー ファイルのパスとファイル名を指定します。 このパラメーターを指定する必要があります。|
|/g:\<GPODisplayName>|GPO の表示名を指定します。 このパラメーターを指定する必要があります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

Scwcmd.exe は Windows Server 2008 R2、Windows Server 2008 または Windows Server 2003 を実行するコンピューターにできるだけです。

## <a name="BKMK_Examples"></a>例

FileServerPolicy.xml という名前のファイルから FileServerSecurity という名前の GPO を作成するには、次のように入力します。
```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)