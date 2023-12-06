[TOC]

# 11月

## 2023/11/02

昨日、管理ポータルの仕様書を設計書によって書き直しました。

今日は、続けて仕様書をちょっど直して、改修部分のプログラムを実装していました。

## 2023/11/06

修正した仕様書に基づいて管理ポータルのプログラムを実装しています

ポイント申請/レンジ

## 2023/11/07

昨日新規ユーザー登録画面とユーザー情報画面のプログラムを直しました。

今日は、各ページにエーラ処理のプログラムを実装する予定です。

また、管理ポータルUIの打ち合わせがあるようです。

統合IDについて少し質問したいです。レルムとIDを入力し、統合IDの情報をサーバーに送信します。それらの情報をサーバー側で利用して統合IDを登録する、という流れでしょうか

ユーザーは自分で作成したレルムが重複していないか確認しますよね？

すみません、細かい点を少し確認したいのですが、レルムとクライアントIDはサーバー側で作成しますよね。しかし、新規契約画面でそれらの情報を入力する際に、一致するかどうかを確認する、という理解でよろしいですか？」という表現がより自然です。

## 2023/11/08

打ち合わせのことを整理して、管理ポータルの改修を進んでいます。

## 2023/11/10

昨日から、管理ポータルの上限アップに関する内部処理のプログラムの実装を行いました。今日は、9時半からAWSの一日研修を受講します。

## 2023/11/13

先週金曜日は研修でした。今日は、引き続き管理ポータルに関して、管理カメラの上限アップ対応のプログラムを実装します。

管理ポータル仕様書で管理ポータルの見た目をいま実装していた見た目を一致にしました。

## 2023/11/14

管理ポータルに関して、管理カメラの上限アップ対応のプログラムを実装して終わりました。今日は、管理ポータルの仕様書に定められたsadame見た目を実装する作業を行います。また、午後には新入社員向けのフレッシュプランセミナーに参加する予定です

## 2023/11/15

```
昨日は、管理ポータルのこれまでに作成した画面を仕様書とJiraで整理しました。

今日から、ユーザー一覧画面にページング機能を実装する予定です
```

## 2023/11/16

昨日はユーザー一覧画面にページネーション機能を実装しました。今日は、カメラ一覧画面にページネーションを実装する予定です。

## 2023/11/17

昨日はカメラ一覧画面にページネーションを実装しました。

統合ID対応などのサーバー側の処理が実装する予定です。

## 2023/11/20

管理ポータルに関して、金曜日に統合IDのAPIがローカル環境に導入されましたが、サーバー側の対応はまだ完了していません。ただ今、統合IDに対応するプログラムの実装を修正中です。

## 2023/11/21

昨日、管理ポータルでの作業中に、統合ID対応のAPI処理のプログラムを書き直しました。時間はかかりましたが、サブ環境でサーバー側から正しいレスポンスを戻してきたため、契約登録画面と契約情報更新画面が正常に動作することを確認しました。今日は、パラメータなどもうちょっと変更したので、別の画面のプログラムも修正する予定です。

## 2023/11/27

管理ポータルの実装は少し進んでいます。午前中に終わりそうです

午後、何か指示（しじ）がありましたら、どうぞよろしくお願いいたします。



## 2023/11/28

##　管理ポータル

### API連携専用ユーザー 登録、更新、ciidのとき更新できない

~~~jsx
     {/* API連携専用ユーザー */}
​      {!*userForEdit* ?
​       renderKeyOnly('API連携専用ユーザー', false,

​          <*StyledCheckbox*

​           label='API連携専用ユーザー'

​           checked={linkageUserFlag}

​           color='text.primary'

​           onChange={handleChangeLinkageUserFlag}

​          />
​       ) : renderKeyOnly('API連携専用ユーザー', false,

​          <*StyledCheckbox*

​           label='API連携専用ユーザー'

​           checked={linkageUserFlag}

​           color='text.primary'

​           disabled={*tenant*?.auth?.type == "ciid"? true : false}
​           onChange={handleChangeLinkageUserFlag}
​          />
​       )
​     }
~~~

### 登録パスワード

~~~jsx
 * 登録ボタンがクリックされた
   */
  const handleCreateUser = () => {
    // 新規登録ケース
    const createRequest: CreateUserRequest = {
      tenantId: tenantId ?? undefined,
      userId: userId,
      userPassword:  tenant?.auth?.type == "ciid" && ! linkageUserFlag ? undefined : userPassword,
      department: department.length > 0 ? department : undefined,
      userName: userName.length > 0 ? userName : undefined,
      role: role,
      userGroupId: userGroupId,
      linkageUserFlag: linkageUserFlag,
    };
    onClickPositive(createRequest);
  };
~~~

### 変更　パスワード

~~~jsx
 // 変更点のみパラメータを設定する
    const updateRequest: UpdateUserRequest = {
      tenantId: tenantId ?? undefined,
      userNo: userForEdit.user_number,
      userId: userId !== userForEdit.user_id ? userId : undefined,
      userPassword: userPassword.length > 0 && (tenant?.auth?.type == "ciid" && ! linkageUserFlag) ? userPassword : undefined,
      department: department !== userForEdit.department ? department : undefined,
      userName: userName !== userForEdit.user_name ? userName : undefined,
      role: role !== userForEdit.role ? role : undefined,
      userGroupId: JSON.stringify(userGroupId) !== JSON.stringify(userForEdit.user_group_id) ?
        userGroupId : undefined,
      linkageUserFlag: linkageUserFlag !== userForEdit.linkage_user_flag ? linkageUserFlag : undefined,
    };
    onClickPositive(undefined, updateRequest);
  };
~~~

### Password表示

~~~jsx
  {/* パスワード */}
            { !(tenant?.auth?.type == "ciid" && ! linkageUserFlag) && renderKeyOnly('パスワード', !userForEdit,
                <Box
                  sx={{
                    width: '100%',
                    display: 'flex',
                    flexDirection: 'row',
                    position: 'relative',
                  }}
                >
                  <Box
                    sx={{
                      flexGrow: 1,
                    }}
                  >
                    <PasswordField
                      value={userPassword}
                      onChange={handleChangeUserPassword}
                      event={passwordEvent}
                    />
                  </Box>
                  <Button
                    onClick={handleCreatePassword}
                    sx={{
                      'color': 'common.white',
                      'ml': 1,
                      'backgroundColor': 'primary.main',
                      '&:hover': {
                        'backgroundColor': 'primary.dark',
                      },
                    }}
                  >
                    パスワード生成
                  </Button>
                </Box>,
            )}
~~~

### 登録、更新ボタン有効か

~~~jsx
 const isEnabledSubmitButton = () => {
    if (userForEdit) {
      // 更新ケース
      if (userGroupId.length === 0) {
        return false;
      }
      if ((userId && userId !== userForEdit.user_id) ||
        userPassword.length > 0  ||
        (department !== userForEdit.department && (department !== '' || userForEdit.department !== null)) ||
        (userName !== userForEdit.user_name && (userName !== '' || userForEdit.user_name !== null)) ||
        role !== userForEdit.role ||
        JSON.stringify(userGroupId) !== JSON.stringify(userForEdit.user_group_id) ||
        linkageUserFlag !== userForEdit.linkage_user_flag) {
        return true;
      }
    } else if(!(tenant?.auth?.type == "ciid" && ! linkageUserFlag)){
      // 新規登録ケース
      if (userId.length > 0 &&
        userPassword.length > 0  &&
        role.length > 0 &&
        userGroupId.length > 0) {
        // いずれかが空の場合、無効
        return true;
      }
    } else if(tenant?.auth?.type == "ciid" && ! linkageUserFlag){
      if(userId.length > 0 &&
        role.length > 0 &&
        userGroupId.length > 0){
        return true;
      }
    return false;
  };
  }
~~~

### 契約情報更新画面

~~~jsx
{/* 統合ID対応 */}
         <Box>
          {renderSubtitle('統合ID利用する', 3)}

          {/* レルム*/}
          {renderStaticRow('レルム', tenantForEdit?.auth?.realm ?? '')}

          {/* クラインアントID */}
          {renderStaticRow('クラインアントID', tenantForEdit?.auth?.realm ?? '')}
        </Box>

~~~

### 文字列チェック

### エラー対応

### 警告を追加

![image-20231128183023852](C:\Users\4087932\AppData\Roaming\Typora\typora-user-images\image-20231128183023852.png)



---

## 2023/11/29

昨日、間違った箇所のロジックを修正しました。仕様書の誤りを訂正し、さらに仕様書と一致するようにエラー処理やバリデーションチェックなど、管理ポータルのプログラムも改修します。今日は、管理ポータルの改修がなければ、これからユーザーポータルのプログラムを読みます。



## userportal- information page

1. 通知クリック　
2. notificationコンポーネント　potral_c\app\src\pages\MainLayout\Header\index.jsx
3. mui  paper
4. overflow: scroll　スクロールバー
5. 



## sx   vs  style

MUI v5 以降でコンポーネントにカスタムスタイル (CSS) を割り当てる方法には、大きく下記の 2 つのやり方があります。

- sx propを使う方法
  - MUI のコンポーネントには **sx prop** が定義されていて、ここにスタイルオブジェクトを渡すことで、個別にスタイルを調整できます。つまり、使い捨てのスタイル設定を行う方法です。sx prop は HTML 要素本来の style プロパティと比べて簡潔な構文で記述できます。例えば、margin や padding の設定用に 1 文字 (`m`, `p`) のプロパティ名が定義されていたりします。
- styled APIを使う方法
  - 既存のコンポーネントをラップする形で、スタイル拡張したコンポーネントを生成します。sx prop を使った方法に比べて再利用性が高い方法で、複数個所で使用するコンポーネントにスタイル設定したいときに便利です。`styled()` 関数は内部的には [Emotion](https://emotion.sh/) というライブラリが提供する関数につながっていますが、MUI では `@mui/material/styles` パッケージをインポートすることで使えるようになっています。



## 

## 2023/11/30

午前中、引き続きユーザーポータルのソースコードを読みます。

午後から、ユーザーポータルのインフォメーションページを実装する予定です。



## React在组件中共享状态，props的传递 学习一下

## スクロールバー

縦方向のスクロールバーを表示する。横方向のスクロールバーを自動的に表示する。

~~~jsx
style={{   position: 'absolute',
​            top: '50px',
​            right: '70px',
​            padding: '5px',
​            zIndex: 1300,
​            maxHeight: '500px',
​            overflowX: 'auto',
​            overflowY: 'scroll',  //overflowX , overflowY
​          }}
​      \>
~~~

## mui のclick-away利用して、要素の外部でクリックイベントが発生したときにそれを検出します。

click-away : 需要把子元素放在div中

```
`ClickAwayListener`组件需要一个子元素以便正确地添加事件侦听器。当我们点击`ClickAwayListener`之外的任何地方时，`onClickAway`事件都会被触发。
如果`C_IconButton`和`PopupNotification`元素直接作为子元素存在，那么它们之间的空隙可能不会被`ClickAwayListener`组件认为是其内容的一部分。这就是为什么我们通常会将所有的子元素包裹在一个``元素（或者其他任何单一的根元素）内部，以确保`ClickAwayListener`组件能够正确地识别其内容范围并触发`onClickAway`事件。
```

https://mui.com/base-ui/react-click-away-listener/



## 2023/12/01

ユーザーポータルのインフォメーションページの作成を進めています





### 改修ファイル

変更　potral_c\app\src\pages\MainLayout\Header\index.jsx

変更　potral_c\app\src\pages\MainLayout\Header\PopupSubmenu.jsx

変更　potral_c\app\src\component\common\PopupPaper\popup.jsx

追加　potral_c\app\src\component\common\PopupPaper\popupMobile.jsx



# 12月

## 2023/12/04

金曜日ユーザーポータルのインフォメーションページを作成して終わりました。

今日は、レビューを待ってます。また、首藤さんに環境構築の協力をする予定です。



## 什么是CSS层叠上下文？

## 为什么我写的z-index无效

## 修改左边tree 和 下面videobar的zindex



## 2023/12/05

作成したインフォメーションページに関して、レビューをいただきました。展示効果にいくつかの問題があるため、本日は見た目の改修を進めています。



## 修改paper的值zindex無效，父元素的position設置的是static？？

可能原因：父元素的position設置的是static？所以子元素zindex無效

~~~html
<header class="MuiPaper-root MuiPaper-elevation MuiPaper-elevation0 MuiAppBar-root MuiAppBar-colorPrimary MuiAppBar-positionAbsolute css-1tznxx9-MuiPaper-root-MuiAppBar-root" zindex="2000"></header>
~~~

**ツールバーと左側siderBarのzIndexの値を1000に設定する**

変更

potral_c\app\src\component\media\Video\MoveTool\layout.jsx

変更：potral_c\app\src\pages\MainLayout\Sidebar\index.jsx

## 203/12/06

インフォメーションページの見た目の作成を進めています。

