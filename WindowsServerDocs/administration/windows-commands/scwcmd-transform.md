---
title: Scwcmd 変換
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 36ee3a99828c7fdd9d4fc0ca14cbc0e203b01ea0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384310"
---
# <a name="scwcmd-transform"></a>Scwcmd: transform

> 適用対象: Windows Server 2012 R2、Windows Server 2012

新しいグループ ポリシー オブジェクト (GPO) で Active Directory ドメイン サービス セキュリティ構成ウィザード (SCW) を使用して、生成されたセキュリティ ポリシー ファイルを変換します。 変換の処理には、実行されるサーバー上のすべての設定は変わりません。 変換の操作が完了した後、管理者は、サーバーにポリシーを展開する目的の Ou に GPO をリンクする必要があります。

変換操作を完了するには、ドメイン管理者の資格情報が必要です。

> [!IMPORTANT]
> インターネット インフォメーション サービス (IIS) セキュリティ ポリシー設定は、グループ ポリシーを使用して展開できません。</br>> 承認されたアプリケーションを一覧表示するファイアウォールポリシーは、サーバーが最後に起動されたときに Windows ファイアウォールサービスが自動的に開始しない限り、サーバーに展開しないでください。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
scwcmd transform /p:<Policyfile.xml> /g:<GPODisplayName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/p:\<Policyfile .xml >|適用される .xml ポリシー ファイルのパスとファイル名を指定します。 このパラメーターを指定する必要があります。|
|/g:\<GPODisplayName >|GPO の表示名を指定します。 このパラメーターを指定する必要があります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

Scwcmd.exe は Windows Server 2008 R2、Windows Server 2008 または Windows Server 2003 を実行するコンピューターにできるだけです。

## <a name="BKMK_Examples"></a>例

FileServerPolicy.xml という名前のファイルから FileServerSecurity という名前の GPO を作成するには、次のように入力します。
```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)