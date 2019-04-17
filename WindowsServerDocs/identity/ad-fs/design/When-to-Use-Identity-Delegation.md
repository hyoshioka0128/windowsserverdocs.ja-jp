---
ms.assetid: 6e711a96-9055-4508-b6d4-318d6aa95fd1
title: "Id 委任を使用する場合"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: af227d9e87ddb73f194dd46c8ce45fcdf12a34cf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="when-to-use-identity-delegation"></a>Id 委任を使用する場合

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
  
## <a name="what-is-identity-delegation"></a>Id 委任とは何ですか。  
Id 委任は、ユーザーを偽装する administrator\ によって指定されたアカウントは、Active Directory フェデレーション サービス \(AD FS\) の機能です。 ユーザーを偽装するアカウントと呼ばれる、*委任*します。 この委任機能は、多くの分散アプリケーションがあります、一連のアクセス制御チェックを各アプリケーション、データベース、またはサービスの最初の要求の承認チェーン内にある順番に行う必要がある重要です。 多くのための実際のシナリオでは、Web アプリケーション「フロント エンド」がより安全な「バックエンド」、Microsoft SQL Server データベースに接続されている Web サービスなどからのデータを取得する必要がありますが存在します。  
  
たとえば、既存 parts\ 順序の Web サイト拡張できるかプログラムでパートナー組織は独自の購入履歴とアカウントの状態の表示を許可します。 セキュリティ上の理由から、すべてのパートナーの財務データは、専用の構造化照会言語 \(SQL\) サーバー上のセキュリティで保護されたデータベースに格納されます。 このような状況で front\ エンド アプリケーションのコードは、パートナー組織の財務データについて何も認識します。 ホストしているネットワーク上の別のコンピューターからデータをそのため、取得する必要があります \、部品データベース用 Web サービスを (この大文字小文字) で \(the back end\) します。  
  
この data\ 取得プロセスを完了するには、一連の認証を行う必要があります「hand\ の動きを極力目立たなく」配置 Web アプリケーションと部品データベース用の Web サービスの間で、次の図に示すようにします。  
  
![Id 委任](media/adfs2_identitydelegationconcept.gif)  
  
Web サーバー自体に、Web サーバーへのアクセスを試みているユーザーの組織から完全に別の組織に存在する可能性がありますが、元の要求が行われたため、要求と共に送信されるセキュリティ トークンは、Web サーバー以外の他のコンピューターにアクセスするために必要な承認条件を満たしていません。 そのため、発信元のユーザーの要求を満たすことができます唯一の方法は、適切なアクセス権があるセキュリティ トークンを再発行を支援する、リソース パートナー組織に中間フェデレーション サーバーを配置することによってです。  
  
## <a name="how-does-identity-delegation-work"></a>Id 委任のしくみ  
多層アプリケーション アーキテクチャ内の Web アプリケーションは、多くの場合、共通のデータや機能にアクセスする Web サービスを呼び出します。 この Web サービス、サービスは承認の判断を行うし、監査を容易にするため、元のユーザーの ID を把握して重要です。 ここで、front\ ツー エンドの Web アプリケーションは、代理人として Web サービスにユーザーを表します。 AD FS では、Active Directory アカウントを別の証明書利用者のパーティーにユーザーとして動作するようにすることによってこのシナリオを容易になります。 Id 委任のシナリオは次の図に示します。  
  
![Id 委任](media/adfs2_identitydelegationsteps.gif)  
  
1.  Frank が別の組織で Web アプリケーションから part\ 注文履歴にアクセスしようとするとします。 彼のクライアント コンピューターは、要求して、front\ エンド part\ 順序 Web アプリケーション用の AD FS からトークンを受信します。  
  
2.  クライアント コンピューターは、クライアントの身元を証明するために、手順 1 で取得したトークンを含む、Web アプリケーションに要求を送信します。  
  
3.  Web アプリケーションは、クライアントのトランザクションを完了する Web サービスと通信する必要があります。 Web アプリケーションでは、Web サービスと対話する委任トークンを取得する AD FS を接続します。 委任トークンとは、ユーザーとして動作する代理人に発行されるセキュリティ トークンです。 AD FS では、Web サービスの対象とした、クライアントの信頼性情報と共に、委任トークンを返します。  
  
4.  Web アプリケーションが、取得したトークンをから手順 3 での AD FS クライアントとして動作している Web サービスへのアクセスを使用します。 Web サービス、委任トークンを調べると、Web アプリケーションがクライアントとして機能していることを決定できます。 Web サービスは、承認ポリシーを実行し、要求をログに記録および部品 Web アプリケーションに Frank が要求されていた履歴データを提供し、したがって Frank にします。  
  
特定の委任では、AD FS は、Web アプリケーションが委任トークンを要求が Web サービスを制限できます。 クライアント コンピューターには、Active Directory アカウントを成功させるのには、この操作ではありません。 最後に、前述のように、Web サービス簡単に確認できますユーザーとして動作している代理人の id。 これにより、かどうかが会話しているクライアント コンピューターに直接またはデリゲートを通じてに基づいてさまざまな現象が発生する Web サービスです。  
  
## <a name="configuring-ad-fs-for-identity-delegation"></a>AD FS ID 委任の構成  
AD FS 管理スナップインを使用して、データの取得プロセスを容易にする必要がある場合は、常には、id 委任用の AD FS を構成することができます。 AD FS が back\ バックエンド サービスを必要とする承認コンテキストに含まれる、新しいセキュリティ トークンを生成を構成した後、保護されたデータにアクセスを提供する前にします。  
  
AD FS は、権限を借用できるユーザーを制限しません。 Id 委任用の AD FS を構成した後は、次は。  
  
-   どのサーバーに委任できると判断したユーザーを偽装するトークンを要求する権限。  
  
-   確立し、個別に保持委任されているクライアントのアカウントと代理として動作するサーバーの両方の ID コンテキスト。  
  
Id 委任を構成するには、AD FS 管理スナップインで証明書利用者信頼に委任承認規則を追加します。 これを行う方法の詳細については、次を参照してください。[チェックリスト: Creating Claim Rules for a Relying Party Trust](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md)します。  
  
## <a name="configuring-the-front-end-web-application-for-identity-delegation"></a>Id 委任用 front\ ツー エンドの Web アプリケーションを構成します。  
開発者には、AD FS のコンピューターに委任要求をリダイレクトする front\ ツー エンドの Web アプリケーションまたはサービスを適切にプログラムを使用できるいくつかのオプションがあります。 Id 委任を使用する Web アプリケーションをカスタマイズする方法の詳細については、次を参照してください。、[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
