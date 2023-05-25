# Internationalization (i18n) in Your Hop Application

This README guide will help you implement internationalization (i18n) in your Hop application, allowing you to localize your app's text in different languages.

## Folder Structure and Resource Files

1. Create an `i18n` folder at the same level as the the file that requires translation resources.
 
![Here, files from the List folder are using translation resources from the i18n folder](https://github.com/guibros/HopTest/assets/116329812/629ccc32-7def-421c-9a0d-a585124fdc9c "Here files from the List folder are using translation resources from the i18n folder")



2. Inside the `i18n` folder, add one "Content" file for each language you want to support.  Create the first file named `Content.resx` for the default language (e.g., English). 
 
 ![Content files are put in the i18n folder. Here we have two files, one for neutral/english (Content.resx), and one for french (Content.fr.resx)](https://github.com/guibros/HopTest/assets/116329812/80a6d852-757b-48dc-8793-5cbbab8cc96d "Content files are put in the i18n folder.  Here we have two files, one for neutral/english (Content.resx), and one for french (Content.fr.resx)")



3. To add a "Content" file, right-click on the `i18n` folder, select "Add" -> "New Item," and choose "Resource File (C# Items)". Name it `Content.resx`.
<p align="center">
<img width="520" alt="image" src="https://github.com/guibros/HopTest/assets/116329812/693714b2-ca9a-4b7f-9682-161f04cd7838">
<img width="307" alt="image" src="https://github.com/guibros/HopTest/assets/116329812/8033fb4f-5f9f-4ae8-872d-5b6551e6d0d4">
</p>


4. Repeat step 3 for each additional language, but this time add the language suffix to the file name, such as `Content.fr.resx` for French, `Content.es.resx` for Spanish, etc.

## Using Resx Manager

1. Right-click on the `Content.resx` file (the base/neutral file) and click on "Resx Manager".
<img width="352" alt="image" src="https://github.com/guibros/HopTest/assets/116329812/103548f9-6d55-4f22-a0be-e4be5a8db1b7">



2. In the Resx Manager window, you'll see columns.  The "key" column represents the reference name used in your regular code.
![image](https://github.com/guibros/HopTest/assets/116329812/8dedd111-848c-4a5f-aca7-b0f19f8b7489 "Key column, neutral/english column and french column")


3. The "neutral" column is for the base string attached to the key.  For each additional language (each additional `Content.XX.resx` file), a dedicated column will be available (Here, French column). 
 
 
4. To add a keyword, press the white plus button.  Input in cameltoe a keyword corresponding with the words that will be translated. In the neutral and other columns, enter the strings equivalent corresponding to the different column languages.
<img width="676" alt="image" src="https://github.com/guibros/HopTest/assets/116329812/82a84805-7256-4828-ae42-697b82702be9">


## Implementing Translation

There are three ways to implement the translation process:

### Static Translation

Import the NameSpace associated with the current i18n path, for example :

``` xmlns:i18n="clr-namespace:Hop.Study.App.Views.Participants.Edit.i18n"```

Use the syntax `{Static i18n:Content.KeywordForTranslatedString}` to statically load the translation when the page or view is generated.

### Dynamic Translation

Import the NameSpace: 

``` xmlns:i18n="clr-namespace:Hop.Xamarin.Extensions.Localization;assembly=Hop.Xamarin” ```

Use the syntax `{i18n:Translate KeywordForTranslatedString}` to dynamically refresh the translated string when the app's language culture is changed.

### Csharp/CodeBehind translation

Use the syntax `i18n.Content.KeywordForTranslatedString` to statically load the translation when the page or view is generated.

## Changing App Language

To change the app's language, follow these steps:

1. Import the `ILocalizationAdapter` extension.

2. Set the `CurrentCulture` property to the desired culture. For example, to set the language to French, use the following code:

```csharp

ILocalizationAdapter.CurrentCulture = new CultureInfo("fr-FR"); 
```

3. The CurrentCulture property change will raise the OnCultureChanged event, which triggers the event handler. This handler refreshes the translation Resx keywords included in the active pages or views.

Example Code

Here's an example using C#:

```csharp

// Title: Changing App Language

// ILocalizationAdapter is the extension used for dynamic translation.

// When the "CurrentCulture" variable (field "_currentLanguage") changes, it raises the "OnCultureChanged" event.

// The event handler refreshes the translation Resx keywords in the active pages or views.

// Import the ILocalizationAdapter extension.

using Hop.Localization;

// Set the CurrentCulture property.

ILocalizationAdapter.CurrentCulture = new CultureInfo("fr-FR");

```
