---
title: を使用してファイルサーバーをクラウドと同期する Azure File Sync
description: Azure File Sync を使用すると、オンプレミスのファイルサーバーの柔軟性、パフォーマンス、および互換性を維持しながら、Azure で組織のファイル共有を一元化できます。 Azure File Sync は、Windows Server を、オプションのクラウドの階層化機能を使用して、Azure ファイル共有の高速キャッシュに変換します。
ms.technology: manage
ms.topic: article
author: fauhse
ms.author: fauhse
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: fe0e3337962b7d9c2f025a9d4eba826f3349c1f9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357377"
---
# <a name="sync-your-file-server-with-the-cloud-by-using-azure-file-sync"></a>を使用してファイルサーバーをクラウドと同期する Azure File Sync

>適用対象:Windows Admin Center、Windows Admin Center Preview

Azure File Sync を使用すると、オンプレミスのファイルサーバーの柔軟性、パフォーマンス、および互換性を維持しながら、Azure で組織のファイル共有を一元化できます。 Azure File Sync は、Windows Server を、オプションのクラウドの階層化機能を使用して、Azure ファイル共有の高速キャッシュに変換します。 Windows Server で使用できる任意のプロトコルを使用して、ローカル (SMB、NFS、FTPS など) にデータにアクセスできます。

ファイルがクラウドに同期されたら、同じ Azure ファイル共有に複数のサーバーを接続して、コンテンツをローカルに同期してキャッシュすることができます。アクセス許可 (Acl) も常に転送されます。 Azure Files には、Azure ファイル共有の差分スナップショットを生成できるスナップショット機能が用意されています。 これらのスナップショットは、参照と復元を容易にするために、SMB 経由で読み取り専用ネットワークドライブとしてマウントすることもできます。 クラウドの階層化と組み合わせることで、オンプレミスのファイルサーバーを簡単に実行できるようになりました。

詳細については、「 [Planning for a Azure File Sync deployment](https://aka.ms/afs)」を参照してください。