# Job Compass MVP - Google Apps Script コード集

このファイルに記載されたコードを Google スプレッドシート内に「Apps Script」として登録することで、より高度な自動化が可能です。

---

## 準備方法

```
1. Google スプレッドシート を開く
2. メニュー → 拡張機能 → Apps Script
3. 新規プロジェクトを作成
4. 下記のコードをコピー＆ペースト
5. 保存して実行
```

---

## コード1: スコアリング関数の自動化

```javascript
/**
 * 案件スコアを計算する関数
 * @param {number} hourlyRate - 時給（単価÷時間）
 * @param {number} clientRating - 発注者評価（0-5）
 * @param {boolean} beginnerOK - 初心者OK フラグ
 * @param {string} riskLevel - リスクレベル（低/中/高）
 * @param {boolean} continuing - 継続案件 フラグ
 * @return {number} スコア（0-100）
 */
function calculateScore(hourlyRate, clientRating, beginnerOK, riskLevel, continuing) {
  let score = 0;

  // 1. 報酬の妥当性（25点）
  if (hourlyRate >= 1200) {
    score += 25;
  } else if (hourlyRate >= 1000) {
    score += 20;
  } else if (hourlyRate >= 800) {
    score += 15;
  } else if (hourlyRate >= 600) {
    score += 10;
  } else {
    score += 0;
  }

  // 2. 発注者の信頼度（20点）
  if (clientRating >= 4.5) {
    score += 20;
  } else if (clientRating >= 4.0) {
    score += 17;
  } else if (clientRating >= 3.5) {
    score += 14;
  } else if (clientRating >= 3.0) {
    score += 10;
  } else {
    score += 5;
  }

  // 3. 初心者向け度（15点）
  score += beginnerOK ? 15 : 7;

  // 4. リスク判定（15点）
  if (riskLevel === "低") {
    score += 15;
  } else if (riskLevel === "中") {
    score += 7;
  } else {
    score += 0; // 高リスク
  }

  // 5. 継続可能性（10点）
  score += continuing ? 10 : 0;

  // 6. スキルマッチ度（10点）
  score += 10;

  // 7. 作業内容の明確性（5点）
  score += 5;

  // スコアを 0-100 の範囲で制限
  return Math.max(0, Math.min(100, score));
}
```

---

## コード2: リスク判定関数

```javascript
/**
 * リスク度を判定する関数
 * @param {string} jobTitle - 案件タイトル
 * @param {string} description - 案件説明
 * @param {number} hourlyRate - 時給
 * @return {Object} リスク情報 {level: "低/中/高", score: 0-100, keywords: []}
 */
function assessRisk(jobTitle, description, hourlyRate) {
  const fullText = (jobTitle + " " + description).toLowerCase();
  
  // リスク判定用のキーワードリスト
  const dangerKeywords = [
    "line登録", "line誘導", "ライン",
    "メルマガ", "メール登録",
    "報酬なし", "テスト記事", "テスト案件",
    "月100万", "月50万", "稼ぐ", "ビジネスノウハウ"
  ];
  
  const warningKeywords = [
    "成果型", "相談しながら", "単価要相談",
    "報酬要相談", "内容は応募後"
  ];

  let detectedDangerKeywords = [];
  let detectedWarningKeywords = [];
  let riskScore = 0;

  // 危険キーワードの検出
  for (let keyword of dangerKeywords) {
    if (fullText.includes(keyword)) {
      detectedDangerKeywords.push(keyword);
      riskScore += 20;
    }
  }

  // 注意キーワードの検出
  for (let keyword of warningKeywords) {
    if (fullText.includes(keyword)) {
      detectedWarningKeywords.push(keyword);
      riskScore += 10;
    }
  }

  // 時給による判定
  if (hourlyRate < 600) {
    riskScore += 30;
    if (!detectedDangerKeywords.includes("時給低")) {
      detectedDangerKeywords.push("時給が著しく低い（" + hourlyRate + "円）");
    }
  } else if (hourlyRate < 800) {
    riskScore += 15;
  }

  // リスクレベルの決定
  let riskLevel;
  if (riskScore >= 65 || detectedDangerKeywords.length >= 3) {
    riskLevel = "高";
  } else if (riskScore >= 35 || detectedWarningKeywords.length >= 3) {
    riskLevel = "中";
  } else {
    riskLevel = "低";
  }

  return {
    level: riskLevel,
    score: Math.min(100, riskScore),
    dangerKeywords: detectedDangerKeywords,
    warningKeywords: detectedWarningKeywords
  };
}
```

---

## コード3: 推奨度ランクを返す関数

```javascript
/**
 * スコアから推奨度ランクを返す関数
 * @param {number} score - スコア（0-100）
 * @param {string} riskLevel - リスクレベル（低/中/高）
 * @return {string} 推奨度ランク（S/A/B/C/D）
 */
function getRecommendationRank(score, riskLevel) {
  // リスク「高」の場合は初心者ユーザーは D ランク
  if (riskLevel === "高") {
    return "D ⛔ 避けた方が無難";
  }

  // スコアに基づくランク判定
  if (score >= 85) {
    return "S ⭐⭐⭐⭐⭐ 今すぐ応募！";
  } else if (score >= 70) {
    return "A ⭐⭐⭐⭐ 強く推奨";
  } else if (score >= 55) {
    return "B ⭐⭐⭐ 検討推奨";
  } else if (score >= 40) {
    return "C ⭐⭐ 条件次第";
  } else {
    return "D ⭐ 避けた方が無難";
  }
}
```

---

## コード4: 一括でジャンル別統計を計算する関数

```javascript
/**
 * ジャンル別の統計情報を計算する関数
 * @param {string} category - ジャンル名
 * @param {Range} dataRange - Input シートのデータ範囲
 * @return {Object} 統計情報
 */
function calculateCategoryStats(category, dataRange) {
  const values = dataRange.getValues();
  
  let count = 0;
  let rewards = [];
  let beginnerOKCount = 0;
  let continuingCount = 0;
  let highRiskCount = 0;

  // データ行をループ
  for (let i = 1; i < values.length; i++) {
    const row = values[i];
    const jobCategory = row[2]; // C列
    const reward = row[3]; // D列
    const beginnerOK = row[7]; // H列
    const continuing = row[8]; // I列
    const riskLevel = row[10]; // K列

    if (jobCategory === category && reward) {
      count++;
      rewards.push(reward);
      if (beginnerOK === true) beginnerOKCount++;
      if (continuing === true) continuingCount++;
      if (riskLevel === "高") highRiskCount++;
    }
  }

  if (count === 0) {
    return null;
  }

  // 平均と中央値を計算
  const avgReward = rewards.reduce((a, b) => a + b, 0) / rewards.length;
  rewards.sort((a, b) => a - b);
  const medianReward = rewards[Math.floor(rewards.length / 2)];

  return {
    count: count,
    avgReward: Math.round(avgReward),
    medianReward: medianReward,
    beginnerOKRate: (beginnerOKCount / count * 100).toFixed(1),
    continuingRate: (continuingCount / count * 100).toFixed(1),
    riskRate: (highRiskCount / count * 100).toFixed(1)
  };
}
```

---

## コード5: 月5万円シミュレーション

```javascript
/**
 * 月5万円達成までのシミュレーション
 * @param {number} monthlyGoal - 月目標金額
 * @param {number} availableHours - 月の使える時間
 * @param {number} avgReward - 案件の平均報酬
 * @param {number} avgHours - 案件の平均時間
 * @return {Object} シミュレーション結果
 */
function simulate50kMonthly(monthlyGoal, availableHours, avgReward, avgHours) {
  // 必要な案件数
  const jobsNeeded = Math.ceil(monthlyGoal / avgReward);
  
  // 必要な時間
  const hoursNeeded = jobsNeeded * avgHours;
  
  // 実現性判定
  const isRealistic = hoursNeeded <= availableHours;
  
  // 実効時給
  const effectiveHourlyRate = monthlyGoal / hoursNeeded;
  
  return {
    jobsNeeded: jobsNeeded,
    hoursNeeded: hoursNeeded,
    isRealistic: isRealistic,
    effectiveHourlyRate: Math.round(effectiveHourlyRate),
    advice: isRealistic ? 
      "達成可能です！" : 
      "目標に到達するには、より高単価の案件を探すか、時間を増やす必要があります。"
  };
}
```

---

## コード6: 応募文テンプレートの自動生成

```javascript
/**
 * テンプレートと入力情報から応募文を生成
 * @param {string} templateType - テンプレートタイプ
 * @param {Object} userInfo - ユーザー情報 {name, skills, experience}
 * @param {Object} jobInfo - 案件情報 {title, description}
 * @return {string} 生成された応募文
 */
function generateApplicationText(templateType, userInfo, jobInfo) {
  const { name, skills, experience } = userInfo;
  const { title, description } = jobInfo;

  let template = "";

  switch(templateType) {
    case "beginner":
      template = `件名: ${title}への応募

いつもお世話になっております。
${name}と申します。

この度は${title}へのご応募をさせていただきたく、ご連絡しました。

【自己紹介】
私は現在、${skills || "文章作成"}の業務に従事しており、
スキルを磨いています。

貴社の案件により、さらにスキルを高めたいと考えております。

【実績】
${experience || "初心者ですが、丁寧な対応を心がけています。"}

【対応能力】
- 丁寧で正確な作業
- 納期厳守
- 修正対応への迅速な対応

よろしくお願いいたします。

${name}`;
      break;

    case "ai_focused":
      template = `件名: ${title}への応募（AI活用で効率化します）

いつもお世話になっております。
${name}と申します。

この度は${title}へのご応募をさせていただきたく、ご連絡しました。

【スキル紹介】
私は以下のAIツールを活用できます：
- ChatGPT / Claude による効率的な文章作成
- Google スプレッドシートの自動化
- 画像生成AI（Midjourney、Stable Diffusion）

これらのツールにより、高速で高品質な成果物をお納めできます。

【過去実績】
${experience || "AI活用による業務効率化"}

是非、この機会にご一緒させていただきたいです。

よろしくお願いいたします。

${name}`;
      break;

    case "short":
      template = `件名: ${title}への応募

${name}と申します。

${title}への応募をさせていただきたくご連絡しました。

【スキル】
${skills || "文章作成、データ入力"}

【経験】
${experience || "初心者ですが、丁寧な対応ができます。"}

ご検討のほど、よろしくお願いいたします。

${name}`;
      break;

    default:
      template = "テンプレートが見つかりません";
  }

  return template;
}
```

---

## コード7: スプレッドシート内からの実行用ヘルパー関数

```javascript
/**
 * スプレッドシートのセルから直接呼び出せる関数
 * =CALCULATE_SCORE(E2, F2, G2, H2, I2) のような形式で使用
 */
function CALCULATE_SCORE(hourlyRate, clientRating, beginnerOK, riskLevel, continuing) {
  return calculateScore(hourlyRate, clientRating, beginnerOK, riskLevel, continuing);
}

function ASSESS_RISK(jobTitle, description, hourlyRate) {
  const result = assessRisk(jobTitle, description, hourlyRate);
  // スプレッドシート内で表示するため、リスクレベルのみ返す
  return result.level;
}

function GET_RISK_SCORE(jobTitle, description, hourlyRate) {
  const result = assessRisk(jobTitle, description, hourlyRate);
  return result.score;
}

function GET_RECOMMENDATION_RANK(score, riskLevel) {
  return getRecommendationRank(score, riskLevel);
}

function SIMULATE_MONTHLY(monthlyGoal, availableHours, avgReward, avgHours) {
  const result = simulate50kMonthly(monthlyGoal, availableHours, avgReward, avgHours);
  return result.jobsNeeded; // 必要な案件数を返す
}

function IS_REALISTIC(monthlyGoal, availableHours, avgReward, avgHours) {
  const result = simulate50kMonthly(monthlyGoal, availableHours, avgReward, avgHours);
  return result.isRealistic ? "達成可能" : "要検討";
}
```

---

## 使用方法

### 例1: スコアを自動計算

Input シート上の案件データから、スコアを自動計算したい場合：

```
Apps Script に上記のコード を登録

Jobs シートの I2 セルに：
=CALCULATE_SCORE(
  ROUND(D2/E2, 0),      // 時給
  F2,                    // 発注者評価
  G2,                    // 初心者OK
  H2,                    // リスク判定
  I2                     // 継続案件
)
```

### 例2: リスクを判定

RiskCheck シートで、入力された案件タイトルからリスクを判定：

```
B22 セルに：
=ASSESS_RISK(B2, B5:B20, ROUND(C2/D2, 0))

結果は「低」「中」「高」のいずれかが表示される
```

### 例3: 月5万円の必要案件数

Settings シートで目標額と時間から必要案件数を計算：

```
B5（必要な案件数）に：
=SIMULATE_MONTHLY(
  B4,        // 月目標金額
  B6,        // 月の使える時間
  C4,        // 平均報酬（CategoryAnalysis から参照）
  E4         // 平均時間
)
```

---

## トラブルシューティング

### エラー：「関数が見つかりません」

解決：
1. Apps Script が正しく保存されているか確認
2. スプレッドシートを一度閉じて再度開く
3. ブラウザキャッシュをクリア

### スコアが 0 または 100 になってしまう

解決：
1. 入力値が正しいか確認（数値型か文字列型か）
2. リスクレベルが「低」「中」「高」のいずれかか確認
3. 初心者OK / 継続案件が TRUE / FALSE か確認

### 関数の実行が遅い

解決：
1. Apps Script の実行ログを確認
2. 大量のデータ処理の場合は、バッチ処理に変更
3. キャッシュを活用

---

## 参考資料

- [Google Apps Script 公式ドキュメント](https://developers.google.com/apps-script)
- [Googleスプレッドシート関数リスト](https://support.google.com/docs/table/25273)

---

## 次のステップ

このスクリプトをさらに拡張して、以下の機能を追加できます：

1. **自動メール通知** - おすすめ案件が見つかったときに通知
2. **データの自動バックアップ** - 日ごとにコピーを作成
3. **クラウドワークス API 連携**（将来） - 案件情報を自動取得
4. **Slack 連携** - チャットで結果を共有

これらの機能は Phase 1（Webアプリ化）で実装予定です。
