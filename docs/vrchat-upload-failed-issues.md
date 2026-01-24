

# VRChatアップロード不可問題まとめ


# ArgumentException: Illegal byte sequence encounted in the input.
```
ArgumentException: Illegal byte sequence encounted in the input.
Parameter name: string
```


原因は2つあり、両方試すのが望ましい。

## SDKが旧バージョンの場合に発生

<img width="360" height="240" alt="image" src="https://github.com/user-attachments/assets/69185ef6-38cf-4980-9712-f880b4c6b649" />

VRC SDKを最新バージョンに更新します。

## デバイス名が英語でない場合に発生

<img width="572" height="817" alt="image" src="https://github.com/user-attachments/assets/585dbc30-37a2-4161-87d2-18c8dd21b98d" />


<img width="890" height="582" alt="image" src="https://github.com/user-attachments/assets/a241f236-2269-4a0c-868b-2494c4285652" />

CC

Unity Hub

Unity実行ファイル

ユーザー名

プロジェクトパス

デバイス名をすべて英語パスに変更し、ファイアウォールを許可すればよい

特にデバイス名が一番重要


デバイス名は
```
設定 ＞ システム ＞ 情報 ＞ デバイス名
```
順番で入ったら存在する



# アップロードを押した後、停止したまま動作しない場合

<img width="579" height="498" alt="image" src="https://github.com/user-attachments/assets/634442b3-3732-4d61-89ef-b040b10bc616" />

上記の「デバイス名が英語でない場合に発生」と同一の問題、該当項目を参照してください。



# Images used for Actions & Moods are too large.

```
Images used for Actions & Moods are too large.
```
<img width="488" height="548" alt="image" src="https://github.com/user-attachments/assets/7ca2bf6f-ceeb-4964-8cc4-caec874b141e" />


ExpressionsMenu アイコンの解像度を 256 以下に合わせると解決される



# Error while saving Prefab


<img width="836" height="51" alt="image" src="https://github.com/user-attachments/assets/9dd0cd3b-b033-498a-bdfb-9d64c1dd0a0e" />
```
Error while saving Prefab: 'Assets/prefab-id-v1_avtr_.prefab'. You are trying to save a Prefab with a missing script. This is not allowed.
Please change the script or remove it from the GameObject 'Head'.
```
```
A UnityEditor.BuildPipeline:BuildAssetBundles (string UnityEditor.AssetBundleBuild[], UnityEditor.BuildAssetBundleOptions, UnityEditor.BuildTarget)
No AssetBundle has been set for this build.
```

ミシンコンポーネントが存在するからなのさ


<img width="511" height="310" alt="image" src="https://github.com/user-attachments/assets/e6db73bc-4570-49f2-9dc6-92b215a1d7bd" />

全部探して消す



# まともにアクティブになっているのにダメなとき

```
Encountered the following validation issues during build:
UnityEngine.Debug:LogError (object)
Your avatar is disabled in the scene hierarchy!
UnityEngine.Debug:LogError (object)
```

<img width="511" height="76" alt="image" src="https://github.com/user-attachments/assets/ac9fe61d-26be-4991-9076-e476b6e517c4" />

無アクティブにしてからもう一度アクティブにする

<img width="367" height="183" alt="image" src="https://github.com/user-attachments/assets/c91086ed-b81c-46c6-ab71-c9273bfb5b3f" />


セレクトアバターももう一度選んでくれる


# VRCExpressionsMenu uses a parameter that is not defined.

<img width="387" height="38" alt="image" src="https://github.com/user-attachments/assets/4b841920-2e96-41fb-ac5b-3ebf0c9d6f0f" />

```
VRCExpressionsMenu uses a parameter that is not defined.
```


メニューにないパラメータが入っているからなのさ

こんな時は


<img width="424" height="394" alt="image" src="https://github.com/user-attachments/assets/7050a3f0-e268-42f9-b705-e988784049b0" />

<img width="420" height="123" alt="image" src="https://github.com/user-attachments/assets/e52a2659-7d34-43f1-9d76-92a1bc3647ec" />


こうやってメニューでパラメータ名を修正したらよい。


# [Always] Attempted to load the data for an avatar we do not own, clearing blueprint ID


<img width="578" height="83" alt="image" src="https://github.com/user-attachments/assets/b9dd3bb7-c725-46a6-987e-270c6f00f4e2" />


```
[Always] Attempted to load the data for an avatar we do not own, clearing blueprint ID
```

<img width="758" height="41" alt="image" src="https://github.com/user-attachments/assets/c2849c0c-736b-4f12-a9e0-a0cbb0200012" />

```
ApiErrorException: Exception of type 'VRC.SDKBase.Editor.Api.ApiErrorException' was thrown.
```

ブループリント特権問題


<img width="320" height="585" alt="image" src="https://github.com/user-attachments/assets/a93098f1-ce01-41a5-8dca-d39eb1d2dc7e" />


ブループリントを新しく作って解決した


Detachして新しくアップロードると終わり

# UploadException: Failed to upload file

<img width="599" height="82" alt="image" src="https://github.com/user-attachments/assets/0e081e55-db58-4ef7-9877-6d5c9a090293" />


```
UploadException: Failed to upload file
Attempted to load the data for an avatar we do not own, clearing blueprint ID
```

もしくは

<img width="387" height="80" alt="image" src="https://github.com/user-attachments/assets/2813cade-fe11-4da1-b042-fc1c7b0c3701" />



もしくは

<img width="612" height="161" alt="image" src="https://github.com/user-attachments/assets/2a05fd83-1e1e-41ab-85ad-bfde5a388317" />


```
ApiErrorException: Exception of type 'VRC.SDKBase.Editor.Api.ApiErrorException' was thrown.
Unauthorized, try logging out and in again
"Missing Credentials"
NullReferenceException: Object reference not set to an instance of an object
```


もしくは

<img width="382" height="84" alt="image" src="https://github.com/user-attachments/assets/8602827c-8dbc-48d4-8ecb-82084cc4f1e6" />

```
Error fetching your uploaded avatars:
"Missing Credentials"
Could not fetch worlds, with error - "Missing Credentials"
```

全部同じ問題です。

最初のエラーメッセージだけを見ると、ブループリントの問題だと思われるかもしれない

だがブループリント問題ではない

そもそもブループリントを空の状態でアップロードしていたからだ


この問題はログイン認証キーの期限切れによるものだ
だから、Unity 上の SDK でログアウトして再ログインすれば解決する。

その後、知人が追加でテストしたところ、Unity を再起動しても直るらしい
で、最初は API 認証キーの期限切れだと思っていたが、実際はログイン認証キーの期限切れだったと分かった。







