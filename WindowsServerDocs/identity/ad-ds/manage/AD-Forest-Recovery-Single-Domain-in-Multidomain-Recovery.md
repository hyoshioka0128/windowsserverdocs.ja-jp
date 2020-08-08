---
title: AD フォレストの回復-マルチドメインフォレスト内の単一ドメインの回復
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.openlocfilehash: 60f965c90fd8b383689f1b7d0a55bd365c07ee01
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953199"
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>AD フォレストの回復-マルチドメインフォレスト内の単一ドメインの回復

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

フォレストの完全復旧ではなく、複数のドメインを持つフォレスト内の単一ドメインのみを回復する必要がある場合があります。 このトピックでは、単一ドメインを回復するための考慮事項について説明します。

単一ドメインの回復には、グローバルカタログ (GC) サーバーを再構築するための固有の課題があります。 たとえば、ドメインの最初のドメインコントローラー (DC) が1週間前に作成されたバックアップから復元された場合、フォレスト内の他のすべての Gc は、復元された DC よりもそのドメインの最新のデータを保持します。 GC データの一貫性を再確立するには、いくつかのオプションがあります。

- 回復されたドメイン内のパーティションを除き、再ホストを解除してから、回復したドメインパーティションをフォレスト内のすべての Gc から同時に再ホストします。
- フォレストの回復プロセスに従ってドメインを回復し、他のドメインの Gc から残留オブジェクトを削除します。

以下のセクションでは、各オプションに関する一般的な考慮事項について説明します。 回復に必要な手順の完全なセットは、Active Directory 環境によって異なります。

## <a name="rehost-all-gcs"></a>すべての Gc を再ホスト

> [!WARNING]
> すべてのドメインのドメイン管理者アカウントのパスワードは、問題が発生した場合に使用できるように準備しておく必要があります。

すべての Gc の再ホストは、repadmin/unhost コマンドと repadmin/rehost コマンド (repadmin/experthelp の一部) を使用して行うことができます。 Repadmin コマンドは、復旧されていない各ドメインのすべての GC で実行します。 すべての Gc が復旧したドメインのコピーを保持していないことを確認する必要があります。 これを実現するには、最初に、フォレストのすべての回復されていないドメインのすべてのドメインコントローラーからドメインパーティションをまずホストしないようにします。 すべての Gc にパーティションが含まれなくなると、パーティションを再ホストできます。 再ホストする場合は、フォレストのサイトとレプリケーション構造を検討してください。たとえば、サイトの他の Dc を再ホストする前に、サイトごとに1つの DC の再ホストを完了します。

このオプションは、ドメインごとに少数のドメインコントローラーを持つ小規模な組織にとって有利です。 すべての Gc は、金曜日の夜に再構築できます。必要に応じて、すべての読み取り専用ドメインパーティションについて、月曜日の朝前に完全なレプリケーションを完了できます。 しかし、世界中のサイトをカバーする大規模なドメインを回復する必要がある場合は、他のドメインのすべての Gc で読み取り専用ドメインパーティションを再ホストすると、操作に大きな影響を与え、ダウンタイムが生じる可能性があります。

## <a name="remove-lingering-objects"></a>残留オブジェクトの削除

フォレストの回復プロセスと同様に、回復する必要があるドメインのバックアップから1つの DC を復元し、残りの Dc のメタデータのクリーンアップを実行してから、AD DS を再インストールしてドメインを構築します。 フォレスト内の他のすべてのドメインの Gc で、回復されたドメインの読み取り専用パーティションの残留オブジェクトを削除します。

残留オブジェクトのクリーンアップのソースは、復旧されたドメインの DC である必要があります。 ソース DC にドメインパーティションの残留オブジェクトがないことを確認するには、グローバルカタログが GC であれば削除できます。

残留オブジェクトの削除は、他のオプションに関連するダウンタイムのリスクがない大規模な組織にとっては便利です。

詳細については、「 [Repadmin を使用して残留オブジェクトを削除する](/previous-versions/windows/it-pro/windows-server-2003/cc785298(v=ws.10))」を参照してください。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)
- [AD フォレストの回復-カスタムフォレストの復旧計画の作成](AD-Forest-Recovery-Devising-a-Plan.md)
- [AD フォレストの回復-問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復-回復方法を決定する](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復-最初の回復を実行する](AD-Forest-Recovery-Perform-initial-recovery.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
- [AD フォレストの回復-よく寄せられる質問](AD-Forest-Recovery-FAQ.md)
- [AD フォレストの回復-マルチドメインフォレスト内の単一ドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [AD フォレストの回復-Windows Server 2003 ドメインコントローラーを使用したフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)
