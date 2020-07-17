---
title: AD フォレストの回復-krbtgt パスワードのリセット
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.technology: identity-adds
ms.openlocfilehash: e2d19621c80b40fa70706bf75434dce74693990d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823635"
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>AD フォレストの回復-krbtgt パスワードのリセット

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

ドメインの krbtgt パスワードをリセットするには、次の手順に従います。 次の手順では、書き込み可能な Dc を適用しますが、読み取り専用ドメインコントローラー (Rodc) は適用しません。
  
> [!IMPORTANT]
> フォレストの回復中に Rodc をオンラインで回復する予定がある場合は、Rodc の krbtgt アカウントを削除しないでください。 RODC の krbtgt アカウントは krbtgt_*number*の形式で一覧表示されます。
>
> DC でカスタマイズされたパスワードフィルター (passfilt.dll など) を使用する場合、krbtgt パスワードをリセットしようとするとエラーが発生することがあります。 回避策を含む詳細については、マイクロソフトサポート技術情報の[記事 2549833](https://support.microsoft.com/kb/2549833) (https://support.microsoft.com/kb/2549833)を参照してください。
  
## <a name="to-reset-the-krbtgt-password"></a>Krbtgt パスワードをリセットするには  
  
1. **[スタート]** をクリックし、 **[コントロールパネル]** をポイントします。次に、 **[管理ツール]** をポイントし、 **[Active Directory ユーザーとコンピューター]** をクリックします。
2. **[表示]** をクリックし、 **[高度な機能]** をクリックします。
3. コンソールツリーで、ドメインコンテナーをダブルクリックし、 **[ユーザー]** をクリックします。
4. 詳細ウィンドウで、 **krbtgt**ユーザーアカウントを右クリックし、 **[パスワードのリセット]** をクリックします。
   パスワードのリセット ![](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)
5. **[新しいパスワード]** に新しいパスワードを入力し、 **[パスワードの確認]** 入力 にパスワードを再入力して、[ **OK]** をクリックします。 指定したパスワードは、指定したパスワードとは無関係に自動的に強力なパスワードが生成されるため、重要ではありません。
  
> [!NOTE]
> この操作は2回実行する必要があります。 Krbtgt アカウントのパスワードの履歴は2です。つまり、最新の2つのパスワードが含まれています。 パスワードを2回リセットすると、履歴から古いパスワードが実質的にクリアされるため、別の DC がこの DC で古いパスワードを使用してレプリケートする方法はありません。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md) 
