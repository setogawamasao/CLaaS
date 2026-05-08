[← README に戻る](../../../README.md)

# 要件定義書

## はじめに

本ドキュメントは、大学生向け「Campus Life as a Service（CLaaS）」の要件を定義するものです。

本アプリは、大学生が楽に単位を取れる授業（楽単）の情報や過去問を共有し合うプラットフォームです。さらに、AIによる自動時間割生成、空きコマ時間に合わせた娯楽・就活コンテンツの提案、空きコマを活用したユーザー間マッチング・コミュニティ機能、AIによるシラバス解析、代返支援機能、企業連携クーポン機能、空きコマ情報の企業提供機能、そして情報投稿を促進するガクチカクレジット（Gakuchika Credit）エコノミーの仕組みを提供します。

---

## 用語集

- **CLaaS**: Campus Life as a Service の略称。本アプリ全体のシステム
- **Campus_Info_App**: CLaaS システムの旧称。本ドキュメント内では CLaaS と同義
- **User**: アプリに登録した大学生ユーザー
- **Post**: 楽単情報または過去問情報の投稿データ
- **Syllabus_Analyzer**: AIによるシラバス解析モジュール
- **Timetable_Generator**: 大学・学部・年度を入力として最適な時間割と半期予定表を自動生成するAIモジュール
- **Token_System**: ガクチカクレジット（Gakuchika Credit）の発行・管理・消費を担うモジュール
- **Content_Recommender**: 空きコマに合わせた娯楽・就活コンテンツを提案するモジュール
- **Auth_Service**: ユーザー認証・認可を担うモジュール
- **Search_Engine**: 授業・過去問の検索機能を担うモジュール
- **University**: 大学を表すエンティティ（大学名・学部・学科情報を含む）
- **Course**: 授業を表すエンティティ（授業名・担当教員・シラバス情報を含む）
- **Past_Exam**: 過去問データ（科目・年度・ファイル情報を含む）
- **Token**: アプリ内で使用される仮想通貨単位。現在の正式名称は「ガクチカクレジット（Gakuchika Credit）」。技術的文脈では Token とも表記する
- **Gakuchika_Credit**: アプリ内で使用される仮想通貨単位。旧称「Token」。ユーザーの情報共有・出席・企業への空きコマ情報提供などの行動に応じて付与・消費される
- **Free_Period**: ユーザーの空きコマ時間帯
- **Semester**: 半期（前期または後期）を表す期間単位
- **Difficulty_Score**: AIが算出する授業の難易度スコア（1〜10の整数値）
- **Attendance_Ticket**: 物理的な出席票を表すエンティティ（固有コード・QRコード・発行者・有効期限・使用状態を含む）
- **Ticket_Issuer**: 出席票を発行するユーザー（物理的な出席票を他のユーザーに渡す側）
- **Ticket_Receiver**: 出席票を受け取り、アプリ上で確認・承認するユーザー
- **Ticket_Code**: 出席票に紐付けられた一意の英数字コード（QRコードのペイロードとしても使用）
- **Ticket_Manager**: 出席票の発行・検証・トークン付与を管理するモジュール
- **Proxy_Attendance**: 代返（他のユーザーの代わりに出席票を提出する行為）
- **Proxy_Requester**: 代返を依頼するユーザー
- **Proxy_Agent**: 代返を引き受けるユーザー
- **Trust_Score**: ユーザーの信頼性を示すスコア（代返の評価実績に基づいて算出）
- **Proxy_Manager**: 代返依頼・受諾・評価・ペナルティを管理するモジュール
- **Matching_Service**: 空きコマが重複するユーザー同士のマッチングを担うモジュール
- **Community**: 共通の趣味・目的を持つユーザーが参加するグループ
- **Chat_Service**: ユーザー間のリアルタイムチャットを担うモジュール
- **Partner_Service**: 企業連携・クーポン発行・管理を担うモジュール
- **Coupon**: 企業が発行するクーポン。使用することでガクチカクレジットを獲得できる
- **Partner**: CLaaS と連携する企業（映画館・出版社・スポッチャ・マイナビ等）
- **Map_Service**: 地図情報を提供し、近隣施設の検索・表示を担うモジュール
- **Marketplace**: 授業テキスト・教材の譲渡・売買を仲介するマーケットプレイス機能全体のモジュール
- **Listing**: マーケットプレイスに出品された教材の出品データ（出品物情報・取引形式・状態・価格等を含む）
- **Listing_Seller**: 教材を出品するユーザー（出品者）
- **Listing_Buyer**: 出品された教材に申し込むユーザー（受取希望者）
- **Transaction**: 出品者と受取者の間で成立した取引データ（取引形式・受け渡し方法・完了状態を含む）
- **Item_Condition**: 出品物の状態を示す区分（良好・書き込みあり・傷あり・その他）
- **Transaction_Type**: 取引形式の区分（無料譲渡・トークン交換・現金取引の3種類）
- **Delivery_Method**: 受け渡し方法の区分（手渡し〔キャンパス内〕または郵送）
- **Seller_Rating**: 取引完了後に受取者が出品者に付ける評価（1〜5の整数値）
- **Buyer_Rating**: 取引完了後に出品者が受取者に付ける評価（1〜5の整数値）
- **Marketplace_Trust_Score**: マーケットプレイスにおける取引評価の加重平均に基づくユーザーの信頼スコア
- **Free_Period_Data**: ユーザーの空きコマ情報（時間帯・曜日・大学・学部）を匿名化・集計した統計データ。個人を特定できる情報は含まない
- **Data_Consent**: ユーザーが空きコマ情報の企業提供に同意する設定。オプトイン方式で管理され、ユーザーはいつでも撤回できる
- **Analytics_Service**: 空きコマ統計データの集計・匿名化・企業向け提供を担うモジュール。Partner_Service と連携して企業向けダッシュボードにデータを提供する

---

## 要件

### 要件1: ユーザー認証・アカウント管理

**ユーザーストーリー:** 大学生として、大学メールアドレスで登録・ログインしたい。そうすることで、自分の大学に関連した情報にアクセスできる。

#### 受け入れ基準

1. WHEN ユーザーが大学メールアドレスとパスワードを入力して登録を試みる, THE Auth_Service SHALL メールアドレスの形式を検証し、確認メールを送信する
2. WHEN ユーザーが確認メールのリンクをクリックする, THE Auth_Service SHALL アカウントを有効化し、ユーザーをログイン済み状態にする
3. WHEN ユーザーが登録済みのメールアドレスとパスワードでログインを試みる, THE Auth_Service SHALL 認証情報を検証し、セッショントークンを発行する
4. IF ログイン試行が5回連続で失敗した場合, THEN THE Auth_Service SHALL アカウントを30分間ロックし、ユーザーにロック通知を送信する
5. WHEN ユーザーがパスワードリセットを要求する, THE Auth_Service SHALL 登録済みメールアドレスにリセット用リンクを送信する
6. THE Auth_Service SHALL パスワードを平文で保存せず、bcryptアルゴリズムでハッシュ化して保存する
7. WHEN ユーザーがプロフィールに大学・学部・学年を登録する, THE CLaaS SHALL その情報をユーザープロフィールに保存する

---

### 要件2: 楽単情報の投稿・閲覧

**ユーザーストーリー:** 大学生として、楽に単位が取れる授業の情報を投稿・閲覧したい。そうすることで、履修計画を効率的に立てられる。

#### 受け入れ基準

1. WHEN ユーザーが楽単情報（授業名・担当教員・評価方法・コメント・難易度評価）を入力して投稿する, THE CLaaS SHALL 投稿データを保存し、同じ大学の他のユーザーに公開する
2. THE CLaaS SHALL 楽単情報を大学・学部・授業名・担当教員名で絞り込み検索できる機能を提供する
3. WHEN ユーザーが授業の楽単情報一覧を閲覧する, THE CLaaS SHALL 投稿日時の新しい順・評価の高い順・閲覧数の多い順で並び替えて表示する
4. WHEN ユーザーが楽単情報に「役に立った」評価を付ける, THE CLaaS SHALL その評価を集計し、投稿の評価スコアに反映する
5. IF 投稿内容が不適切なコンテンツ（個人情報・誹謗中傷・著作権侵害）を含む場合, THEN THE CLaaS SHALL 通報機能を提供し、管理者に通知する
6. WHILE ユーザーが自分の投稿を編集中, THE CLaaS SHALL 投稿者本人のみが編集・削除できる状態を維持する
7. THE CLaaS SHALL 1つの授業に対して複数のユーザーが楽単情報を投稿できる仕組みを提供する

---

### 要件3: 過去問の共有・ダウンロード

**ユーザーストーリー:** 大学生として、授業の過去問をアップロード・ダウンロードしたい。そうすることで、試験対策を効率的に行える。

#### 受け入れ基準

1. WHEN ユーザーが過去問ファイル（PDF・画像形式）と関連情報（授業名・年度・試験種別）を入力してアップロードする, THE CLaaS SHALL ファイルを安全に保存し、同じ大学のユーザーがダウンロードできる状態にする
2. THE CLaaS SHALL アップロード可能なファイル形式をPDF・PNG・JPG・JPEGに限定し、1ファイルあたりの最大サイズを50MBとする
3. WHEN ユーザーが過去問をダウンロードする, THE CLaaS SHALL ダウンロード数を記録し、投稿者のガクチカクレジット残高に1クレジットを加算する
4. THE Search_Engine SHALL 過去問を大学・学部・授業名・年度・試験種別で検索できる機能を提供する
5. IF アップロードされたファイルがウイルス検査で問題を検出した場合, THEN THE CLaaS SHALL そのファイルを隔離し、アップロードユーザーに通知する
6. WHEN ユーザーが過去問の著作権侵害を通報する, THE CLaaS SHALL 該当ファイルを一時非公開にし、管理者に通知する
7. THE CLaaS SHALL 過去問のプレビュー機能（PDFの1ページ目・画像のサムネイル）をダウンロード前に提供する

---

### 要件4: AIによるシラバス解析

**ユーザーストーリー:** 大学生として、シラバスをAIに解析させて授業の難易度や楽さを客観的に評価してほしい。そうすることで、履修選択の判断材料を得られる。

#### 受け入れ基準

1. WHEN ユーザーがシラバスのテキストまたはPDFファイルをアップロードする, THE Syllabus_Analyzer SHALL シラバスの内容を解析し、Difficulty_Scoreと評価根拠を生成する
2. THE Syllabus_Analyzer SHALL Difficulty_Scoreを1（非常に楽）から10（非常に難しい）の整数値で算出する
3. THE Syllabus_Analyzer SHALL 評価根拠として「出席要件」「試験の有無」「レポート課題の量」「成績評価方法」の各項目を個別に分析した結果を提供する
4. WHEN シラバス解析が完了する, THE Syllabus_Analyzer SHALL 解析結果を対応する授業の楽単情報ページに表示する
5. IF シラバスのテキストが解析に不十分な情報量（500文字未満）である場合, THEN THE Syllabus_Analyzer SHALL ユーザーに追加情報の入力を求めるメッセージを表示する
6. THE Syllabus_Analyzer SHALL シラバスのテキストを解析する際、個人情報（教員の連絡先等）を解析結果に含めない
7. WHEN 同一授業のシラバスが複数回解析される, THE Syllabus_Analyzer SHALL 最新の解析結果を保持しつつ、過去の解析履歴を参照できる状態を維持する

---

### 要件5: 空きコマへの娯楽・就活コンテンツ提案

**ユーザーストーリー:** 大学生として、空きコマの時間に合わせた娯楽や就活コンテンツを提案してほしい。そうすることで、空き時間を有効活用できる。

#### 受け入れ基準

1. WHEN ユーザーが時間割を登録する, THE CLaaS SHALL 空きコマの時間帯（Free_Period）を自動的に算出する
2. WHEN ユーザーが空きコマ中にアプリを開く, THE Content_Recommender SHALL 残り時間と登録済みの興味・関心カテゴリに基づいてコンテンツを提案する
3. THE Content_Recommender SHALL 娯楽コンテンツ（動画・音楽・ゲーム・読書）と就活コンテンツ（インターン情報・企業説明会・自己分析ツール・業界研究）の2カテゴリでコンテンツを提供する
4. WHEN ユーザーがコンテンツの興味・関心カテゴリを設定する, THE Content_Recommender SHALL その設定を保存し、以降の提案に反映する
5. THE Content_Recommender SHALL 空きコマの残り時間が30分未満の場合は短時間で完結するコンテンツを、60分以上の場合はより深いコンテンツを優先して提案する
6. WHEN ユーザーが提案されたコンテンツを「興味なし」と評価する, THE Content_Recommender SHALL 同カテゴリの類似コンテンツの提案頻度を下げる
7. WHERE ユーザーが就活モードを有効にしている場合, THE Content_Recommender SHALL 就活関連コンテンツを娯楽コンテンツより優先して提案する
8. WHEN ユーザーの半期予定表が登録されている, THE Content_Recommender SHALL 各Free_Periodの時間長に応じた娯楽コンテンツ・就活情報・資格取得情報（必要な学習時間を含む）をレコメンドする
9. WHEN ユーザーが娯楽コンテンツの地図情報を要求する, THE Map_Service SHALL ユーザーの現在地または指定地点から近隣の映画館・美術館・カフェ等の施設を地図上に表示する
10. THE Content_Recommender SHALL 空きコマの残り時間内に読了可能な漫画・書籍を提案する際、作品の平均読了時間がFree_Periodの残り時間以内であることを条件として絞り込む
11. WHEN ユーザーが読書コンテンツの提案を要求する, THE Content_Recommender SHALL 空きコマの残り時間（分単位）と平均読了時間が一致する漫画・書籍を優先して提案する

---

### 要件6: ガクチカクレジットエコノミー

**ユーザーストーリー:** 大学生として、楽単情報や過去問を投稿・授業に出席・レビューを投稿することでガクチカクレジットを獲得し、そのクレジットで娯楽・就活コンテンツにアクセスしたい。そうすることで、情報共有への動機付けが生まれる。

#### 受け入れ基準

1. WHEN ユーザーが楽単情報を新規投稿する, THE Token_System SHALL そのユーザーのガクチカクレジット残高に5クレジット（基礎点）を加算する
2. WHEN ユーザーが過去問を新規アップロードする, THE Token_System SHALL そのユーザーのガクチカクレジット残高に10クレジット（基礎点）を加算する
3. WHEN ユーザーがノートまたはレポートを新規アップロードする, THE Token_System SHALL そのユーザーのガクチカクレジット残高に8クレジット（基礎点）を加算する
4. WHEN ユーザーが授業評価（レビュー）を新規投稿する, THE Token_System SHALL そのユーザーのガクチカクレジット残高に3クレジット（基礎点）を加算する
5. WHEN 他のユーザーがユーザーの投稿に「役に立った」評価を付ける, THE Token_System SHALL 投稿者のガクチカクレジット残高に1クレジット（動的報酬）を加算する
6. WHEN ユーザーが授業に出席し出席記録が確認される, THE Token_System SHALL そのユーザーのガクチカクレジット残高に2クレジットを加算する
7. THE Token_System SHALL 最初のSemester（初回登録後の最初の半期）は自動時間割生成機能を含む全機能を無料で提供し、2学期目以降は課金またはガクチカクレジット消費によるアクセスを要求する
8. WHEN ユーザーがガクチカクレジットを消費してプレミアムコンテンツにアクセスする, THE Token_System SHALL クレジット残高を消費量分だけ減算し、残高が0を下回らないことを保証する
9. IF ユーザーのガクチカクレジット残高がプレミアムコンテンツのアクセスに必要なクレジット数を下回る場合, THEN THE Token_System SHALL アクセスを拒否し、必要なクレジット数と現在の残高をユーザーに通知する
10. THE Token_System SHALL ガクチカクレジットの全取引履歴（発行・消費・日時・理由・種別）をユーザーが参照できる形で保存する
11. THE Token_System SHALL ガクチカクレジットの不正取得（同一コンテンツの重複投稿・自己評価）を検出し、不正と判定した場合はクレジットを付与しない
12. WHEN ユーザーが投稿を削除する, THE Token_System SHALL その投稿によって付与された基礎点クレジットをユーザーの残高から回収する

---

### 要件7: 大学・授業データ管理

**ユーザーストーリー:** 大学生として、自分の大学・学部・授業を正確に選択・登録したい。そうすることで、関連性の高い情報のみを閲覧できる。

#### 受け入れ基準

1. THE CLaaS SHALL 日本国内の大学データベースを保持し、ユーザーが大学名・学部・学科を選択できる機能を提供する
2. WHEN ユーザーが大学名を入力する, THE Search_Engine SHALL 入力文字列に部分一致する大学名の候補を最大10件表示する
3. WHEN 管理者が新しい大学・学部・学科データを登録する, THE CLaaS SHALL そのデータを即時にユーザーの選択肢に反映する
4. IF ユーザーが登録されていない大学・学部・学科を入力した場合, THEN THE CLaaS SHALL ユーザーに追加申請フォームを提示し、管理者に承認依頼を送信する
5. THE CLaaS SHALL 同一授業の情報が複数の投稿に分散しないよう、授業エンティティ（Course）を一意に管理する仕組みを提供する

---

### 要件8: シラバスのパース・フォーマット

**ユーザーストーリー:** 大学生として、様々な形式のシラバスをアップロードしても正確に解析してほしい。そうすることで、手動入力の手間なく解析結果を得られる。

#### 受け入れ基準

1. WHEN ユーザーがPDF形式のシラバスをアップロードする, THE Syllabus_Analyzer SHALL PDFからテキストを抽出し、構造化されたシラバスオブジェクトに変換する
2. THE Syllabus_Analyzer SHALL 構造化されたシラバスオブジェクトを標準フォーマット（JSON形式）に変換して出力する
3. THE Syllabus_Analyzer SHALL 標準フォーマットのシラバスオブジェクトを再度テキスト形式に変換できる（ラウンドトリップ変換）
4. FOR ALL 有効なシラバスオブジェクト, THE Syllabus_Analyzer SHALL テキスト変換後に再度パースした結果が元のオブジェクトと等価であることを保証する（ラウンドトリップ特性）
5. IF PDFからのテキスト抽出に失敗した場合, THEN THE Syllabus_Analyzer SHALL ユーザーにテキスト形式での手動入力を促すエラーメッセージを表示する
6. THE Syllabus_Analyzer SHALL 解析対象のシラバスから「授業名」「担当教員」「評価方法」「授業概要」「到達目標」の各フィールドを抽出する

---

### 要件9: 通知機能

**ユーザーストーリー:** 大学生として、自分の投稿への反応やトークン獲得をリアルタイムで通知してほしい。そうすることで、アプリへの関与度を高められる。

#### 受け入れ基準

1. WHEN 他のユーザーがユーザーの投稿に「役に立った」評価を付ける, THE CLaaS SHALL 投稿者にプッシュ通知またはアプリ内通知を送信する
2. WHEN ユーザーがガクチカクレジットを獲得する, THE Token_System SHALL ユーザーにクレジット獲得の通知（獲得量・理由）を送信する
3. WHEN ユーザーの投稿が管理者によって削除・非公開にされる, THE CLaaS SHALL 投稿者に理由を含む通知を送信する
4. WHEN 空きコマが始まる15分前, THE Content_Recommender SHALL ユーザーにコンテンツ提案の通知を送信する
5. WHILE ユーザーが通知設定でプッシュ通知をオフにしている, THE CLaaS SHALL プッシュ通知を送信せず、アプリ内通知のみを提供する

---

### 要件10: プライバシーとデータ保護

**ユーザーストーリー:** 大学生として、自分の個人情報が適切に保護されることを確認したい。そうすることで、安心してアプリを利用できる。

#### 受け入れ基準

1. THE CLaaS SHALL ユーザーの個人情報（氏名・メールアドレス・大学情報）を暗号化して保存する
2. WHEN ユーザーがアカウント削除を要求する, THE CLaaS SHALL 30日以内にユーザーの個人情報を完全に削除する
3. THE CLaaS SHALL ユーザーの同意なしに個人情報を第三者に提供しない
4. WHEN ユーザーが自分のデータのエクスポートを要求する, THE CLaaS SHALL 30日以内にJSON形式でユーザーデータを提供する
5. THE CLaaS SHALL 個人情報保護法（日本）および関連法規に準拠したプライバシーポリシーを提供する

---

### 要件11: 物理的出席票によるトークン付与

**ユーザーストーリー:** 大学生として、他のユーザーに物理的な出席票を渡した際にトークンを獲得したい。そうすることで、リアルな情報共有行動が報酬として認められ、コミュニティへの貢献意欲が高まる。

#### 受け入れ基準

1. WHEN ユーザーが出席票の発行を要求する, THE Ticket_Manager SHALL 一意のTicket_Codeを生成し、そのコードを埋め込んだQRコードとともにTicket_Issuerのアプリ画面に表示する
2. THE Ticket_Manager SHALL 生成するTicket_Codeを英数字32文字以上のランダム文字列とし、推測不可能な形式で生成する
3. WHEN Ticket_ReceiverがQRコードをスキャンまたはTicket_Codeを手動入力する, THE Ticket_Manager SHALL そのコードの有効性（存在・未使用・有効期限内）を検証する
4. WHEN Ticket_ReceiverがTicket_Codeの受け取りを承認する, THE Token_System SHALL Ticket_Issuerのガクチカクレジット残高に3クレジットを加算する
5. THE Ticket_Manager SHALL 各Ticket_Codeの有効期限を発行から24時間以内に設定し、期限切れのコードによるトークン付与を拒否する
6. IF Ticket_ReceiverとTicket_Issuerが同一ユーザーである場合, THEN THE Ticket_Manager SHALL 承認を拒否し、自己承認によるトークン付与を行わない
7. IF 同一のTicket_Codeが既に使用済みである場合, THEN THE Ticket_Manager SHALL 承認を拒否し、重複付与を防止する
8. THE Ticket_Manager SHALL 1人のTicket_Issuerが同一のTicket_Receiverに対して付与できるトークンを24時間あたり1回に制限する
9. THE Ticket_Manager SHALL 出席票の全取引履歴（発行者・受取者・コード・承認日時・付与トークン数）をToken_Systemの取引履歴と連携して保存する
10. WHEN Ticket_ReceiverがTicket_Codeの検証に失敗する, THE Ticket_Manager SHALL 失敗理由（無効なコード・期限切れ・使用済み・自己承認不可）をTicket_Receiverに通知する
11. THE Ticket_Manager SHALL 短時間に大量のTicket_Codeを発行するユーザー（1時間あたり10件超）を不正利用の疑いとして検出し、管理者に通知する
12. WHEN Ticket_Issuerがガクチカクレジットを獲得する, THE Token_System SHALL 獲得理由として「出席票承認」と承認者のユーザーIDをクレジット取引履歴に記録する

---

### 要件12: AIによる自動時間割生成

**ユーザーストーリー:** 大学生として、大学・学部・年度を入力するだけでAIが最も労力の少ない時間割と半期分の予定表を自動生成してほしい。そうすることで、履修計画の手間を大幅に削減できる。

#### 受け入れ基準

1. WHEN ユーザーが大学・学部・年度・希望取得単位数を入力する, THE Timetable_Generator SHALL 登録済みの楽単情報・Difficulty_Score・過去の履修データを参照し、最も総合的な労力が少ない時間割候補を3パターン以上生成する
2. WHEN Timetable_Generatorが時間割を生成する, THE Timetable_Generator SHALL 生成した時間割に基づいてSemester単位（半期分）の予定表を自動生成し、ユーザーのカレンダーに反映する
3. THE Timetable_Generator SHALL 時間割生成の根拠として、各授業のDifficulty_Score・出席要件・試験日程・レポート締切を含む評価理由を提示する
4. THE CLaaS SHALL 最初のSemesterにおける自動時間割生成機能を無料で提供する
5. WHEN ユーザーが2学期目以降に自動時間割生成機能を利用する, THE CLaaS SHALL 課金またはトークン消費によるアクセスを要求する
6. WHEN ユーザーが生成された時間割を手動で編集する, THE Timetable_Generator SHALL 編集後の時間割に基づいて半期予定表を再計算し更新する
7. IF 指定された大学・学部のシラバスデータが不足している場合, THEN THE Timetable_Generator SHALL ユーザーに不足データの手動入力を促し、入力されたデータを元に時間割生成を実行する
8. THE Timetable_Generator SHALL 生成した時間割の空きコマ情報をContent_RecommenderおよびMatching_Serviceと連携して提供する

---

### 要件13: 代返機能

**ユーザーストーリー:** 大学生として、やむを得ない事情で授業に出席できない場合に代返を依頼し、また他のユーザーの代返を引き受けることでトークンを獲得したい。そうすることで、相互扶助のコミュニティが形成される。

#### 受け入れ基準

1. WHEN Proxy_Requesterが代返依頼を作成する, THE Proxy_Manager SHALL 依頼内容（授業名・日時・教室・報酬トークン数）を登録し、同じ大学の対象授業に出席可能なユーザーに通知する
2. WHEN Proxy_Agentが代返依頼を受諾する, THE Proxy_Manager SHALL 依頼ステータスを「受諾済み」に更新し、Proxy_RequesterとProxy_Agentの双方に確認通知を送信する
3. WHEN Proxy_Agentが代返を完了し出席確認コードを提出する, THE Proxy_Manager SHALL 提出されたコードの有効性を検証し、有効な場合はProxy_RequesterのガクチカクレジットをProxy_Agentに移転する
4. WHEN 代返取引が完了する, THE Proxy_Manager SHALL Proxy_RequesterとProxy_Agentの双方に相互評価（1〜5の整数値）の入力を要求する
5. WHEN ユーザーが相互評価を入力する, THE Proxy_Manager SHALL 評価値を集計し、対象ユーザーのTrust_Scoreを更新する
6. THE Proxy_Manager SHALL Trust_Scoreを過去の代返取引における評価の加重平均（直近10件を重視）で算出し、1.0〜5.0の範囲で管理する
7. WHILE ユーザーのTrust_Scoreが4.0以上である, THE Proxy_Manager SHALL そのユーザーを代返依頼の優先候補として上位表示する
8. IF Proxy_Agentが代返を実際には実行せず不正が確認された場合, THEN THE Proxy_Manager SHALL Proxy_AgentのTrust_Scoreから2.0ポイントを減算し、受け取ったガクチカクレジットを没収してProxy_Requesterに返還する
9. IF ユーザーのTrust_Scoreが2.0を下回る場合, THEN THE Proxy_Manager SHALL そのユーザーの代返依頼受諾機能を30日間停止する
10. THE Proxy_Manager SHALL 代返取引の全履歴（依頼者・代行者・授業・日時・評価・トークン移転額）を保存し、管理者が参照できる状態を維持する
11. THE Proxy_Manager SHALL 1ユーザーが同一授業に対して依頼できる代返回数を1学期あたり3回以内に制限する

---

### 要件14: 空きコママッチング・コミュニティ機能

**ユーザーストーリー:** 大学生として、空きコマが被っている他のユーザーとマッチングし、共通の趣味を持つコミュニティに参加したい。そうすることで、大学生活をより充実させられる。

#### 受け入れ基準

1. WHEN ユーザーがマッチング機能を有効にする, THE Matching_Service SHALL 同じ大学内でFree_Periodが重複する他のユーザーを検索し、共通の空きコマ時間帯・興味カテゴリに基づいてマッチング候補を提示する
2. WHEN 2人のユーザーが相互にマッチングを承認する, THE Matching_Service SHALL 両ユーザー間のチャットセッションをChat_Serviceに作成する
3. THE Chat_Service SHALL マッチングしたユーザー間のリアルタイムテキストチャット機能を提供する
4. WHEN ユーザーがコミュニティへの参加を申請する, THE CLaaS SHALL 申請を受理し、ユーザーをコミュニティメンバーとして登録する
5. THE CLaaS SHALL 以下のカテゴリのコミュニティを提供する：スポーツ（野球・テニス等）・ボードゲーム（麻雀・カタン等）・ゲーム（スマブラ・フォートナイト等）・合コン参加者募集・バイト募集・その他趣味
6. WHEN ユーザーがコミュニティ内でメッセージを投稿する, THE Chat_Service SHALL そのコミュニティの全メンバーにメッセージを配信する
7. THE Matching_Service SHALL マッチング候補の提示にあたり、ユーザーのプライバシー設定を尊重し、マッチング機能をオフにしているユーザーを候補から除外する
8. WHEN ユーザーがコミュニティを新規作成する, THE CLaaS SHALL コミュニティ名・カテゴリ・説明・公開設定（公開・大学限定・招待制）を登録し、作成者をコミュニティ管理者として設定する
9. IF コミュニティ内で不適切なコンテンツが通報された場合, THEN THE CLaaS SHALL 該当メッセージを非表示にし、管理者に通知する

---

### 要件15: 企業連携・クーポン機能

**ユーザーストーリー:** 大学生として、連携企業のクーポンを利用することでガクチカクレジットを獲得し、就活・娯楽サービスをお得に活用したい。そうすることで、アプリ利用と実生活の両方でメリットを得られる。

#### 受け入れ基準

1. THE Partner_Service SHALL 映画館・出版社・スポッチャ・マイナビ等のPartnerがCLaaSと連携し、クーポンを発行・管理できる機能を提供する
2. WHEN Partnerがクーポンを発行する, THE Partner_Service SHALL クーポン情報（内容・有効期限・付与クレジット数・利用条件・発行数上限）を登録し、対象ユーザーに配信する
3. WHEN ユーザーがクーポンを使用する, THE Partner_Service SHALL クーポンの有効性（有効期限・使用済み・発行数上限）を検証し、有効な場合はユーザーのガクチカクレジット残高にクーポンに設定されたクレジット数を加算する
4. IF クーポンが既に使用済みまたは有効期限切れである場合, THEN THE Partner_Service SHALL 使用を拒否し、失敗理由をユーザーに通知する
5. THE Partner_Service SHALL Partnerが発行したクーポンの使用状況（使用数・残数・使用日時・ユーザー属性の集計）をPartner向けダッシュボードで提供する
6. THE Partner_Service SHALL 1ユーザーが同一クーポンを使用できる回数をクーポン設定に従って制限する（デフォルト：1回）
7. WHEN ユーザーがクーポンを使用する, THE Token_System SHALL 獲得理由として「クーポン使用」とPartner名・クーポンIDをガクチカクレジット取引履歴に記録する
8. THE CLaaS SHALL Partnerのクーポン情報をContent_Recommenderと連携し、ユーザーの興味カテゴリおよびFree_Periodに合わせたクーポンを優先して提案する

---

### 要件16: 授業テキスト・教材の譲渡マーケットプレイス

**ユーザーストーリー:** 大学生として、授業が終わって不要になった教科書・テキスト・プリント・参考書などを他のユーザーに譲渡・売却したい。また、同じ大学・学部の後輩や同学年のユーザーとして、必要な教材を入手したい。そうすることで、教材の有効活用とコスト削減が実現できる。

#### 受け入れ基準

1. WHEN Listing_Sellerが出品情報（教材名・著者・出版社・授業との紐付け・Item_Condition・Transaction_Type・価格またはトークン数・Delivery_Method・説明文・写真）を入力して出品を登録する, THE Marketplace SHALL 出品データをListingとして保存し、同じ大学・学部のユーザーに公開する
2. THE Marketplace SHALL Transaction_Typeとして「無料譲渡」「トークン交換」「現金取引」の3種類をサポートし、Listing_Sellerが出品時にいずれか1つを選択できる機能を提供する
3. THE Marketplace SHALL Item_Conditionとして「良好」「書き込みあり」「傷あり」「その他」の4区分をサポートし、Listing_Sellerが出品時に必ず1つを選択することを要求する
4. WHEN Listing_SellerがListingをCourseエンティティと紐付ける, THE Marketplace SHALL その授業を履修済みまたは履修中のユーザーに対してListingを優先表示する
5. THE Marketplace SHALL Listingを大学・学部・授業名・教材名・Transaction_Type・Item_Conditionで絞り込み検索できる機能を提供する
6. WHEN Listing_BuyerがListingへの申し込みを送信する, THE Marketplace SHALL 申し込みをListing_Sellerに通知し、Listing_Sellerが承認または拒否できる状態にする
7. WHEN Listing_SellerがListing_Buyerの申し込みを承認する, THE Marketplace SHALL TransactionステータスをTransactionを「取引中」に更新し、双方のユーザーにChat_Serviceを通じた連絡手段を提供する
8. WHEN Transaction_Typeが「トークン交換」であり取引が完了する, THE Token_System SHALL Listing_BuyerのガクチカクレジットをListing_Sellerに移転し、移転理由として「教材取引」とListing IDをガクチカクレジット取引履歴に記録する
9. WHEN Transaction_Typeが「無料譲渡」であり取引が完了する, THE Token_System SHALL Listing_Sellerのガクチカクレジット残高に5クレジットを加算し、加算理由として「無料教材譲渡」とListing IDをガクチカクレジット取引履歴に記録する
10. WHEN 取引が完了する, THE Marketplace SHALL Listing_SellerとListing_Buyerの双方に相互評価（Seller_RatingおよびBuyer_Rating：1〜5の整数値）の入力を要求する
11. WHEN ユーザーが評価を入力する, THE Marketplace SHALL 評価値を集計し、対象ユーザーのMarketplace_Trust_Scoreを更新する
12. THE Marketplace SHALL Marketplace_Trust_Scoreを過去の取引評価の加重平均（直近10件を重視）で算出し、1.0〜5.0の範囲で管理する
13. WHILE Listing_SellerのMarketplace_Trust_Scoreが4.0以上である, THE Marketplace SHALL そのユーザーの出品物を検索結果の上位に表示する
14. IF Listing_Sellerが存在しない商品または著作権侵害コンテンツ（違法コピー・スキャンデータ等）を出品していることが通報された場合, THEN THE Marketplace SHALL 該当Listingを即時非公開にし、管理者に通知する
15. IF Listing_Sellerが出品した商品が著作権侵害と管理者に判定された場合, THEN THE Marketplace SHALL そのListingを削除し、Listing_SellerのMarketplace_Trust_Scoreから1.0ポイントを減算する
16. THE Marketplace SHALL 1ユーザーが同時に出品できるListingの上限を20件とし、上限を超える出品登録を拒否する
17. WHEN Listing_Sellerが出品を取り消す, THE Marketplace SHALL 取引中でないListingのみ取り消しを許可し、取引中のListingの取り消しを拒否する
18. WHEN Delivery_Methodが「手渡し（キャンパス内）」である, THE Marketplace SHALL 受け渡し場所としてキャンパス内の場所を指定できる機能を提供する
19. THE Marketplace SHALL 出品写真のアップロードを最大5枚まで許可し、1枚あたりの最大ファイルサイズを10MBとし、対応形式をPNG・JPG・JPEGに限定する
20. WHEN ユーザーがマーケットプレイスのトップページを閲覧する, THE Marketplace SHALL ユーザーのプロフィールに登録された大学・学部・履修授業に関連するListingを優先して表示する
21. THE Marketplace SHALL 取引の全履歴（出品者・受取者・教材名・Transaction_Type・Delivery_Method・完了日時・評価）を保存し、管理者が参照できる状態を維持する
22. IF Transaction_Typeが「トークン交換」であり、Listing_BuyerのガクチカクレジットがListingに設定されたクレジット数を下回る場合, THEN THE Marketplace SHALL 申し込みを拒否し、必要なクレジット数と現在の残高をListing_Buyerに通知する

---

### 要件17: 空きコマ情報の企業提供機能

**ユーザーストーリー:** 大学生として、自分の空きコマ情報を企業に提供することに同意することでガクチカクレジットを獲得したい。そうすることで、プライバシーを守りながら情報提供の対価を得られる。また、企業として、大学生の空きコマ統計情報を活用してマーケティング・広告配信・採用活動を効率化したい。

#### 受け入れ基準

1. WHEN ユーザーが空きコマ情報の企業提供に同意する（Data_Consentをオンにする）, THE Analytics_Service SHALL ユーザーの同意状態を記録し、以降の統計集計対象にユーザーを含める
2. WHEN ユーザーがData_Consentをオンにする, THE Token_System SHALL そのユーザーのガクチカクレジット残高に10クレジットを加算し、加算理由として「空きコマ情報提供同意」をガクチカクレジット取引履歴に記録する
3. WHEN ユーザーがData_Consentをオフにする（同意を撤回する）, THE Analytics_Service SHALL ユーザーの同意状態を即時に「撤回済み」に更新し、以降の統計集計対象からユーザーを除外する
4. THE Analytics_Service SHALL Data_Consentを取得する際、オプトイン方式（デフォルトはオフ）を採用し、ユーザーが明示的に同意操作を行った場合のみ同意状態をオンに設定する
5. THE Analytics_Service SHALL 企業に提供するデータをFree_Period_Data（大学名・学部・曜日・時限・同意ユーザー数の集計値）のみとし、個人を特定できる情報（氏名・メールアドレス・ユーザーID等）を一切含めない
6. THE Analytics_Service SHALL 集計単位が5名未満となる組み合わせ（大学・学部・曜日・時限）のFree_Period_Dataを企業向けに提供せず、個人の特定リスクを排除する
7. WHEN Partnerが企業向けダッシュボードにアクセスする, THE Analytics_Service SHALL Partner_Serviceと連携し、大学名・学部・曜日・時限・同意ユーザー数の集計データを表示する
8. WHEN Partnerが企業向けダッシュボードでFree_Period_Dataのエクスポートを要求する, THE Analytics_Service SHALL CSV形式で集計データをエクスポートする機能を提供する
9. THE Analytics_Service SHALL Free_Period_Dataの集計に使用するユーザーの空きコマ情報を、Timetable_Generatorが生成した時間割データから取得する
10. WHILE ユーザーのData_Consentがオフである, THE Analytics_Service SHALL そのユーザーの空きコマ情報を統計集計に使用しない状態を維持する
11. IF ユーザーがアカウント削除を要求した場合, THEN THE Analytics_Service SHALL そのユーザーのData_Consentを即時に撤回済みに設定し、以降の統計集計からユーザーのデータを除外する
12. THE CLaaS SHALL 個人情報保護法（日本）に準拠し、Data_Consentの取得・管理・撤回の全プロセスを要件10のプライバシーポリシーと整合した形で運用する
13. WHEN ユーザーがData_Consentの設定画面を開く, THE CLaaS SHALL 提供されるデータの内容（大学名・学部・曜日・時限・人数の集計のみ）・利用目的（マーケティング・採用活動等）・同意撤回の方法を明示した説明文を表示する
14. THE Analytics_Service SHALL Free_Period_Dataの集計結果を24時間ごとに更新し、企業向けダッシュボードに最新の統計データを提供する

---

[← README に戻る](../../../README.md)
