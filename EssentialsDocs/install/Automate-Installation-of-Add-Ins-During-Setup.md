---
title: セットアップ時のアドインのインストールの自動化
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 2e6ff6e4-8d68-4d49-9e38-8088bc8bf95e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b43b112de5a6bc3d7a27deed66fade65cf6da5a7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817365"
---
# <a name="automate-installation-of-add-ins-during-setup"></a>セットアップ時のアドインのインストールの自動化

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="automate-installing-add-ins-during-setup"></a><a name="BKMK_AddIns"></a>セットアップ時のアドインのインストールの自動化  
 セットアップ時にアドインをインストールするには、このドキュメントの「[初期構成後のタスクを実行するための PostIC.cmd ファイルの作成](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md)」で説明されている PostIC.cmd メソッドを使用します。  
  
 次のエントリを PostIC.cmd に追加します。  
  
```  
C:\Program Files\Windows Server\bin\Installaddin.exe <full path to wssx file> -q  
```  
  
 アドインでは、プレインストールとカスタマイズされたアンインストール手順がサポートされます。  
  
 プレインストール手順は、addin.xml で指定されたすべての **.msi** ファイルがインストールされる前に実行されます。 対話モードで実行している場合、進行状況ダイアログは表示されますが、進行状況は変化しません。 プレインストール フェーズ中は、取り消しボタンは無効になります。 プレインストール手順を実行するには、次の内容をパッケージ直下の addin.xml に追加します。  
  
> [!NOTE]
>  XML スキーマは、次の内容と正確に一致する必要があります。  
  
```  
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
  <Id>...</Id>  
  <Version>...</Version>  
  <Name>...</Name>  
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>  
  <ServerBinary>...</ServerBinary>  
  <ClientBinary32>...</ClientBinary32>  
  <ClientBinary64>...</ClientBinary64>  
  <SupportedSkus>...</SupportUrl>    
  <SupportUrl>...</SupportUrl>  
  <Location>...</Location>    
  <PrivacyStatement>...</PrivacyStatement>  
  <OtherBinaries>...</OtherBinaries>   
  <Preinstall>  
<Executable>exefile</Executable>  
<NormalArgs>args-for-interactive-mode</NormalArgs>  
<SilentArgs>args-for-silent-mode</SilentArgs>  
<IgnoreExitCode>true</IgnoreExitCode>  
  </Preinstall>  
  <UninstallConfirm>...</UninstallConfirm>      
</Package>  
<¦>  
<¦>  
```  
  
 **exefile** はプレインストール手順を実行するためのアドイン パッケージの実行可能ファイルであり、指定する必要があります。 **NormalArgs** は、対話モードを使用している場合にコマンド ラインで exefile に渡される引数を指定します。 このモードでは、ユーザーの操作中に exefile によって複数のダイアログが表示されることがあります。 **SilentArgs** は、サイレント モードを使用している場合にコマンド ラインで exefile に渡される引数を指定します (installaddin.exe を起動する場合は -q を指定)。 このモードでは、exefile によってウィンドウは表示されません。 **IgnoreExitCode** に true を指定すると、プレインストール手順は常に成功と見なされます。指定しない場合、終了コード 0 は成功を、1 は取り消しを、その他の値は失敗を示します。 タグ **NormalArgs**、**SilentArgs**、および **IgnoreExitCode** はすべてオプションです。  
  
 カスタマイズされたアンインストール手順は次のいずれかの目的で使用できます。  
  
- 組み込みの確認ダイアログの置換。  
  
- アンインストール前のカスタマイズされたダイアログの事前設定。  
  
- アンインストール前の特定タスクの実行。  
  
  アンインストール手順を実行するには、次の内容をパッケージ直下の addin.xml に追加します。  
  
```  
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
  <Id>...</Id>  
  <Version>...</Version>  
  <Name>...</Name>  
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>  
  <ServerBinary>...</ServerBinary>  
  <ClientBinary32>...</ClientBinary32>  
  <ClientBinary64>...</ClientBinary64>  
  <SupportedSkus>...</SupportUrl>    
  <SupportUrl>...</SupportUrl>  
  <Location>...</Location>    
  <PrivacyStatement>...</PrivacyStatement>  
  <OtherBinaries>...</OtherBinaries>   
  <Preinstall>¦</Preinstall>  
<UninstallConfirm>  
<Executable>full-path-to-exefile</Executable>  
<Arguments>command-line-arguments</Arguments>  
</UninstallConfirm>  
</Package>  
```  
  
 **full-path-to-exefile** は、システムにインストールされている exefile を指定します。 **Arguments** は、exefile のコマンド ライン引数を指定します。この指定は省略できます。 exefile は、組み込みのアンインストールの確認ダイアログが表示される前に呼び出されます。  
  
 exefile は、このフェーズで次のタスクを実行できます。  
  
- ユーザーの操作中におけるダイアログの表示。  
  
- バックグラウンド タスクの実行。  
  
  この実行可能ファイルの終了コードによって、次のようにアンインストール プロセスの続行方法が決定されます。  
  
- 0: アンインストール プロセスは、ユーザーの確認が完了している場合と同様に、組み込みの確認ダイアログを事前に設定することなく続行されます。 (このアプローチは、組み込みの確認ダイアログを置換するために使用できます。)  
  
- 1: アンインストール プロセスは取り消され、最終的にユーザーに取り消しのメッセージが表示されます。 すべての設定が変更されずに残ります。  
  
- その他: アンインストール プロセスは、カスタマイズされたアンインストール手順が存在しない場合と同様に、組み込みの確認ダイアログを使用して続行されます。  
  
  exefile の起動に失敗した場合は、exefile が 0 または 1 以外のコードを返した場合と同じ動作になります。  
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)