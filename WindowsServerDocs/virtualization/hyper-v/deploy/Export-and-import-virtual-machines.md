---
title: 仮想マシンをエクスポートおよびインポートする
description: エクスポートし、HYPER-V マネージャーまたは Windows PowerShell を使用して仮想マシンをインポートする方法を示します。
ms.prod: windows-server-threshold
author: KBDAzure
ms.author: kathydav
manager: dongill
ms.technology: compute-hyper-v
ms.date: 12/13/2016
ms.topic: article
ms.assetid: 7fd996f5-1ea9-4b16-9776-85fb39a3aa34
ms.openlocfilehash: b326fe8d7ff05ba73fc94225fa38921b42eb3fc6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844323"
---
>適用先:Windows 10、Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

# <a name="export-and-import-virtual-machines"></a>仮想マシンのエクスポートとインポート

この記事では、エクスポートしに移動またはコピーする簡単な方法は、仮想マシンをインポートする方法を示します。 この記事では、エクスポートを実施する際にインポートしたりする選択肢をいくつかも説明します。

## <a name="export-a-virtual-machine"></a>仮想マシンのエクスポート

エクスポート - 仮想ハード ディスク ファイル、仮想マシンの構成ファイル、およびすべてのチェックポイント ファイルの 1 つの単位に必要なすべてのファイルを収集します。 開始または停止の状態にある仮想マシンで、これを行うことができます。

### <a name="using-hyper-v-manager"></a>Hyper-V マネージャーの使用

仮想マシンのエクスポートを作成するには

1. HYPER-V マネージャーでは、仮想マシンを右クリックし、選択 **エクスポート**です。

2. エクスポートされたファイルを格納し、をクリックする場所を選択**エクスポート**します。

エクスポートが完了したら、エクスポートの場所にエクスポートされたファイルすべてを確認できます。

### <a name="using-powershell"></a>PowerShell を使用する

管理者としてセッションを開き、交換した後、次のようなコマンドを実行\<vm 名\>と\<パス\>:

```powershell
Export-VM -Name \<vm name\> -Path \<path\>
```

詳細については、次を参照してください。 [EXPORT-VM](https://docs.microsoft.com/powershell/module/hyper-v/export-vm)します。

## <a name="import-a-virtual-machine"></a>仮想マシンのインポート 

仮想マシンをインポートすると、仮想マシンが Hyper-V ホストに登録されます。 ホスト、または新しいホストにインポートすることができます。 同じホストにインポートしている場合は、HYPER-V で使用可能なファイルから仮想マシンを再作成しようとするため、最初に、仮想マシンをエクスポートする必要はありません。 仮想マシンをインポートする登録が、HYPER-V ホスト上に使用できるようにします。

仮想マシンのインポート ウィザードから別のホストに移動するときに存在可能な非互換性を解決するのにも役立ちます。 これは、メモリ、仮想スイッチ、仮想プロセッサなどの物理ハードウェアの相違では一般的です。

### <a name="import-using-hyper-v-manager"></a>HYPER-V マネージャーを使用したインポート

仮想マシンをインポートするには。

1. **アクション**、HYPER-V マネージャーでは、メニュー**仮想マシンのインポート**します。

2. **[次へ]** をクリックします。

3. エクスポートされたファイルを含むフォルダーを選択し、クリックして**次**します。

4. インポートする仮想マシンを選択します。

5. インポートの種類を選択し、クリックして**次**します。 (詳細については、次を参照してください[型をインポート](#import-types)、後述します。)。

6. **[Finish]**(完了) をクリックします。

### <a name="import-using-powershell"></a>PowerShell を使用したインポート

使用して、 **IMPORT-VM**するインポートの種類の例を次のコマンドレット。 型の説明については、次を参照してください。[型をインポート](#import-types)、後述します。 

#### <a name="register-in-place"></a>インプレース登録します。

この種類のインポート ファイルのインポート時の格納を使用して、仮想マシンの ID を保持 次のコマンドは、インポート ファイルの例を示します。 独自の値と同様のコマンドを実行します。

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' 
```

#### <a name="restore"></a>[復元]

仮想マシン ファイルのパスを指定する仮想マシンをインポートするには、例を値に置き換えて、このようなコマンドを実行します。

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -VhdDestinationPath 'D:\Virtual Machines\WIN10DOC' -VirtualMachinePath 'D:\Virtual Machines\WIN10DOC'
```

#### <a name="import-as-a-copy"></a>コピーとインポートします。

コピーのインポートを完了し、仮想マシン ファイルを HYPER-V の既定の場所に移動するには、例を値に置き換えて、このようなコマンドを実行します。

``` PowerShell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -GenerateNewId
```

詳細については、次を参照してください。 [IMPORT-VM](https://docs.microsoft.com/powershell/module/hyper-v/import-vm)します。

### <a name="import-types"></a>種類のインポート

HYPER-V には、次の 3 つの種類のインポートが用意されています。

- **インプレース登録**– この種類は、ここで保存したり、仮想マシンの実行場所でのエクスポート ファイルが前提としています。 インポートされた仮想マシンは、エクスポート時に、同様に、同じ ID を持ちます。 このため、仮想マシンが HYPER-V では、既に登録されている場合、削除する必要のインポート動作させるには。 エクスポート ファイルが実行中になる、インポートが完了したら、ファイルの状態にあり、削除することはできません。

- **仮想マシンを復元**-仮想マシンを選択すると、場所に復元します。 または、Hyper-v の既定値を使用します。 このインポートの種類は、エクスポートされたファイルのコピーを作成し、選択した場所に移動します。 インポートすると、仮想マシンはエクスポート時と同じ ID を持ちます。 このため場合は、HYPER-V で仮想マシンが既に実行されている必要が、インポートを完了する前に削除します。 インポートが完了したら、エクスポートされたファイルがそのまま残りますおよび削除したり再度インポートします。

- **仮想マシンをコピー** – ファイルの場所を選択することで、復元の種類に似ています。 違いは、インポートされた仮想マシンに新しい一意な ID、インポートを意味することができます、仮想マシンを同じホストに複数回です。

