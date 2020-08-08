---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: Windows Server 2000 組織への AD DS の展開
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 64fac281e1038f80ed4119b2462beda3311ba877
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943191"
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Windows Server 2000 組織への AD DS の展開

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

組織で現在 Windows 2000 Active Directory が実行されている場合、windows server 2008 Active Directory Domain Services (AD DS) を展開するには、ドメインコントローラーのオペレーティングシステムの一部またはすべてを Windows Server 2008 にインプレースアップグレードするか、Windows Server 2008 を実行するドメインコントローラーを環境に導入します。

Windows Server 2008 を実行しているドメインコントローラーを既存の Windows 2000 Active Directory ドメインに追加するには、その前に、コマンドラインツール**adprep**を実行する必要があります。 Adprep は AD DS スキーマを拡張し、選択したオブジェクトの既定のセキュリティ記述子を更新し、一部のアプリケーションに必要な新しいディレクトリオブジェクトを追加します。 Adprep は、Windows Server 2008 インストールディスク (\sources\adprep\adprep.exe) で使用できます。 詳細については、「 [Adprep](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731728(v=ws.11))」を参照してください。

> [!NOTE]
> 既存の Windows 2000 AD DS ドメインコントローラーを Windows Server 2008 にインプレースアップグレードする場合は、まずサーバーを Windows Server 2003 にアップグレードしてから、Windows Server 2008 にアップグレードする必要があります。

次の図は、windows 2000 Active Directory を現在実行しているネットワーク環境に Windows Server 2008 AD DS を展開する手順を示しています。

![windows 2000 組織での展開](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)

> [!NOTE]
> ドメインまたはフォレストの機能レベルを Windows Server 2008 に設定する場合は、環境内のすべてのドメインコントローラーで Windows Server 2008 オペレーティングシステムを実行する必要があります。

Windows Server 2008 AD DS の展開の一部として Windows 2000 環境からアップグレードされたリソースおよびアカウントドメインを統合するには、フォレスト間またはフォレスト内のドメイン再構築が必要になることがあります。 フォレスト間で AD DS ドメインを再構築すると、組織の複雑さと、関連する管理コストを削減することができます。 フォレスト内の AD DS ドメインを再構築すると、レプリケーショントラフィックを削減し、必要なユーザーとグループ管理の量を減らし、グループポリシーの管理を簡素化することで、組織の管理オーバーヘッドを減らすことができます。 詳細については、「 [ADMT Guide: Active Directory ドメインの移行と再構築](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc974332(v=ws.10))」を参照してください。

現在 Windows 2000 Active Directory を実行している組織で AD DS を計画および展開するために使用できる詳細なタスクの一覧については、「[チェックリスト: windows 2000 組織での AD DS の展開](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc732737(v=ws.10))」を参照してください。
