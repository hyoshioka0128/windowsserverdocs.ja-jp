---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: "機能レベルのアップグレードを識別します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9527a186cb20c470e0b5644fff58f90786520f97
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="identifying-your-functional-level-upgrade"></a>機能レベルのアップグレードを識別します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインとフォレストの機能レベルを上げることができます、前に、現在の環境を評価し、組織のニーズに最も合った機能のレベル要件を特定する必要があります。 ドメイン、フォレスト内の各ドメイン、オペレーティング システムとサービス パック各ドメイン コント ローラーを実行している、およびドメイン コント ローラーをアップグレードする予定の日付に格納されているドメイン コント ローラーを識別することによって、現在の環境を評価します。 ドメイン コント ローラーをインベントリから削除する場合は、操作を行ってので、環境で必要がある完全への影響を理解することを確認します。  
  
次の状況できない場合があります、Windows Server 2008 または Windows Server 2008 R2 の機能レベルに以前のバージョンの Windows Server オペレーティング システムをアップグレードします。  
  
-   不足しているハードウェア  
  
-   Windows Server 2008 または Windows Server 2008 R2 と互換性がないのウイルス対策プログラムを実行するドメイン コント ローラー   
  
-   Windows Server 2008 または Windows Server 2008 R2 で実行されないバージョン固有のプログラムの使用   
  
-   最新の service pack を使用してプログラムをアップグレードする必要があります。  
  
この情報を文書化することを完全に機能の Windows Server 2008 または Windows Server 2008 R2 環境があることを確認するための手順を特定するのに役立ちます。  
  
現在の環境を評価した後、組織に適用される機能レベルのアップグレードを識別するがあります。 これらのオプションを使用できます。  
  
-   Windows Server 2008 または Windows Server 2008 R2 に Windows 2000 ネイティブ モード環境   
  
-   Windows Server 2008 または Windows Server 2008 R2 に Windows Server 2003 フォレスト   
  
-   Windows Server 2008 の新しいフォレスト  
  
-   Windows Server 2008 R2 の新しいフォレスト  
  
## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>ネイティブの Windows 2000 Active Directory フォレストでの機能レベルのアップグレード  
Windows 2000 ベースのドメイン コント ローラーののみで構成されている Windows 2000 ネイティブ環境の機能レベルは既定では、次のレベルに設定し、手動で生成されるまで、これらのレベルで残っています。  
  
-   Windows 2000 ネイティブ ドメインの機能レベル  
  
-   Windows 2000 フォレストの機能レベル  
  
Windows Server 2008 または Windows Server 2008 R2 のすべてのフォレスト レベルとドメイン レベルの機能を使用するには、Windows Server 2008 または Windows Server 2008 R2 にこの Windows 2000 環境をアップグレードする必要があります。 このアップグレードは、次の方法のいずれかで実行できます。  
  
-   新しくインストールした Windows Server 2008 の導入-ベースまたは Windows Server 2008 R2-はフォレストにドメイン コント ローラーをベースし、し、Windows 2000 を実行しているすべてのドメイン コント ローラーを削除します。  
  
-   Windows Server 2003 を実行するドメイン コント ローラーをフォレストに Windows 2000 を実行している既存のすべてのドメイン コントローラのインプレース アップグレードを実行します。 次に、これらのドメイン コント ローラーを Windows Server 2008 または Windows Server 2008 R2 のインプレース アップグレードを実行します。 詳細については、次を参照してください。[を Windows Server 2008 AD DS ドメイン \[LH\ の Active Directory ドメインのアップグレード]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)します。  
  
    > [!IMPORTANT]  
    >  Windows Server 2008 R2 は、x64 ベースのオペレーティング システムです。 サーバーが、x64 ベース バージョンの Windows Server 2003 を実行している場合は、Windows Server 2008 R2 へのこのコンピューターのオペレーティング システムのインプレース アップグレードを正常に実行できます。 サーバーが、x86 ベースのバージョンの Windows Server 2003 を実行している場合、このコンピューターを Windows Server 2008 R2 にアップグレードできません。  
  
使用するには、Windows Server 2008 または Windows Server 2008 R2 ドメイン レベルの機能を Windows Server 2008 または Windows Server 2008 R2、Windows 2000 フォレスト全体をアップグレードすることがなく、ドメイン機能レベルを Windows Server 2008 または Windows Server 2008 R2 のみを生成します。  
  
> [!NOTE]  
> ドメインの機能レベルを上げると、前に、Windows Server 2008 または Windows Server 2008 R2 にそのドメイン内のすべての Windows 2000 ベースのドメイン コント ローラーをアップグレードする必要があります。  
  
Windows Server 2008 または Windows Server 2008 R2 を実行するドメイン コント ローラーで、フォレスト内のすべての Windows 2000 ベースのドメイン コント ローラーを交換した後に、Windows Server 2008 または Windows Server 2008 R2 フォレストの機能レベルを増やすことができます。 自動的に Windows 2000 ネイティブ以上に Windows Server 2008 または Windows Server 2008 R2 に設定されているフォレスト内のすべてのドメインの機能レベルを生成します。  
  
フォレストおよびドメインの機能レベルを上げるの詳細については、これらのタスクを実行する手順については、次を参照してください。 [、Windows Server 2008 フォレスト ルート ドメイン \[LH\ を展開する]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)します。  
  
## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Windows Server 2003 の Active Directory フォレストでの機能レベルのアップグレード  
Windows Server 2003 ベースのドメイン コント ローラーのみで構成される、Windows Server 2003 環境の機能レベルは既定では、次のレベルに設定し、手動で生成されるまで、これらのレベルで残っています。  
  
-   Windows 2000 ネイティブ ドメインの機能レベル  
  
-   Windows 2000 フォレストの機能レベル  
  
Windows Server 2008 または Windows Server 2008 R2 のすべてのフォレスト レベルとドメイン レベルの機能を使用するには、Windows Server 2008 または Windows Server 2008 R2 にこの Windows Server 2003 環境をアップグレードする必要があります。 このアップグレードは、次の方法のいずれかで実行できます。  
  
-   新たにインストールされた Windows Server 2008 の導入-ベースのまたは Windows Server 2008 R2 ではフォレストにドメイン コント ローラーをベースしし、Windows Server 2003 を実行しているすべてのドメイン コント ローラーをインベントリから削除または Windows Server 2008 または Windows Server 2008 R2 にアップグレードします。  
  
-   Windows Server 2008 または Windows Server 2008 R2 を実行するドメイン コント ローラーを Windows Server 2003 を実行している既存のすべてのドメイン コントローラのインプレース アップグレードを実行します。 詳細については、次を参照してください。[を Windows Server 2008 AD DS ドメイン \[LH\ の Active Directory ドメインのアップグレード]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)します。  
  
> [!IMPORTANT]  
>  Windows Server 2008 R2 は、x64 ベースのオペレーティング システムです。 サーバーが、x64 ベース バージョンの Windows Server 2003 を実行している場合は、Windows Server 2008 R2 へのこのコンピューターのオペレーティング システムのインプレース アップグレードを正常に実行できます。 サーバーが、x86 ベースのバージョンの Windows Server 2003 を実行して、Windows Server 2008 R2 を実行するには、このコンピューターをアップグレードすることはできません。  
  
機能を使用するすべての Windows Server 2008 または Windows Server 2008 R2 ドメイン レベルを Windows Server 2008 または Windows Server 2008 R2、Windows Server 2003 フォレスト全体をアップグレードすることがなく、ドメイン機能レベルを Windows Server 2008 または Windows Server 2008 R2 のみを生成します。  
  
> [!NOTE]  
> ドメインの機能レベルを上げると、前に、Windows Server 2008 または Windows Server 2008 R2 にそのドメイン内のすべての Windows Server 2003 ベースのドメイン コント ローラーをアップグレードする必要があります。  
  
フォレスト内のすべての Windows Server 2003 ベースのドメイン コント ローラーを Windows Server 2008 または Windows Server 2008 R2 にアップグレードした後は、Windows Server 2008 または Windows Server 2008 R2 フォレストの機能レベルを増やすことができます。 自動的に Windows Server 2008 または Windows Server 2008 R2、Windows Server 2003 に設定されているフォレスト内のすべてのドメインの機能レベルを生成します。  
  
フォレストおよびドメインの機能レベルを上げるの詳細については、これらのタスクを実行する手順については、次を参照してください。 [、Windows Server 2008 フォレスト ルート ドメイン \[LH\ を展開する]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)します。  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>新しい Windows Server 2008 フォレストでの機能レベルのアップグレード  
新しい Windows Server 2008 フォレストの最初のドメイン コント ローラーをインストールするときの機能レベルは既定では、次のレベルに設定し、手動で生成されるまでこれらのレベルで維持します。  
  
-   Windows 2000 ネイティブ ドメインの機能レベル  
  
-   Windows 2000 フォレストの機能レベル  
  
機能レベルは、Windows 2000 または Windows Server 2003 ベースのドメイン コント ローラーを新しい Windows Server 2008 フォレストに追加するオプションを提供するこれらの既定のレベルに設定されます。 フォレスト ルート ドメインを作成した後、Windows Server 2008 フォレストに追加する各ドメインのドメインの機能レベルは設定を Windows 2000 ネイティブされます。 ただし、する場合はすべてのドメイン コント ローラーを Windows Server 2008 を実行する新しい Windows Server 2008 環境で、設定、フォレストの機能レベルし、ドメインの機能レベルを Windows Server 2008、フォレスト内の最初のドメイン コント ローラーをインストールするときにします。 これを行うと、時間を節約し、Windows Server 2008 のすべてのフォレスト レベルとドメイン レベルの機能を有効にします。  
  
> [!IMPORTANT]  
> フォレストは、Windows Server 2008 の機能で機能します。 場合は、Active Directory、Windows Server 2003 ベースのメンバー サーバーをインストールしようレベルとするか、Windows 2000 ベース メンバー サーバーで、インストールは失敗します。  
  
フォレストおよびドメインの機能レベルを上げるの詳細については、これらのタスクを実行する手順については、次を参照してください。 [、Windows Server 2008 フォレスト ルート ドメイン \[LH\ を展開する]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)します。  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>新しい Windows Server 2008 R2 フォレストの機能レベルのアップグレード  
新しい Windows Server 2008 R2 フォレストの最初のドメイン コント ローラーをインストールするときの機能レベルは既定では、次のレベルに設定し、手動で生成されるまでこれらのレベルで維持します。  
  
-   Windows Server 2003 ドメインの機能レベル  
  
-   Windows Server 2003 フォレストの機能レベル  
  
機能レベルは、新しい Windows Server 2008 R2 フォレストに Windows Server 2003 ベースのドメイン コント ローラーを追加するオプションを提供するこれらの既定のレベルに設定されます。 フォレスト ルート ドメインを作成した後、Windows Server 2008 R2 フォレストに追加する各ドメインのドメインの機能レベルが Windows Server 2003 に設定します。 ただし、する場合はすべてのドメイン コント ローラーを Windows Server 2008 R2 を実行する新しい Windows Server 2008 R2 環境で、フォレストの機能レベルと、ドメインの機能レベルに設定、フォレスト内の最初のドメイン コント ローラーをインストールするときに、Windows Server 2008 R2。 これを行うと、時間を節約し、Windows Server 2008 R2 でのすべてのフォレスト レベルとドメイン レベル機能を有効にします。  
  
> [!IMPORTANT]  
> フォレストは、Windows Server 2008 R2 の機能レベルで機能します。 場合、Windows Server 2008 で Active Directory をインストールしようとして -ベースまたは Windows Server 2003 ベースのメンバー サーバーまたは Windows 2000 ベースのメンバー サーバーで、インストールは失敗します。  
  
フォレストおよびドメインの機能レベルを上げるの詳細については、これらのタスクを実行する手順については、次を参照してください。 [、Windows Server 2008 フォレスト ルート ドメイン \[LH\ を展開する]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)します。  
  
> [!NOTE]  
> Windows Server 2008 には、ADMT v3.1 をインストールする必要があります、ADMT v3.1 を使用してオブジェクトを移行する 1 つまたは複数の Windows Server 2008 R2 ドメイン コント ローラーによってホストされているドメインにことができます。 詳細については、次を参照してください。[記事 976659](https://go.microsoft.com/fwlink/?LinkId=180398)で、Microsoft サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=180398)。  
  


