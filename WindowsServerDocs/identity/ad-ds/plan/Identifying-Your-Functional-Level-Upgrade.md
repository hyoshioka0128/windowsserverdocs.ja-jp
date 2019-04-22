---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: 機能レベルのアップグレードを識別する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8aee6a5560edfae656582b3c2812ca69c6b90f57
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812043"
---
# <a name="identifying-your-functional-level-upgrade"></a>機能レベルのアップグレードを識別する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

ドメインおよびフォレスト機能レベルを上げることができます、前に、現在の環境を評価し、組織のニーズに最も合う機能レベルの要件を特定する必要があります。 ドメイン フォレストで、各ドメイン、オペレーティング システムとサービス パックを実行している各ドメイン コント ローラーとドメインをアップグレードする予定の日付に配置されているドメイン コント ローラーを識別することによって、現在の環境を評価します。コント ローラー。 そうが環境に与える影響をすべてを理解する場合は、ドメイン コント ローラーをインベントリから削除することを確認します。  
  
次の状況では、以前のバージョンの Windows Server オペレーティング システムを Windows Server 2008 または Windows Server 2008 R2 の機能レベルにアップグレードを妨げる可能性があります。  
  
-   ハードウェアの不足  
  
-   Windows Server 2008 または Windows Server 2008 R2 と互換性がないウイルス対策プログラムを実行するドメイン コント ローラー   
  
-   Windows Server 2008 または Windows Server 2008 R2 で実行していないバージョンに固有のプログラムの使用   
  
-   最新の service pack を使用してプログラムをアップグレードする必要があります。  
  
この情報を文書化すると、完全に機能の Windows Server 2008 または Windows Server 2008 R2 環境があることを確認するための手順を特定できます。  
  
現在の環境を評価したら、組織に適用される機能のレベルのアップグレードを識別するためがあります。 これらのオプションを使用できます。  
  
-   Windows Server 2008 または Windows Server 2008 R2 を Windows 2000 ネイティブ モード環境   
  
-   Windows Server 2008 または Windows Server 2008 R2 を Windows Server 2003 フォレスト   
  
-   Windows Server 2008 の新しいフォレスト  
  
-   Windows Server 2008 R2 の新しいフォレスト  
  
## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>ネイティブの Windows 2000 Active Directory フォレストの機能レベルをアップグレードします。  
Windows 2000 ベースのドメイン コント ローラーのみで構成される Windows 2000 ネイティブ環境で、機能レベルが既定では、次のレベルに設定し、手動で生成されるまでこれらのレベルで維持します。  
  
-   Windows 2000 ネイティブ ドメイン機能レベル  
  
-   Windows 2000 フォレストの機能レベル  
  
Windows Server 2008 または Windows Server 2008 R2 のすべてのフォレスト レベルとドメイン レベルの機能を使用するには、Windows Server 2008 または Windows Server 2008 R2 にこの Windows 2000 環境をアップグレードする必要があります。 このアップグレードは、次の方法のいずれかで実行できます。  
  
-   新しくインストールされた Windows Server 2008 の導入-ベースまたは Windows Server 2008 R2 のフォレストにドメイン コント ローラーをベースし、し、Windows 2000 を実行しているすべてのドメイン コント ローラーをインベントリから削除します。  
  
-   Windows Server 2003 を実行するドメイン コント ローラーをフォレストに Windows 2000 を実行している既存のすべてのドメイン コントローラのインプレース アップグレードを実行します。 次に、Windows Server 2008 または Windows Server 2008 R2 ドメイン コント ローラーのインプレース アップグレードを実行します。 詳細については、次を参照してください。[を Windows Server 2008 AD DS ドメインの Active Directory ドメインのアップグレード\[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)します。  
  
    > [!IMPORTANT]  
    >  Windows Server 2008 R2 では、x64 ベースのオペレーティング システムです。 サーバーで Windows Server 2003 の x64 ベースのバージョンが実行されている場合は、Windows Server 2008 R2 へのこのコンピューターのオペレーティング システムのインプレース アップグレードを正常に実行できます。 サーバーで Windows Server 2003 の x86 ベースのバージョンが実行されている場合は、このコンピューターを Windows Server 2008 R2 にアップグレードできません。  
  
Windows Server 2008 または Windows Server 2008 R2 ドメイン レベルの機能を使用して、Windows Server 2008 または Windows Server 2008 R2、Windows 2000 フォレスト全体をアップグレードすることがなく、ドメイン機能レベルを Windows Server 2008 または Windows Server 2008 のみを上げるR2。  
  
> [!NOTE]  
> ドメインの機能レベルを上げると、前に、Windows Server 2008 または Windows Server 2008 R2 にそのドメイン内のすべての Windows 2000 ベースのドメイン コント ローラーをアップグレードする必要があります。  
  
Windows Server 2008 または Windows Server 2008 R2 を実行するドメイン コント ローラーに、フォレスト内のすべての Windows 2000 ベースのドメイン コント ローラーを置き換えると後から Windows Server 2008 または Windows Server 2008 R2 フォレストの機能レベルを上げることができます。 自動的には、ネイティブ以降から Windows Server 2008 または Windows Server 2008 R2、Windows 2000 に設定されているフォレスト内のすべてのドメインの機能レベルが発生させます。  
  
フォレストおよびドメインの機能レベルを引き上げる詳細については、およびそれらのタスクを実行するプロシージャを参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する\[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)します。  
  
## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Windows Server 2003 の Active Directory フォレストの機能レベルをアップグレードします。  
Windows Server 2003 ベースのドメイン コント ローラーのみで構成される Windows Server 2003 環境で機能レベルが既定では、次のレベルに設定し、手動で生成されるまでこれらのレベルで維持します。  
  
-   Windows 2000 ネイティブ ドメイン機能レベル  
  
-   Windows 2000 フォレストの機能レベル  
  
Windows Server 2008 または Windows Server 2008 R2 のすべてのフォレスト レベルとドメイン レベルの機能を使用するには、Windows Server 2008 または Windows Server 2008 R2 にこの Windows Server 2003 環境をアップグレードする必要があります。 このアップグレードは、次の方法のいずれかで実行できます。  
  
-   新しくインストールされた Windows Server 2008 の導入-ベースまたは Windows Server 2008 R2 のフォレストにドメイン コント ローラーをベースしし、Windows Server 2003 を実行しているすべてのドメイン コント ローラーをインベントリから削除または Windows Server 2008 または Windows Server 2008 R2 にアップグレードします。  
  
-   Windows Server 2008 または Windows Server 2008 R2 を実行するドメイン コント ローラーを Windows Server 2003 を実行している既存のすべてのドメイン コントローラのインプレース アップグレードを実行します。 詳細については、次を参照してください。[を Windows Server 2008 AD DS ドメインの Active Directory ドメインのアップグレード\[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)します。  
  
> [!IMPORTANT]  
>  Windows Server 2008 R2 では、x64 ベースのオペレーティング システムです。 サーバーで Windows Server 2003 の x64 ベースのバージョンが実行されている場合は、Windows Server 2008 R2 へのこのコンピューターのオペレーティング システムのインプレース アップグレードを正常に実行できます。 サーバーで Windows Server 2003 の x86 ベースのバージョンが実行されている場合は、Windows Server 2008 R2 を実行するには、このコンピューターをアップグレードできません。  
  
ドメイン レベルのすべての Windows Server 2008 または Windows Server 2008 R2 の機能を使用して、Windows Server 2008 または Windows Server 2008 R2、Windows Server 2003 フォレスト全体をアップグレードすることがなく、のみ、Windows Server 2008 または Windows のドメイン機能レベルを上げるサーバー 2008 R2。  
  
> [!NOTE]  
> ドメインの機能レベルを上げると、前に、Windows Server 2008 または Windows Server 2008 R2 にそのドメイン内のすべての Windows Server 2003 ベースのドメイン コント ローラーをアップグレードする必要があります。  
  
Windows Server 2008 または Windows Server 2008 R2 に、フォレスト内のすべての Windows Server 2003 ベースのドメイン コント ローラーをアップグレードした後から Windows Server 2008 または Windows Server 2008 R2 フォレストの機能レベルを上げることができます。 自動的に Windows Server 2008 または Windows Server 2008 R2、Windows Server 2003 に設定されているフォレスト内のすべてのドメインの機能レベルを発生させます。  
  
フォレストおよびドメインの機能レベルを引き上げる詳細については、およびそれらのタスクを実行するプロシージャを参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する\[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)します。  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>新しい Windows Server 2008 フォレスト機能レベルをアップグレードします。  
新しい Windows Server 2008 フォレストの最初のドメイン コント ローラーをインストールするときの機能レベルは既定では、次のレベルに設定し、手動で生成されるまでこれらのレベルで維持します。  
  
-   Windows 2000 ネイティブ ドメイン機能レベル  
  
-   Windows 2000 フォレストの機能レベル  
  
機能レベルは、新しい Windows Server 2008 フォレストに Windows 2000 または Windows Server 2003 ベースのドメイン コント ローラーを追加するオプションが提供するこれらの既定のレベルで設定されます。 フォレスト ルート ドメインを作成すると、Windows Server 2008 フォレストに追加する各ドメインのドメインの機能レベルに設定されます Windows 2000 ネイティブです。 ただし、Windows Server 2008 を実行する新しい Windows Server 2008 環境ですべてのドメイン コント ローラーをする場合、フォレストの機能レベルと、ドメインの機能レベルに設定、fores に最初のドメイン コント ローラーをインストールするときに、Windows Server 2008t です。 これを行う時間を節約し、Windows Server 2008 のすべてのフォレスト レベルとドメイン レベルの機能を有効にします。  
  
> [!IMPORTANT]  
> フォレストが Windows Server 2008 の機能で動作する場合は、Active Directory、Windows Server 2003 ベースのメンバー サーバーをインストールしようレベルとするまたは Windows 2000 ベースのメンバー サーバーをインストールが失敗します。  
  
フォレストおよびドメインの機能レベルを引き上げる詳細については、およびそれらのタスクを実行するプロシージャを参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する\[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)します。  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>新しい Windows Server 2008 R2 フォレストの機能レベルをアップグレードします。  
新しい Windows Server 2008 R2 フォレストの最初のドメイン コント ローラーをインストールするときにの機能レベルは既定では、次のレベルに設定し、手動で生成されるまでこれらのレベルで維持します。  
  
-   Windows Server 2003 ドメイン機能レベル  
  
-   Windows Server 2003 フォレストの機能レベル  
  
機能レベルは、新しい Windows Server 2008 R2 フォレストに Windows Server 2003 ベースのドメイン コント ローラーの追加のオプションが提供するこれらの既定のレベルで設定されます。 フォレスト ルート ドメインを作成した後、Windows Server 2008 R2 フォレストに追加する各ドメインのドメインの機能レベルが Windows Server 2003 に設定します。 ただし、Windows Server 2008 R2 を実行する新しい Windows Server 2008 R2 環境ですべてのドメイン コント ローラーをする場合フォレストの機能レベルと設定し、ドメインの機能レベルでは、Windows Server 2008 R2 をインストールすると最初のドメイン コント ローラー yo へフォレスト。 これを行う時間を節約し、Windows Server 2008 R2 のすべてのフォレスト レベルとドメイン レベルの機能を有効にします。  
  
> [!IMPORTANT]  
> フォレストが、Windows Server 2008 R2 の機能レベルで動作し、Active Directory、Windows Server 2008 をインストールしようとしたかどうか、ベースまたは Windows Server 2003 ベースのメンバー サーバー、または Windows 2000 ベースのメンバー サーバーで、インストールが失敗しました。  
  
フォレストおよびドメインの機能レベルを引き上げる詳細については、およびそれらのタスクを実行するプロシージャを参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する\[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)します。  
  
> [!NOTE]  
> ADMT v3.1 は、Windows Server 2008 にインストールする必要があります、1 つまたは複数の Windows Server 2008 R2 ドメイン コント ローラーによってホストされているドメインにオブジェクトを移行するのに ADMT v3.1 を使用できます。 詳細については、次を参照してください。[記事 976659](https://go.microsoft.com/fwlink/?LinkId=180398)でマイクロソフト サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=180398)します。  
  


