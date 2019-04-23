---
title: AD フォレストの回復 - プールの RID を発生させる
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adds
ms.openlocfilehash: c8f91226e10ea6681933d5a5dc00b92f5ab2179c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862983"
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>AD フォレストの回復に使用可能な RID プールの値を上げる 

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

相対 ID (RID) の値を上げるには、次の手順は、その DC を復元した後は、RID 操作マスタを割り当てますをプールに使用します。 使用可能な RID プールの値を生成するには、DC、ドメインの復元に使用したバックアップの後に作成されたセキュリティ プリンシパルは、RID 割り当てなしを保証できます。 

## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Active Directory の RID プールと rIDAvailablePool について

各ドメインは、オブジェクト**CN = RID Manager, cn = System, DC**=<*domain_name*>。 このオブジェクトがという名前の属性を持つ**rIDAvailablePool**します。 この属性値では、ドメイン全体のグローバル RID 空間は保持します。 値は、上限と下限の部分を持つ大きな整数です。 上の部分では、(0x3FFFFFFF または 10億を超えるだけ) は、各ドメインに対して割り当て可能なセキュリティ プリンシパルの数を定義します。 下の部分は、ドメインに割り当てられている Rid の数です。 
  
> [!NOTE]
> Windows Server 2016 と 2012 で割り当てることができるセキュリティ プリンシパルの数が 20億を徐々 に増えます。 詳細については、次を参照してください。[管理 RID 発行の](https://technet.microsoft.com/library/jj574229.aspx)します。 
  
- サンプルの値:4611686014132422708  
- 低い部分。2100 (次の RID プールが割り当てられるの始点)  
- 上の部分。1073741823 (ドメイン内に作成できる Rid の合計数)  
  
大きい整数の値を大きくと、下位部分の値を増やします。 たとえば、4611686014132522708 合計 4611686014132422708 のサンプル値を 100,000 を追加する場合、新しい下位部分には、102100 は。 これは、RID マスターによって割り当てられる次の RID プールの先頭は 2100 ではなく 102100 でことを示します。 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator"></a>Adsiedit と電卓を使用して、使用可能な RID プールの値を上げる

1. サーバー マネージャーを開き、**ツール**クリック**ADSI Edit**します。
2. 右クリックし、選択**への接続**接続および既定の名前付けコンテキストを行い、をクリックして**OK**。
   ![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi1.png) 
3. 次の識別名のパスを参照してください。**CN RID Manager$、CN を = = System, DC =<domain name>** します。
   ![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi2.png) 
3. 右クリックし、プロパティの CN = RID Manager$。 
4. 属性を選択**rIDAvailablePool**、 をクリックして**編集**、し、大きな整数値をクリップボードにコピーします。
   ![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi3.png)  
5. 電卓を起動してから、**ビュー**メニューの **科学計算モード**。 
6. 現在の値には、100,000 を追加します。
   ![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi4.png) 
7. Ctrl + c を使用して、または**コピー**コマンドから、**編集**] メニューの [値をクリップボードにコピーします。 
8. Adsiedit の編集 ダイアログ ボックスで、この新しい値を貼り付けます。 
   ![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi5.png) 
9. をクリックして**OK**ダイアログ ボックスと**適用**を更新するプロパティ シートで、 **rIDAvailablePool**属性。 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>LDP を使用して、使用可能な RID プールの値を上げる  
  
1. コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。  
   **ldp**  
2. をクリックして**接続**、] をクリックして**Connect**RID マネージャーの名前を入力し、[クリックして**OK**。 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp1.png)
3. をクリックして**接続**、 をクリックして**バインド**を選択します**資格情報によるバインド**と管理者の資格情報を入力し、クリックして**OK**します。 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp2.png)
4. クリックして**ビュー**、 をクリックして**ツリー**し、次の識別名のパスを入力します。CN = RID Manager, cn = System, DC =*ドメイン名*  
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp3.png)
5. をクリックして**参照**、 をクリックし、**変更**します。 
6. 100,000 に現在追加**rIDAvailablePool**値とに合計を入力し、**値**します。 
7. **Dn**、型`cn=RID Manager$,cn=System,dc=` *< ドメイン名\>* します。 
8. **エントリ属性の編集**、型`rIDAvailablePool`します。 
9. 選択**置換**操作、およびクリックとして **」と入力**します。
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp4.png) 
10. クリックして**実行**操作を実行します。 **[閉じる]** をクリックします。
11. 変更を検証するには、次のようにクリックします。**ビュー**、 をクリック**ツリー**、し、次の識別名のパスを入力します。 CN = RID Manager, cn = System, DC =*ドメイン名*します。   チェック、 **rIDAvailablePool**属性。 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp5.png)

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
