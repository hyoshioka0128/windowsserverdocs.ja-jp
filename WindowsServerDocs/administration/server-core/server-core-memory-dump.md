---
title: Server Core インストールのメモリ ダンプ ファイルを構成します。
description: Windows Server の Server Core インストールのメモリ ダンプ ファイルを構成する方法について説明します
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: bd22378ec7ce5a1ff4e39546246e6e85ca859c45
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828843"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>Server Core インストールのメモリ ダンプ ファイルを構成します。

>適用先:Windows Server (半期チャネル) および Windows Server 2016

次の手順を使用すると、メモリ ダンプ、Server Core インストールを構成できます。 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>手順 1:自動システム ページのファイルの管理を無効にします。

最初の手順では、手動でシステムの障害と回復のオプションを構成します。 これは、残りの手順に必要です。

次のコマンドを実行します。 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>手順 2:メモリ ダンプの保存先を構成します。

オペレーティング システムがインストールされているパーティションのページ ファイルが存在する必要はありません。 別のパーティションのページファイルを配置するには、という名前の新しいレジストリ エントリを作成する必要があります**DedicatedDumpFile**します。 使用して、ページング ファイルのサイズを定義することができます、 **DumpFileSize**レジストリ エントリ。 DedicatedDumpFile と DumpFileSize レジストリ エントリを作成するには、次の手順を実行します。 

1. コマンド プロンプトでは、実行、 **regedit**レジストリ エディターを開くコマンド。
2. 次のレジストリ サブキーを探してクリックします。次
3. **[編集]、[新規]、[文字列値]** の順にクリックします。
4. 新しい値に名前を**DedicatedDumpFile**、し、ENTER キーを押します。
5. 右クリックして**DedicatedDumpFile**、 をクリックし、**変更**します。
6. **値データ**型**\<ドライブ\>:\\\<Dedicateddumpfile.sys\>**、順にクリックします**OK**.

   >[!NOTE] 
   > 置換\<ドライブ\>、ページング ファイルの場所し、置き換えるための十分なディスクのあるドライブに\<Dedicateddumpfile.dmp\>専用のファイルへの完全なパス。
 
7. クリックして**編集 > 新しい > DWORD 値**します。
8. 型**DumpFileSize**、し、ENTER キーを押します。
9. 右クリックして**DumpFileSize**、 をクリックし、**変更**します。
10. **DWORD 値の編集**[**ベース**、] をクリックして**Decimal**します。
11. **値のデータ**に、適切な値を入力して、クリックして**OK**します。
   >[!NOTE]
   > メガバイト (MB) では、ダンプ ファイルのサイズです。
12. レジストリ エディターを終了します。

メモリ ダンプのパーティションの場所を決定したら、ページのファイルの保存先を構成します。 ページのファイルの現在の変換先のパスを表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get DebugFilePath
```

既定の転送先**DebugFilePath** %systemroot%\memory.dmp です。 現在のデプロイ先のパスを変更するには、次のコマンドを実行します。

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

設定\<FilePath\>先のパスにします。 たとえば、次のコマンドは、C:\WINDOWS\MEMORY にメモリ ダンプ先のパスを設定します。DMP: 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>手順 3:メモリ ダンプの種類を設定します。

サーバーの構成にメモリ ダンプの種類を決定します。 現在のメモリ ダンプの種類を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get DebugInfoType
```

現在のメモリ ダンプの種類を変更するには、次のコマンドを実行します。 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\<値\>の下に定義されている、0、1、2、3、または指定できます。

- 0:メモリ ダンプの削除を無効にします。
- 1:完全メモリ ダンプします。 コンピューターが予期せず停止したときに、すべてのシステム メモリの内容を記録します。 完全メモリ ダンプには、メモリ ダンプの収集時に実行されていたプロセスからデータを含めることができます。
- 2:カーネル メモリ ダンプ (既定値)。 カーネル メモリのみを記録します。 これは、コンピューターが予期せず停止したときに、ログ ファイルの情報を記録するプロセスが速くなります。
- 3:小さいメモリ ダンプします。 コンピューターが予期せず停止した理由を判別するのに役立つ情報の最小セットを記録します。

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>手順 4:メモリ ダンプを生成した後に自動的に再起動するサーバーを構成します。

サーバー、既定では、メモリ ダンプの生成後が自動的に再起動します。 現在の構成を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get AutoReboot
```

場合の値は、 **AutoReboot**が true の場合、メモリ ダンプを生成した後、サーバーが自動的に再起動されます。 構成は必要ありませんし、次の手順に進むことができます。

場合の値は、 **AutoReboot** false で、サーバーは自動的に再起動しません。 値を変更するには、次のコマンドを実行します。

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>手順 5:既存のメモリ ダンプ ファイルを上書きするサーバーを構成します。

既定では、サーバーは、新しい 1 つは作成時に既存のメモリ ダンプ ファイルを上書きします。 を上書きして、既存のメモリ ダンプ ファイルが既に構成されてかどうかを判断するには、次のコマンドを実行します。

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

値が 1 の場合、サーバーによって、既存のメモリ ダンプ ファイルが上書きされます。 構成は必要ありませんし、次の手順に進むことができます。

値が 0 の場合、サーバーは、既存のメモリ ダンプ ファイルを上書きしません。 値を変更するには、次のコマンドを実行します。 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>手順 6:管理者に警告を設定します。

管理者に警告に設定して、適切なかどうかを確認する**SendAdminAlert**それに応じて。 SendAdminAlert の現在の値を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get SendAdminAlert
```

SendAdminAlert の可能な値は TRUE または FALSE。 True に、既存の SendAdminAlert 値を変更するには、次のコマンドを実行します。 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>手順 7:メモリ ダンプのページ ファイル サイズを設定します。

現在のページファイルの設定を確認するには、次のコマンドのいずれかを実行します。

   ```
   wmic.exe pagefile
   ```

   または

   ```
   wmic.exe pagefile list /format:list
   ```

たとえば、ページファイルの初期および最大サイズを構成する次のコマンドを実行します。

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>手順 8:手動でメモリ ダンプを生成するサーバーを構成します。

Ps/2 キーボードを使用して、メモリ ダンプを手動で生成することができます。 既定では、この機能が無効になり、ユニバーサル シリアル バス (USB) のキーボード使用できなくなります。

手動のメモリを有効にするには、次のコマンドを実行して、ps/2 キーボードを使用してダンプします。

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

機能が正しく有効にされているかどうかを確認するのには、次のコマンドを実行します。

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

変更を有効にするサーバーを再起動する必要があります。 サーバーを再起動するには、次のコマンドを実行します。

```
Shutdown / r / t 0
```

2 回、SCROLLLOCK キーを押しながら右 CTRL キーを押しながら、サーバーに接続されている ps/2 キーボードを使用して手動メモリ ダンプを生成することができます。 これにより、コンピューター バグのエラー コード 0 xe2 でチェックします。 サーバーを再起動すると、手順 2. で確立されている先のパスに新しいダンプ ファイルが表示されます。

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>手順 9:そのメモリ ダンプが正しく作成されているファイルを確認します。

Dumpchk.exe もうを使用すると、メモリ ダンプ ファイルが正しく作成されることを確認します。 Dumpchk.exe ユーティリティは、Server Core インストール オプションでインストールされていないため、デスクトップ エクスペリエンス搭載サーバーまたは Windows 10 からそれを実行する必要があります。 また、Windows 用デバッグ ツールをインストールする必要があります。  

Dumpchk.exe ユーティリティを使用して、任意のメディアを使用して、他のコンピューターに Windows Server 2008 の Server Core インストールからメモリ ダンプ ファイルを転送できます。

> [!WARNING]
> ページのファイルを注意深くメソッドとメソッドを必要とするリソースは、転送を検討してください、非常に大きなできます。
 

その他の参照情報

メモリ ダンプ ファイルの使用についての概要については、次を参照してください。[メモリ ダンプ ファイルの概要については、Windows のオプション](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows)します。

専用のダンプ ファイルの詳細については、次を参照してください。 [DedicatedDeumpFile レジストリ値を使用して、システムのメモリ ダンプをキャプチャ中にシステム ドライブの領域の制限を克服する方法](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/)します。



