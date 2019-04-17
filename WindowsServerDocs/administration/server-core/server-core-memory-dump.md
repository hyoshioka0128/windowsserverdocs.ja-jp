---
title: サーバーの主要なインストールのメモリ ダンプ ファイルを構成します。
description: Windows Server のサーバー コア インストールのメモリ ダンプのファイルを構成する方法について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: bd22378ec7ce5a1ff4e39546246e6e85ca859c45
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1448108"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>サーバーの主要なインストールのメモリ ダンプ ファイルを構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

インストール済みの Server Core のメモリ ダンプを構成するのには、次の手順を使用します。 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>手順 1: 自動システム ページのファイルの管理を無効にします。

最初の手順では、手動でシステム障害と回復のオプションを構成します。 これは、手順を完了する必要があります。

次のコマンドを実行します。 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>手順 2: メモリ ダンプのパスを構成します。

パーティション ページ ファイルをオペレーティング システムがインストールされている必要はありません。 パーティションを別のページのファイルを挿入するには、 **DedicatedDumpFile**という名前の新しいエントリを作成する必要があります。 **DumpFileSize**レジストリ エントリを使用してページング ファイルのサイズを定義できます。 DedicatedDumpFile と DumpFileSize レジストリ エントリを作成するには、次の手順を実行します。 

1. コマンド プロンプトで、レジストリ エディターを開く**regedit**コマンドを実行します。
2. 移動し、次のレジストリ サブキーをクリックします次。
3. クリックして**編集 > 新しい > 文字列値**します。
4. **DedicatedDumpFile**、新しい値の名前を付けるし、ENTER キーを押します。
5. **DedicatedDumpFile**] を右クリックし、[**変更**] をクリックします。
6. **値のデータ**型で**\ < Drive\ >: \\\ < Dedicateddumpfile.sys\ >**]、[ **OK**] をクリックします。

   >[!NOTE] 
   > 置き換える \ < Drive\ > ページング ファイル用のスペースし、置換は、十分なディスク ドライブと \ < Dedicateddumpfile.dmp\ > 専用のファイルへのフル パスにします。
 
7. クリックして**編集 > 新しい > DWORD 値**します。
8. **DumpFileSize**] を入力し、ENTER キーを押します。
9. **DumpFileSize**] を右クリックし、[**変更**] をクリックします。
10. **DWORD 値の編集**] で [**情報**] をクリックして**10 進数**します。
11. **値のデータ**をでは、適切な値を入力し、[ **OK**] をクリックします。
   >[!NOTE]
   > ダンプ ファイルのサイズはメガバイト (MB)
12. レジストリ エディターを終了します。

メモリ ダンプのパーティションの場所を決定すると、ページのファイルの保存先を構成します。 現在ページ ファイルのパスを表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get DebugFilePath
```

**DebugFilePath**の既定の宛先は、%systemroot%\memory.dmp です。 現在保存先を変更するには、次のコマンドを実行します。

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

設定 \ < FilePath\ > 先にします。 たとえば、次のコマンドは、メモリ ダンプ先のパスを C:\WINDOWS\MEMORY に設定します。DMP: 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>手順 3: メモリ ダンプの種類を設定します。

お使いのサーバーを構成するのには、メモリ ダンプの種類を確認します。 現在のメモリ ダンプの種類を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get DebugInfoType
```

現在のメモリ ダンプの種類を変更するには、次のコマンドを実行します。 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\ < Value\ > できる 0、1、2、または 3] の下にある定義されています。

- 0: メモリ ダンプの削除を無効にします。
- 1: フル メモリ ダンプします。 お使いのコンピューターが予期せず停止した場合は、システムのメモリの内容すべてを記録します。 フル メモリ ダンプ メモリ ダンプを収集するときに実行されていたプロセスからのデータがあります。
- 2: カーネル メモリ ダンプ (既定)。 カーネル メモリのみを記録します。 これは、お使いのコンピューターが予期せず停止したときに、ログ ファイルに情報を記録するためのプロセスをすばやく行うことがします。
- 3: 最小メモリ ダンプします。 最小お使いのコンピューターが予期せず停止した理由を特定するのに役立つ情報が記録されます。

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>手順 4: メモリ ダンプを生成した後に自動的に再開するのには、サーバーを構成します。

サーバー既定では、メモリ ダンプを生成後に自動的に再起動します。 現在の設定を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get AutoReboot
```

**だけ待ってから自動的**に値が TRUE の場合は、サーバーはメモリ ダンプを生成した後に自動的に再起動します。 構成する必要はありませんし、次の手順に進むことができます。

**だけ待ってから自動的**に値が FALSE の場合は、サーバーが自動的に再起動されません。 値を変更するのには、次のコマンドを実行します。

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>手順 5: 既存のメモリ ダンプ ファイルを上書きするのには、サーバーを構成します。

既定では、既存のメモリ ダンプ ファイルと新しい 1 つ作成されますが、サーバーに上書きされます。 メモリ ダンプの既存のファイルが既にを上書きする構成されているかどうかを確認するのには、次のコマンドを実行します。

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

値が 1 である場合は、既存のメモリ ダンプ ファイルがサーバーに上書きされます。 構成は必要ありませんし、次の手順に進むことができます。

値が 0 の場合は、サーバーは、既存のメモリ ダンプ ファイルを上書きしません。 値を変更するのには、次のコマンドを実行します。 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>手順 6: 通知を設定する管理

管理通知が適切かどうかを確認し、 **SendAdminAlert**を設定します。 SendAdminAlert の現在の値を表示するには、次のコマンドを実行します。

```
wmic RECOVEROS get SendAdminAlert
```

SendAdminAlert の値は TRUE または false を指定します。 True に既存の SendAdminAlert 値を変更するには、次のコマンドを実行します。 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>手順 7: メモリ ダンプのページのファイル サイズを設定します。

現在のページ ファイル設定を確認するには、次のコマンドのいずれかを実行します。

   ```
   wmic.exe pagefile
   ```

   または

   ```
   wmic.exe pagefile list /format:list
   ```

たとえば、ページ ファイルの初期と最大サイズを構成するのには、次のコマンドを実行します。

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>手順 8: 手動でメモリ ダンプを生成するのには、サーバーを構成します。

PS/2 キーボードを使用して、メモリ ダンプを手動で生成できます。 既定では、この機能が無効になっているし、はユニバーサル シリアル バス (USB) キーボードの利用できません。

手動のメモリを有効にするには、PS/2 キーボードで、次のコマンドの実行を使用してダンプします。

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

調べるには、この機能が適切に有効なかどうかは、次のコマンドを実行します。

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

変更を反映させるためにサーバーを再起動する必要があります。 サーバーは、次のコマンドを実行して再起動できます。

```
Shutdown / r / t 0
```

SCROLLLOCK キーを 2 回押しながら右 CTRL キーを押し、サーバーに接続されている PS/2 キーボードを使用して手動メモリ ダンプを生成することができます。 これにより、コンピューターにエラー コード省略チェックのバグします。 サーバーを再起動すると、手順 2 で設定した先のパスに新しいダンプ ファイルが表示されます。

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>手順 9: メモリ ダンプがファイルが正常に作成されていることを確認します。

メモリ ダンプ ファイルが正しく作成されていることを確認するのには、dumpchk.exe もうを使用することができます。 Dumpchk.exe ユーティリティが Server Core インストール オプションで、インストールされていないため、デスクトップ エクスペリエンスをサーバーから、または Windows 10 を実行する必要があります。 また、Windows 製品のデバッグ ツールをインストールする必要があります。  

Dumpchk.exe ユーティリティを使用して、任意のメディアを使用して、他のコンピューターに Windows Server 2008 の Server Core インストールのメモリ ダンプ ファイルを転送できます。

> [!WARNING]
> ページのファイルを慎重に転送方法とメソッドが必要なリソースを検討してください、非常に大きくできます。
 

その他の参照

メモリ ダンプ ファイルの使用に関する一般的な情報は、 [Windows のメモリ ダンプ ファイルのオプションの概要](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows)を参照してください。

専用ダンプ ファイルの詳細については、[システムのメモリ ダンプを取り込み中にシステム ドライブの容量制限を回避する DedicatedDeumpFile レジストリ値を使用する方法](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/)を参照してください。



