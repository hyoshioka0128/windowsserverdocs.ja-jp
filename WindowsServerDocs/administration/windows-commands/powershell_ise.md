---
title: PowerShell_ise
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 32c41b5b-a210-47d9-bd8c-91eb9830b4f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5fb143c3d365b47f66aee5c64bfdc7dc26e5794f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723281"
---
# <a name="powershell_ise"></a>PowerShell_ise



Windows PowerShell Integrated Scripting Environment (ISE) は、読み取り、書き込み、実行、デバッグ、およびグラフィック支援型の環境でスクリプトおよびモジュールをテストすることができますグラフィカル ホスト アプリケーションです。 IntelliSense などの機能をキー Show コマンド、スニペット、タブ補完、構文の色分け、視覚的デバッグ、および状況依存のヘルプが豊富なスクリプトの操作性を提供します。

**PowerShell_ISE.exe** ツールは Windows PowerShell ISE セッションを開始します。 使用すると **PowerShell_ISE.exe**, 、Windows PowerShell ISE でファイルを開くか、プロファイルなしで、またはマルチ スレッド アパートメントで Windows PowerShell ISE のセッションを開始する、省略可能パラメーターを使用することができます。

**PowerShell_ISE.exe** Windows PowerShell 2.0 で導入され、Windows PowerShell 3.0 では大幅に拡大されました。

## <a name="using-powershell_iseexe"></a>PowerShell_ISE.exe を使用します。

使用する **PowerShell_ISE.exe** を開始し、次のように Windows PowerShell セッションを終了します。
- Windows PowerShell、または [スタート] メニューでは、コマンド プロンプト ウィンドウで、Windows PowerShell ISE のセッションを開始するには、次のように入力します。  
  ```
  PowerShell_Ise
  ```  
- Windows PowerShell ISE でスクリプト (.ps1)、スクリプト モジュール (.psm1)、モジュール マニフェスト (.psd1)、XML ファイル、またはその他のサポートされているファイルを開くには、次のコマンド形式を使用します。  
  ```
  PowerShell_Ise <FilePath>
  ```  
  Windows PowerShell 3.0 で使用できます、省略可能な **ファイル** パラメーターとして次のとおりです。  
  ```
  PowerShell_Ise -File <FilePath>
  ```  
- Windows PowerShell プロファイルいない Windows PowerShell ISE のセッションを開始するには、使用、 **NoProfile** パラメーター。 (、 **NoProfile** パラメーターは Windows PowerShell 3.0 で導入されました)。  
  ```
  PowerShell_Ise -NoProfile
  ```  
- 表示する、 **PowerShell_ISE.exe** の支援のファイルは、コマンド プロンプト ウィンドウで、次のコマンド形式を使用します。  
  ```
  PowerShell_Ise -help, -?, /?
  ```  
  完全な一覧については、 **PowerShell_ISE.exe** コマンド ライン パラメーターを参照して [about_PowerShell_Ise.exe](https://go.microsoft.com/fwlink/?LinkId=256512)します。

## <a name="start-windows-powershell-ise-in-other-ways"></a>その他の方法で Windows PowerShell ISE を開始します。

Windows PowerShell ISE を開始するには、その他の方法については、次を参照してください。 [Windows PowerShell の開始](https://go.microsoft.com/fwlink/?LinkID=135259)します。

## <a name="remarks"></a>Remarks

Windows PowerShell は、Windows Server オペレーティング システムの Server Core インストール オプションで実行されます。 ただし、Windows PowerShell ISE には、グラフィック ユーザー インターフェイスが必要であるために、Server Core インストールで実行にしないとはされません。

## <a name="additional-references"></a>その他の参照情報

[about_PowerShell_Ise about_PowerShell](https://go.microsoft.com/fwlink/?LinkId=256512)
windows powershell[を使用した](https://technet.microsoft.com/scriptcenter/dd742419)[windows](https://go.microsoft.com/fwlink/?LinkID=107116)
powershell スクリプト[about_PowerShell.exe](https://go.microsoft.com/fwlink/?LinkID=113439)
