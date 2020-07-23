---
title: ソフトウェア制限ポリシー
description: Windows Server のセキュリティ
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: 5c0befad-07c3-4262-b418-372d01850305
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 28a4773899d0ccd53f6c7facd36898225ca7e007
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966154"
---
# <a name="software-restriction-policies"></a>ソフトウェア制限ポリシー

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

IT 担当者向けのこのトピックでは、windows Server 2012 および Windows 8 でのソフトウェアの制限のポリシー (SRP) について説明し、Windows Server 2003 以降の SRP に関する技術情報へのリンクを示します。

手順とトラブルシューティングのヒントについては、「[ソフトウェア制限ポリシーの管理](administer-software-restriction-policies.md)」および「[ソフトウェアの制限のポリシーのトラブルシューティング](troubleshoot-software-restriction-policies.md)」を参照してください。

## <a name="software-restriction-policies-description"></a><a name="BKMK_OVER"></a>ソフトウェアの制限のポリシーの説明
ソフトウェアの制限のポリシー (SRP) はグループ ポリシー ベースの機能で、ドメイン内のコンピューターで実行されているソフトウェア プログラムを識別し、これらのプログラムを実行する機能を制御します。 ソフトウェアの制限のポリシーは、マイクロソフトのセキュリティと管理に関する戦略の一環として、企業のコンピューターの信頼性、整合性、および管理容易性の向上に寄与します。

ソフトウェアの制限のポリシーを使えば、コンピューターの構成に厳格な制限を加え、指定したアプリケーションに限って実行を許可することもできます。 ソフトウェアの制限のポリシーは、Microsoft Active Directory とグループ ポリシーに統合されています。 スタンドアロン コンピューター上でソフトウェアの制限のポリシーを作成することも可能です。 ソフトウェアの制限のポリシーは信頼ポリシーであり、スクリプトなどの必ずしも信頼できないコードの実行を制限するために管理者が設定する規則です。

このポリシーを定義するには、Microsoft 管理コンソール (MMC) のローカル グループ ポリシー エディター スナップインまたはローカル セキュリティ ポリシー スナップインの "ソフトウェアの制限のポリシー" 拡張機能を使います。

SRP の詳細については、「[ソフトウェア制限ポリシーの技術概要](software-restriction-policies-technical-overview.md)」を参照してください。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>実際の適用例
管理者は次のタスクにソフトウェアの制限のポリシーを使用できます。

-   信頼できるコードの定義

-   スクリプト、実行可能ファイル、および ActiveX コントロールの制御用の柔軟なグループ ポリシーの設計

ソフトウェアの制限のポリシーは、ソフトウェアの制限のポリシーに準拠しているオペレーティング システムとアプリケーション (スクリプト アプリケーションなど) によって適用されます。

具体的には、管理者は次の用途にソフトウェアの制限のポリシーを使用できます。

-   クライアントで実行できるソフトウェア (実行可能ファイル) を指定する

-   共有のコンピューター上でユーザーによって特定のプログラムが実行されるのを防ぐ

-   信頼できる発行元をクライアントに追加できるユーザーを指定する

-   ソフトウェアの制限のポリシーの範囲を設定する (ポリシーがクライアントの全ユーザーに適用となるのか、一部ユーザーのみに適用となるのかを指定する)

-   実行可能ファイルがローカル コンピューター、組織単位 (OU)、サイト、ドメインで実行されるのを防ぐ。 悪意のあるユーザーによって引き起こされる問題の予防にソフトウェアの制限のポリシーを使っていない場合には、これが適しています。

## <a name="new-and-changed-functionality"></a><a name="BKMK_NEW"></a>新機能と変更された機能
ソフトウェアの制限のポリシーの機能については変更はありません。

## <a name="removed-or-deprecated-functionality"></a><a name="BKMK_DEP"></a>削除された機能または非推奨の機能
ソフトウェアの制限のポリシーの機能については削除された機能や非推奨の機能はありません。

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>ソフトウェア要件
ローカル グループ ポリシー エディターの "ソフトウェアの制限のポリシー" 拡張機能は、MMC からアクセスできます。

ローカル コンピューターでソフトウェアの制限のポリシーを作成して管理するには、次の機能が必要です。

-   ローカル グループ ポリシー エディター

-   Windows インストーラー

-   Authenticode および WinVerifyTrust

このポリシーをドメインに展開する必要がある場合には、上に挙げた機能のほか、次の機能が必要です。

-   Active Directory ドメイン サービス

-   グループ ポリシー

## <a name="server-manager-information"></a><a name="BKMK_INSTALL"></a>サーバー マネージャー情報
ソフトウェアの制限のポリシーは、ローカル グループ ポリシー エディターの拡張機能の 1 つであり、サーバー マネージャーや [役割と機能の追加] からインストールするものではありません。

## <a name="see-also"></a><a name="BKMK_LINKS"></a>関連項目
SRP に関する情報と使用方法についてのリソースへのリンクを次の表に示します。

|コンテンツ タイプ|参考資料|
|--------|-------|
|**製品評価**|[ソフトウェアの制限のポリシーによるアプリケーションのロックダウン](/previous-versions/technet-magazine/cc510322(v=msdn.10)?pr=blog)|
|**計画**|[ソフトウェアの制限のポリシーの技術概要](software-restriction-policies-technical-overview.md)(Windows Server 2012)<p>[ソフトウェアの制限のポリシーのテクニカル リファレンス](/previous-versions/windows/it-pro/windows-server-2003/cc728085(v=ws.10)) (Windows Server 2003)|
|**デプロイ**|リソースはありません。|
|**操作**|[ソフトウェアの制限のポリシーの管理](administer-software-restriction-policies.md)(Windows Server 2012)<p>[ソフトウェアの制限のポリシーの製品ヘルプ](/previous-versions/windows/it-pro/windows-server-2003/cc779607(v=ws.10))(Windows Server 2003)|
|**トラブルシューティング**|[ソフトウェアの制限のポリシーのトラブルシューティング](troubleshoot-software-restriction-policies.md)(Windows Server 2012)<p>[ソフトウェアの制限のポリシーのトラブルシューティング](/previous-versions/windows/it-pro/windows-server-2003/cc737011(v=ws.10)) (Windows Server 2003)|
|**Security**|[ソフトウェアの制限のポリシーに関する脅威と対策](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd349795(v=ws.10)) (Windows Server 2008)<p>[ソフトウェアの制限のポリシーに関する脅威と対策](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh125926(v=ws.10)) (Windows Server 2008 R2)|
|**ツールと設定**|[ソフトウェアの制限のポリシーのツールと設定](/previous-versions/windows/it-pro/windows-server-2003/cc782454(v=ws.10))(Windows Server 2003)|
|**コミュニティ リソース**|[ソフトウェアの制限のポリシーによるアプリケーションのロックダウン](/previous-versions/technet-magazine/cc510322(v=msdn.10)?pr=blog)|
