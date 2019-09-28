---
title: DiskPart コマンド
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 0826b773927f09cc846fb1cfdf4d5dfbf75d5cca
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377833"
---
# <a name="diskpart-commands"></a>DiskPart コマンド

適用先:Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、windows server 2008 R2、Windows Server 2008

DiskPart コマンドを使用すると、PC のドライブ (ディスク、パーティション、ボリューム、または仮想ハードディスク) を管理できます。 DiskPart コマンドを使用するには、まず、オブジェクトを一覧表示してから、フォーカスを与えるオブジェクトを選択する必要があります。 オブジェクトにフォーカスがある場合、入力した DiskPart コマンドはそのオブジェクトに対して動作します。

**List disk、list volume、list partition**、および**list vdisk**コマンドを使用して、使用可能なオブジェクトの一覧を表示し、オブジェクトの番号またはドライブ文字を特定できます。 **List disk、list vdisk** 、および**list volume**コマンドは、コンピューター上のすべてのディスクとボリュームを表示します。 ただし、 **list partition**コマンドは、フォーカスのあるディスク上のパーティションのみを表示します。 **List**コマンドを使用すると、フォーカスがあるオブジェクトの横にアスタリスク (\*) が表示されます。

オブジェクトを選択すると、別のオブジェクトを選択するまでフォーカスがそのオブジェクトに残ります。 たとえば、フォーカスがディスク0に設定されていて、ディスク2で [ボリューム 8] を選択した場合、フォーカスはディスク0からディスク2のボリューム8に移ります。 一部のコマンドでは、フォーカスが自動的に変更されます。 たとえば、新しいパーティションを作成すると、フォーカスは自動的に新しいパーティションに切り替わります。

選択したディスクのパーティションにのみフォーカスを移すことができます。 パーティションにフォーカスがある場合、関連するボリューム (存在する場合) にもフォーカスがあります。 ボリュームにフォーカスがある場合、関連するディスクとパーティションには、ボリュームが1つの特定のパーティションにマップされている場合にもフォーカスがあります。 そうでない場合は、ディスクとパーティションにフォーカスが失われます。

## <a name="diskpart-commands"></a>DiskPart コマンド

DiskPart コマンドインタープリターを起動するには、コマンドプロンプトで次のように入力します。

`diskpart`

> [!IMPORTANT]
> DiskPart を実行するには、ローカルの**Administrators**グループのメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。 

Diskpart コマンドインタープリターでは、次のコマンドを実行できます。

  - [Active](active.md)  
      
  - [[追加]](add.md)  
      
  - [割り当てる](assign.md)  
      
  - [Vdisk のアタッチ](attach-vdisk.md)  
      
  - [Attributes](attributes.md)  
      
  - [オートマ](automount.md)  
      
  - [改](break.md)  
      
  - [中身](clean.md)  
      
  - [Compact vdisk](compact-vdisk.md)  
      
  - [[変換]](convert.md)  
      
  - [作成](create.md)  
      
  - [削除](delete.md)  
      
  - [Vdisk のデタッチ](detach-vdisk.md)  
      
  - [データ](detail.md)  
      
  - [終了](exit.md)  
      
  - [Vdisk を展開する](expand-vdisk.md)  
      
  - [Extend](extend.md)  
      
  - [ファイルシステム](filesystems.md)  
      
  - [形式](format.md)  
      
  - [GPT](gpt.md)  
      
  - [ヘルプ](help.md)  
      
  - [[インポート]](import.md)  
      
  - [稼動](inactive.md)  
      
  - [表](list.md)  
      
  - [マージ vdisk](merge-vdisk.md)  
      
  - [なっ](offline.md)  
      
  - [オンライン](online.md)  
      
  - [回復](recover.md)  
      
  - [Rem](rem.md)  
      
  - [[削除]](remove.md)  
      
  - [回復](repair.md)  
      
  - [再スキャン](rescan.md)  
      
  - [日数](retain.md)  
      
  - [San](san.md)  
      
  - [Select](select.md)  
      
  - [Id の設定](set-id.md)  
      
  - [伸縮](shrink.md)  
      
  - [Uniqueid](uniqueid.md)  
      

## <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

[Windows PowerShell の記憶域コマンドレット](https://docs.microsoft.com/powershell/module/storage/)
