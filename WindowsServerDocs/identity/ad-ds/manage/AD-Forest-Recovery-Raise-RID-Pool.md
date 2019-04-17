---
title: "AD フォレストの回復 - プールを RID を上げる"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adfs
ms.openlocfilehash: e6b5dc8b9c0b701fe2cd1b0c88f7edc22802c393
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>AD フォレストの回復 - 利用可能な RID プールの値を上げる 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:
 
 その DC が復元した後、RID 操作マスタを割り当てることを相対 ID (RID) の値を上げるには、次の手順をプールに使用します。 利用可能な RID プールの値を発生することによって DC がドメインの復元に使用したバックアップ後に作成したセキュリティ プリンシパルは、RID 割り当てありませんを確認することができます。  
 
## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Active Directory の RID プールと rIDAvailablePool について
 各ドメイン オブジェクトには**CN = RID Manager$、CN = System, DC**=<*domain_name*> します。 このオブジェクトは、という名前の属性を持つ**rIDAvailablePool**します。 この属性値には、ドメイン全体の場合、グローバル RID 空間が維持されます。 値は、上部と下部の部分と大きな整数です。 上の部分では、(0x3FFFFFFF またはだけ 10億) ドメインごとに割り当てることができるセキュリティ プリンシパルの数を定義します。 下の部分は、ドメインに割り当てられている Rid の数です。  
  
> [!NOTE]
>  Windows Server 2016 と 2012 で割り当てることができるセキュリティ プリンシパルの数がだけ 20億に向上します。 詳細については、次を参照してください。[管理 RID 発行の](https://technet.microsoft.com/library/jj574229.aspx)します。  
  
-   サンプルの値: 4611686014132422708  
  
-   低パート: 2100 ([次へ] の RID プールが割り当てられるの先頭)  
  
-   上部: 1073741823 (ドメイン内に作成できる Rid の合計数)  
  
 大きな整数の値を大きくと、低の一部の値を増やします。 たとえば、100,000 4611686014132522708 の合計 4611686014132422708 のサンプルの値に追加する場合、新しい低い部分は 102100 です。 これは、RID マスターによって割り当てられる [次へ] の RID プールが 2100 ではなく 102100 で開始されることを示します。  
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator--"></a>Adsiedit と電卓を使用して、利用可能な RID プールの値を上げる '  
1.  サーバー マネージャーを開き、[**ツール**] をクリック**ADSI Edit**します。    
2.  右クリックし、[**への接続**接続および既定の名前付けコンテキストを実行し、をクリックして**OK**します。
![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi1.png) 
3. 次の識別名のパスを参照: **CN = RID Manager$、CN = System, DC =<domain name>**します。
![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi2.png) 
3.  右クリックし、CN のプロパティ] を選択 = RID Manager$ します。  
4.  属性を選択**rIDAvailablePool**、] をクリックして**編集**、し、大きな整数値をクリップボードにコピーします。
![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi3.png)  
5.  電卓を起動してから、**ビュー**メニューで、**電卓**します。  6.  100,000 を現在の値に追加します。  
![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi4.png) 
7.  Ctrl + c を使用して、または**コピー**コマンドを**編集**メニューで、値をクリップボードにコピーします。  
8.  Adsiedit の編集] ダイアログ ボックスで、この新しい値を貼り付けます。 
![Adsi エディター](media/AD-Forest-Recovery-Raise-RID-Pool/adsi5.png) 
9. をクリックして**OK**ダイアログ ボックスで、および**適用**を更新して、プロパティ シートで、**rIDAvailablePool**属性します。  
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>LDP を使用して、利用可能な RID プールの値を上げる  
  
1.  コマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。  
  
     **ldp**  
  
2.  をクリックして**接続**、] をクリックして**接続**RID マネージャーの名前を入力し、[クリックして**OK**します。  
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp1.png)
3.  をクリックして**接続**、] をクリックして**バインド**を選択**資格情報によるバインド**管理者の資格情報を入力し、をクリックし、**OK**します。  
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp2.png)
4.  をクリックして**ビュー**、] をクリックして**ツリー**し、次の識別名のパスを入力: CN = RID Manager$、CN = System, DC =*ドメイン名*  
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp3.png)
5.  をクリックして**参照**、] をクリックし、**変更**します。  
6.  100,000 に現在追加**rIDAvailablePool**値、し、入力に合計**値**します。  
7.  **Dn**、種類`cn=RID Manager$,cn=System,dc=`*< ドメインの名前 \/>*します。  
8.  **エントリ属性の編集**、種類`rIDAvailablePool`します。  
9. 選択**置換**操作、およびクリックとして**Enter**します。 </br>
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp4.png) 
10. をクリックして**実行**操作を実行します。  をクリックして**閉じる**します。
11. 変更を確認する] をクリックして**ビュー**、] をクリックして**ツリー**、し、次の識別名のパスを入力: CN = RID Manager$、CN = System, DC =*ドメイン名*します。    確認、**rIDAvailablePool**属性です。  
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp5.png)

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
 
