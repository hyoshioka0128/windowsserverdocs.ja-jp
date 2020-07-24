---
title: PowerShell_ise
description: Windows PowerShell Integrated Scripting Environment (ISE) セッションを開始する PowerShell_ise コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 32c41b5b-a210-47d9-bd8c-91eb9830b4f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 24fc3c6dca5ba3fea872f625b2ef81f1c78f59fb
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956574"
---
# <a name="powershell_ise"></a>PowerShell_ise

Windows PowerShell Integrated Scripting Environment (ISE) は、読み取り、書き込み、実行、デバッグ、およびグラフィック支援型の環境でスクリプトおよびモジュールをテストすることができますグラフィカル ホスト アプリケーションです。 IntelliSense などの機能をキー Show コマンド、スニペット、タブ補完、構文の色分け、視覚的デバッグ、および状況依存のヘルプが豊富なスクリプトの操作性を提供します。

## <a name="using-powershellexe"></a>PowerShell.exe を使用します。

**PowerShell_ISE.exe** ツールは Windows PowerShell ISE セッションを開始します。 使用すると **PowerShell_ISE.exe**, 、Windows PowerShell ISE でファイルを開くか、プロファイルなしで、またはマルチ スレッド アパートメントで Windows PowerShell ISE のセッションを開始する、省略可能パラメーターを使用することができます。

- コマンドプロンプトウィンドウ、Windows PowerShell、または [**スタート**] メニューで Windows PowerShell ISE セッションを開始するには、次のように入力します。

  ```powershell
  PowerShell_Ise.exe
  ```

- スクリプト (ps1)、スクリプトモジュール (. hbase-runner.psm1)、モジュールマニフェスト (.psd1)、XML ファイル、またはその他のサポートされている Windows PowerShell ISE ファイルを開くには、次のように入力します。

  ```powershell
  PowerShell_Ise.exe <filepath>
  ```

  Windows PowerShell 3.0 で使用できます、省略可能な **ファイル** パラメーターとして次のとおりです。

  ```powershell
  PowerShell_Ise.exe -file <filepath>
  ```

- Windows PowerShell プロファイルいない Windows PowerShell ISE のセッションを開始するには、使用、 **NoProfile** パラメーター。 ( **Noprofile**パラメーターは Windows PowerShell 3.0 で導入されました)。次のように入力します。

  ```powershell
  PowerShell_Ise.exe -NoProfile
  ```

- PowerShell_ISE.exe ヘルプファイルを表示するには、次のように入力します。

    ```powershell
    PowerShell_Ise.exe -help
    PowerShell_Ise.exe -?
    PowerShell_Ise.exe /?
    ```

### <a name="remarks"></a>注釈

- **PowerShell_ISE.exe**のコマンドラインパラメーターの完全な一覧については、「 [about_PowerShell_Ise.Exe](/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe)」を参照してください。

- Windows PowerShell を起動するには、その他の方法については、次を参照してください。 [Windows PowerShell の開始](/powershell/scripting/windows-powershell/starting-windows-powershell)します。

- Windows PowerShell は、Windows Server オペレーティング システムの Server Core インストール オプションで実行されます。 ただし、Windows PowerShell ISE には、グラフィック ユーザー インターフェイスが必要であるために、Server Core インストールで実行にしないとはされません。

## <a name="additional-references"></a>その他のリファレンス

- [about_PowerShell_Ise.exe](/powershell/module/microsoft.powershell.core/about/about_powershell_exe)
