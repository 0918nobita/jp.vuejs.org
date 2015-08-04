title: Computed Properties
type: guide
order: 8
---

Vue.js のインライン expression は非常に便利ですが、最良のユースケースはシンプルな boolean 演算や文字列の連結を使用したものです。より複雑なロジックに関しては、 **computed properties** を活用しましょう。

Vue.js では `computed` オプションを使って computed properties を定義します。

``` js
var demo = new Vue({
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: {
      // getter で望む値を返します
      get: function () {
        return this.firstName + ' ' + this.lastName
      },
      // setter は任意です
      set: function (newValue) {
        var names = newValue.split(' ')
        this.firstName = names[0]
        this.lastName = names[names.length - 1]
      }
    }
  }
})

demo.fullName // 'Foo Bar'
```

getter のみしか必要がない場合は、オブジェクトの代わりに関数を一つ渡すこともできます:

``` js
// ...
computed: {
  fullName: function () {
    return this.firstName + ' ' + this.lastName 
  }    
}
// ...
```

要するに computed property は getter/setter 関数を定義したプロパティです。あたかも通常のプロパティとして使用することができますが、実際にアクセスした時は getter 関数によって値が返されます。また、値を変更した時は、その新しい値を引数として setter 関数をトリガします。

0.12.8 より前は、computed properties は getter のように振舞います。それにアクセスするたびに、getter 関数は再評価されます。0.12.8 ではこれは改善されました。computed properties はキャッシュされ、必要なときにだけ、lazily に再評価されます。

次: [カスタムディレクティブ](/guide/custom-directive.html)
