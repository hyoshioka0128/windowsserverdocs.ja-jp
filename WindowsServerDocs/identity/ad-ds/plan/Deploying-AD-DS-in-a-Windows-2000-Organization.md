---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: Windows Server 2000 組織への AD DS の展開
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5015c0ca2c01fca966927af4207a7e3501d9cd39
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854283"
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Windows Server 2000 組織への AD DS の展開

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

一部またはすべての Windows ドメイン コント ローラーのオペレーティング システムのインプレース アップグレードを実行して Windows Server 2008 Active Directory Domain Services (AD DS) を展開するには、組織が Windows 2000 Active Directory を実行中の場合Server 2008 またはお客様の環境に Windows Server 2008 を実行しているドメイン コント ローラーを導入することで。  
  
実行する必要がある既存の Windows 2000 Active Directory ドメインに Windows Server 2008 を実行するドメイン コント ローラーを追加する前に**adprep**、コマンド ライン ツール。 Adprep は、AD DS スキーマを拡張し、選択したオブジェクトの既定のセキュリティ記述子を更新、および一部のアプリケーションで必要に応じて新しいディレクトリ オブジェクトを追加します。 Adprep は Windows Server 2008 のインストール ディスク (\sources\adprep\adprep.exe) でご確認いただけます。 詳細については、Adprep を参照してください ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215))。  
  
> [!NOTE]  
> Windows Server 2008 に既存の Windows 2000 の AD DS ドメイン コント ローラーのインプレース アップグレードを実行する場合は、サーバーに Windows Server 2003 では、まずアップグレードし、Windows Server 2008 にアップグレードする必要があります。  
  
次の図は、Windows 2000 Active Directory を現在実行中のネットワーク環境で Windows Server 2008 AD DS を展開する手順を示します。  
  
![windows 2000 の組織で展開します。](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)  
  
> [!NOTE]  
> Windows Server 2008 へのドメインまたはフォレストの機能レベルを設定する場合は、環境内のすべてのドメイン コント ローラーは、Windows Server 2008 オペレーティング システムを実行する必要があります。  
  
Windows Server 2008 AD DS の一部として、Windows 2000 環境からインプレース アップグレードはリソースとアカウントのドメインを統合するフォレストまたはフォレスト内のドメインの再構築、展開は必要があります。 フォレスト間での AD DS ドメインの再構築すると、組織と関連付けられている管理コストの複雑さを軽減するのに役立ちます。 レプリケーション トラフィックを減らし、ユーザーおよびグループの管理を必要とされる量を削減しの管理を簡素化して、組織の管理オーバーヘッドを軽減することにより、フォレスト内の AD DS ドメインの再構築グループ ポリシー。 詳細については、ADMT v3.1 移行ガイドを参照してください ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678))。  
  
計画や、Windows 2000 Active Directory が現在実行されている組織で AD DS の展開に使用できる詳細なタスクの一覧は、次を参照してください。[チェックリスト。Windows 2000 の組織内の AD DS 展開](https://technet.microsoft.com/library/cc732737.aspx)します。  
  


