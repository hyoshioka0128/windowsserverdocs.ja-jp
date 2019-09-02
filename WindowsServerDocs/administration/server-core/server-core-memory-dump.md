---
title: Server Core インストール用にメモリダンプファイルを構成する
description: Windows Server の Server Core インストール用にメモリダンプファイルを構成する方法について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: 0cea3118abce156acdd9ad933518015a25f8afbf
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476556"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>Server Core インストール用にメモリダンプファイルを構成する

>適用対象:Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

次の手順を使用して、Server Core インストール用にメモリダンプを構成します。 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>手順 1:システムページファイルの自動管理を無効にする

最初の手順として、システムの障害と回復のオプションを手動で構成します。 これは、残りの手順を完了するために必要です。

次のコマンドを実行します。 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>手順 2:メモリダンプの宛先パスを構成する

オペレーティングシステムがインストールされているパーティションにページファイルを配置する必要はありません。 ページファイルを別のパーティションに配置するには、 **DedicatedDumpFile**という名前の新しいレジストリエントリを作成する必要があります。 ページファイルのサイズを定義するには、Dumpfilesizeファイルサイズのレジストリエントリを使用します。 DedicatedDumpFile と DumpFileSize 両方のレジストリエントリを作成するには、次の手順を実行します。 

1. コマンドプロンプトで、 **regedit**コマンドを実行してレジストリエディターを開きます。
2. 次のレジストリ サブキーを探してクリックします。HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl
3. **[編集]、[新規]、[文字列値]** の順にクリックします。
4. 新しい値に**DedicatedDumpFile**という名前を入力し、enter キーを押します。
5. [ **DedicatedDumpFile**] を右クリックし、[**変更**] をクリックします。
6. [**値のデータ**型] に「  **\<\>\\\<Drive:Dedicateddumpfile」と入力し、[OK]をクリックします。\>**

   >[!NOTE] 
   > ドライブ\< \<\>を、ページングファイルに十分なディスク領域があるドライブに置き換え、Dedicateddumpfile を専用ファイルの完全なパスに置き換えます。\>
 
7. [編集] をクリックし **> 新しい DWORD 値 >** ます。
8. 「 **Dumpfilesize サイズ**」と入力し、enter キーを押します。
9. [Dumpfilesize**サイズ**] を右クリックし、[**変更**] をクリックします。
10. [ **DWORD 値の編集**] の [**ベース**] で、[ **10 進**] をクリックします。
11. [**値のデータ**] に適切な値を入力し、[ **OK]** をクリックします。
    >[!NOTE]
    > ダンプファイルのサイズはメガバイト (MB) 単位です。
12. レジストリ エディターを終了します。

メモリダンプのパーティションの場所を決定したら、ページファイルの保存先のパスを構成します。 ページファイルの現在の宛先パスを表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get DebugFilePath
```

**Debugfilepath**の既定の出力先は%systemroot%\memory.dmp. です。 現在の移行先パスを変更するには、次のコマンドを実行します。

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

\<FilePath\>を対象のパスに設定します。 たとえば、次のコマンドは、メモリダンプの宛先パスを C:\WINDOWS\MEMORY. に設定します。MEMORY.DMP 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>手順 3:メモリダンプの種類を設定する

サーバー用に構成するメモリダンプの種類を決定します。 現在のメモリダンプの種類を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get DebugInfoType
```

現在のメモリダンプの種類を変更するには、次のコマンドを実行します。 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\<次\>に定義されているように、値には0、1、2、または3を指定できます。

- 0メモリダンプの削除を無効にします。
- 1:完全なメモリダンプ。 コンピューターが予期せず停止したときに、システムメモリのすべての内容を記録します。 メモリダンプ全体には、メモリダンプが収集されたときに実行されていたプロセスのデータが含まれている場合があります。
- 2:カーネルメモリダンプ (既定値)。 カーネル メモリのみを記録します。 これにより、コンピューターが予期せず停止したときに、情報をログファイルに記録する処理が高速化されます。
- 3:メモリダンプが小さい。 コンピューターが予期せず停止した理由を特定するのに役立つ、有用な情報の最小セットを記録します。

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>手順 4:メモリダンプの生成後に自動的に再起動するようにサーバーを構成する

既定では、メモリダンプを生成した後にサーバーが自動的に再起動します。 現在の構成を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get AutoReboot
```

**Autoreboot**の値が TRUE の場合、メモリダンプの生成後にサーバーが自動的に再起動します。 構成は必要ありません。次の手順に進むことができます。

**Autoreboot**の値が FALSE の場合、サーバーは自動的に再起動されません。 次のコマンドを実行して値を変更します。

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>手順 5:既存のメモリダンプファイルを上書きするようにサーバーを構成する

既定では、新しいメモリダンプファイルが作成されると、サーバーは既存のメモリダンプファイルを上書きします。 既存のメモリダンプファイルが上書きされるように既に構成されているかどうかを確認するには、次のコマンドを実行します。

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

値が1の場合、サーバーは既存のメモリダンプファイルを上書きします。 構成は必要ありません。次の手順に進むことができます。

値が0の場合、サーバーは既存のメモリダンプファイルを上書きしません。 次のコマンドを実行して値を変更します。 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>手順 6:管理アラートの設定

管理アラートが適切かどうかを判断し、それに応じて**Sendadminalert**を設定します。 SendAdminAlert の現在の値を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get SendAdminAlert
```

SendAdminAlert に指定できる値は、TRUE または FALSE です。 既存の SendAdminAlert 値を true に変更するには、次のコマンドを実行します。 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>手順 7:メモリダンプのページファイルサイズを設定する

現在のページファイルの設定を確認するには、次のコマンドのいずれかを実行します。

   ```
   wmic.exe pagefile
   ```

   または

   ```
   wmic.exe pagefile list /format:list
   ```

たとえば、次のコマンドを実行して、ページファイルの初期サイズと最大サイズを構成します。

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>手順 8:手動メモリダンプを生成するようにサーバーを構成する

PS/2 キーボードを使用して、メモリダンプを手動で生成できます。 この機能は既定で無効になっており、ユニバーサルシリアルバス (USB) キーボードでは使用できません。

PS/2 キーボードを使用してメモリダンプを手動で有効にするには、次のコマンドを実行します。

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

機能が正しく有効になっているかどうかを判断するには、次のコマンドを実行します。

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

変更を有効にするには、サーバーを再起動する必要があります。 サーバーを再起動するには、次のコマンドを実行します。

```
Shutdown / r / t 0
```

サーバーに接続されている PS/2 キーボードを使用して手動メモリダンプを生成するには、右 CTRL キーを押しながら、スクロールロックキーを2回押します。 これにより、コンピューターのバグチェックにエラーコード0xE2 が使用されます。 サーバーを再起動すると、手順 2. で設定した移行先パスに新しいダンプファイルが表示されます。

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>手順 9:メモリダンプファイルが正しく作成されていることを確認する

Dumpchk utlity を使用して、メモリダンプファイルが正しく作成されていることを確認できます。 Dumpchk ユーティリティは、Server Core インストールオプションと共にインストールされないため、デスクトップエクスペリエンスまたは Windows 10 を使用してサーバーから実行する必要があります。 また、Windows 製品用のデバッグツールをインストールする必要があります。  

Dumpchk ユーティリティを使用すると、任意のメディアを使用して、Windows Server 2008 の Server Core インストールから他のコンピューターにメモリダンプファイルを転送できます。

> [!WARNING]
> ページファイルは非常に大きくなる可能性があるため、転送方法とその方法で必要なリソースを慎重に検討してください。
 

その他の参照情報

メモリダンプファイルの使用に関する一般的な情報については、「 [Windows のメモリダンプファイルオプションの概要](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows)」を参照してください。

専用ダンプファイルの詳細については、「 [DedicatedDeumpFile レジストリ値を使用してシステムメモリダンプをキャプチャ](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/)する」を参照してください。



