## Lombok実装方針（全面利用）

### 目的
- 学習目的の試作であり、開発スピードを最優先するため、Lombokを全面的に利用する
- 冗長なボイラープレートコード（Getter/Setter、コンストラクタ、equals/hashCode/toStringなど）を削減し、ビジネスロジックに集中できる環境を整える

### 利用方針
- DTO・Entity・Serviceクラスなど、ほぼすべてのクラスでLombokを利用する
- 主要アノテーション
  - @Data：Getter/Setter、equals、hashCode、toStringを一括生成
  - @Builder：柔軟なインスタンス生成を可能にする
  - @AllArgsConstructor / @NoArgsConstructor：コンストラクタを自動生成
  - @Slf4j：ロガーを自動生成し、ログ出力を簡略化

### 推奨パターン
- DTOや簡易的なモデルクラス → @Data + @Builder
- JPAエンティティ → @Getter/@Setterを基本とし、必要に応じて@Builder
- サービスやユーティリティクラス → @Slf4jでログ管理

### 注意点
- JPAエンティティに@Dataを使う場合、equalsやhashCodeの自動生成が予期せぬ挙動を招く可能性があるため、学習目的では許容するが、本番環境では再検討する。
- IDEやビルド環境でLombokプラグインが必要になるため、環境構築時に必ず設定を確認する。
- 将来的に本番運用を視野に入れる場合は、限定利用方針への切り替えを検討する。

### コード例

#### DTOクラス例
```
import lombok.Data;
import lombok.Builder;

@Data
@Builder
public class UserDto {
    private Long id;
    private String name;
    private String email;
}
```

#### JPAエンティティ例
```
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import lombok.Getter;
import lombok.Setter;
import lombok.NoArgsConstructor;
import lombok.AllArgsConstructor;
import lombok.Builder;

@Entity
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class Product {
    @Id
    private Long id;
    private String name;
    private Double price;
}
```

#### サービスクラス例
```
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Service;

@Slf4j
@Service
public class UserService {

    public void createUser(String name) {
        log.info("Creating user with name: {}", name);
        // ビジネスロジックをここに記述
    }
}
```
