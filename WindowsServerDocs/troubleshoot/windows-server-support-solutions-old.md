---
title: Windows Server 向けの上位のサポート ソリューション
description: Windows Server の問題のソリューションへのリンクを示します。
manager: alant
ms.date: 03/16/2018
ms.topic: article
author: kaushika-msft
ms.author: elizapo
ms.openlocfilehash: 6e76c54f0adf97e506dc7ce77ca103ba70d9c5c1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935546"
---
# <a name="top-support-solutions-for-windows-server-2016"></a>Windows Server 2016 向けの上位のサポート ソリューション

Microsoft では Windows Server 用の更新プログラムとソリューションの両方を定期的にリリースします。 お客様のサーバーでセキュリティ更新プログラムなどの今後の更新プログラムを受信できることを確認するには、サーバーを最新の状態に維持する必要があります。 リリースされた更新プログラムの完全なリストについては、「[Windows 10 および Windows Server 2016 の更新履歴](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)」をご覧ください。

これらは、Windows Server 2016 を使用する際に発生する最も一般的な問題に関する上位の Microsoft サポート ソリューションです。 次のリンクには、サポート技術情報の記事、更新プログラム、ライブラリの記事へのリンクが含まれます。

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

## <a name="solutions-for-installing-or-upgrading-windows-server"></a>Windows Server のインストールとアップグレードに関連するソリューション

- [Windows 10 のアップグレード エラーの解決: IT 担当者向けの技術情報](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)
- [Windows 10 バージョン 1607 および Windows Server 2016 のサービス スタック更新プログラム: 2017 年 8 月 8 日](https://support.microsoft.com/help/4035631)
- [Windows 10 バージョン 1607 および Windows Server 2016 アップグレード用互換性更新プログラム: 2017 年 8 月 3 日](https://support.microsoft.com/help/4033524)
- [Windows ベースの Azure VM では、システムのインプレース アップグレードはサポートされていません](https://support.microsoft.com/help/4014997)
- [Windows Server 2016 のアップグレード オプションと変換オプション](../get-started/supported-upgrade-paths.md)
- [Windows Server 2016 向けのサーバーの役割のアップグレードと移行に関する一覧表](../get-started/server-role-upgradeability-table.md)
- [Windows Server のインストールとアップグレード](../get-started/installation-and-upgrade.md)
- [リリース ノート:Windows Server 2016 に関する重要な問題](../get-started/windows-server-2016-ga-release-notes.md)
- [Windows Server 2016 への移行に関する推奨事項](../get-started/recommendations-moving-to-server2016.md)

## <a name="solutions-for-volume-activation"></a>ボリューム ライセンス認証のソリューション
- [Windows Server 2016 のライセンス認証](../get-started/server-2016-activation.md)
- [ライセンス認証の方法の確認と選択](https://technet.microsoft.com/library/jj134256(ws.11).aspx)
- [ボリューム ライセンス認証のためのライセンス認証エラー コード](https://technet.microsoft.com/library/dn502528.aspx)
- [キー管理サービス (KMS) をトラブルシューティングする方法](https://technet.microsoft.com/library/ee939272.aspx)
- [ボリューム ライセンス認証のトラブルシューティング](https://technet.microsoft.com/library/ff793439.aspx)
- [ライセンス認証エラー コード](https://technet.microsoft.com/library/ff793399.aspx)
- [Windows のインストールが失敗し、"入力されたプロダクトキーは、インストール可能な Windows イメージのいずれとも一致しません。別のプロダクトキーを入力してください "](https://support.microsoft.com/help/2796988/windows-8-or-windows-server-2012-installation-may-fail-with-error-mess)

## <a name="solutions-related-to-dcpromo-and-installing-domain-controllers"></a>DCPromo とドメイン コントローラーのインストールに関連するソリューション
- [Active Directory および Active Directory Domain Services のポートの要件](https://technet.microsoft.com/library/dd772723(v=ws.10).aspx)
- [Active Directory ファイアウォールのポート-単純にする](http://blogs.msmvps.com/acefekay/2011/11/01/active-directory-firewall-ports-let-s-try-to-make-this-simple/)
- [Exchange Server による Windows Server 2016 のサポート](https://technet.microsoft.com/library/ff728623(v=exchg.150).aspx)
- [Ntdsutil.exe を使用してドメイン コントローラーに FSMO の役割を転送または停止する](https://support.microsoft.com/kb/255504)
- [ドメイン コントローラーの展開のトラブルシューティング](../identity/ad-ds/deploy/troubleshooting-domain-controller-deployment.md)
- [Active Directory インストール ウィザードの問題のトラブルシューティング](https://msdn.microsoft.com/library/bb727058.aspx)
- [AD DS のインストールおよび削除に関する既知の問題](https://technet.microsoft.com/library/cc754463(v=ws.10).aspx)

## <a name="solutions-for-active-directory-federation-services-ad-fs"></a>Active Directory フェデレーション サービス (AD FS) のソリューション
- [Azure Active Directory への Windows ドメイン参加済みデバイスの自動登録の構成方法](/azure/active-directory/active-directory-conditional-access-automatic-device-registration-setup)
- [要求の発行のセットアップ](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup#step-2-setup-issuance-of-claims)
- [LDAP ディレクトリに保存されたユーザーを認証するように AD FS を構成する](../identity/ad-fs/operations/configure-ad-fs-to-authenticate-users-stored-in-ldap-directories.md)
- [AD FS での証明書認証のための代替ホスト名バインドのサポート](../identity/ad-fs/operations/ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)
- [パスワード攻撃に対する保護が実現](https://blogs.technet.microsoft.com/tspring/2017/01/20/federated-to-microsoft-cloud-and-account-lockouts/)
- [WID データベースを使用した、Windows Server 2016 での AD FS へのアップグレード](../identity/ad-fs/deployment/upgrading-to-ad-fs-in-windows-server-2016.md)
- [Windows 10 のサインオン: AD FS でデバイス認証を有効にする](../identity/ad-fs/operations/configure-device-based-conditional-access-on-premises.md)
- [Windows Server 2016 の AD FS と WAP で SSL 証明書を管理する](../identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap-2016.md)
- [Windows Server 2016 AD FS のアクセス制御ポリシー](../identity/ad-fs/operations/access-control-policies-in-ad-fs.md)

## <a name="solutions-related-to-active-directory-replication"></a>Active Directory のレプリケーションに関連するソリューション

- [Active Directory レプリケーションの問題のトラブルシューティングに関するページ](../identity/ad-ds/manage/troubleshoot/troubleshooting-active-directory-replication-problems.md)
- [Microsoft ダウンロード センターからの Active Directory Replication Status ツールのダウンロード](https://www.microsoft.com/en-in/download/details.aspx?id=30005)
- [e2e: 一般的な Active Directory レプリケーション エラーをトラブルシューティングする方法](https://support.microsoft.com/kb/3108513)
- [AD レプリケーション エラー 8606: "オブジェクトの作成に必要な属性が足りません" のトラブルシューティング](https://support.microsoft.com/kb/2028495)
- [Windows 2000 Server および Windows Server 2003 で、Active Directory の入力方向のレプリケーション実行中にイベント ID 2108 およびイベント ID 1084 が発生する](https://support.microsoft.com/kb/837932)
- [AD レプリケーション エラー 8451: "レプリケーション操作中に、データベースのエラーが発生しました" のトラブルシューティング](https://support.microsoft.com/kb/2645996)
- [AD レプリケーション エラー 1127: "ハード ディスクにアクセスするときに、再試行の後もディスク操作を正しく実行できませんでした" のトラブルシューティング](https://support.microsoft.com/kb/2025726)
- [サーバー メタデータのクリーンアップ](https://technet.microsoft.com/library/cc816907.aspx)