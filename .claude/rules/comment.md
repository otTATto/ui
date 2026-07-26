# コメントに関するルールや考え方

## 全般

- 自明な処理にコメントしない
- 既存のコメントを破壊しない
- 対話後の修正時に修正箇所に関する説明をコメントで強調しない（コードの最終的な読み手はその経緯を知らない）
- コメントの量はその影響範囲、つまりどれだけ多くの場所から呼び出されるかに依存する
  - 他の場所から呼び出されうる定数・関数は丁寧に説明する
  - 関数は JSDoc に近い書き方を心がける

## コメントの例

### 型定義

```typescript
// src/types/user.ts

/**
 * 配送先住所
 *
 * - id           : 住所の一意識別子
 * - postalCode   : 郵便番号
 * - fullAddress  : 住所
 * - recipientName: 受取人名
 * - isDefault    : デフォルト住所かどうか
 */
export type Address = {
  id: string;
  postalCode: string;
  fullAddress: string;
  recipientName: string;
  isDefault: boolean;
};
```

### 関数定義

```typescript
/**
 * @function 健診項目キーと結果バリューを受け取り、日本語ラベルや単位を付け加えた形に整形して返す
 *
 * @param items 健診項目のキーとその健診結果のバリュー
 * @returns 健診項目をキーとし、その健診結果・日本語ラベル・単位を持つ Record
 *
 * NOTE:
 *   - fetch 失敗時は null を返す
 *   - 入力されたキーのうち CHECKUP_ITEM_KEYS に合致するもののみ返す
 *   - つまり、返り値のキーに引数のキーすべてが存在するとは限らない
 *
 * e.g.
 *   - @param items { 'height': '165', 'weight': '45', 'VisualAcuityLeft': '1.2' }
 *     ↓
 *     @returns {
 *       'height': { label: '身長', value: '165', unit: 'cm' },
 *       'weight': { label: '体重', value: '45', unit: 'kg' },
 *       'VisualAcuityLeft': { label: '視力（左）', value: '1.2' }
 *     }
 */
export const formatCheckupItems = async (
  items: Partial<Record<CheckupItemKey, string>>,
): Promise<Partial<CheckupItems> | null> => {
  ...
};
```
