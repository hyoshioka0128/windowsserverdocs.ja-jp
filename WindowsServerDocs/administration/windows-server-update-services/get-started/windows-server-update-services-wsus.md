---
title: Windows Server Update Services (WSUS) の概要します。
description: Windows Server Update Service (WSUS) のトピックで、サーバーの役割とその実際のアプリケーションの概要
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09ec5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 5/22/2017
ms.openlocfilehash: 7a6c64e0a4321553162b426e3d6857ff6ac3581c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830263"
---
# <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server Update Services (WSUS) を使用すると、IT 管理者は Microsoft 製品の最新の更新プログラムを展開できます。 WSUS を使用すると、ネットワーク上のコンピューターに Microsoft Update を通じてリリースされる更新プログラムの配布を完全に管理します。 このトピックでは、このサーバーの役割の概要に加え、WSUS を展開および保守する方法の詳細について説明します。

## <a name="wsus-server-role-description"></a>WSUS サーバー ロールの説明
WSUS サーバーでは、管理コンソールから更新プログラムの配布の管理に使用できる機能を提供します。 WSUS サーバーには、組織内で他の WSUS サーバーの更新ソースことができます。 更新プログラムの供給元として機能する WSUS サーバーは、"アップストリーム サーバー" と呼ばれます。 WSUS 実装では、ネットワーク上の少なくとも 1 つの WSUS サーバーは、利用可能な更新情報を取得する Microsoft Update に接続できる必要があります。 管理者は、指定できます - ネットワーク セキュリティと構成 - に基づくその他の WSUS サーバーの数に直接接続 Microsoft Update。

### <a name="practical-applications"></a>実際の適用例
更新プログラムの管理は、中間リリース版のソフトウェアの展開と保守を運用環境の中で管理していくプロセスであり、 作業効率の管理、セキュリティ上の脆弱性の解消、運用環境の安定性維持に役立ちます。 組織のオペレーティング システムやアプリケーション内で周知された信頼性を特定したり保持できない場合は、悪用されると収益や知的財産権の損失につながりかねないセキュリティ上の脆弱性を多くはらんでいる可能性があります。 このような脅威を最小限に抑えるには、システムが正しく構成されていること、最新ソフトウェアを使用すること、および推奨されているソフトウェア更新プログラムをインストールすることが必要です。

WSUS がビジネスに価値を負荷する主なシナリオは次のとおりです。

-   更新プログラム管理の一元化

-   更新プログラム管理の自動化

### <a name="new-and-changed-functionality"></a>新機能と変更された機能

> [!NOTE]
> Windows Server 2012 R2 への WSUS 3.2 をサポートする Windows Server のバージョンからのアップグレードでは、まず WSUS 3.2 をアンインストールする必要があります。
> 
> Windows Server 2012 で WSUS 3.2 がインストールされている Windows Server の任意のバージョンからのアップグレードがブロック インストール プロセス中に WSUS 3.2 が検出されます。 その場合は、まず、サーバーをアップグレードする前に Windows Server Update Services をアンインストールするように求められます。
> 
> ただし、このリリースの Windows Server および Windows Server 2012 R2、Windows Server と WSUS 3.2 のすべてのバージョンからアップグレードする場合が変更されたのため、インストールはブロックされません。 Windows Server 2012 R2 のアップグレードを実行する前に WSUS 3.2 をアンインストールできなかった場合により投稿 WSUS のインストールのタスクが失敗する Windows Server 2012 R2 でされます。 この場合、唯一の既知是正メジャーは、ハード ドライブをフォーマットして、Windows Server を再インストールは。

Windows Server Update Services は組み込みのサーバーの役割で、次のような機能強化が行われています。

-   サーバー マネージャーを使用して追加および削除できます。

-   WSUS で最も重要な管理タスクを管理する Windows PowerShell コマンドレットが含まれています

-   セキュリティ強化のための SHA256 ハッシュ機能が追加されています。

-   クライアントとサーバーの分離を提供します Windows Update エージェント (WUA) のバージョンが WSUS に関係なく出荷できる。

### <a name="using-windows-powershell-to-manage-wsus"></a>Windows PowerShell を使用した WSUS の管理
操作を自動化するシステム管理者は、コマンド ラインの自動化への対応が必要です。 主な目的は、システム管理者が日常的な操作を自動化できるようにすることで、WSUS 管理を容易にすることです。

**この変更の利点**

システム管理者は、Windows PowerShell を使って主な WSUS 操作を公開することで、生産性を向上したり、新しいツールを習得するまでの時間を短縮したりできます。また、同様の操作において一貫性がないことが原因で発生する思い違いによるエラーを低減させることもできます。

**動作の相違点**

以前のバージョンの Windows Server オペレーティング システムでは、Windows PowerShell コマンドレットがなかったため、更新プログラムの管理の自動化は困難でした。 WSUS 操作用の Windows PowerShell コマンドレットにより、システム管理者に柔軟性と迅速さが加わりました。

## <a name="in-this-collection"></a>このコレクションに
計画するため、次のガイド、展開、および WSUS の管理は、このコレクションには。

-   [Windows Server Update Services をデプロイします。](../deploy/deploy-windows-server-update-services.md)

-   [Windows Server Update Services を使用して更新プログラムを管理します。](../manage/update-management-with-windows-server-update-services.md)


