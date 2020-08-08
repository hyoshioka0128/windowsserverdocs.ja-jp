---
title: パスワードの概要
description: Windows Server のセキュリティ
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 4f38ee2062b2c154cc99a22a398e02e823a47ca2
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996079"
---
# <a name="passwords-overview"></a>パスワードの概要

>適用先:Windows Server (半期チャネル)、Windows Server 2016

IT 担当者向けのこのトピックでは、Windows オペレーティングシステムで使用されるパスワードについて説明し、資格情報管理戦略でのパスワードの使用に関するドキュメントとディスカッションへのリンクを示します。

## <a name="feature-description"></a><a name="BKMK_OVER"></a>機能の説明
現在、オペレーティングシステムとアプリケーションはパスワードを中心に設計されており、スマートカードや生体認証システムを使用している場合でも、すべてのアカウントにパスワードがあり、状況によっては引き続き使用できます。 一部のアカウント (特にサービスの実行に使用されるアカウント) では、スマートカードと生体認証トークンを使用できないため、認証にパスワードを使用する必要があります。 Windows は、暗号化ハッシュを使用してパスワードを保護します。

Windows パスワードの詳細については、「[パスワードの技術概要](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh994558(v=ws.10))」を参照してください。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>実際の適用例
Windows およびその他の多くのオペレーティングシステムでは、ユーザーの id を認証する最も一般的な方法は、シークレットパスフレーズまたはパスワードを使用することです。 ネットワーク環境をセキュリティで保護するには、すべてのユーザーが強力なパスワードを使用する必要があります。 これにより、悪意のあるユーザーが悪意のあるユーザーによる脆弱なパスワードの推測を防ぐことができます。これには、手動の方法を使用するか、ツールを使用して、侵害されたユーザーアカウントの資格情報を取得します。 これは、特に管理者アカウントに当てはまります。 複雑なパスワードを定期的に変更すると、パスワード攻撃によってそのアカウントが侵害される可能性が低くなります。

## <a name="new-and-changed-functionality"></a><a name="BKMK_NEW"></a>新機能と変更された機能
Windows Server 2012 と Windows 8 では、ピクチャパスワードが新しくなっています。 ピクチャパスワードは、ユーザーが選択したイメージと一連のジェスチャを組み合わせたものです。 ドメインに参加しているコンピューターでは、ピクチャパスワード機能が無効になってい \- ます。 ピクチャパスワードに関する詳細情報へのリンクについては、以下を[参照してください](#BKMK_LINKS)。

Windows Server 2012 および Windows 8 では、パスワード機能が変更されていません。 新しいグループポリシー設定は追加されていません。 ただし、資格情報とパスワードの管理機能の強化と強化が行われています。 \( \) たとえば、ピクチャパスワード、資格情報の保管、windows 8 へのサインインなどの Microsoft アカウントが WINDOWS Live ID と呼ばれていました。

## <a name="deprecated-functionality"></a><a name="BKMK_DEP"></a>非推奨の機能
Windows Server 2012 および Windows 8 では、パスワード機能が非推奨とされます。

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>ソフトウェア要件
エンタープライズ環境では、通常、パスワードは Active Directory Domain Services で管理されます。 ローカルコンピューターで、[ローカルセキュリティ設定]、[アカウントポリシー]、[パスワードポリシー] の設定を使用して、パスワードを管理することもできます。

## <a name="see-also"></a><a name="BKMK_LINKS"></a>関連項目
次の表に、パスワード機能、テクノロジ、および資格情報の管理に関するその他のリソースを示します。

|コンテンツ タイプ|参考資料|
|--------|-------|
|**シナリオ ドキュメント**|[デジタル ID の保護](https://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**操作**|[Active Directory ユーザーとコンピューティング](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754217(v=ws.11))|
|**トラブルシューティング**|[パスワードの有効期限が切れる日時を確認する \- Active Directory PowerShell ブログ](https://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**Security**| Windows Server 2008 R2 および Windows 7 の[脅威と対策ガイド: アカウントポリシー](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh125920(v=ws.10))<p>[強力なパスワードを変更および作成](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)するためのガイダンス|
|**ツールと設定**|[Microsoft ダウンロードセンターの「Windows および Windows Server 用のグループポリシー設定のリファレンス」](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**コミュニティ リソース**|[デジタル ID の保護](https://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<p>[Windows Live ID を使って Windows 8 にサインインする](https://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<p>[ピクチャパスワードを使用したサインイン](/archive/blogs/b8/signing-in-with-a-picture-password)<p>[ピクチャパスワードのセキュリティの最適化](/archive/blogs/b8/optimizing-picture-password-security)|