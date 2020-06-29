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
ms.openlocfilehash: b4addd18629bd54cd9d5fc2df5c660c621e735de
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473789"
---
# <a name="choose-a-namespace-type"></a>名前空間の種類を選択する

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間を作成するとき、2 種類 (スタンドアロン名前空間またはドメイン ベース名前空間) の名前空間のいずれかを選択する必要があります。 加えて、ドメイン ベースの名前空間を選択した場合、名前空間モード (Windows 2000 Server モードまたは Windows Server 2008 モード) を選択する必要があります。

## <a name="choosing-a-namespace-type"></a>名前空間の種類を選択する

次の条件のいずれかが環境に当てはまる場合、スタンドアロンの名前空間を選択します。

-   組織で Active Directory Domain Services (AD DS) を使用していない。
-   フェールオーバー クラスターを使うことで名前空間の可用性を高めたいと思っている。
-   このトピックの後方で説明するように、ドメイン ベースの名前空間 (Windows Server 2008 モード) の要件を満たしていないドメインで、DFS フォルダーが 5,000 を超える単一の名前空間を作成する必要があります。

> [!NOTE]
> 名前空間のサイズを確認するには、DFS 管理コンソールで名前空間を右クリックして、**[プロパティ]** をクリックし、**[名前空間のプロパティ]** ダイアログ ボックスで名前空間サイズを表示します。 DFS 名前空間のスケーラビリティについて詳しくは、Microsoft Web サイトの[ファイル サービス](https://technet.microsoft.com/library/cc771548.aspx)に関するページをご覧ください。

次の条件のいずれかが環境に当てはまる場合、ドメイン ベースの名前空間を選択します。

-   複数の名前空間サーバーを使うことで名前空間の可用性を確保したいと思っている。
-   ユーザーから名前空間サーバーの名前を非表示にしたいと思っている。 これにより、名前空間サーバーを置き換えたり、別のサーバーに名前空間を移行したりしやすくなります。

## <a name="choosing-a-domain-based-namespace-mode"></a>ドメイン ベースの名前空間モードを選択する

ドメイン ベースの名前空間を選択した場合、Windows 2000 Server モードまたは Windows Server 2008 モードを使うかどうかを選択する必要があります。 Windows Server 2008 モードには、アクセス ベースの列挙とスケーラビリティの向上のサポートが含まれています。 Windows 2000 Server で導入されたドメイン ベースの名前空間は、"ドメイン ベースの名前空間 (Windows 2000 Server モード)" と呼ばれます。

Windows Server 2008 モードを使うには、ドメインと名前空間は次の最小要件を満たす必要があります。

-   フォレストは、Windows Server 2003 以上のフォレスト機能レベルを使います。
-   ドメインは Windows Server 2008 以上のドメイン機能レベルを使います。
-   すべての名前空間サーバーは、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 を実行しています。

環境でサポートされている場合は、新しいドメイン ベースの名前空間を作成するときに Windows Server 2008 モードを選択します。 このモードでは、新しい機能が追加されており、スケーラビリティも向上しています。さらに、名前空間を Windows 2000 Server モードから移行する手間も省けます。

Windows Server 2008 モードへの名前空間の移行については、「[ドメイン ベースの名前空間を Windows Server 2008 モードに移行する](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)」をご覧ください。

お使いの環境で Windows Server 2008 モードのドメイン ベースの名前空間がサポートされていない場合、名前空間に既存の Windows 2000 Server モードを使います。

## <a name="comparing-namespace-types-and-modes"></a>名前空間の種類とモードの比較

名前空間の各種類とモードの特性については、次の表で説明します。

|特徴|スタンドアロンの名前空間|ドメイン ベースの名前空間 (Windows 2000 Server モード) |ドメイン ベースの名前空間 (Windows Server 2008 モード) |
|---|---|---|---|
|名前空間へのパス|\\\ *ServerName\RootName* |\\\ *NetBIOSDomainName\RootName* <br />\\\ *DNSDomainName\RootName*|\\\ *NetBIOSDomainName\RootName* <br /> \\\ *DNSDomainName\RootName*|
|名前空間情報の格納場所|名前空間サーバー上のレジストリおよびメモリ キャッシュ|各名前空間サーバー上の AD DS およびメモリ キャッシュ|各名前空間サーバー上の AD DS およびメモリ キャッシュ|
|名前空間のサイズの推奨事項|名前空間には、ターゲットを持つフォルダーを 5,000 以上含めることができます。ターゲットを持つフォルダーの推奨される上限は 50,000 です|AD DS の名前空間オブジェクトのサイズは、Windows Server 2008 を実行していないドメイン コントローラーとの互換性を維持するため、5 メガバイト (MB) 未満にする必要があります。 これは、ターゲットを持つフォルダーがおよそ 5,000 個未満であることを意味します。|名前空間には、ターゲットを持つフォルダーを 5,000 以上含めることができます。ターゲットを持つフォルダーの推奨される上限は 50,000 です |
|最小 AD DS フォレスト機能レベル|AD DS は必須ではありません|Windows 2000|Windows Server 2003|
|最小 AD DS ドメイン機能レベル|AD DS は必須ではありません|Windows 2000 混在|Windows Server 2008|
|サポートされている最小名前空間サーバー|Windows 2000 Server|Windows 2000 Server|Windows Server 2008|
|アクセス ベースの列挙 (有効な場合) のサポート|○ (Windows Server 2008 名前空間サーバーが必要)|いいえ|はい|
|名前空間の可用性を確保するためのサポートされる方法|フェールオーバー クラスターにスタンドアロン名前空間を作成します。|複数の名前空間サーバーを使って名前空間をホストします。 (名前空間サーバーは同じドメイン内にある必要があります)。|複数の名前空間サーバーを使って名前空間をホストします。 (名前空間サーバーは同じドメイン内にある必要があります)。|
|DFS レプリケーションを使ったフォルダー ターゲットのレプリケートのサポート|AD DS ドメインに参加しているときにサポート対象|サポートされています|サポートされています|

## <a name="additional-references"></a>その他のリファレンス

-   [DFS 名前空間を展開する](deploying-dfs-namespaces.md)
-   [ドメインベースの名前空間を Windows Server 2008 モードに移行する](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)


