---
title: PowerShell
description: Powershell コマンドのリファレンス記事。コマンドプロンプトから PowerShell コンソールを開きます。
ms.topic: article
ms.assetid: 694fc970-0b6c-4046-b1b5-7eb1a0d26609
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 8608f10ae96d6137ce2dd7983d78236775af0df0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884884"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell は、特にシステム管理用に設計された、タスクベースのコマンドラインシェルおよびスクリプト言語です。 .NET Framework 上に構築された Windows PowerShell は、IT 技術者およびパワー ユーザーが Windows オペレーティング システムと Windows 上で実行するアプリケーションの管理の自動化を制御するときに役立ちます。

## <a name="using-powershellexe"></a>PowerShell.exe を使用します。

**PowerShell.exe** コマンド ライン ツールは、コマンド プロンプト ウィンドウで、Windows PowerShell セッションを開始します。 使用すると **PowerShell.exe**, 、セッションをカスタマイズする、省略可能パラメーターを使用することができます。 たとえば、特定の実行ポリシーまたは Windows PowerShell プロファイルを除外する 1 つを使用するセッションを開始することができます。 それ以外の場合、セッションは、Windows PowerShell コンソールで起動している任意のセッションと同じです。

- コマンド プロンプト ウィンドウで、Windows PowerShell セッションを開始するには、入力 `PowerShell`します。 A **PS** プレフィックスは、Windows PowerShell セッションであることを示すために、コマンド プロンプトに追加します。

- 特定の実行ポリシーを使用してセッションを開始するには、 **set-executionpolicy**パラメーターを使用し、次のように入力します。

    ```powershell
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Windows PowerShell プロファイルを使用せずに Windows PowerShell セッションを開始するには、 **Noprofile**パラメーターを使用し、次のように入力します。

    ```powershell
    PowerShell.exe -NoProfile
    ```

- セッションを開始するには、 **set-executionpolicy**パラメーターを使用して、次のように入力します。

    ```powershell
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- PowerShell.exe ヘルプファイルを表示するには、次のように入力します。

    ```powershell
    PowerShell.exe -help
    PowerShell.exe -?
    PowerShell.exe /?
    ```

- コマンド プロンプト ウィンドウで、Windows PowerShell セッションを終了するには、入力 `exit`します。 一般的なコマンド プロンプトに戻ります。

### <a name="remarks"></a>Remarks

- 完全な一覧については、 **PowerShell.exe** コマンド ライン パラメーターを参照して [about_PowerShell.Exe](/powershell/module/microsoft.powershell.core/about/about_powershell_exe)します。

- Windows PowerShell を起動するには、その他の方法については、次を参照してください。 [Windows PowerShell の開始](/powershell/scripting/windows-powershell/starting-windows-powershell)します。

- Windows PowerShell は、Windows Server オペレーティング システムの Server Core インストール オプションで実行されます。 ただし、 [Windows PowerShell Integrated Scripting Environment (ISE)](/previous-versions//hh849182(v=technet.10))などのグラフィックユーザーインターフェイスを必要とする機能や、 [Out GridView](/powershell/module/microsoft.powershell.utility/out-gridview)および[Show Command コマンド](/powershell/module/microsoft.powershell.utility/show-command)レットは、Server Core インストールでは実行されません。

## <a name="additional-references"></a>その他の参照情報

- [about_PowerShell.Exe](/powershell/module/microsoft.powershell.core/about/about_powershell_exe)

- [about_PowerShell_Ise.exe](/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe)

- [Windows PowerShell](/powershell/)
