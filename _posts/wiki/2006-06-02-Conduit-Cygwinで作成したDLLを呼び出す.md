---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>ちょっと一般的な JNI の話です。</p>
<p>Java から呼び出す DLL は <a href="http://cygwin.com/">Cygwin</a> の gcc で作成することが可能。ここで紹介した環境は以下の通り。</p>
<ul>
<li>Java(TM) 2 Runtime Environment, Standard Edition (build 1.4.1_01-b01)</li>
<li>gcc version 3.2 20020927 (prerelease)</li>
<li>GNU dllwrap 2.13.90 20021118</li>
</ul>
<p>作成手順は以下の通り。</p>
<h4>1. JNI ヘッダファイルを修正</h4>
<p><a href="http://java.sun.com/j2se/">J2SDK</a> のインストール先の include\win32\jni_md.h を開き、jlong の定義を</p>
<pre>#ifdef __GNUC__
typedef long long jlong;
#else
typedef __int64 jlong;
#endif
</pre>
<p>と修正。</p>
<h4>2. JNI 呼び出し用の各ファイルの用意</h4>
<pre>private static synchronized native int nativeInstallFile(byte[] user, byte[] filename);
</pre>
<p>というような native メソッドを持ったクラスを用意する。また、このクラスの static initializer あたりに、</p>
<pre>static {
  System.loadLibrary(&quot;clipsyncjni&quot;);
}
</pre>
<p>というような、DLLを読み込むコードを入れておく。クラスをコンパイルしたら、</p>
<pre>javah クラス名
</pre>
<p>としてヘッダファイルを生成する。このヘッダファイルに沿って、C の関数を用意する。この際の注意点は、</p>
<ul>
<li>DLL に文字列等を渡す場合は、Java 側でコード変換を行って byte で渡したほうが無難。</li>
<li>DLL からさらに DLL を呼び出す場合は、LoadLibrary, GetProcAddress, FreeLibrary を使う。</li>
</ul>
<p>というところ。</p>
<h4>3. Cのソースのコンパイル</h4>
<p>Cのソースは、</p>
<pre>gcc -c -Ic:/j2sdk1.4.1/include -Ic:/j2sdk1.4.1/include/win32 -O2 -mno-cygwin InstAideBridgeJNI.c
</pre>
<p>などとしてコンパイルする。-I の指定先は <a href="http://java.sun.com/j2se/">J2SDK</a> のインストール先に応じて変更する。</p>
<p>-mno-cygwin を指定していないと、DLL の利用時に cygwin1.dll が必要になる。</p>
<h4>4. DLL の作成</h4>
<p>DLLは、</p>
<pre>dllwrap -mno-cygwin --add-stdcall-alias -mwindows --target=i386-mingw32 -o clipsyncjni.dll -s InstAideBridgeJNI.o
</pre>
<p>などとして作成する。特に --target=.. がないと、DLL の読み込み時にエラーになる。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
