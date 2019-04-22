---
ms.assetid: e6b72a80-e8b7-4305-be0c-0a290f468d36
title: Windows Server 2003 組織への AD DS の展開
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 033973ad7a726054f6c47c7154fa54a3767beab4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816363"
---
# <a name="deploying-ad-ds-in-a-windows-server-2003-organization"></a>Windows Server 2003 組織への AD DS の展開

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

一部またはすべてのドメイン コント ローラーのオペレーティング システムのインプレース アップグレードを実行して Windows Server 2008 Active Directory Domain Services (AD DS) を展開するには、組織が Windows Server 2003 の Active Directory を実行中の場合 Windows Server 2008、またはお客様の環境に Windows Server 2008 を実行しているドメイン コント ローラーを導入することで。  
  
実行する必要がある既存の Windows Server 2003 の Active Directory ドメインに Windows Server 2008 を実行するドメイン コント ローラーを追加する前に**adprep**、コマンド ライン ツール。 Adprep は、AD DS スキーマを拡張し、選択したオブジェクトの既定のセキュリティ記述子を更新、および一部のアプリケーションで必要に応じて新しいディレクトリ オブジェクトを追加します。 Adprep は Windows Server 2008 のインストール ディスク (\sources\adprep\adprep.exe) でご確認いただけます。 詳細については、Adprep を参照してください ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215))。  
  
次の図は、Windows Server 2003 の Active Directory を現在実行中のネットワーク環境で Windows Server 2008 AD DS を展開する手順を示します。  
  
![windows 2003 の組織で展開します。](media/Deploying-AD-DS-in-a-Windows-Server-2003-Organization/900c4eee-1119-4a9a-9310-755597428b71.gif)  
  
> [!NOTE]  
> Windows Server 2008 へのドメインまたはフォレストの機能レベルを設定する場合は、環境内のすべてのドメイン コント ローラーは、Windows Server 2008 オペレーティング システムを実行する必要があります。  
  
リソースのドメインと Windows Server 2008 AD DS の展開の一部には、フォレスト間またはフォレスト内のドメインの再構築が必要とする可能性があります、Windows Server 2003 環境からのインプレース アップグレードしたアカウントのドメインを統合します。 フォレスト間での AD DS ドメインの再構築では、AD DS に組織の表現の複雑さを軽減でき、関連する管理コストが軽減されます。 レプリケーション トラフィックを減らし、ユーザーおよびグループの管理を必要とされる量を削減し、グループの管理を簡素化して、組織の管理オーバーヘッドを減らすことにより、フォレスト内の AD DS ドメインの再構築ポリシー。 詳細については、ADMT v3.1 移行ガイドを参照してください ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678))。  
  
計画し、Windows Server 2003 の Active Directory を実行している組織で AD DS の展開に使用できる詳細なタスクの一覧は、次を参照してください。[チェックリスト。Windows Server 2003 組織で AD DS 展開](https://technet.microsoft.com/library/cc771407.aspx)します。  
  


