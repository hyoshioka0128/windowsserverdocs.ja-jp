---
title: 'AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 概要'
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
ms.assetid: ea19f0f0-6cc0-4322-b387-c0873f7795ad
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.openlocfilehash: 48c7d771c7ec75a4bc340608a96410ea388418e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874623"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-overview"></a>AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。概要

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このセクションのトピックでは、Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシを使って、ワーク フォルダーを展開するための手順を提供します。 この手順は、完全に機能するワーク フォルダーの設定を作成し、オンプレミスでもインターネットを経由しても、ワーク フォルダーを使用できるクライアント コンピューターを設定するように、提供されています。  
  
ワーク フォルダーは Windows Server 2012 R2 で導入されたコンポーネントです。ワーク フォルダーを使うと、インフォメーション ワーカーはデバイス間で仕事用のファイルを同期できます。 ワーク フォルダーについて詳しくは、「[ワーク フォルダーの概要](Work-Folders-Overview.md)」をご覧ください。  
  
ユーザーがインターネット経由でワーク フォルダーを同期できるようにするには、リバース プロキシによってワーク フォルダーを公開して、ワーク フォルダーを外部のインターネットから利用できるようにする必要があります。 AD FS に含まれる Web アプリケーション プロキシは、リバース プロキシ機能を提供するために使用できる 1 つのオプションです。 Web アプリケーション プロキシは、AD FS を使用して、ワーク フォルダー Web アプリケーションへのアクセスを事前認証し、ユーザーがすべてのデバイスで企業ネットワークの外部からワーク フォルダーにアクセスできるようにします。 

> [!NOTE]
>   このセクションで説明する手順は、Windows Server 2016 環境を対象としています。 Windows Server 2012 R2 を使用している場合には、[Windows Server 2012 R2 の手順](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx) に従います。
  
これらのトピックでは、以下について説明します。  
  
-   Windows Server のユーザー インターフェイスを使い、AD FS と Web アプリケーション プロキシを使用して、ワークフォルダーを設定して展開するための詳しい手順。 この手順では、自己署名証明書を使って、簡単なテスト環境を設定する方法について説明します。 このテストの例をガイドとして使用し、公的に信頼された証明書を使用して、実稼働環境を作成することができます。  
  
## <a name="prerequisites"></a>前提条件  
このトピックの手順と例に従うには、次のコンポーネントを準備する必要があります。  
  
-   複数のファイル サーバーを使用する場合、PC やデバイスでの適切なファイル サーバーの自動参照をサポートする、Windows Server 2012 R2 のスキーマ拡張機能を使用した Active Directory® Domain Services フォレスト。 フォレスト内 では DNS を有効化することを推奨しますが、これは必須ではありません。  
  
-   ドメイン コント ローラー:有効になっている、AD DS の役割を持つドメインが構成されているサーバー (テスト例では、contoso.com)。  
  
    Workplace Join のデバイス登録をサポートするには、Windows Server 2012 R2 以降を実行するドメイン コントローラーが必要です。 Workplace Join を使用しない場合には、ドメイン コント ローラーとして Windows Server 2012 を実行できます。  
  
-   ドメイン (contoso.com など) に参加し、Windows Server 2016 を実行している 2 台のサーバー。 1 台のサーバーは AD FS に使用し、他のサーバーはワーク フォルダーに使用します。  
  
-   Windows Server 2016 を実行している、ドメインに参加していない 1 台のサーバー。 このサーバーは Web アプリケーション プロキシを実行し、1 つのネットワーク カードをネットワーク ドメイン (contoso.com など) に接続し、もう 1 つのネットワーク カードを外部ネットワークに接続する必要があります。  
  
-   Windows 7 以降を実行し、ドメインに参加している 1 台のクライアント コンピューター。  
  
-   Windows 7 以降を実行し、ドメインに参加していない 1 台のクライアント コンピューター。  
  
このガイドで説明するテスト環境のトポロジは、次の図に示すとおりです。 これらのコンピューターは、物理コンピューターまたは仮想マシン (VM) のいずれかを使用できます。 
  
![インターネット、DMZ、Contoso ネットワーク セグメントを示す図。 インターネットのセグメント。Client2;境界ネットワーク: WAP サーバーです。Contoso セグメント。フォルダーのサーバー、ドメイン コント ローラー、AD FS サーバー、および Client1 を動作します。](media/deploy-work-folders-adfs/WF_ADFS_WAP_Diagram.png)

## <a name="deployment-overview"></a>展開の概要  
この一連のトピックでは、テスト環境において AD FS の設定、Web アプリケーション プロキシの設定、ワーク フォルダーの設定を行う手順の例を詳しく説明します。 次の順序で、コンポーネントのセットアップを行います。  
  
1.  AD FS  
  
2.  ワーク フォルダー  
  
3.  Web アプリケーション プロキシ  
  
4.  ドメインに参加しているワークステーションおよびドメインに参加していないワークステーション  
  
Windows PowerShell スクリプトを使用して、自己署名証明書を作成することもできます。  
  
## <a name="deployment-steps"></a>展開の手順  
Windows Server のユーザー インターフェイスを使用して展開を実行するには、これらのトピックの手順に従います。  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 1、AD FS の設定](deploy-work-folders-adfs-step1.md)  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 2 では、AD FS の構成後の作業](deploy-work-folders-adfs-step2.md)  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 3 では、ワーク フォルダーの設定](deploy-work-folders-adfs-step3.md)  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 4、Web アプリケーション プロキシの設定](deploy-work-folders-adfs-step4.md)  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 5 では、クライアントをセットアップします。](deploy-work-folders-adfs-step5.md)  

## <a name="see-also"></a>関連項目  
[ワーク フォルダーの概要](Work-Folders-Overview.md)  
[ワーク フォルダーの実装の設計](Plan-Work-Folders.md)  
[ワーク フォルダーの展開](Deploy-Work-Folders.md)  
  

