---
title: AD フォレストの回復 - サービスの DNS サーバーの構成
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b2c37428a0fb685e6a7fa4875366f3cd13401bd9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842963"
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>AD フォレストの回復 - DNS サーバー サービスを構成します。

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

バックアップから復元する DC の DNS サーバーの役割がインストールされていない場合は、インストールし、DNS サーバーを構成する必要があります。 

## <a name="install-and-configure-the-dns-server-service"></a>インストールして、DNS サーバー サービスの構成

復元が完了したら、DNS サーバーとして実行されていない各復元された DC のこの手順を完了します。 

> [!NOTE]
> バックアップから復元された DC で Windows Server 2008 R2 が実行されている場合は、DNS サーバーをインストールするには、分離されたネットワークに DC を接続する必要があります。 相互に共有、分離されたネットワークには、各復元された DNS サーバーを接続します。 復元された DNS サーバー間でレプリケーションが機能していることを確認する、repadmin/replsum を実行します。 レプリケーションを確認した後は、DNS サーバーの役割が既にインストールされている場合、復元された Dc を実稼働ネットワークに接続することができますの DNS サーバーは、サーバーがネットワークに接続されていないときに開始できるようにする修正プログラムを適用することができます。 自動化されたビルド プロセス中にオペレーティング システムのインストール イメージに修正プログラムをスリップ ストリームする必要があります。 修正プログラムの詳細については、次を参照してください。[記事 975654](https://go.microsoft.com/fwlink/?LinkId=184691)でマイクロソフト サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=184691)します。 

次のインストールと構成手順を完了します。

### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>インストールおよびサーバー マネージャーを使用して DNS サーバー サービス  

1. サーバー マネージャーを開き、をクリックして**役割と機能の追加**します。 
2. 役割の追加ウィザードの場合、**開始する前に**ページが表示されたら、をクリックして**次**します。 
3. **インストールの種類**画面で **[役割ベースまたは機能ベースのインストール]** をクリック **[次へ]** します。
4. **サーバーの選択**画面は、サーバーを選択し、をクリックして**次**します。
5. **サーバーの役割**画面で [ **DNS サーバー**クリックを求められた場合、**機能の追加**] をクリック**次**します。
6. **機能**画面をクリック**次**します。
7. 情報を読み、 **DNS サーバー** ] ページの [クリックして**次**します。
   ![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8. **確認** ページで、DNS サーバーの役割をインストールすることを確認 をクリックし、**インストール**します。 

### <a name="to-configure-the-dns-server-service"></a>DNS サーバー サービスを構成するには

1. サーバー マネージャーを開き、**ツール**クリック**DNS**します。
   ![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns2.png)
2. 重要な誤動作する前に、DNS サーバーにホストされていた同じ DNS ドメイン名の DNS ゾーンを作成します。 詳細については、Add a Forward Lookup Zone を参照してください ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574))。
3. 重要な誤動作する前に存在していた DNS データを構成します。 次に、例を示します。  

   - AD DS に格納される DNS ゾーンを構成します。 詳細については、変更、ゾーンの種類を参照してください ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579))。
   - 安全な動的更新を許可するドメイン コント ローラー ロケーター (DC ロケーター) リソース レコードに対する権限のある DNS ゾーンを構成します。 詳細については、許可 Only Secure Dynamic Updates を参照してください ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580))。

4. 親 DNS ゾーンにはでこの DNS サーバーでホストされている子ゾーンの委任リソース レコード (ネーム サーバー (NS) とグルー ホスト (A) リソース レコード) が含まれていることを確認します。 詳細については、ゾーンの委任を作成するを参照してください ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562))。
5. DNS を構成した後は、NETLOGON レコードの登録を短縮できます。

   > [!NOTE]
   > 安全な動的更新は、グローバル カタログ サーバーが使用可能な場合にのみ機能します。 

   コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。  

   **net stop netlogon**  

6. 次のコマンドを入力して、Enter キーを押します。  

   **net start netlogon**  

   ![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
