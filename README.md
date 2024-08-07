
# app_local

**Localize your Flutter app to multiple locales within seconds**

### ** Note: This package is updated version from [flutter_locales](https://github.com/iampopal/flutter_locales) **
## Why Flutter Locales
✅ Easily Localize your app
✅ Change App Locale within the app
✅ Get Last Changed locale on App starts
✅ Save Locale Language After changed buy `LocaleNotifier`
✅ Get Translation with `LocaleText('key')` Widget

## Example App
![Example app assets/lang](https://abom.me/packages/flutter_locales2/locales2_gif.gif)


## 1) Create locales assets
Create an assets/lang folder at the root of your project and add your locales json files.   
**like:**  
![Example app assets/lang](https://abom.me/packages/flutter_locales2/ex2.png)

write the json code and add the text you want and give it a key like the img:  
![Example app assets/lang](https://abom.me/packages/flutter_locales2/ex.png)
* your locale files name shall be Name of the language
  * like:
    * **en.json** For english locales
    * **ar.json** for Arabic locales

````json  
/// English lang code  
{  
  "welcome": "Welcome to the App",  
  "change_lang": "Change the language"  
}  
  
/// Arabic lang code  
{  
  "welcome": "مرحبا بك في التطبيق",  
  "change_lang": "تغيير لغة التطبيق"  
}  
  
  
````  
## 2) Include package and assets
> Include latest dependency of app_local
```  
dependencies:  
  flutter:  
    sdk: flutter  
  app_local:  
```  
> Include {languages} folder  path
```  
flutter:  
  uses-material-design: true  
  assets:  
    - assets/lang/  
    # OR ANY FOLDER YOU WANT
```  


## 3) Initialize app

> Replace your main app with
```dart  
void main() async {  
  WidgetsFlutterBinding.ensureInitialized();  
  await Locales.init(
  // Languages codes
  localeNames: ['en', 'ar'],
  // the path of the languages folder
  localPath: "assets/lang/"); // get last saved language  
  // remove await if you want to get app default language  
  
  runApp(MyApp());  
}  
```  
* `['en','ar']` are language codes of `.json` files located in located in `{languages}` folder
* You can replace these languages with your languages

> Wrap your `MaterialApp` with `LocaleBuilder` then provide locale to app
```dart  
class MyApp extends StatelessWidget {  
  @override  
  Widget build(BuildContext context) {  
    return LocaleBuilder(  
      builder: (locale) => MaterialApp(  
        title: 'App Local',  
        /// Make sure to add this line   
        localizationsDelegates: Locales.delegates,  
        /// Make sure to add this line   
        supportedLocales: Locales.supportedLocales,  
        /// Make sure to add this line   
        locale: locale,  
        home: HomeScreen(),  
      ),  
    );  
  }  
}  
```  
* `LocaleBuilder` rebuild the app you change the app locale by `Locales.change(context, 'ar')`

## Locale Text
`LocaleText` Widget Use to translate a key
```dart  
LocaleText(`welcome`);  
```  
* `LocaleText` Translate a key to string

### Locale String
* To get a key translated call
```dart  
Locales.string(context, 'welcome')  
  
// with extension  
context.localeString('welcome');  
```  

## Change App Locale
To change app locale language
```dart  
Locales.change(context, 'ar');  
  
//with extension  
context.changeLocale('ar');  
```  
- When you change app automatically saves at Locale

### Current Locale Language
- To get current locale call
```dart Locales.currentLocale(context);  
  
//with extension  
context.currentLocale;  
```