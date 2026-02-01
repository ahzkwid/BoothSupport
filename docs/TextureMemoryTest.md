# テクスチャメモリとパフォーマンスの関連性

メモリは処理装置ではなく記憶装置なのに処理速度を向上させるという噂がある

テクスチャメモリがパフォーマンスに大きく影響するという噂が流れているが

いくら調べても脳内推測でそうだろうという推測性資料ばかり存在し

どれくらいパフォーマンスに影響を与えるかテストした資料が全く見当たらなかったのでテストしてみた

<img width="800" alt="image" src="https://github.com/user-attachments/assets/4e80342d-86a3-42eb-9e6c-afe751ad4f25" />

<img width="800" alt="image" src="https://github.com/user-attachments/assets/a9765837-4e89-4d51-bd23-24a54ebc01ae" />

<img width="390" height="1072" alt="image" src="https://github.com/user-attachments/assets/cd87df5f-10d0-4738-86c9-6c3ae3f3efa1" />

<img width="694" height="92" alt="image" src="https://github.com/user-attachments/assets/0efaf86f-6d49-4f61-9a9b-32c12b526ccf" />


使用されたコード 

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TextureMemoryTest : MonoBehaviour
{
    public Renderer renderTarget;
    public Texture[] textures;
    public int max = 800;
    public bool useTexture = false;
    // Start is called before the first frame update
    void Start()
    {

        var wid = (int)Mathf.Sqrt(textures.Length);
        var i = 0;
        foreach (var texture in textures)
        {
            var instance = Instantiate(renderTarget.gameObject);
            if (useTexture)
            {
                instance.GetComponent<Renderer>().material.SetTexture("_MainTex", texture);
            }
            var x = i % wid;
            var y = i / wid;
            instance.transform.position = new Vector3(x * 0.5f, y * 0.5f, i * 0.01f);

            i++;
            if (i>max)
            {
                return;
            }
        }
        renderTarget.gameObject.SetActive(false);

    }

}
```

\-テスト環境-

CPU : Ryzen 5 1600

メモリ : 32GB 1333Mhz

GPU : RTX 3050 8GB

4k~8kテクスチャ800枚使用

使用されたテクスチャメモリは14GB

あることはあるが無視してもいいレベルで小さい

ミップマップにかかったからかドライバ段階でロードを阻止しているのか

テクスチャメモリがグラフィックカードメモリの2倍にも関わらず

問題が全く発生しない

処理量が最小のUnlitでも大差ないのに

ライト処理が入るStandardやToonシェーダなどでは差がもっと少ないだろう

むしろあの多くのテクスチャを表示するためにドローコールが大幅に増えてしまい

わざと馬鹿みたいにフラグメント段でtex2D関数を数十回呼び出したりミップマップを全部オフにして使ったりカメラの真ん前にキャラクターが1000人立っていたりしない限り

一般的な状況ではバーテックスとドローコール、シェーダだけ気にすればいいだろう

実際に一部集会ではこの話だけを信じてテクスチャメモリで入場制限をかけたが当然ながら全く効果がなかった

むしろ最近はテクスチャメモリだけちょこっと調整して他は何も触らないのでラグがより酷くなったようだ

ゲーム開発者は皆理論的には知っているのでどうでもいい話だが

VRChatで論争になったのでテストしてみた

そもそも最適化技法というものはCPUやGPUの演算量をできるだけメモリに転換するのが基本だ

こんなに複雑に考える必要なく、そんなに重要な要素だったら

Unity側でStatsタブにドローコールと一緒にテクスチャメモリも一緒に表示してくれただろう(...)

ここまでやっても信じない人がいるだろうから

直接目で見られるように

下に4kテクスチャで埋め尽くしたキャラクターを立てたワールドも公開した

[https://vrchat.com/home/world/wrld\_10abac1c-0493-4822-9426-e0f1a5eeedd3](https://vrchat.com/home/world/wrld_10abac1c-0493-4822-9426-e0f1a5eeedd3)

最近VRAMが増えたからパフォーマンスのためだと誤解しているようだが

VRAMが増えるのはパフォーマンス向上ではなくAI駆動時のメモリ不足防止だ

AI駆動時にメモリが不足すると駆動自体ができなくなる

関連文書は下の方

[chat:AI画像認識方法]


-After

<img width="281" height="55" alt="image" src="https://github.com/user-attachments/assets/64cc4421-786d-42cd-82a3-46b6c1677beb" />

今回のテストでは、テクスチャのうち約5%に Mip Streaming が含まれていましたが、

今回は Mip Streaming を完全に削除してロードしたにもかかわらず、同じ結果が得られました。

え？ 自分が学んできた知識では、Mip Streaming は VRAM 調整の要だと思っていたのに、Mip Streaming がなくてもそうなるのか？

もしかすると本当に Unity エンジン自体が VRAM のロード制限を掛けているのだろうか。

ひとつ確かなのは、Unity が優れたエンジンであるということであり、少なくとも Unity 内においては、テクスチャメモリがグラフィックカード容量の 2 倍に達しても性能に大きな影響はないことを改めて確認できた、ということです。



#タグ

VRChat テクスチャメモリ 最適化
