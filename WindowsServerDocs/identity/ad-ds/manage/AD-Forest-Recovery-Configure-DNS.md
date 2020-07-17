---
title: AD フォレストの回復-DNS サーバーサービスの構成
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 144a45f2a835d9cca60b5be5aac7569809c45b7c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824175"
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>AD フォレストの回復-DNS サーバーサービスの構成

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

バックアップから復元する DC に DNS サーバーの役割がインストールされていない場合は、DNS サーバーをインストールして構成する必要があります。 

## <a name="install-and-configure-the-dns-server-service"></a>DNS サーバーサービスのインストールと構成

復元が完了した後で、DNS サーバーとして実行されていない復元された各 DC に対して、この手順を完了します。 

> [!NOTE]
> バックアップから復元した DC が Windows Server 2008 R2 を実行している場合は、DNS サーバーをインストールするために、DC を分離されたネットワークに接続する必要があります。 その後、復元された各 DNS サーバーを相互共有された分離されたネットワークに接続します。 Repadmin/replsum を実行して、復元された DNS サーバー間でレプリケーションが機能していることを確認します。 レプリケーションを確認した後、復元された Dc を実稼働ネットワークに接続できます。 DNS サーバーの役割が既にインストールされている場合は、サーバーがどのネットワークにも接続されていない状態で DNS サーバーを起動できる修正プログラムを適用できます。 自動ビルドプロセス中に、修正プログラムをオペレーティングシステムのインストールイメージにスリップストリームする必要があります。 修正プログラムの詳細については、Microsoft サポート技術情報の[記事 975654](https://go.microsoft.com/fwlink/?LinkId=184691) (https://go.microsoft.com/fwlink/?LinkId=184691)を参照してください。 

以下のインストールと構成の手順を完了します。

### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>サーバーマネージャーを使用してと DNS サーバーサービスをインストールするには  

1. サーバーマネージャーを開き、 **[役割と機能の追加]** をクリックします。 
2. 役割の追加ウィザードで、 **[開始する前に]** ページが表示されたら、 **[次へ]** をクリックします。 
3. **[インストールの種類]** 画面で **[役割ベースまたは機能ベースのインストール]** を選択し、 **[次へ]** をクリックします。
4. **[サーバーの選択]** 画面で、サーバーを選択し、 **[次へ]** をクリックします。
5. **[サーバーの役割]** 画面で **[DNS サーバー]** を選択します。メッセージが表示されたら、 **[機能の追加]** をクリックし、 **[次へ]**
6. **[機能]** 画面で **[次へ]** をクリックします。
7. **[DNS サーバー]** ページの情報を読み、 **[次へ]** をクリックします。
   ![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8. **[確認]** ページで、DNS サーバーの役割がインストールされていることを確認し、 **[インストール]** をクリックします。 

### <a name="to-configure-the-dns-server-service"></a>DNS サーバーサービスを構成するには

1. サーバーマネージャーを開き、 **[ツール]** をクリックし、 **[DNS]** をクリックします。
   ![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns2.png)
2. 重大な誤動作を行う前に、DNS サーバーでホストされていたのと同じ DNS ドメイン名の DNS ゾーンを作成します。 詳細については、「前方参照ゾーンを追加する ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574))」を参照してください。
3. 重大な障害の前に存在していた DNS データを構成します。 例 :  

   - AD DS に格納されるように DNS ゾーンを構成します。 詳細については、「ゾーンの種類を変更する ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579))」を参照してください。
   - ドメインコントローラーロケーター (DC ロケーター) リソースレコードに対して権限のある DNS ゾーンを構成して、セキュリティで保護された動的更新を実行できるようにします。 詳細については、「セキュリティで保護された動的更新のみを許可する ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580))」を参照してください。

4. 親 DNS ゾーンに、この DNS サーバーでホストされている子ゾーンの委任リソースレコード (ネームサーバー (NS) とグルーホスト (A) リソースレコード) が含まれていることを確認します。 詳細については、「ゾーンの委任を作成する」 ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)) を参照してください。
5. DNS を構成した後、NETLOGON レコードの登録を高速化できます。

   > [!NOTE]
   > セキュリティで保護された動的更新は、グローバルカタログサーバーが使用可能な場合にのみ機能します。 

   コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。  

   **net stop netlogon**  

6. 次のコマンドを入力して、Enter キーを押します。  

   **net start netlogon**  

   ![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
