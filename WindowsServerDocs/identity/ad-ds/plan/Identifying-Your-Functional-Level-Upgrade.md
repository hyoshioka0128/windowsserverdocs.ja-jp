---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: 機能レベルのアップグレードを識別する
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 7036a3be6a504f91cc6545484d7cd4f0dbd485ef
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943026"
---
# <a name="identifying-your-functional-level-upgrade"></a>機能レベルのアップグレードを識別する

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

ドメインとフォレストの機能レベルを上げるには、現在の環境を評価し、組織のニーズに最も合った機能レベルの要件を特定する必要があります。 フォレスト内のドメイン、各ドメインに配置されているドメインコントローラー、各ドメインコントローラーで実行されているオペレーティングシステムとサービスパック、およびドメインコントローラーをアップグレードする予定日を識別して、現在の環境を評価します。 ドメインコントローラーのインベントリからの削除を計画している場合は、環境に与える影響について十分に理解しておいてください。

次の状況では、以前のバージョンの Windows Server オペレーティングシステムを Windows Server 2008 または Windows Server 2008 R2 の機能レベルにアップグレードできない場合があります。

- ハードウェアの不足

- Windows Server 2008 または Windows Server 2008 R2 と互換性のないウイルス対策プログラムを実行しているドメインコントローラー

- Windows Server 2008 または Windows Server 2008 R2 で実行されないバージョン固有のプログラムの使用

- プログラムを最新の Service Pack にアップグレードする必要がある場合

この情報を文書化すると、完全に機能する Windows Server 2008 または Windows Server 2008 R2 環境を使用できるようにするための手順を特定するのに役立ちます。

現在の環境を評価した後、組織に適用される機能レベルのアップグレードを特定する必要があります。 次のオプションを使用できます。

- Windows Server 2008 または Windows Server 2008 R2 への windows 2000 ネイティブモード環境

- Windows server 2003 フォレストから Windows Server 2008 または Windows Server 2008 R2 へ

- 新しい Windows Server 2008 フォレスト

- 新しい Windows Server 2008 R2 フォレスト

## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>ネイティブ Windows 2000 Active Directory フォレストの機能レベルのアップグレード
Windows 2000 ベースのドメインコントローラーのみで構成される Windows 2000 ネイティブ環境では、機能レベルは既定で次のレベルに設定され、手動で起動するまでこれらのレベルにとどまります。

- Windows 2000 ネイティブドメインの機能レベル

- Windows 2000 フォレストの機能レベル

Windows Server 2008 または Windows Server 2008 R2 のフォレストレベルとドメインレベルのすべての機能を使用するには、この Windows 2000 環境を Windows Server 2008 または Windows server 2008 R2 にアップグレードする必要があります。 このアップグレードは、次のいずれかの方法で実行できます。

- 新しくインストールされた Windows Server 2008 ベースまたは Windows Server 2008 R2 ベースのドメインコントローラーをフォレストに導入し、Windows 2000 を実行しているすべてのドメインコントローラーを削除します。

- フォレスト内の Windows 2000 を実行しているすべての既存のドメインコントローラーを、Windows Server 2003 を実行しているドメインコントローラーにインプレースアップグレードします。 その後、これらのドメインコントローラーを Windows Server 2008 または Windows Server 2008 R2 にインプレースアップグレードします。 詳細については、「 [Windows server 2008 および Windows server 2008 R2 AD DS ドメインへの Active Directory ドメインのアップグレード](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731188(v=ws.10))」を参照してください。

    > [!IMPORTANT]
    >  Windows Server 2008 R2 は、x64 ベースのオペレーティングシステムです。 サーバーで x64 ベースバージョンの Windows Server 2003 が実行されている場合は、このコンピューターのオペレーティングシステムを Windows Server 2008 R2 にインプレースアップグレードできます。 サーバーで x86 ベースのバージョンの Windows Server 2003 が実行されている場合は、このコンピューターを Windows Server 2008 R2 にアップグレードすることはできません。

Windows server 2008 または windows Server 2008 R2 のドメインレベル機能を windows server 2008 または windows server 2008 R2 に2000アップグレードせずに使用するには、Windows Server 2008 または windows server 2008 R2 に対してドメインの機能レベルのみを上げます。

> [!NOTE]
> ドメインの機能レベルを上げる前に、そのドメイン内のすべての Windows 2000 ベースのドメインコントローラーを Windows Server 2008 または Windows Server 2008 R2 にアップグレードする必要があります。

フォレスト内のすべての Windows 2000 ベースのドメインコントローラーを、Windows Server 2008 または Windows Server 2008 R2 を実行するドメインコントローラーに置き換えた後、フォレストの機能レベルを Windows Server 2008 または windows server 2008 R2 に上げることができます。 これにより、windows 2000 ネイティブ以上に設定されているフォレスト内のすべてのドメインの機能レベルが Windows Server 2008 または Windows Server 2008 R2 に自動的に設定されます。

フォレストおよびドメインの機能レベルを上げる方法、およびこれらのタスクを実行する手順については、「 [Windows Server 2008 のフォレストルートドメインの展開](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))」を参照してください。

## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Windows Server 2003 Active Directory フォレストの機能レベルのアップグレード
Windows server 2003 ベースのドメインコントローラーのみで構成される Windows Server 2003 環境では、機能レベルは既定で次のレベルに設定され、手動で起動するまでこれらのレベルにとどまります。

- Windows 2000 ネイティブドメインの機能レベル

- Windows 2000 フォレストの機能レベル

Windows Server 2008 または Windows Server 2008 R2 のフォレストレベルとドメインレベルのすべての機能を使用するには、この Windows Server 2003 環境を Windows Server 2008 または Windows server 2008 R2 にアップグレードする必要があります。 このアップグレードは、次のいずれかの方法で実行できます。

- 新しくインストールされた Windows Server 2008 ベースまたは Windows Server 2008 R2 ベースのドメインコントローラーをフォレストに導入し、Windows Server 2003 を実行しているすべてのドメインコントローラーを削除するか、windows server 2008 または Windows Server 2008 R2 にアップグレードします。

- Windows server 2003 を実行している既存のすべてのドメインコントローラーを、Windows Server 2008 または Windows Server 2008 R2 を実行しているドメインコントローラーにインプレースアップグレードします。 詳細については、「 [Windows server 2008 および Windows server 2008 R2 AD DS ドメインへの Active Directory ドメインのアップグレード](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731188(v=ws.10))」を参照してください。

> [!IMPORTANT]
> Windows Server 2008 R2 は、x64 ベースのオペレーティングシステムです。 サーバーで x64 ベースバージョンの Windows Server 2003 が実行されている場合は、このコンピューターのオペレーティングシステムを Windows Server 2008 R2 にインプレースアップグレードできます。 サーバーで x86 ベースのバージョンの Windows Server 2003 が実行されている場合は、Windows Server 2008 R2 を実行するようにこのコンピューターをアップグレードすることはできません。

Windows server 2003 フォレスト全体を Windows server 2008 または windows Server 2008 R2 にアップグレードせずに、すべての Windows Server 2008 または Windows Server 2008 R2 のドメインレベル機能を使用するには、ドメインの機能レベルを Windows Server 2008 または Windows server 2008 R2 に上げます。

> [!NOTE]
> ドメインの機能レベルを上げる前に、そのドメイン内のすべての Windows Server 2003 ベースのドメインコントローラーを Windows Server 2008 または Windows Server 2008 R2 にアップグレードする必要があります。

フォレスト内の Windows Server 2003 ベースのすべてのドメインコントローラーを Windows Server 2008 または windows Server 2008 R2 にアップグレードした後で、フォレストの機能レベルを Windows Server 2008 または windows server 2008 R2 に上げることができます。 これにより、Windows Server 2003 に設定されているフォレスト内のすべてのドメインの機能レベルが、windows server 2008 または Windows Server 2008 R2 に自動的に設定されます。

フォレストおよびドメインの機能レベルを上げる方法、およびこれらのタスクを実行する手順については、「 [Windows Server 2008 のフォレストルートドメインの展開](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))」を参照してください。

## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>新しい Windows Server 2008 フォレストの機能レベルをアップグレードする
新しい Windows Server 2008 フォレストに最初のドメインコントローラーをインストールすると、既定では次のレベルに機能レベルが設定され、手動で起動するまでこれらのレベルのままになります。

- Windows 2000 ネイティブドメインの機能レベル

- Windows 2000 フォレストの機能レベル

機能レベルは、これらの既定のレベルで設定され、Windows 2000 または Windows Server 2003 ベースのドメインコントローラーを新しい Windows Server 2008 フォレストに追加するオプションを提供します。 フォレストルートドメインを作成した後、Windows Server 2008 フォレストに追加する各ドメインのドメイン機能レベルは、Windows 2000 native に設定されます。 ただし、新しい Windows Server 2008 環境内のすべてのドメインコントローラーで Windows Server 2008 を実行する場合は、フォレストに最初のドメインコントローラーをインストールするときに、フォレストの機能レベルとドメインの機能レベルを Windows Server 2008 に設定します。 これにより、時間が節約され、Windows Server 2008 のフォレストレベルおよびドメインレベルのすべての機能が有効になります。

> [!IMPORTANT]
> フォレストが Windows Server 2008 の機能レベルで動作し、Windows Server 2003 ベースのメンバーサーバーまたは Windows 2000 ベースのメンバーサーバーに Active Directory をインストールしようとすると、インストールは失敗します。

フォレストおよびドメインの機能レベルを上げる方法、およびこれらのタスクを実行する手順については、「 [Windows Server 2008 のフォレストルートドメインの展開](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))」を参照してください。

## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>新しい Windows Server 2008 R2 フォレストでの機能レベルのアップグレード
新しい Windows Server 2008 R2 フォレストに最初のドメインコントローラーをインストールすると、既定では、機能レベルは次のレベルに設定され、手動で起動するまでこれらのレベルのままになります。

- Windows Server 2003 ドメインの機能レベル

- Windows Server 2003 フォレストの機能レベル

機能レベルは、これらの既定のレベルで設定され、Windows Server 2003 ベースのドメインコントローラーを新しい Windows Server 2008 R2 フォレストに追加するオプションを提供します。 フォレストルートドメインを作成すると、Windows Server 2008 R2 フォレストに追加する各ドメインのドメイン機能レベルが Windows Server 2003 に設定されます。 ただし、新しい Windows Server 2008 R2 環境内のすべてのドメインコントローラーで Windows Server 2008 R2 を実行する必要がある場合は、フォレストの最初のドメインコントローラーをインストールするときに、フォレストの機能レベルとドメインの機能レベルを Windows Server 2008 R2 に設定します。 これにより、時間が節約され、Windows Server 2008 R2 のフォレストレベルおよびドメインレベルのすべての機能が有効になります。

> [!IMPORTANT]
> フォレストが Windows Server 2008 R2 の機能レベルで動作し、windows Server 2008 ベースまたは Windows Server 2003 ベースのメンバーサーバーまたは Windows 2000 ベースのメンバーサーバーに Active Directory をインストールしようとすると、インストールは失敗します。

フォレストおよびドメインの機能レベルを上げる方法、およびこれらのタスクを実行する手順については、「 [Windows Server 2008 のフォレストルートドメインの展開](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))」を参照してください。

> [!NOTE]
> ADMT version 3.1 は Windows Server 2008 にインストールする必要がありますが、ADMT v4.0 を使用して、1つまたは複数の Windows Server 2008 R2 ドメインコントローラーでホストされているドメインにオブジェクトを移行することができます。 詳細については、Microsoft サポート技術情報の記事976659、「 [ADMT 3.1 を使用して Windows Server 2008 R2 ドメインコントローラーを含むドメインに移行するときに発生する可能性がある既知の問題](https://support.microsoft.com/help/976659/)」を参照してください。
