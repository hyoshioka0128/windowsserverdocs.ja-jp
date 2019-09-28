---
title: 名前空間の種類を選択する
description: この記事では、名前空間の種類を選択する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: becaab1b4c35492200ad3d75d5f31829d85e10f8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402194"
---
# <a name="choose-a-namespace-type"></a>名前空間の種類を選択する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間を作成するとき、2 種類 (スタンドアロン名前空間またはドメイン ベース名前空間) の名前空間のいずれかを選択する必要があります。 また、ドメインベースの名前空間を選択する場合は、名前空間モードを選択する必要があります。Windows 2000 サーバーモードまたは Windows Server 2008 モード。

## <a name="choosing-a-namespace-type"></a>名前空間の種類を選択する

次の条件のいずれかが環境に当てはまる場合、スタンドアロンの名前空間を選択します。

-   組織は Active Directory Domain Services (AD DS) を使用していません。
-   フェールオーバー クラスターを使うことで名前空間の可用性を高めたいと思っている。
-   このトピックで後述するように、ドメインベースの名前空間 (Windows Server 2008 モード) の要件を満たしていないドメインに、5000を超える DFS フォルダーを含む1つの名前空間を作成する必要があります。

> [!NOTE]
> 名前空間のサイズを確認するには、DFS 管理コンソールで名前空間を右クリックして、 **[プロパティ]** をクリックし、 **[名前空間のプロパティ]** ダイアログ ボックスで名前空間サイズを表示します。 DFS 名前空間のスケーラビリティについて詳しくは、Microsoft Web サイトの[ファイル サービス](https://technet.microsoft.com/library/cc771548.aspx)に関するページをご覧ください。

次の条件のいずれかが環境に当てはまる場合、ドメイン ベースの名前空間を選択します。

-   複数の名前空間サーバーを使うことで名前空間の可用性を確保したいと思っている。
-   ユーザーから名前空間サーバーの名前を非表示にしたいと思っている。 これにより、名前空間サーバーを置き換えたり、別のサーバーに名前空間を移行したりしやすくなります。

## <a name="choosing-a-domain-based-namespace-mode"></a>ドメイン ベースの名前空間モードを選択する

ドメインベースの名前空間を選択する場合は、Windows 2000 サーバーモードと Windows Server 2008 モードのどちらを使用するかを選択する必要があります。 Windows Server 2008 モードでは、アクセスベースの列挙とスケーラビリティの向上がサポートされています。 Windows 2000 Server で導入されたドメインベースの名前空間は、"ドメインベースの名前空間 (Windows 2000 サーバーモード)" と呼ばれるようになりました。

Windows Server 2008 モードを使用するには、ドメインと名前空間が次の最小要件を満たしている必要があります。

-   フォレストは、Windows Server 2003 以上のフォレスト機能レベルを使います。
-   ドメインは、Windows Server 2008 以上のドメイン機能レベルを使用しています。
-   すべての名前空間サーバーでは、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 が実行されています。

環境でサポートされている場合は、新しいドメインベースの名前空間を作成するときに、Windows Server 2008 モードを選択します。 このモードでは、追加の機能とスケーラビリティが提供されます。また、Windows 2000 サーバーモードから名前空間を移行することもできなくなります。

名前空間を Windows Server 2008 モードに移行する方法の詳細については、「[ドメインベースの名前空間を Windows server 2008 モードに移行](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)する」を参照してください。

環境で Windows Server 2008 モードのドメインベースの名前空間がサポートされていない場合は、名前空間に対して既存の Windows 2000 サーバーモードを使用します。

## <a name="comparing-namespace-types-and-modes"></a>名前空間の種類とモードの比較

名前空間の各種類とモードの特性については、次の表で説明します。

|特性|スタンドアロンの名前空間|ドメイン ベースの名前空間 (Windows 2000 Server モード) |ドメイン ベースの名前空間 (Windows Server 2008 モード) | 
|---|---|---|---|
|名前空間へのパス|\\ @ no__t-1*ServerName\RootName* |\\ @ no__t-1*NetBIOSDomainName\RootName* <br />\\ @ no__t-1*DNSDomainName\RootName*|\\ @ no__t-1*NetBIOSDomainName\RootName* <br /> \\ @ no__t-1*DNSDomainName\RootName*|
|名前空間情報の格納場所|名前空間サーバー上のレジストリおよびメモリ キャッシュ|各名前空間サーバー上の AD DS およびメモリ キャッシュ|各名前空間サーバー上の AD DS およびメモリ キャッシュ|
|名前空間のサイズの推奨事項|名前空間には、ターゲットを持つフォルダーを 5,000 以上含めることができます。ターゲットを持つフォルダーの推奨される上限は 50,000 です|AD DS の名前空間オブジェクトのサイズは、Windows Server 2008 を実行していないドメイン コントローラーとの互換性を維持するため、5 メガバイト (MB) 未満にする必要があります。 これは、ターゲットを持つフォルダーがおよそ 5,000 個未満であることを意味します。|名前空間には、ターゲットを持つフォルダーを 5,000 以上含めることができます。ターゲットを持つフォルダーの推奨される上限は 50,000 です |
|最小 AD DS フォレスト機能レベル|AD DS は必須ではありません|Windows 2000|Windows Server 2003|
|最小 AD DS ドメイン機能レベル|AD DS は必須ではありません|Windows 2000 混在|Windows Server 2008|
|サポートされている最小名前空間サーバー|Windows 2000 Server|Windows 2000 Server|Windows Server 2008|
|アクセス ベースの列挙 (有効な場合) のサポート|○ (Windows Server 2008 名前空間サーバーが必要)|いいえ|はい|
|名前空間の可用性を確保するためのサポートされる方法|フェールオーバー クラスターにスタンドアロン名前空間を作成します。|複数の名前空間サーバーを使って名前空間をホストします。 (名前空間サーバーは同じドメイン内にある必要があります)。|複数の名前空間サーバーを使って名前空間をホストします。 (名前空間サーバーは同じドメイン内にある必要があります)。|
|DFS レプリケーションを使ったフォルダー ターゲットのレプリケートのサポート|AD DS ドメインに参加しているときにサポート対象|Supported|Supported|

## <a name="see-also"></a>関連項目

-   [DFS 名前空間を展開する](deploying-dfs-namespaces.md)
-   [ドメインベースの名前空間を Windows Server 2008 モードに移行する](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)


