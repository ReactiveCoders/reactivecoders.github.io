---
layout: post
title: Fonksiyonel Programlama

status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Fonksiyonel Programlama, günümüz web dünyasında her programcının bilmesi ve uygulaması gereken bir programlama paradigmasıdır. Nedenini bu yazının ilerleyen satırlarında bulacaksınız. Bu konu hakkında araştırma yaparken Türkçe kaynağın çok az ve yetersiz olduğunu gördüm. Bende bu konuyu dilim döndüğünce blogumda paylaşmaya karar verdim. Yeni öğrendiğim bir konu olduğu için, hatalı ve yanlış anlaşılmaya müsait olan noktalar olabilir. Eğer fonksiyonel programlamaya yıllarınızı verdiyseniz bu yazıya katkıda bulunabilirsiniz. Eğer benim gibi bu konuda yeniyseniz (devamının gelmesini umduğum) bu giriş yazısı umarım sizin için iyi bir başlangıç olur. 

Fazla vakit kaybetmeden gelin fonksiyonel programlama paradigmasını daha yakından inceleyelim.

![Fonksiyonel Programlama](/files/2013/03/functional-programming.png)

## Nedir? ##

Programlama dilleri, imperatif (Java, C, C++ vb.) ve dekleratif (Lisp, Haskel vb.) diller olmak üzere  ikiye ayrılır. Fonksiyonel programlamada bir deklaratif bir dildir. Bu dil, matematikteki fonksiyonlara ait tüm özellikleri taşır. Fonksiyonların aldıkları parametreler ve geri dönüş değerleri sabittir ve değişiklik göstermez. Yani, yan-etkiler (**side-effect**) bulunmaz.

Yıllarca nesne yönelimli programlama dilleriyde çalışmış birinin, hemen fonksiyonel paradigmaya ait konuları anlaması çok kolay olmuyor maalesef. Nesne yönelimli bir programcının öncellikle değişkenler ve döngüler olmadan nasıl kod yazacağını düşünmesi gerekiyor. Bize hep herşeyi nesneler olarak küçük görevlere ayırmamız sonra bu görevleri doğru bir şekilde sınıflamamız öğretildi. Fonksiyonel programlamada, herşey fonksiyonlarla yapılır. Merak etmeyin fonksiyonel programlamanın ne olduğunu *"Nasıl"* başlığı altında ve örnekler yaptıkça daha iyi anlayacağız. 

Fonksiyonel programlamada değişkensiz ve döngüsüz bir hayat *nasıl olur* sorusuna güzel bir örnek olarak; hepimizin az-çok bildiğini düşündüğüm excel gibi elektronik tablo (spreadsheets) türevi yazılımları verebiliriz. Elektronik tablo yazılımlarında her hücre bir değer alır ve geri döner. İç içe fonksiyonlar çağrılabilir. Hücre grubu liste olarak bir başka hücreye parametre olarak verilebilir. Birbirinden habersiz olarak sadece kendi etki alanlarından beklenen işi yaparlar. Bu konuda stackoverflow'da okuduğum [makalelere](http://stackoverflow.com/a/1956514/204928) göz atabilirsiniz.

Bir başka örnekte, unix terminallerde, bir komut çıktısını başka bir komut setine aktarmak için kullanılan pipe (|) güzel bir fonksiyonel çağrı örneği olabilir. Aşağıdaki örneği inceleyebilirsiniz.

<!-- highlight sh lineos -->
{% highlight sh %}
# "IMPERATIVE TERMINAL"
$ ./program1
$ ./program2 --param1=1
$ ./program3
 
# "FUNCTIONAL TERMINAL"
$ ./program1 | ./program2 --param1=1 | ./program3
{% endhighlight %}

Fonksiyonel programlama deyince; web geliştiricisi olarak, hepimiz aslında fonksiyonel programlamanın bazı özelliklerini farkında olarak yada olmayarak kullanıyoruz. Eğer fonksiyonel programlama hakkında biraz araştırma yaptıysanız, "javascript fonksiyonel bir dildir" gibi birşeyler duymuş olabilirsiniz. **first-class** fonksiyonları ve **lambda**ları desteklemesi göz önünde bulundurulursa fonksiyonel bir dil olarak düşünülebilir. Fakat fonksiyonel programlama sadece bu konulardan ibaret değildir. Bu yüzden literatülde javascript bir fonksiyonel programla dili olarak kabul edilmez. [stackoverflow'daki şu tartışmayı](http://stackoverflow.com/a/3962690/204928) inceleyebilirsiniz.

Şimdi gelin neden fonksiyonel programlama gerekli onu biraz irdeleyelim.


## Neden? ##

Günümüz dünyasında web eş-zamanlı, dinamik ve ölçeklenebilir bir hale geldi. Örneğin, gönderdiğimiz bir tweet anlık olarak takipçiler tarafından görüntülenir ve arama sonuçlarına yansıtılır. Yüzlerce insan aynı anda bir web sitesini, bir fotoğrafı veya bir blog yazısını facebookta beğenebiliyor yada paylaşabiliyor. Altında ciddi bir mühendislik olan bu siteler nasıl hızlı ve anlık olarak çalışabiliyorlar hiç düşündünüz mü? Cevabınız işlemcilerin veya donanımların güçlenmesi, moore yasası kanunun geçerliliğini koruması vb gibi cevaplar aklınıza geliyorsa maalesef yanılıyorsunuz. Donanımların güçlenmesi tek başına asla yeterli olmamış ve olmayacaktır.

> **Moore Yasası** Her 18 ayda bir tümleşik devre üzerine yerleştirilebilecek bileşen sayısının iki katına çıkacacağını, bunun bilgisayarların işlem kapasitelerinde büyük artışlar yaratacağını, üretim maliyetlerinin ise aynı kalacağını, hatta düşme eğilimi göstereceğini öngören deneysel gözlem.

Donanım mühendisleri *Moore Yasası* doğrultusunda, fiziksel sınırları zorlayarak sona geldiklerinde, paralel çekirdek mimarileri tasarlamaya ve geliştirmeye başladılar. Böylece hayatımıza 2, 4 vb... şeklinde çok çekirdekli, paralel çalışabilen işlemciler girdi. Hız için yapılan bu geliştirme beraberinde paralel programlama ihtiyacınıda beraberinde getirdi. 

Paralel programlama yaparken dikkat edilmesi gereken en önemli konu non-deterministik olmasıdır. Yani aynı sonuçlar altında aynı durumu vermesidir. Web dünyasında bu nedenle durum tutmayan (**stateless**) önemlidir. Concurrent programlamada thread konuları söz konusu olduğunda değişmeyen veriler (**immutable**) kullanmak ve saf yani (**pure-function**) yan-etkisi olmayan fonksiyonlar kullanmak gereklidir. 

Bu yüzden paralel programlama algoritmaları ve çözümlerinin yolu mutlaka fonksiyonel programlama pratiklerinden geçer.

Paralel programlama ve donanım neden yeterli olmadığı bir Google örneği vermek istiyorum. Google'ın ilk kurulduğu yıllarda tüm interneti depolamak için neden normal PCler kullandı hiç düşündünüz mü? Bunun yerine süper bilgisayarlar üzerinde koşan verilerin kudretli kahini Oracle'ın veritabanı ile siteleri indekslemek yerine elektronik tablo gibi kolon tabanlı bir veri mimarisi kullandı? Maalesef çok büyük verileri yönetmek için ilişkisiel veritabanlarının yük dağılımı ile ilgili sorunları oluşmaya başlıyor. Ayrıca Oracle gibi veritabanları pahalı bilgisayarlar üzerinde koşarlar. Bozulma ihtimallerine karşı yedekleme maaliyeti çok yüksek. Google bir mühendislik şirketi olarak fonksiyonel programlamada olduğu gibi bir çok  düğümden (node) oluşan mozaik bir mimari kurdu. Bu mimari sayesinde, ölçeklenebilirliğin gerektirdiği bölünebilme toleransı *(partition tolerance)*  sağlanmış oldu *(bknz. [CAP Theorem](http://en.wikipedia.org/wiki/CAP_theorem))*. Ucuz maaliyetli bu bilgisayarlardan bir yada birkaçı bozulsa bile arama motoru çalışmaya ve sonuçlar getirmeye devam edecekti. Kısacası Google'ın *BigTable* adını verdiği sonra *Apache Foundation* tarafından bir benzeri yapılan *Hadoop* teknolojisi fonksiyonel programlama paradigmasını kuralları üzerine kurulmuştur. (bknz. [Map-Reduce](http://hadoop.apache.org/docs/r1.0.4/mapred_tutorial.html))

İşte web dünyasında fonksiyonel programlama dillerine sıcak bakmasının sebebi budur. *Dağıtık mimariler kurmak!* Fonksiyonel programlama dilleri dağıtık mimariler için bir kodlama disiplini sağlar. Paralel programlamada istenmeyen yan-etkisi (side-effect) bulunan fonksiyonlar olmasına izin verilmez. Eğer yan etki gerektiren bir durum varsa, Bu gibi durumlarda **monad** diye adlandırılan bir teknik kullanılır.

İşte bu sebeple bir web programcısı için fonksiyonel programlama önemlidir. Belki bu disiplini kazandırmak için; PHP, Java gibi eski web dilleri fonksiyonel paradigmayı destekler özellikleri kendilerine katmaya başladılar.


## Nasıl? ##

Aşağıda genel fonksiyonel programlama kavramlarına kısaca değinilmiş ve örnekler verilmiştir.

### Pure Functions ###

Saf fonksiyonlar, yan etki barındırmayan fonksiyonlara denir. Peki yan etki nedir?

Yan-etki *(side-effect)*, genel olarak programlamada bir fonksiyonun kendi kapsama (scope) alanı dışında birşeyleri değiştirmesi durumudur. 

Fonksiyonel programlamada "değisken" diye bir kavram olmadığından ve her şey eninde sonunda bir fonksiyon oldugundan "degistirebileceginiz" degiskenler ve durumlar aslında yoktur. Ama yan etki illa, değişken olması gerekmez. Konsola çıktı yazmak, loglama yapmak, ekrana pencere çıkarmak, sistemdeki dosya, yazıcı, kamera gibi başka kaynaklara erişmek hepsi yan etkiye sebep olur.

Bu yüzden derleyici yan etkiye yol açan fonksiyonları sıralı olarak çağırır. Paralel çalışmalarına izin vermez.

{% highlight scala %}
def pureFunc(x : Int, y : Int) = x + y
{% endhighlight %}

{% highlight scala %}
def nonPureFunc(x : Int, y : Int) = println(x + y)
// because write to screen (side-effect alert!)
{% endhighlight %}

### Lists and Tuples ###

Fonksiyonel programlamada listeler çok önemlidir. Veri grupları (tuples) ise farklı veri tiplerini barındırabilir.

{% highlight scala %}
// tuples example
val tuple = new Tuple3(1, "hello", Console)
 
// list example
val days = List("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday")
{% endhighlight %}


### Recursive Functions ###

Döngü yerine kendini çağıran (**recursive**) fonksiyonlar kullanılarak yapılır demiştik hatırlarsanız. Değişken diye birşey yoktur, değişkenlerde fonksiyonların kendisidir demiştik.

{% highlight scala %}
def whileLoop(cond: =>Boolean, block: =>Unit) : Unit =
  if(cond) {
    block
    whileLoop(cond, block)
  }
 
//scala> val a = Array(1, 2, 3)
//scala> var i = 0
//scala> whileLoop(i < a.length, { println(i); i += 1 })
//1
//2
//3
{% endhighlight %}

### High-Order Functions ###

Herşey fonksiyonlar yapılır ve fonksiyonlarda değişken gibidir demişken, bir fonksiyon başka bir fonksiyonu parametre olarak alabilir. Buna **high-order functions** denir.

{% highlight scala %}
def apply(f: Int => String, v: Int) = f(v)
def layout[A](x: A) = "[" + x.toString() + "]"

// println( apply( layout, 10) )
//[10]
{% endhighlight %}

### Anonymous Functions (Lambda Expressions) ###

Bir fonksiyon tanımı yapılmadan yani bir kod blogu olarak kullanılabilir. Buna **lambda** yada **anonymous functions** denir. 

{% highlight scala %}
(x: Int) => x + 1
{% endhighlight %}

### Currying ###

Fonksiyona ait parametrelerin azaltılması gerekebilir. Buna **currying** denir.

{% highlight scala %}
def divisibleby(factor : Int) (value : Int) = value % factor == 0 
val evens = (1 to 10).filter(divisibleby(2))

// divisibleby: (factor: Int)(value: Int)Boolean
// evens: scala.collection.immutable.IndexedSeq[Int] = Vector(2, 4, 6, 8, 10)
{% endhighlight %}

Ayrıca domain specific bir dil tanımlarken de kullanabilirsiniz, Güzel bir sintatik görünüm sağlar. Aşağıda bununla ilgili bir örnek bulabilirsiniz.

{% highlight scala %}
def whileLoop(cond : =>Boolean)(block : =>Unit) : Unit =
  if(cond) {
    block
    whileLoop(cond)(block)
  }

//whileLoop(i < a.length) {
//  println(a(i))
//  i += 1
//}
{% endhighlight %}

Bir fonksiyon currying haline aşağıdaki şekilde getirilebilir.

{% highlight scala %}
def add(x:Int, y:Int) = x + y
val addCurried = Function.curried(add _)

add(1, 2)   // 3
addCurried(1)(2)   // 3
{% endhighlight %}

Currying olan bir fonksiyon currying'siz hale aşağıdaki şekilde getirilebilir.

{% highlight scala %}
def add(x:Int)(y:Int) = x + y
val addUncurried = Function.uncurried(add _)

add(3)(4)  // 7
addUncurried(3, 4)  // 7
{% endhighlight %}

### First-Class Functions (Closure) ###

Fonksiyonel programlamada tip sınıfı **first-class citizen** diye bir konu vardır. Üç çeşittir. Öğelerinden biri, **first-class function** konusunudur. Buna göre;

 - bir fonksiyon başka bir fonksiyonu parametre olarak alabilir. 
 - bir fonksiyonu geri dönüş değeri olarak verebilir. 
 - bir fonksiyon bir değer olarak atanabilir.

**first-class function** aynı zamanda **closure** olarakta bilinir.

{% highlight scala %}
def makeIncrementer(inc: Int): (Int => Int) = (x: Int) => x + inc

val a = makeIncrementer(10)
// a: (Int) => Int = 

val b = a(25)
// res4: Int = 35
{% endhighlight %}

### Monads ###

Monad'lar fonksiyonlara kontrollü yan-etki desteği vermek için kullanılan bir tekniktir. Monad bir tür context olarak düşünüebilir. Monadlar 3 operatörle tanımlanır. Bunlar;

**bind**

Context içindeki bir değeri geçici olarak dışarı çıkarıp, ona bir değişiklik uygulayıp tekrar context'e sokar.

**return**

Herhangi bir değeri olabilecek en basit sekilde context'e sokar.

**run**

bir monad ayrica bir programi (~ computation) temsil ediyor olarak da
dusunulebilir. temsil edilen programi calistirip sonucu hesaplamak icin
kullanilir.

{% highlight scala %}
trait Monad[M[_]] {
  def unit[A](x : A) : M[A]

  def bind[A, B](m : M[A], f : A => M[B]) : M[B]
}

implicit object OptionMonad extends Monad[Option] {
  def unit[A](x : A) = Some(x)

  def bind[A, B](m : Option[A], f : A => Option[B]) = m.flatMap(f)
}

implicit object ListMonad extends Monad[List] {
  def unit[A](x : A) = List(x)

  def bind[A, B](m : List[A], f : A => List[B]) = m.flatMap(f)
}
{% endhighlight %}

Philip Wadler'ın [Monads and Composable Continuations](http://mirrors.csl.sri.com/www.brics.dk/%257Ehosc/local/LaSC-7-1-pp39-56.pdf) hakkındaki makalesi önerilir. 

### First-Class Controls (Continuations) ###

Bir nevi fonksiyonel programlamanın GOTO deyimidir. 

{% highlight scala %}
import scala.util.continuations._

def reify[A, M[+_]](x : => A @cpsParam[M[A], M[A]])(implicit monad : Monad[M]) : M[A] =
  reset { monad.unit(x) }

class Reflective[+A, M[_]](m : M[A], monad : Monad[M]) {
  def reflect[B]() : A @cpsParam[M[B], M[B]] = {
    shift { (k : A => M[B]) =>
      monad.bind(m, k)
    }
  }
}

implicit def reflective[A](xs : Option[A])(implicit monad : Monad[Option]) =
  new Reflective[A, Option](xs, monad)

implicit def reflective[A](xs : List[A])(implicit monad : Monad[List]) =
  new Reflective[A, List](xs, monad)

reify {
  val left = List("x", "y", "z").reflect[(String, Int)]
  val right = List(4, 5, 6).reflect[(String, Int)]

  (left, right)
}
{% endhighlight %}

Monad ve Continuation konusunda araştırmalarım devam ediyor. Daha detaylı bir bilgilendirme, bir sonraki yazımda olacak.

**Günceleme:** 2014 yılı boyunca bu konuda bir yazım olamadı.
