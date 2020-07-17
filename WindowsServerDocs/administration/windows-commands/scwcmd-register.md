---
title: Scwcmd レジスタ
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe4d126a-9f27-4076-b7b1-fbefa45f378a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7917cfe8f71673ad45d8d3e32d29798757367c2a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932648"
---
# <a name="scwcmd-register"></a>Scwcmd: 登録

> 適用対象: Windows Server 2012 R2、Windows Server 2012

拡張または役割、タスク、サービス、またはポートの定義を含むセキュリティの構成データベース ファイルを登録することによってセキュリティ構成ウィザード (SCW) のセキュリティの構成データベースをカスタマイズします。

## <a name="syntax"></a>構文

```
scwcmd register /kbname:<MyApp> [/kbfile:<kb.xml>] [/kb:<path>] [/d]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/kbname:\<MyApp>|セキュリティ構成データベースの拡張機能の登録を使用する名前を指定します。 このパラメーターを指定する必要があります。|
|/kbfile\<Kb.xml>|拡張またはカスタマイズの基本のセキュリティの構成データベースに使用されるセキュリティの構成データベース ファイルのパスとファイル名を指定します。 セキュリティの構成データベース ファイルが SCW のスキーマに準拠したことを確認するには、%windir%\security\KBRegistrationInfo.xsd スキーマ定義ファイルを使用します。 しない限り、このオプションを指定する必要があります、 **/d** パラメーターを指定します。|
|/kb\<Path>|更新するセキュリティの構成データベース ファイルを含むディレクトリへのパスを指定します。 このオプションが指定されていない場合は、%windir%\security\msscw\kbs が使用されます。|
|/d|セキュリティの構成データベースからセキュリティの構成データベースの拡張機能の登録を解除します。 登録を解除する拡張機能は、/kbname パラメーターを指定します。 ( **/Kb ファイル**パラメーターを指定しないでください)。拡張機能の登録を解除するセキュリティ構成データベースは、 **/kb**パラメーターによって指定されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

Scwcmd.exe は Windows Server 2008 R2、Windows Server 2008 または Windows Server 2003 を実行するコンピューターにできるだけです。

## <a name="examples"></a>例

SCWKBForMyApp.xml という名前のセキュリティ構成データベースファイルを、次の場所にある MyApp という名前で登録するには \\ \\ 、次のように入力します。
```
scwcmd register /kbfile:d:\SCWKBForMyApp.xml /kbname:MyApp /kb:\\kbserver\kb
```
Kb にあるセキュリティ構成データベース MyApp の登録を解除するには \\ \\ 、次のように入力します。
```
scwcmd register /d /kbname:MyApp /kb:\\kbserver\kb
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)