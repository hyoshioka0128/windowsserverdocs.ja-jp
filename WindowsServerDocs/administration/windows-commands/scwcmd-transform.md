---
title: Scwcmd 変換
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f1116b42d356cc36f478089cdf487a38e792e87
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722121"
---
# <a name="scwcmd-transform"></a>Scwcmd: 変換

> 適用対象: Windows Server 2012 R2、Windows Server 2012

新しいグループ ポリシー オブジェクト (GPO) で Active Directory ドメイン サービス セキュリティ構成ウィザード (SCW) を使用して、生成されたセキュリティ ポリシー ファイルを変換します。 変換の処理には、実行されるサーバー上のすべての設定は変わりません。 変換の操作が完了した後、管理者は、サーバーにポリシーを展開する目的の Ou に GPO をリンクする必要があります。

変換操作を完了するには、ドメイン管理者の資格情報が必要です。

> [!IMPORTANT]
> インターネット インフォメーション サービス (IIS) セキュリティ ポリシー設定は、グループ ポリシーを使用して展開できません。</br>> 承認されたアプリケーションを一覧表示するファイアウォールポリシーは、サーバーが最後に起動されたときに Windows ファイアウォールサービスが自動的に開始しない限り、サーバーに展開しないでください。



## <a name="syntax"></a>構文

```
scwcmd transform /p:<Policyfile.xml> /g:<GPODisplayName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|/p:\<policyfile .xml>|適用される .xml ポリシー ファイルのパスとファイル名を指定します。 このパラメーターを指定する必要があります。|
|/g:\<GPODisplayName>|GPO の表示名を指定します。 このパラメーターを指定する必要があります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

Scwcmd.exe は Windows Server 2008 R2、Windows Server 2008 または Windows Server 2003 を実行するコンピューターにできるだけです。

## <a name="examples"></a>例

FileServerPolicy.xml という名前のファイルから FileServerSecurity という名前の GPO を作成するには、次のように入力します。
```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)