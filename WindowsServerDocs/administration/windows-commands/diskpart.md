---
Title: DiskPart コマンド
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 54b34b6d8849caecae2123ddab91a658a4692ba3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849343"
---
# <a name="diskpart-commands"></a>DiskPart コマンド


適用先:Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2、Windows Server 2008

DiskPart コマンドを使用して、PC のドライブ (ディスク、パーティション、ボリューム、または仮想ハード_ディスク) を管理するのに役立ちます。 DiskPart コマンドを使用するには、最初に一覧表示、およびフォーカスを設定するオブジェクトを選択する必要があります。 オブジェクトにフォーカスがある場合は、入力した任意の DiskPart コマンドはそのオブジェクトに対して機能します。

使用可能なオブジェクトを表示およびを使用して、オブジェクトの番号またはドライブ文字を決定できます、**リスト ディスク、ボリュームのリスト、リスト パーティション**、および**vdisk を一覧表示**コマンド。 **リスト ディスク、リスト vdisk**と**ボリュームを一覧表示**コマンドでは、コンピューターにすべてのディスクとボリュームが表示されます。 ただし、**パーティションを一覧表示**コマンドでは、フォーカスのあるディスク上のパーティションのみが表示されます。 使用すると、**一覧**コマンド、アスタリスク (\*) フォーカスを持つオブジェクトの横に表示されます。

オブジェクトを選択すると、フォーカスは、別のオブジェクトを選択するまでそのオブジェクトに残ります。 たとえば、ディスク 0 のフォーカスを設定し、2 のディスクのボリューム 8 を選択して場合にフォーカスを移動ディスク 0 からディスク 2 のボリューム 8。 一部のコマンドは、フォーカスを自動的に変更します。 たとえば、新しいパーティションを作成するときに、フォーカスは自動的に新しいパーティションに切り替わります。

のみを選択したディスクのパーティションにフォーカスを与えることができます。 パーティションにフォーカスがある場合は、(ある場合) に関連するボリュームはフォーカスもあります。 ときに、ボリュームは、フォーカス、関連するディスクとパーティション、ボリュームが 1 つの特定のパーティションにマップされている場合は、フォーカスがあることもあります。 これでない場合は、ディスクにフォーカスし、パーティションが失われるとします。

## <a name="diskpart-commands"></a>DiskPart コマンド

コマンド プロンプトで、DiskPart コマンド インタープリターを開始するには。

`diskpart`


> [!IMPORTANT]
> ローカル メンバーシップ<STRONG>管理者</STRONG>は DiskPart を実行するために必要な最小のグループ、またはそれと同等です。 
<br>


Diskpart コマンド インタープリターでは、次のコマンドを実行できます。

  - [Active](active.md)  
      
  - [[追加]](add.md)  
      
  - [割り当てる](assign.md)  
      
  - [vdisk をアタッチします。](attach-vdisk.md)  
      
  - [Attributes](attributes.md)  
      
  - [自動マウント](automount.md)  
      
  - [break](break.md)  
      
  - [クリーンアップ](clean.md)  
      
  - [vdisk を最適化します。](compact-vdisk.md)  
      
  - [[変換]](convert.md)  
      
  - [作成](create.md)  
      
  - [削除](delete.md)  
      
  - [Vdisk をデタッチします。](detach-vdisk.md)  
      
  - [詳細](detail.md)  
      
  - [終了](exit.md)  
      
  - [vdisk を展開します。](expand-vdisk.md)  
      
  - [Extend](extend.md)  
      
  - [ファイル システム](filesystems.md)  
      
  - [形式](format.md)  
      
  - [GPT](gpt.md)  
      
  - [ヘルプ](help.md)  
      
  - [[インポート](import.md)]  
      
  - [非アクティブ](inactive.md)  
      
  - [一覧](list.md)  
      
  - [Vdisk をマージします。](merge-vdisk.md)  
      
  - [オフライン](offline.md)  
      
  - [オンライン](online.md)  
      
  - [回復](recover.md)  
      
  - [rem](rem.md)  
      
  - [[削除]](remove.md)  
      
  - [修復](repair.md)  
      
  - [再スキャン](rescan.md)  
      
  - [保持](retain.md)  
      
  - [San](san.md)  
      
  - [Select](select.md)  
      
  - [セット id](set-id.md)  
      
  - [縮小](shrink.md)  
      
  - [一意の id](uniqueid.md)  
      

## <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[Windows PowerShell の記憶域コマンドレット](https://docs.microsoft.com/en-us/powershell/module/storage/)

