---
title: "ソフトウェアの制限のポリシー"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c0befad-07c3-4262-b418-372d01850305
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: ab44013b947d33adc12c54b527415bf16c46a4c6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="software-restriction-policies"></a>ソフトウェアの制限のポリシー

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

IT プロフェッショナル向けのこのトピックでは、Windows Server 2012 および Windows 8 では、ソフトウェア制限ポリシー (SRP) を説明し、Windows Server 2003 以降の SRP に関する技術情報へのリンクを示します。

手順とトラブルシューティングのヒントについては、次を参照してください。[ソフトウェア制限ポリシーの管理](administer-software-restriction-policies.md)と[ソフトウェア制限ポリシーのトラブルシューティングを行う](troubleshoot-software-restriction-policies.md)します。

## <a name="BKMK_OVER"></a>ソフトウェアの制限のポリシーの説明
ソフトウェア制限ポリシー (SRP) は、ドメイン内のコンピューターで実行されているソフトウェア プログラムを指定し、これらのプログラムを実行する機能を制御する、グループ ポリシー ベースの機能です。 ソフトウェアの制限のポリシーは、Microsoft のセキュリティと信頼性、整合性、および自分のコンピューターの管理容易性を強化する企業をサポートする管理戦略の一部です。

ソフトウェアの制限のポリシーを使用して、厳しく制限されているしたアプリケーションに限って実行を許可する、コンピューターの構成を作成することができます。 ソフトウェアの制限のポリシーは、Microsoft Active Directory とグループ ポリシーに統合されています。 スタンドアロン コンピューター上でソフトウェアの制限のポリシーを作成することもできます。 ソフトウェアの制限のポリシーは、信頼ポリシーは、スクリプトとその他のコードの実行を完全に信頼されていないことを制限する管理者によって設定する規則です。

Microsoft 管理コンソール (MMC) には、ローカル グループ ポリシー エディターまたはローカル セキュリティ ポリシー スナップインのソフトウェアの制限のポリシーの拡張機能によってこれらのポリシーを定義できます。

SRP の詳細については、次を参照してください。、[ソフトウェア制限ポリシーの技術概要](software-restriction-policies-technical-overview.md)します。

## <a name="BKMK_APP"></a>実際の適用
管理者は、次のタスクをソフトウェアの制限のポリシーを使用できます。

-   信頼されたコードを定義します。

-   スクリプト、実行可能ファイル、および ActiveX コントロールを制御する柔軟性のあるグループ ポリシーの設計します。

オペレーティング システムやソフトウェアの制限のポリシーに準拠しているアプリケーション (スクリプト アプリケーションなど) によって、ソフトウェアの制限のポリシーが適用されます。

具体的には、管理者は、次の目的でソフトウェアの制限のポリシーを使用できます。

-   必要のあるソフトウェア (実行可能ファイル) がクライアントで実行できるかを指定します。

-   ユーザーが共有コンピューター上の特定のプログラムを実行していることを防ぐ

-   クライアントに信頼された発行元を追加できるユーザーを指定します。

-   (ポリシーがすべてのユーザーに影響するかどうか、またはクライアント上のユーザーのサブセットを指定)、ソフトウェアの制限のポリシーのスコープを設定します。

-   実行可能ファイルがローカル コンピューター、組織単位 (OU)、サイト、またはドメインで実行できないようにします。 悪意のあるユーザーと潜在的な問題を解決するソフトウェアの制限のポリシーを使用していないときの場合は適切になります。

## <a name="BKMK_NEW"></a>新機能と変更された機能
ソフトウェアの制限のポリシーの機能の変更はありません。

## <a name="BKMK_DEP"></a>削除されたまたは推奨されなくなった機能
ソフトウェアの制限のポリシーの削除されたまたは推奨されなくなった機能はありません。

## <a name="BKMK_SOFT"></a>ソフトウェアの要件
ソフトウェアの制限のポリシーの拡張機能には、ローカル グループ ポリシー エディターは、MMC からアクセスできます。

次の機能を作成し、ローカル コンピューター上のソフトウェアの制限のポリシーの管理が必要です。

-   ローカル グループ ポリシー エディター

-   Windows インストーラー

-   Authenticode および WinVerifyTrust

上記の一覧だけでなく、これらのポリシーのドメインに展開の設計を呼び出す場合は、次の機能が必要です。

-   Active Directory ドメイン サービス

-   グループ ポリシー

## <a name="BKMK_INSTALL"></a>サーバー マネージャー情報
ソフトウェア制限ポリシーは、ローカル グループ ポリシー エディターの拡張機能し、サーバー マネージャー、追加の役割および機能を介してがインストールされていません。

## <a name="BKMK_LINKS"></a>参照してください。
次の表と SRP の使用方法について関連するリソースへのリンクを提供します。

|コンテンツの種類|参照|
|--------|-------|
|**製品評価**|[ソフトウェアの制限のポリシーによるアプリケーションのロックダウン](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|
|**計画**|[ソフトウェア制限ポリシーの技術概要](software-restriction-policies-technical-overview.md)(Windows Server 2012)<br /><br />[ソフトウェア制限ポリシーのテクニカル リファレンス](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx)(Windows Server 2003)|
|**展開**|リソースはありません。|
|**操作**|[ソフトウェアの制限のポリシーを管理](administer-software-restriction-policies.md)(Windows Server 2012)<br /><br />[ソフトウェア制限ポリシーの製品ヘルプ](https://technet.microsoft.com/library/cc779607(v=WS.10).aspx)(Windows Server 2003)|
|**トラブルシューティング**|[ソフトウェアの制限のポリシーのトラブルシューティングを行う](troubleshoot-software-restriction-policies.md)(Windows Server 2012)<br /><br />[ソフトウェアの制限のポリシーのトラブルシューティング](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx)(Windows Server 2003)|
|**セキュリティ**|[ソフトウェアの制限のポリシーの脅威と対策](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx)(Windows Server 2008)<br /><br />[ソフトウェアの制限のポリシーの脅威と対策](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx)(Windows Server 2008 R2)|
|**ツールと設定**|[ソフトウェアの制限のポリシーのツールと設定](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx)(Windows Server 2003)|
|**コミュニティ リソース**|[ソフトウェアの制限のポリシーによるアプリケーションのロックダウン](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|



