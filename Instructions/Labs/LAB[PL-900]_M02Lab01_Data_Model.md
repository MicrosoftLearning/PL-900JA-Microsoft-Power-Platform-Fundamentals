---
lab:
    title: '課題 1: データ モデリング'
    module: 'モジュール 2: Common Data Service の概要'
---

# モジュール 2: Common Data Service の概要
## 課題: データ モデリング

### 重要な注意事項 (有効日: 2020 年 11 月):
Common Data Service は、Microsoft Dataverse に名称が変更されました。Microsoft Dataverse では、用語が一部変更されています。たとえば、「エンティティ」は「テーブル」に変更されました。また Dataverse のデータベースでは、「フィールド」は「列」、「レコード」は「行」と呼ばれます。

アプリケーションは現在ユーザー エクスペリエンスを更新中ですが、「エンティティ」 (現在は **テーブル**) や「フィールド」 (現在は **列**)、「レコード」 (現在は **行**) など Microsoft Dataverse の用語を指す一部の用語が古い用語のまま使用されている可能性があります。ラボに取り組む際は、この点に注意してください。出来る限り早急に、コンテンツを完全に最新版に更新することを予定しています。 

詳細および影響のある用語の一覧は、「[Dataverse とは？](https://docs.microsoft.com/ja-jp/powerapps/maker/common-data-service/data-platform-intro#terminology-updates)」にアクセスしてご確認ください。

# シナリオ

ベローズ カレッジは、キャンパス内に複数の建物を持つ教育機関です。キャンパス訪問は現在、紙の記録簿に記録されています。情報は一貫してキャプチャされず、キャンパス全体の訪問に関するデータを収集して分析する手段はありません。 

キャンパス管理は、建物へのアクセスがセキュリティ担当者によって制御され、すべての訪問がホストによって事前登録され、記録される必要がある訪問者登録システムを近代化したいと考えています。

このコース全体を通して、アプリケーションを構築するとともに自動化を行って、ベローズ・カレッジの管理担当者とセキュリティ担当者がキャンパス内の建物へのアクセスを管理および制御できるようにします。 

この課題では、環境をセットアップし、Common Data Service (CDS) データベースを作成し、変更を追跡するソリューションを作成します。また、次の要件をサポートするデータ モデルも作成します。

-   R1 – キャンパス訪問の場所 (建物) を追跡する
-   R2 – 訪問者を識別し、追跡するための基本情報を記録します 
-   R3 – 訪問をスケジュール、記録、および管理します 

最後に、サンプル データを Common Data Serviceにインポートします。

# ハイレベルのラボ手順

学習環境を準備するには、次の手順を実行します。

* ソリューションと発行元を作成します
* アプリケーション要件を満たすために必要な新規コンポーネントと既存のコンポーネントの両方を追加します。メタデータの説明 (エンティティおよびリレーションシップ) については、「[データ モデル ドキュメント](../../Allfiles/Campus%20Management.png)」を参照してください。Ctrl キーを押しながらクリックするか、リンクを右クリックして、データ モデル ドキュメントを新しいウィンドウで開くことができます。

すべてのカスタマイズが完了すると、ソリューションに複数のエンティティが含まれます。

-   連絡先
-   建物
-   訪問

## 前提条件:

* **モジュール 0 ラボ 0 - ラボ環境の検証**の完了

## 始める前に考慮すべきこと

* 名前付け規則

* データ型、制限事項 (名前の最大長など)

* 簡単なローカライズをサポートする日時の書式設定

# 演習 \#1: ソリューションを作成する

## タスク \#1: ソリューションと発行元を作成する

1.  ソリューションを作成する

    -   <https://make.powerapps.com> に移動します。再認証が必要な場合は、「**サインイン**」 をクリックし、必要に応じて指示に従ってください。

    -   画面の右上隅にある 「**環境**」 をクリックし、ドロップダウン メニューから自分の環境を選択します。

    -   左側のメニューから 「**ソリューション**」 を選択し、「**新しいソリューション**」 をクリックします。

    -   「**表示名**」 に、「**「姓」 キャンパス管理**」と入力します。

2.  発行元を作成する

    -   「**発行元**」 ドロップダウンをクリックし、「**発行元**」 を選択します。

    -   ポップアップ表示されるウィンドウで、「**表示名**」 に「**Bellows College**」と入力します。 
    
    -   「**プレフィックス**」 に「**bc**」と入力します

    -   「**保存して閉じる**」 をクリックします
    
    -   ポップアップ ウィンドウで 「**作成**」 をクリックします。

3.  ソリューションの作成を完了します。

    -   次に、「**発行元**」ドロップダウンをクリックし、「**ベローズ カレッジ**」 を選択します。
        発行元を選択します。

    -   **バージョン** が 「**1.0.0.0**」 に設定されていることを確認します。 
    
    -   「**作成**」 をクリックします。

## タスク \#2: 既存のエンティティを追加する

1.  今作成した **キャンパス管理** ソリューションをクリックして開きます。

2.  「**既存のものを追加**」 をクリックして、「**エンティティ**」 を選択します。

3.  **連絡先** を見つけて選択します。

4.  「**次へ**」 をクリックします。

5.  「連絡先」  の下の 「**コンポーネントの選択**」 をクリックします。

6.  「**ビュー**」 タブを選択し、「**アクティブな連絡先**」 ビューを選択します。クリック
    **追加**。
    
7.  「**コンポーネントを選択**」 を再度クリックします。

8.  「**フォーム**」 タブを選択し、「**連絡先**」 フォームを選択します。
    
9.  「**追加**」 をクリックします。

    > **1 つのビュー** と **1 つのフォーム**が選択されている必要があります。 
    
10.  **「Add」** をもう一度クリックします。これにより、選択したビューとフォームを持つ連絡先エンティティが、新しく作成されたソリューションに追加されます。 
    
11.  ソリューションに次の 1 つのエンティティが追加されました。連絡先。

# 演習 \#2: エンティティとリレーションシップの作成

**目的:** この演習ではエンティティとリレーションシップを作成します
エンティティ間で作成します。

## タスク #1: 建物エンティティとフィールドの作成

1.  キャンパス管理ソリューションに対してブラウザーを開いたままにする必要があります。表示されていない場合は、次の手順でキャンパス管理ソリューションを開きます。

    * サインインします <https: make.powerapps.com> (まだサインインしていない場合)
    
    * 「**ソリューション**」 を選択し、今作成した 「**「姓」 キャンパス管理**」
          ソリューションをクリックして開きます。
          
2.  建物エンティティの作成

    -   **「新規」** をクリックして **「エンティティ」** を選択します。
    
    -   「**表示名**」 に「**建物**」と入力します。 
    
    -   **「完了」** をクリック します。これにより、他のエンティティとフィールドの追加を開始する間に、バックグラウンドでエンティティのプロビジョニングが開始されます。

## タスク #2: 訪問の作成エンティティとフィールド

**訪問** エンティティには、建物、訪問者、スケジュールされた時間、および各訪問の実際の時間を含むキャンパス訪問に関する情報が含まれます。 

訪問チェックイン プロセス中に尋ねられたときに、訪問者が簡単に入力して解釈できる一意の番号を毎回ごとの訪問に割り当てたいと思います。

> 訪問の時刻は常に建物の場所に対してローカルであり、異なるタイム ゾーンから表示しても変更してはならないため、**タイム ゾーンに依存しない** 動作を使用して、日付と時刻の情報を記録します。 

1.  **キャンパス管理** ソリューションを選択します

2. 訪問の作成エンティティ

   * **「新規」** をクリックして **「エンティティ」** を選択します。
   
   * 「**表示名**」 に「**訪問**」と入力します 
   
   * **「完了」** をクリック します。これにより、バックグラウンドでエンティティのプロビジョニングが開始され、他のフィールドの追加を開始できます。

3. スケジュール済みの開始の作成

   * **フィールド** タブを確実に選択して、**「フィールドの追加」** をクリックします。
   
   * **表示名**に対して**スケジュール済みの開始** と入力します。
   
   * **「データ型」** の **「日付と時刻」** を選択します。
   
   * 「**必須**」 フィールドで、「**必須**」 を選択します。
   
   * 「**詳細オプション**」 セクションを展開します。
   
   * 「**動作**」 フィールドで、「**タイム ゾーンに依存しない**」 を選択します。
   
   * **「完了」** をクリック します。

4.  スケジュール済みの終了フィールドの作成

    * **「フィールドの追加」** をクリックします。
    
    * **表示名**に**スケジュール済みの終了**と入力 します。
    
    * **「データ型」** の **「日付と時刻」** を選択します。
    
    * 「**必須**」 フィールドで、「**必須**」 を選択します。
    
    * 「**詳細オプション**」 セクションを展開します。
    
    * 「**動作**」 フィールドで、「**タイム ゾーンに依存しない**」 を選択します。
    
    * **「完了」** をクリック します。
    
5.  実際の開始日フィールドの作成

    * **「フィールドの追加」** をクリックします。
    
    * **表示名**に **実際の開始**と入力します。
    
    * **「データ型」** の **「日付と時刻」** を選択します。
    
    * 「**必須**」 フィールドで、これを 「**省略可能**」 のままにします。
    
    * 「**詳細オプション**」 セクションを展開します。
    
    * 「**動作**」 フィールドで、「**タイム ゾーンに依存しない**」 を選択します。
    
    * **「完了」** をクリック します。
    
6.  実際の終了フィールドの作成

    * **「フィールドの追加」** をクリックします。
    
    * **表示名**に**実際の終了**と入力します。
    
    * **「データ型」** の **「日付と時刻」** を選択します。
    
    * 「**必須**」 フィールドで、これを 「**省略可能**」 のままにします。
    
    * 「**詳細オプション**」 セクションを展開します。
    
    * 「**動作**」 フィールドで、「**タイム ゾーンに依存しない**」 を選択します。
    
    * **「完了」** をクリック します。
    
7.  コード フィールドを作成する

    * **「フィールドの追加」** をクリックします。
    
    * **表示名**に**コード**と入力します。
    
    * **「データ型」** で **「オートナンバー」** を選択します。
    
    * **オートナンバー型**に **「日付接頭辞番号」** を選択します。
    
    * **「完了」** をクリック します。
    
8.  **「エンティティの保存」** をクリックします。

## タスク #3: リレーションシップの作成

1.  **キャンパス管理** ソリューションの **訪問** エンティティを引き続き表示していることを確認します。そうでない場合は、そこに移動します。

2.  訪問と連絡先のリレーションシップを作成します

    * **「リレーションシップ」** タブを選択します。
    
    * **「リレーションシップの追加」** をクリックし、**「多対一」** を選択します。
    
    * **関連する (1 つ)** の **連絡先** を選択します 
    
    * **ルックアップ フィールドの表示名**に**訪問者**を入力 します 
    
    * **「完了」** をクリック します。
    
3.  訪問の建物へのリレーションシップへの作成

    * **「リレーションシップの追加」** をクリックし、**「多対一」** を選択します。
    
    * **関連する (1)** **建物**を選択する 
    
    * **「完了」** をクリック します。
    
4.  **「エンティティの保存」** をクリックします。

5.  トップ メニューから 「**ソリューション**」 を選択し、「**すべて公開のカスタマイズを公開する**」 をクリックします。

# 演習 \#3: データをインポートします

**目的:** この演習では、サンプル データを Common Data Service データベースにインポートします。

## タスク #1: ソリューションをインポートする

このタスクでは、データのインポートを完了するために必要な Power Automate フローを含むソリューションをインポートします。

1. デスクトップに **DataImport_managed.zip** ファイル ストアが必要です。ダウンロードしていない場合は、[データ インポート ソリューション](../../Allfiles/DataImport_managed.zip)をダウンロードしてください。

2. <https://make.powerapps.com> にサインインします。

3. まだ選択されていない場合は、右上にある **[自分のイニシャル] 練習**環境を選択します。

4. 左側のナビゲーション パネルで 「**ソリューション**」 を選択します。

5. 「**インポート**」 をクリックしてから、「**参照**」 をクリックします。デスクトップから **DataImport_managed.zip** を参照して選択し、「**次へ**」 を押します。

>   次のメッセージが表示される場合があります。
>
>   ここに依存関係がありません。このソリューションをインストールする前に、次のソリューションをインストールします。
>
>   このメッセージは、データ モデルが完全でないか、
>   公開元のプレフィックスが **bc** でないか、**建物** と **訪問** エンティティの
>   名前が上記の手順で示した名前とは異なることを示しています。

6. 「**次へ**」 を押します。接続を再確立するように求めるメッセージが表示されます。 

7. 「**接続の選択**」 ドロップダウンを展開し、「**新しい接続**」 を選択します。

8. 新しいブラウザーの画面またはタブが開きます。Common Data Service 接続を作成するように求められたら、「**作成**」 を選択します。接続の作成を完了するために、必要に応じてサインインします。

9. ソリューションをインポートしていた前のタブに戻ります。

10. 「**更新**」 をクリックして、接続のリストを更新します。 

11. 作成した接続が選択されていることを確認します。

12. 「**インポート**」 を押します。

13. インポートが完了するまで待機します。

## タスク #2: データをインポートします  

1. 「**データ インポート**」 ソリューションを開きます。

2. 「**インポートデータ**」 フローの**状態**を確認します。

3. 「**状態**」 が 「**オフ**」 の場合は、「**データのインポート**」 の横にある **...** を選択し、「**オン**」 を選択します。

   > **重要:** エラー メッセージが表示された場合は、作成したエンティティとフィールドが上記の手順と一致していることを確認します。

4. 「**データのインポート**」 コンポーネントを開きます。Power Automate の新しいタブが開きます。 

5. ポップアップが表示された場合は、「**開始**」 をクリックします。 

6. 「**実行**」 をクリックしてから、プロンプトが表示されたら 「**フローの実行**」 をクリックします。

7. **「完了」** をクリック します。

8. フロー インスタンスが実行を完了するまで待機します。**28 日間の実行履歴**テーブルを更新して、フローがいつ実行されたかを確認できます。 

    > このフローの目的は、今後のラボのサンプル データを生成することでした。次のタスクでは、データのインポートが正常に完了したことを確認します。 

## タスク #3: データ インポートを確認します

1. 前の 「Power Apps」 タブに戻ります。ポップアップで 「**完了**」 をクリックします。左側のナビゲーション バーで 「**ソリューション**」 を選択し、「**キャンパス管理**」 ソリューションを開きます。

2. 「**訪問**」 エンティティをクリックして開き、「**データ**」 タブを選択します。

3. 右上の 「**アクティブな訪問**」 をクリックしてビュー セレクタを表示し、「**すべてのフィールド**」 を選択します。これにより、訪問データの表示に使用されているビューが変更されます。 

    > 解像度が低く**アクティブな訪問**が表示されない場合は、同じ場所に目のアイコンが表示されます。

    > インポートが成功した場合は、訪問エントリの一覧が表示されます。

4. 「**建物**」 列の任意の値をクリックし、建物フォームが別のウィンドウで開くことを確認します。 

5. 最近起動したウィンドウを閉じます。

6. 「**訪問者**」 列の任意の値をクリックし (ビューを右にスクロールする必要がある場合があります)、連絡先フォームが別のウィンドウで開くことを確認します。

7. 最近起動したウィンドウを閉じます。

# 課題

* ソリューションの一部として*予定* アクティビティを使用することを検討しますか? 何が変わるでしょうか?
* スケジュールされた開始後にスケジュールされた終了を強制する方法とは? 
* 1 回の訪問で複数の会議のサポートを追加する方法は?
* 外部の連絡先だけでなく、内部スタッフのメンバーに対しても建物のアクセスを保護する方法は?
* 特定の建物を訪問するために、マネージメントの承認を要求する方法は? 承認プロセスはデータ モデルで何が変更されますか?

