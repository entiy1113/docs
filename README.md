# docs
Entiyで調査、構築したドキュメントです。


# ssh 接続でpushする設定
## メリット
pushのタイミングで、パスワード入力無しで実行できる。

## 設定手順
1. 既存設定の確認
```
ls -la ~/.ssh
```
githubはrsa, ecdsa, e25519が対応しているので
それがあれば使えそう？

2. 鍵生成
```
ssh-keygen -t ed25519 -C "メールアドレス"
```

ファイル名変更を聞かれるがどちらでもよい。
Enter file in which to save the key

/home/kaito/.ssh/entiy_id_ed25519

3. ファイル名を変更した場合、
    configファイル作成し変更したファイル名を指定する必要がある。
```
Host github github.com
    HostName github.com
    IdentityFile ~/.ssh/entiy_id_ed25519
    User git
```

5. 管理者に、作成したpubファイルを送り、githubに登録してもらう

4. 接続確認
```
ssh -T git@github.com
```

5. push前の確認
httpsか、sshのどちらでpush する設定かを確認
```
git remote -v
```

httpsの場合、以下のコマンドでsshに切り替え
```
git remote set-url origin git@github.com:entiy1113/docs.git
```