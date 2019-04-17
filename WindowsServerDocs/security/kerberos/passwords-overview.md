---
title: "パスワードの概要"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6c1b8d56b5c0da738e7dae5c0072be81040f90d8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="passwords-overview"></a>パスワードの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、Windows オペレーティング システム、およびドキュメントと資格情報の管理方針にパスワードの使用に関するディスカッションへのリンクで使用されているパスワードについて説明します。

## <a name="BKMK_OVER"></a>機能の説明
オペレーティング システムおよびアプリケーション今日がパスワードを構築し、スマート カードまたはシステムの生体認証を使用する場合でもすべてのアカウントはまだパスワードといくつかのような状況で引き続き使用します。 一部のアカウント、サービスの実行に使用されるアカウント特にスマート カードと生体認証トークンを使用してもことはできませんし、そのため、パスワードの認証に使用します。 Windows では、暗号化ハッシュを使用してパスワードを保護します。

For more information about Windows passwords, see [Passwords Technical Overview](https://technet.microsoft.com/library/hh994558(WS.10).aspx).

## <a name="BKMK_APP"></a>実際の適用
Windows と他の多くのオペレーティング システムでは、ユーザーの ID を認証するための最も一般的な方法は、秘密のパスフレーズやパスワードを使用します。 ネットワーク環境をセキュリティで保護するには、すべてのユーザーが強力なパスワードを使用することが必要です。 これにより、手動の方法であるかどうか、または侵害されているユーザー アカウントの資格情報を取得するツールを使用して、脆弱なパスワードを推測悪意のあるユーザーの脅威を回避できます。 これは、管理者アカウントの特に当てはまります。 複雑なパスワードを定期的に変更すると、そのアカウントを損なうことパスワード攻撃の可能性を減らします。

## <a name="BKMK_NEW"></a>新機能と変更された機能
Windows Server 2012 と Windows 8 でピクチャ パスワードは新しいです。 ピクチャ パスワードは、一連のジェスチャと組み合わせると、ユーザーの選択したイメージの組み合わせです。 ピクチャ パスワード機能は \servername に参加しているコンピューターで無効になります。 ピクチャ パスワードに関する詳細情報へのリンクが記載されて[参照](#BKMK_LINKS)下。

Windows Server 2012 および Windows 8 でパスワードの機能への変更はありませんされました。 新しいグループ ポリシー設定が追加されていません。 ただし、強化された機能と拡張機能に加えられた資格情報の \(and password\) 管理、ピクチャ パスワード、資格情報保管ボックスと Microsoft アカウントを使って Windows 8 へのログイン、旧 Windows Live ID など、

## <a name="BKMK_DEP"></a>推奨されなくなった機能
Windows Server 2012 および Windows 8 でないパスワード機能は廃止されました。

## <a name="BKMK_SOFT"></a>ソフトウェアの要件
エンタープライズ環境でのパスワードは通常、Active Directory ドメイン サービスを管理します。 ローカルのセキュリティの設定]、[アカウント ポリシー、パスワード ポリシーの設定を使用して、ローカル コンピューター上のパスワードを管理することもできます。

## <a name="BKMK_LINKS"></a>参照してください。
この表に、パスワードの機能の追加リソース テクノロジと資格情報の管理します。

|コンテンツの種類|参照|
|--------|-------|
|**シナリオ ドキュメント**|[デジタル ID の保護](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**操作**|[Active Directory ユーザーとコンピューター](https://technet.microsoft.com/library/cc754217.aspx)|
|**トラブルシューティング**|[パスワードの有効期限が切れる見つける \-Active Directory PowerShell のブログ](http://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**セキュリティ**| Windows Server 2008 R2  and  Windows 7 [Threats and Countermeasures Guide: Account Policies](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<br /><br />Guidance to [change and create strong passwords](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)|
|**ツールと設定**|[Windows および Windows Server、Microsoft ダウンロード センターでのグループ ポリシー設定のリファレンス](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**コミュニティ リソース**|[デジタル ID の保護](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Windows Live ID を持つ Windows 8 へのをログイン](http://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[ピクチャ パスワードを使用してログイン](http://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[ピクチャ パスワードのセキュリティを最適化します。](http://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


