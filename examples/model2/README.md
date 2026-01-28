# 仕様モデルに基づくインサイドアウト開発

```domain
data 社員 = ???
data 出張者 = 社員
data 承認者 = 社員

data 費目 = 交通費
	OR 宿泊費
	OR 交際費

data 出張予定日程 = 出張予定日付
	AND 費目
	AND 予定金額

data 出張予定費用 = List<出張予定日程>

data 出張予定 = 出張目的
  AND 出張期間
  AND List<出張者>
  AND 出張予定費用

data 出張申請 = 出張予定
	AND 申請者
	AND 申請日時

behavior 出張申請する = 出張予定 AND 申請者 AND 申請日時 -> 出張申請

behavior 高額出張かどうか判断する = 出張予定 -> 高額出張 OR　通常出張

behavior 透明性チェック必要な出張かどうか判断する = 出張予定 -> 透明性チェック必要出張 OR 通常出張

data 事前承認OK = 出張申請
	AND 事前承認者
	AND 承認日時

behavior 事前承認が必要か判断する = 出張申請 -> 事前承認必要な出張申請 OR 事前承認不要な出張申請

behavior 上長が事前承認する =  事前承認必要な出張申請 AND 承認者 AND 承認日時 -> 事前承認OK OR 事前承認NG

data 出張実績日程 = 出張実績日付
	AND 費目
	AND 実績金額

data 出張実績費用 = List<出張実績日程>

data 出張実績 = 出張予定
	AND 出張実績費用
	
behavior 出張実績を登録する = 出張予定 AND 出張実績費用 -> 出張実績

data 最終承認 =　出張実績
	AND 最終承認者
	AND 最終承認日時

data 最終承認する = 出張実績 AND 承認者 -> 最終承認
```