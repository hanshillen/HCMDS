# HCMDS
A script that detects whether images, background images, high contrast mode and custom fonts are currently enabled

## Introduction

The High Contrast Mode Detection JavaScript file performs a series of tests that help determine whether or not styles defined by the website are being overwritten. In most cases when the website's styles are being overwritten, it is due to users applying a high contrast theme on the Windows operating system, utilizing their browser or a browser extension to disable images, or applying a user-defined style sheet. After the tests are performed, a collection of attributes get applied to the `<html>` element, allowing developers to reference them and correct any issues that are introduced.

## Demonstration

The High Contrast Mode Detection Script is executed on page load. The [Demo page](http://hanshillen.github.io/HCMDS/hcmode_detection.html)


demo page shows the detection results below after a short delay. Each test can then be used in reference to the samples below to see how each affects the samples as the test values change. Enabling and disabling a high contrast Windows theme as well as applying a user-defined style sheet to see these tests change. Each time a setting is changed, the page must refresh to execute the function.

*   imageResult = true (<span class="enabled">enabled</span>)
*   backgroundImageResult = true (<span class="enabled">enabled</span>)
*   borderColorResult = true (<span class="enabled">enabled</span>)
*   highContrastModeResult = false (<span class="disabled">disabled</span>)
*   lightOnDarkResult = false (<span class="disabled">disabled</span>)
*   sampleFontFamilyResult = true (<span class="enabled">enabled</span>)


## Dependencies

The High Contrast Mode Detection script consists of both a `hc-detect.js` and `clear.gif` file.

The `hc-detect.js` file contains the actual script logic and must be loaded after jQuery (version 1.7.2 or higher) as a result of a dependency.

The `clear.gif` file is a transparent 1 pixel sized image, required for testing the browser's image capabilities. The image is loaded and utilized by the `hc-detect.js` script, so there is no need for the developer to include it in the HTML code.

## How the Script Works

When the page loads, a `<div id="hcTest">` element and attribute are prepended to the `<body>` tag. As this "test" `<div>` is built, the function will add styles necessary to perform each test. The tests are then executed and compare the set styles against the computed styles of the browser. If the styles are different, then specific classes are added to the `<html>` element.

The tests which are performed are as follows:

1.  `imageResult` - This tests to see if an inline HTML image tag has been changed or is not being displayed.
2.  `backgroundImageResult` - This tests if the CSS background image has been changed or is not being displayed.
3.  `borderColorResult` - This tests to see if the color of the border of the test `<div>` has been changed.
4.  `lightOnDarkResult` - This test compares the color of the text against the color of the background. Currently, this test uses yellow, green, white and black for text colors while using black or white for the background color.
    *   If the text is lighter than the background, the script will add a class of `lightOnDark` to the `<html>` element.
    *   If the text is darker than the background, the script will add a class of `darkOnLight` to the `<html>` element.
5.  `sampleFontFamilyResult` - This test checks the `font-family` set in CSS on the `<div>`. If the `font-family` has changed the script will add a class of `ui-helper-nocustomfonts` to the `<html>` element.
6.  `highContrastModeResult` - This test checks the status of any of the previous tests. If any are true, the script will add a class of `ui-helper-highcontrast` to the `<html>` element.

The `ui-helper-nocustomfonts` class is the only indicator that a user has applied a user-defined style sheet. The `ui-helper-highcontrast` is added to the `<html>` element when any of the tests show a change in styles or when images are disabled.

Each browser allows users to disable images, which disables background images in addition to HTML images and results in the `imageResult` test returning `false`. For instructions about how to disable images in a particular browser, see the [Testing Procedure for Each Browser](#testingSection "jump link to show testing procedures for each browser") section.

## About High Contrast Themes

High contrast themes are available on the Windows operating system and serve as an accessibility feature for low vision users. When these themes are applied, background colors and font colors are changed in order to create a higher color contrast, making text and borders easier to see. These changes are also inherited for web content in Internet Explorer and Firefox. Opera and Chrome do not inherit high contrast themes; however, both have browser extensions available that allow users to change the theme.

</div>

<div class="box-container well well-lg">

## About User-Defined Style Sheets

All browsers allow users to load their own style sheets, either through a browser setting or through browser extensions that the user can install. These style sheets can be used to override a web page's CSS styles defined by the website. This way, users can enhance the appearance of a web page to better fit their needs. Examples of modifications that user-defined style sheet are likely to contain are:

*   Increased font sizes
*   Changes to the `font-family` (e.g., to a sans-serif font that is easier for the user to read).
*   Changes in color (e.g., background colors and foreground colors to improve color contrast).
*   Changes to the page layout, allowing all page content to be viewed as one big column that fits the viewport.
*   Removal of background images to ensure proper color contrast for text.

Such user styles will often be defined with the `!important` keyword to ensure that they will be guaranteed to override author defined styles, regardless of how high the specificity of those style declarations are. If a user style uses the `!important` keyword, there is no way for a web author to override it. If the keyword is not used, it's possible for web authors to still override the styles through the use of `!important`.

<span class="label label-info">Note:</span> It's up to the user (or to the tools installed by the user) to determine what styles a user style sheet contains. The user styles will be different from person to person, depending on what works best for them. Because of this, it is not possible for a web developer to predict what kind of styles a user might load, or whether they will use the `!important` keyword.

### Common Issues with User-Defined Style Sheets

There is good chance that a user style sheet contains styles that modify background and foreground colors to increase contrast or remove background images. In that respect, the issues that can be expected are similar to issues that can be expected when a high contrast theme is applied. This means that the High Contrast Mode Detection script can also be used to determine whether or not a custom style sheet is active and is overriding background and foreground colors.

Additionally, a common issue occurs when a web page uses font based icons (i.e. icons that are actually text characters in a custom font set). Such font icons only work if the correct `font-family` is set. If a user-defined style sheet were to override `font-family` for all elements using the `!important` keyword, then font based icons would break.

<span class="label label-info">Note:</span> The `!important` declaration is a way to have the rules you feel are most crucial always be applied. `!important` declarations should be reserved for special needs and users who want to make web content more accessible by overriding default user agent or website stylesheets. In short, code CSS properly and avoid using `!important` wherever possible.

</div>

<div class="box-container well well-lg">

## Enabling High Contrast Themes

### In Windows XP

1.  In Control Panel, make sure you are in Classic View, with all Control Panel icons showing. If not, click Switch to Classic View in the left pane of Control Panel.
2.  Click Accessibility Options to open the Accessibility Options dialog box. Click the Display tab and select the Use High Contrast check box.
3.  Click Settings to open the Settings for High Contrast dialog box. Select the check boxes for the options you want.
4.  Click OK, click OK again, and then click the Close button.

### In Windows 7

1.  Right click on the desktop, select "Personalize" from the context menu.
2.  Under "Basic and High Contrast Themes", select one of the available high contrast themes

<span class="label label-info">Note:</span> It is also possible to turn a high contrast theme on or off using the <kbd><kbd>Left Alt</kbd> + <kbd>Left Shift</kbd> + <kbd>Print Screen</kbd></kbd> keyboard shortcut.

</div>

<div class="box-container well well-lg">

## Testing Procedure for Each Browser

### Safari OSX:

<span class="label label-info">Notes:</span>

*   OSX does not have native high contrast themes like Windows; however, it does have an option to invert the color scheme or apply a grayscale color filter. These options do not introduce the issues that Windows does (e.g., removing background images) when they are applied.
*   Disabling images also disables background images.
*   <span class="label label-important">ISSUE:</span> Background images are removed when images are disabled, but the script does not report background images as being off (i.e., background images are still exposed as a CSS `<style>` property).
*   After turning images off, a reload without cache ( <kbd><kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>R</kbd></kbd> ) is required for the background images to visually disappear.

#### Testing Procedure

*   Develop (enable this menu in Settings > Advanced) > Disable Images

### IE 8+:

<span class="label label-info">Notes:</span>

*   Disabling images also disables background images, (although some versions of IE don't seem to do this).
*   Data URIs (needed for accurate images-off detection) are only supported in 8 and higher, which is why image detection in this script does not work in older versions of IE.

#### Testing Procedure

*   Tools > Internet Options > Advanced > Multimedia > uncheck "Show Pictures"
*   Turn on a Windows high contrast theme (instructions are located in the Enabling High Contrast Themes section on this page).

### Chrome Windows:

<span class="label label-info">Notes:</span>

*   Disabling images also disables background images.
*   Windows high contrast themes are not inherited by Chrome; however, Google offers a browser extension called High Contrast that can be installed and used to apply a color filter on top of the page. Due to the way the extension works, it is not detectable by this script and will not create the problems created by Windows high contrast themes.

#### Testing Procedure

*   Settings > 'show advanced settings' link at the bottom > Privacy 'Content Settings' button > Images: Do not show any images

### Firefox Windows:

<span class="label label-info">Notes:</span>

*   Disabling images also disables background images.
*   Background images using a Data URI source are not removed when images are disabled (and are therefore not used when the script runs in Firefox).

#### Testing Procedure

*   Tools > Options  > Content > uncheck Load Images Automatically
*   Turn on a Windows high contrast theme (instructions on how to do this are located in the Enabling High Contrast Themes section on this page).

### Opera Windows:

<span class="label label-info">Notes:</span>

*   Script correctly detects removed background images in browser based accessibility and high contrast themes.
*   Border colors not overridden in browser based High Contrast Theme (browser issue, not script issue).
*   Disabling images also disables background images.
*   <span class="label label-important">ISSUE:</span> Background images are removed when images are disabled, but script does not report background images as being off (background images are still exposed as style property).

#### Testing Procedure

*   Settings > Websites > Images > Do not show any images

#### General Notes:

*   All browsers will hide background images when disabling images in the browser. Only Chrome and Firefox correctly expose `backgroundImageResult` as `false` in this case, the others incorrectly expose `true` here. For this reason, `highContrastModeResult` is `true` when either `imageResult`, `backgroundImageResult`, or `borderColorResult` is `false`.

</div>

<div class="box-container well well-lg">

## Problems Caused by High Contrast Themes

When a high contrast theme is enabled, the following changes are applied to the styles on a web page for browsers that inherit high contrast themes:

*   Foreground colors (text, borders) will be overridden to the high contrast foreground color (e.g., yellow)
*   Background colors will be overridden to the high contrast background color (e.g., black)
*   Background images will be removed

These changes can cause the following issues:

*   Any information that relied on CSS background styles will no longer be visible so, for example:
    *   Icon buttons with CSS background images become unusable since the icon will disappear.
    *   CSS background colors used to indicate selection or focus will no longer be visible.
    *   CSS background colors used to create a "fill" (e.g., a progress bar that slowly fills up using a background color) will become invisible.
*   If a container that overlaps other content (such as drop down menus, dialogs, etc.) did not originally have a background color set, it may become transparent.
*   Any information that depended on color (background or foreground) is likely to become invisible. For example, if red and green border colors are used to make a distinction between elements, those elements will all have the same border color in a Windows high contrast theme.
*   When an element is styled with the IE specific `filter` property to create a gradient background, this gradient is not removed or modified. Since the background color does not change and the foreground does, this may result in text being difficult or impossible to read.

</div>

<div class="box-container well well-lg">

## How to Fix Issues Using the Script

When a high contrast theme is detected by the script and the `ui-helper-highcontrast` class has been added to the page's `<html>` element, issues caused by the theme can be fixed either through scripting or through CSS (depending on the specific issue). For example, the following fixes can be applied when the script detects a high contrast theme.

### Example 1: Fixing Issues Related to IE "Filter" Styles

The screenshot below shows how `filter` gradient styles are not properly removed in Internet Explorer when a high contrast theme is active. The foreground colors are changes to a light color (yellow text and light purple links), but the background color is not changed to a dark color. This makes some of the text difficult if not impossible to read.

![Screenshot of a web page in High Contrast Mode, where text is difficult to read because of light foreground colors on a light background](images/screen1.png)  

#### How to Fix Issues Related to IE "Filter" Styles

The code snippet below shows how a problematic `filter` style can be overridden using the `ui-helper-highcontrast` class:

#### Source code for IE Filter Style fix

    #medicare-you a.hdr-link-help {
      padding:8px 10px;
      color: rgb(255,255,255);
      font-weight: bold;
      filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ecf9ff', endColorstr='#ffffff',GradientType=0 ); /* IE6-8 */
    }

    /* Override the previous selector when a high contrast theme is enabled, negate the filter style:*/ 

    .ui-helper-highcontrast #medicare-you a.hdr-link-help{
      filter: none;
    }

### Example 2: Fixing Issues Related to Background Images

The screenshot below shows two versions of a carousel widget. The one on the left is how the carousel normally appears without any user modifications such as a high contrast theme or user-defined style sheet whereas the one on the right has been altered by a high contrast theme. In the high contrast themed version, the "next" and "previous" buttons have become invisible because they were implemented as CSS background images. This example issue can be fixed by using the Adobe Blank `font-family`. To read more about Adobe Blank, please visit the [Font Glyphs page](#fontglyph "Assets Font Glyphs page").

![Screenshot of a web page in High Contrast Mode, where text is difficult to read because of light foreground colors on a light background](images/screen3.png)  

#### How to Fix Issues Related to Background Images

The code snippet below shows how a "home" icon button with a background image is changed to a text button when a high contrast theme is detected. The button normally contains hidden text (which also provides the button's accessible name for screen readers). When a high contrast theme is active, the `ui-helper-highcontrast` class overrides the styles for the hidden text so that it becomes visible. Note that the width of the button needs to be reset to `auto` so that the text is not cut off.

#### Source code for background image fix

    <!-- In this example, the class 'btn-img' links a CSS background image but will disappear when the background images are disabled -->
    <button class="btn btn-primary btn-img">
    <!-- Using the Adobe Blank font will only show in high contrast mode when implemented properly -->
        <span class="adobeBlank">Home</span>
    </button>

### Example 3: Fixing Issues Related to Font Icons

If a user-defined style sheet overrides `font-family` styles, the script will detect this and add the "`ui-helper-nocustomfonts`" class to the `<html>` element.

To prevent the icons from disappearing or breaking when a user has a high contrast theme applied, you should include the `assets.core.js` file to the end of your page. This has a function which will find any Font Awesome Icon or Glyph Icon and add inline styles to keep the correct `font-family`. Assets <span class="AssetsVersion">3.4.1</span> uses this technique.

If you choose not to use the `assets.core.js` file, you may use the function below to achieve the same results.

#### Source code for font icon fix

     $('.fa').attr("style", "font-family:'FontAwesome' !important");
     $('.glyphicon').attr("style", "font-family:'Glyphicons Halflings' !important");

</div>

<div class="box-container well well-lg">

## Notes for Developers

None

</div>

<div class="box-container well well-lg">

## Notes for Testers

*   When testing the High Contrast Mode Detection Script, make sure to turn on a Windows high contrast theme first before loading or refreshing the page. The script will only perform its detection when the page loads. If the page has already rendered, refresh the page to see the script take effect.
*   The script can also be used to check for removed background images or overridden border colors created by user-defined style sheets.
*   The script takes a few seconds when the page loads to perform the detection. Issues related to high contrast themes may still be visible during those few seconds.

</div>

<div class="box-container well well-lg">

## Keyboard Operations

None applicable

</div>

<div class="box-container well well-lg">

## Known Accessibility Issues

In most browsers, disabling images also removes background images, but not in a way that can be detected by the script.

</div>

</section>