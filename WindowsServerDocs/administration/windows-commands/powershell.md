---
title: PowerShell
description: コマンド プロンプトから、PowerShell コンソールを開く方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694fc970-0b6c-4046-b1b5-7eb1a0d26609
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 1e2ccf6187e4480f94b30632b6f8f9f092052541
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811077"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell は、タスク ベースのコマンド ライン シェルおよびスクリプト言語が特にシステム管理用に設計されています。 .NET Framework 上に構築された Windows PowerShell は、IT 技術者およびパワー ユーザーが Windows オペレーティング システムと Windows 上で実行するアプリケーションの管理の自動化を制御する際に役立ちます。

**PowerShell.exe** コマンド ライン ツールは、コマンド プロンプト ウィンドウで、Windows PowerShell セッションを開始します。 使用すると **PowerShell.exe**, 、セッションをカスタマイズする、省略可能パラメーターを使用することができます。 たとえば、特定の実行ポリシーまたは Windows PowerShell プロファイルを除外する 1 つを使用するセッションを開始することができます。 それ以外の場合、セッションは、Windows PowerShell コンソールで起動している任意のセッションと同じです。

## <a name="using-powershellexe"></a>PowerShell.exe を使用します。

使用することができます、 **PowerShell.exe** コマンド ライン ツールをコマンド プロンプト ウィンドウで、Windows PowerShell セッションを開始します。

- コマンド プロンプト ウィンドウで、Windows PowerShell セッションを開始するには、入力`PowerShell`します。 A **PS** プレフィックスは、Windows PowerShell セッションであることを示すために、コマンド プロンプトに追加します。

- 特定の実行ポリシーを使用してセッションを開始するには、 **ExecutionPolicy** パラメーター。

    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Windows PowerShell プロファイルいない Windows PowerShell セッションを開始するには使用、 **NoProfile** パラメーター。

    ```
    PowerShell.exe -NoProfile
    ```
  
- セッションを開始するには、 **ExecutionPolicy** パラメーター。

    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```
  
- PowerShell.exe のヘルプ ファイルを表示するには、次のコマンド形式を使用します。  
    
    ```
    PowerShell.exe -help, -?, /?
    ```

- コマンド プロンプト ウィンドウで、Windows PowerShell セッションを終了するには、入力 `exit`します。 一般的なコマンド プロンプトに戻ります。

完全な一覧については、 **PowerShell.exe** コマンド ライン パラメーターを参照して [about_PowerShell.Exe](https://go.microsoft.com/fwlink/?LinkID=113439)します。

## <a name="other-ways-to-start-windows-powershell"></a>Windows PowerShell を起動するには、その他の方法

Windows PowerShell を起動するには、その他の方法については、次を参照してください。 [Windows PowerShell の開始](https://go.microsoft.com/fwlink/?LinkID=135259)します。

## <a name="remarks"></a>注釈

Windows PowerShell は、Windows Server オペレーティング システムの Server Core インストール オプションで実行されます。 ただし、グラフィック ユーザーを必要とする機能、インターフェイスなど、 [Windows PowerShell Integrated Scripting Environment (ISE)](https://technet.microsoft.com/library/hh849182), 、および [Out-gridview](https://go.microsoft.com/fwlink/?LinkID=113364) と [Show-command](https://go.microsoft.com/fwlink/?LinkID=217448) コマンドレットは、Server Core インストールでは実行されません。

## <a name="additional-references"></a>その他の参照情報

[about_PowerShell.Exe](https://go.microsoft.com/fwlink/?LinkID=113439)
[about_PowerShell_Ise.exe](https://go.microsoft.com/fwlink/?LinkId=256512)
[Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
[Windows を使用したスクリプトPowerShell](https://technet.microsoft.com/scriptcenter/dd742419)も参照してください