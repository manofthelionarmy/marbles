[Links?](#)
[Embbed Videos?](#)
[Dart Docs](https://dart.dev/guides)
[Flutter Tools Nvim plugin](https://github.com/akinsho/flutter-tools.nvim)
[Just in time compilation](https://en.wikipedia.org/wiki/Just-in-time_compilation)
[Ahead of time compilation](https://en.wikipedia.org/wiki/Ahead-of-time_compilation)
[Dart platform](https://dart.dev/overview#platform)
# Summary

----
# Related Stuff
[[Just In Time Compiler]]
#dart
#flutter

----
# Notes:
- I want to learn how to build desktop applications with Flutter, which means I need to learn the Dart programming language.
- I followed the guide on how to install the dart sdk:
	- https://dart.dev/get-dart
- The docs looks really good and there are a lot of new stuff to learn.
	- I guess I can learn some stuff from watching tutorials. 
- Should I do some web app stuff first?
> Dart is a client-optimized language for developing fast apps on any platform. Its goal is to offer the most productive programming language for multi-platform development, paired with a [flexible execution runtime platform](https://dart.dev/overview#platform) for app frameworks.
- I can build multiplatform apps from a single code base in a language called Dart.
- It has what they call an `execution runtime platform`.
> Dart’s compiler technology lets you run code in different ways:
>	- **Native platform**: For apps targeting mobile and desktop devices, Dart includes both a <mark style="background: #FFB86CA6;">Dart VM</mark> with <mark style="background: #FFB86CA6;">just-in-time (JIT) compilation</mark> and an <mark style="background: #FFB86CA6;">ahead-of-time (AOT) compiler</mark> for producing machine code.
>    - **Web platform**: For apps targeting the web, Dart can compile for development or production purposes. Its web compiler translates Dart into JavaScript.
- [Just in time compilation](https://en.wikipedia.org/wiki/Just-in-time_compilation)
### Sat, Nov 25, 2023:
- For some reason, coc-flutter is really slow when using treesitter support for syntax highlighting.
- For some reason, using treesitter syntax-highlighting support in lunar vim (which uses native lsp) with dart lsp works flawlessly and I get no lag.
- I ended up disabling syntax hightlighting via treesiter by uninstalling the treesitter grammar for dart and ensuring it skips installing it all the time. I then googled a dart syntax highlighter and I found it.
- I did find a cool flutter tools plugin, but it seems to have errors if I'm not in a proper flutter project. The issue I got is reported here in the github repo:
- https://github.com/akinsho/flutter-tools.nvim/issues/194  
- Maybe once I install the flutter sdk, things will work properly. 
#### 2:50pm:
- I had to uninstall dart that I had installed and I had to install the flutter sdk. It comes with a compatible version of dart.
- After installing, I had to run:
```bash
flutter doctor -v
```  
- I had to install pkgs via apt:
```bash
sudo apt install clang cmake ninja-build

sudo apt install libgtk-3-dev

```
- After creating a project, I tried to run 
```bash
flutter run
```
- But I got an error a package was missing:
	- https://stackoverflow.com/a/74611723
```bash
sudo apt install libstdc++-12-dev
```
- I then tried to run the project again, but got another error. I then found the solution here:
	- https://github.com/gskinnerTeam/flutter-folio/issues/70#issuecomment-1021325665 
```bash
flutter clean
flutter run -d linux
```
- After this, my project built and came up:
  ![[Pasted image 20231125145720.png]]
### Sun, Nov 26, 2023
- Flutter uses a ui design framework called material:
	- https://m3.material.io/develop/flutter  
> a set of suggestions, rules & guidelines that help you build beautiful user interfaces 
[]()
> highly customizable and extendable

### Sun, Nov 26, 2023
- Dart uses JIT and AOT:
	- https://dart.dev/overview#platform
>During development, a <mark style="background: #FFB86CA6;">fast developer cycle is critical for iteration</mark>. The Dart VM offers a <mark style="background: #FFB86CA6;">just-in-time compiler (JIT)</mark> with incremental recompilation (enabling hot reload), live metrics collections (powering DevTools), and rich debugging support

> When apps are ready to be deployed to production—whether you’re publishing to an app store or deploying to a production backend—the <mark style="background: #FFB86CA6;">Dart ahead-of-time (AOT) compiler can compile to native ARM or x64 machine code</mark>. Your AOT-compiled app launches with consistent, short startup time.

> The AOT-compiled code runs inside an efficient <mark style="background: #FFB86CA6;">Dart runtime</mark> that enforces the sound Dart type system and manages memory using fast object allocation and a [generational garbage collector](https://medium.com/flutter-io/flutter-dont-fear-the-garbage-collector-d69b3ff1ca30).

## Questions:
- Will installing the flutter sdk also install dart? 
	- Do I have to uninstall dart?
## Follow Up:
- Try and setup nvim for flutter and dart. If not, maybe I have to use android studio?
- I want to build desktop apps, not apple or android apps.
- I don't know how much resources the emulators for android and apple apps will take.
