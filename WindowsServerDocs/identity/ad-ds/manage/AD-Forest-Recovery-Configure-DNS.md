---
title: "AD フォレストの回復 - サービスの DNS サーバーの構成"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f24570965fd8b3f3e050779c42758865cbee2728
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>AD フォレストの回復 - DNS サーバー サービスを構成します。 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:
 
バックアップから復元する DC で DNS サーバーの役割がインストールされていない場合は、インストールし、DNS サーバーを構成する必要があります。  
  

## <a name="install-and-configure-the-dns-server-service"></a>インストールして、DNS サーバー サービスを構成します。  
各復元されたドメイン コント ローラー復元が完了したら、DNS サーバーとして実行されていないため、この手順を完了します。  
  
> [!NOTE]
>  バックアップから復元された DC が Windows Server 2008 R2 を実行している場合は、DNS サーバーをインストールするために、DC を隔離されたネットワークに接続する必要があります。 次の復元された DNS サーバーの各を相互に共有、分離されたネットワークに接続します。 復元された DNS サーバー間でレプリケーションが機能していることを確認する repadmin/replsum を実行します。 レプリケーションを確認した後は、DNS サーバーの役割が既にインストールされている場合、復元されたドメイン コント ローラーを実稼働ネットワークに接続することができます、DNS サーバーは、サーバーが任意のネットワークに接続していないときに開始できるようにする修正プログラムを適用することができます。 オペレーティング システムのインストール イメージに修正プログラムをスリップ ストリームを使い、自動ビルド プロセス中にする必要があります。 修正プログラムの詳細については、次を参照してください。[記事 975654](https://go.microsoft.com/fwlink/?LinkId=184691)で、Microsoft サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=184691)。 

次のインストールと構成手順を完了します。
  
### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>インストールし、サーバー マネージャーを使用して、DNS サーバー サービス  
  
1.  サーバー マネージャーを開き] をクリックして**役割と機能の追加**します。  
2.  役割の追加ウィザードの場合、**開始する前に**ページが表示されたら、] をクリックして**次**します。  
3.  **インストールの種類**選択画面**役割ベースまたは機能ベースのインストール**] をクリック**[次へ]**します。
4.  **サーバーの選択**画面は、サーバーを選択し、をクリックして**次**します。
5.  **サーバーの役割**選択画面**DNS サーバー**クリックを求められた場合、**機能の追加**] をクリック**[次へ]**します。
6.  **機能**画面をクリックして**次**します。
7.  情報を読み、 **DNS サーバー**ページで、クリックして**[次へ]**します。
![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8.  **確認**] ページで、DNS サーバーの役割をインストールすることを確認し、をクリックして**インストール**します。  
  
     
### <a name="to-configure-the-dns-server-service"></a>DNS サーバー サービスを構成するには 
1.  サーバー マネージャーを開き、[**ツール**] をクリック**DNS**します。
![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns2.png)    
2.  重要な誤動作する前に、DNS サーバーでホストされている同じ DNS ドメイン名の DNS ゾーンを作成します。 詳細については、追加の前方参照ゾーンを参照してください ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574))。  
3.  重要な誤動作する前に存在していた DNS データを構成します。 例えば：  
  
    -   AD DS に格納する DNS ゾーンを構成します。 詳細については、変更、ゾーンの種類を参照してください ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579))。  
  
    -   保護された動的更新を許可するようにドメイン コントローラー ロケーター (DC ロケーター) リソース レコードに対する権限を持つ DNS ゾーンを構成します。 詳細については、許可をセキュリティで保護動的更新のみを参照してください ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580))。  
  
4. 親 DNS ゾーンにこの DNS サーバーでホストされている子ゾーンの委任リソース レコード (ネーム サーバー (NS) とグルー ホスト (A) リソース レコード) が含まれていることを確認します。 詳細については、ゾーンの委任を作成するを参照してください ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562))。  
5. DNS を構成した後は、NETLOGON レコードの登録を高速化することができます。  
  
    > [!NOTE]
    >  セキュアな動的更新では、グローバル カタログ サーバーが利用可能な場合にのみ機能します。  
  
     コマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。  
  
     **Net stop netlogon**  
  
6. 次のコマンドを入力し、Enter キーを押します。  
  
     **Net start netlogon**  

![DNS サーバー](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
