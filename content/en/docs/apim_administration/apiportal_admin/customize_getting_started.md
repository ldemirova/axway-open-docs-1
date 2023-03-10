---
title: Customize API Portal look and feel
linkTitle: Customize look and feel
weight: 20
date: 2019-07-30T00:00:00.000Z
description: Customize the look and feel of API Portal with your own logos,
  colors, and so on.
---

For internally-facing API deployments, you can deploy API Portal "as is" using the out-of-the-box Axway branding. This type of deployment requires no customization.

For external-facing API deployments, you may want to customize API Portal to provide a branded developer portal experience. This type of deployment contains a collection of style settings that can be configured in your account, including logos, colors, fonts or you can perform advanced modification of the layout and structure.

## Supported API Portal customization

Customization can be performed at the following levels:

* **Customization through configuration**: Use the Joomla! Admin Interface (JAI) (`https://<API Portal host>/administrator`) to change CSS stylesheets, templates, and layouts. These types of customizations can be upgraded and retained when you move to a new version. The customization does not modify the API Portal source code and is supported by Axway.
* **Customization through the addition of Joomla! extensions**: The Joomla! CMS offers thousands of extensions that are available from their website. Axway supports only extensions that are delivered out of the box (EasyBlog and EasyDiscuss).

## Prerequisites

To get started with customization, you need the following:

* API Portal installed and configured. For more details, see the [API Portal Installation and Upgrade Guide](/docs/apim_installation/apiportal_install/).
* An API Portal user account. When you log in, the default API Portal web page is displayed, so you can check how the changes look to your end users.
* Basic understanding of Joomla! ThemeMagic. This feature enables you to change CSS stylesheets, templates, and layouts. For more advanced modifications, you can modify the PHP source code to customize API Portal, such as to change the functionality of pages and to extend by adding new pages.

## Customize using Purity III template

This section describes how to customize your portal using the Purity III template.

### Customize with ThemeMagic

API Portal uses the Joomla! framework to extend the ThemeMagic feature. ThemeMagic is part of the Purity III template that is based on the T3 template framework. For more details on how to use and customize Purity III, see the [official Purity III documentation](https://www.joomlart.com/documentation/joomla-templates/purity-iii).

With ThemeMagic, you have an administrative interface for creating or modifying themes, such as colors and fonts. Use the live preview to follow how your theme configuration looks before saving the changes. Themes are built using theming variables based on the [Less](https://lesscss.org/) language.

#### Open ThemeMagic

1. Log in to the Joomla! Administrator Interface (JAI), and click **System > Site Templates**.
2. Select the style **Purity III - Default**.

    ![Joomla user interface with Purity III selecting the styles](/Images/APIPortal/JoomlaThemeMagicStyles_j4.png)

3. Select **ThemeMagic**. ThemeMagic opens your portal home page with theme variables are displayed on the left.

    ![Joomla User Interface with Purity III theme magic](/Images/APIPortal/joomlathememagic.png)

    {{< alert title="Note" color="primary" >}}The **ThemeMagic** button is no longer available in API Portal versions from [May 2022](/docs/apim_relnotes/20220530_apip_relnotes/) onwards, that is, after the migration to Joomla! 4.x. For more information, see [Theme Customization in Joomla 4](#theme-customization-in-joomla-4).{{< /alert >}}

4. In the ThemeMagic window, sign in to API Portal. You are now ready to start customizing your portal. ![Screenshot on ThemeMagic](/Images/APIPortal/JoomlaThemeMagiconAPIPortal.png)

#### Create a new theme

API Portal includes one theme named **Axway**. Create any additional themes from a copy of the Axway theme to ensure that they work properly.

1. Open the ThemeMagic tool, and ensure that the theme selected is the default **Axway** theme.
2. Click the drop-down next to the **Preview** button, and select **Save As**.

    ![API Portal customize color screen](/Images/APIPortal/portal_customize.png)

3. Enter a name for your theme, click **Accept**, and wait until the new theme is ready. A new folder is created for your new theme in `local/less/themes/`.
4. Ensure that the theme selected is your new theme, and change the theming variables on the left as needed to customize your theme.
5. To check how your changes look on the page, click **Preview**.
6. When you are happy with your theme, click the drop-down and select **Save**.

##### Theming variables

Theming variables are grouped into different levels:

* **Key Colors**: These variables control the base colors for all styles. The default key colors are sea blue and gray.
* **Basic Colors**: These variables control the colors of the major UI elements, such as buttons and menus. The default values for the basic colors are based on the key colors, but you can overridden these to control the styles of individual UI elements.
* **Global Fonts** and **Headings**: These variables control the typefaces and sizes of the main text elements

In addition, there are some other variables for fine-grain customization of the UI elements, if needed. Most of these variables are based on Basic Color variables.

{{< alert title="Note" color="primary" >}}Variable names begin with the "@" character in Less language. In addition to variable values, you can also use Less expressions and functions to set the value of a theme variable.{{< /alert >}}

#### Use the new theme

1. In JAI, click **Sysytem > Site Templates Styles**.
2. Click **Purity III - Default**.
3. Select the **Theme** page, and select your new theme from the **Theme** drop-down menu: ![API Portal sample screen on how to save a new theme in templates](/Images/APIPortal/portal_templates.png)
4. Click **Save**, then click **</> Less to CSS**. This is the preferred option as it will only compile the theme you want to use.

#### Configuration files

API Portal includes files added to the Purity III template's folders and files that replace those belonging to the Purity III template. All paths are relative to the Purity III template's folder.

* Before updating the Purity III template or T3 framework, back up the Purity III files API Portal replaces. After the update, restore or merge the backed up files.
* Before updating the API Portal plugin, if you have customized the Axway theme or any of the mentioned configuration files, back up the files to avoid losing your customizations. After the update, you may have to merge the backed up files.

##### Added files

The following list details the added files:

* `less/themes/axway/template.less` – Styles for the theme.
* `less/themes/axway/variables.less` – Theme values customized in a file editor.
* `less/themes/axway/variables-custom.less` – Theme values customized in the ThemeMagic. Do not edit this file manually.

##### Replaced Purity III files

The following list summarizes the replaced Purity III files:

* `thememagic.xml` – Configuration for the ThemeMagic GUI.
* `language/en-GB/en-GB.tpl_purity_iii.ini` – Language strings displayed in the ThemeMagic GUI. In order to be utilized by ThemeMagic, this file must be copied to Joomla!'s main language folder, `language/en-GB/en-GB.tpl_purity_iii.ini` when the API Portal plugin is installed.
* `less/variables.less` – Global variables for the Purity III template. Default values for theming variables must be defined in this file.

### Theme Customization in Joomla 4

If you are using Joomla! 4.x, the **ThemeMagic** button is no longer available from the Templates screen, and you must customize a new theme as follows:

1. Create a new Theme. All theme folders are located at `templates/purity_iii/less/themes/`, under the API Portal installation. The easiest way to create a new theme is by creating a copy of  `/axway` theme folder, and renaming it as, for example, `/axway_copy`.
2. Select a new Theme. In JAI, click **Sysytem > Site Templates Styles**.
3. Click **Purity III - style**.
4. Select the **Theme** page, and select your newly created `axway_copy` theme from the **Theme** drop-down menu.

    ![API Portal sample screen on how to save a new theme in templates](/Images/APIPortal/portal_templates.png)

5. Customize your Theme. You can manually [Customize CSS styles](/docs/apim_administration/apiportal_admin/customize_css_styles/). For more information, see [T3 Framework Layout]([http://www.t3-framework.org/documentation/bs3-layout-system#about-layout](https://www.t3-framework.org/documentation/bs3-customization#theme-customization)) documentation.

### Customize your home page layout

**apiportal-homepage** layout is assigned to the home menu item by default. This layout is available from the `apiportal-homepage` template.

The home page consists of the following main sections:

* Menu
* Banner
* Tiles section
* Footer

To customize the layout of your portal:

1. In JAI, click **System > Site Templates Styles**.
2. Click **apiportal-homepage**.
3. Customize the layout, and click **Save**. ![Home page layout](/Images/APIPortal/layout.png)

For more details see [T3 Framework Layout](http://www.t3-framework.org/documentation/bs3-layout-system#about-layout) documentation.

#### Customize your banner

Change the banner of your portal using the **Home Page Banner** module.

To customize the banner:

1. In JAI, click **System > Site Modules**.
2. Search for **Home Page Banner** module.
3. Customize the following:

   * **Title** - Free text field for the title of the banner. Defaults to **Enter API Portal**.
   * **Title colour** - Colour picker to choose the color of the title.
   * **Sub-title** - Free text field for the subtitle of the banner. Defaults to **Explore and test our APIs**.
   * **Subtitle colour** - Colour picker to choose the color of the subtitle.
   * **Explore Button** - Show / Hide Explore Button.
   * **Button text** - Free text field for the button text.
   * **Button text colour** - Colour picker to choose the color of the button text.
   * **Button has background** - Yes / No.
   * **Link button to a menu item** - Drop-down list with all menu items. Choose a page to link to when click the button. Defaults to **Sign in** page.
   * **Button border colour** - Colour picker to choose the color of the button border.
   * **Border radius** - Numbers only field for border radius of the button border. Defaults to **500**.
   * **Background image** - Change the background image of the banner. You can choose an image from the media manager or upload a new image.
   * **Text alignment** - Choose one of the three options (left, center, right) to position the text and the button on the banner. The module position defaults to **api-home-banner**.
4. Click **Save**.

#### Customize the tiles

Modify the tiles in the home page using the **Home Tiles** module.

![Tiles home page](/Images/APIPortal/tiles-homepage_j4.png)

By default, there are four instances of this module:

* **Home Tiles 1** (Explore&Test)
* **Home Tiles 2** (Create)
* **Home Tiles 3** (Manage & analyze)
* **Home Tiles 4** (Connect with a community of developers)

To customize the tiles:

1. In JAI, click **System > Site Modules**.
2. Search for **Home Tiles 1**
3. Customize the following:

   * **Title** - Free text field for the title. Defaults to **Explore & Test**.
   * **Title Colour** - Colour picker to choose the colour of the title.
   * **Description** - Free text field for the description of the tile (The short text under the title).
   * **Description colour** - Colour picker to choose the colour of the description text.
   * **Background image** - Change the icon of the tile. You can choose an image from the media manager or upload a new image.
   * **Background colour** - Colour picker to choose the background colour of the whole tile. Defaults to **white**.
   * **Tile has link**:

     * **Menu item** - Drop-down list with all menu items. Choose a menu item to link the Tile to (Defaults to the chosen option).
     * **Custom** - Free text field. Enter any valid URL to link the tile to.
     * **No** - No link at all.

The home page layout is designed to have up to six tiles, so positions **api-home-tiles-5** and **api-home-tiles-6** are available for use.

To add a new tile:

1. In JAI, click **System > Site Modules > New > Home Tiles**.
2. After finishing customizing, click **Save** or **Save & close.**

## Customize using T4 template

This section describes how to customize your portal using the T4 template.

### Customizations of template style

T4 template offers a variety of options for customizations by directly editing the template style. Before you start making changes, you must create a copy of the template styles.

#### Duplicate T4 template styles

1. In Joomla! Administrator Interface (JAI), click **System > Site Template Styles**.
2. Select **T4 - Default** and **T4 - Page Builder**, then click the **Duplicate** button.
3. Open the duplicate of **T4 - Default** and from the **Overview** sidebar menu, enable the **Default** toggle. From this tab you can also set **Style name**.
4. Open the duplicate of **T4 - Page Builder** and click **Menu assignment**. Assign the menu items that you wish to be assigned to this template, then click **Save**. You can also change the **Style name** from the **Overview** sidebar menu.

As a result of this procedure, API Portal starts to use the duplicated templates.

#### T4 Template Style settings

Once the templates are duplicated, you can directly edit your copies. Some of the T4 Template Style settings are covered in the following sections.

##### Customize the theme color

You can change the basic colors of the theme by following the steps:

1. In Joomla! Administrator Interface (JAI), click **System > Site Template Styles**.
2. Open the duplicate of **T4-PageBuilder** template style.
3. Click **Theme Color** from the sidebar menu.
4. Clone the selected theme and edit the cloned theme.
5. Setup the colors and click **Save** to save the template style.

##### Add custom CSS and SCSS

T4 template also allows you to add custom CSS/SCSS code to achieve the desired design for your API Portal.

1. In Joomla! Administrator Interface (JAI), click **System > Site Template Styles**.
2. Open the duplicate of **T4-PageBuilder** template style.
3. Click **Tools** from the sidebar menu.
4. From the **Edit Custom SCSS** section, click **Edit**.
5. Select the **Custom style** tab from the dialog window.
6. Add your CSS/SCSS code, then click **Save and compile**.

### Customize with T4 PageBuilder

All pages in API Portal are built using T4 PageBuilder. T4 PageBuilder is a tool that provides an intuitive user interface with which you can customize page content and styling.

To edit a page with T4 Page Builder, follow these steps:

1. In Joomla! Administrator Interface (JAI), click **Components > T4 Page Builder > All Pages**.
2. Click **Edit page** to open PageBuilder.

The following image shows a preview of the page.

![T4 Page Builder](/Images/APIPortal/pagebuilder.png)

There is a toolbar at the top of the page to allow you to see the page in different resolutions. Also, there is a **Code editor** button from which you can add custom HTML and CSS code.

On the left-side menu, there is an **Add-ons** item, from which you can add new elements to the page by directly dragging-and-dropping them. You can also edit existing elements by clicking on them and changing their properties from the toolbar that is shown on the right-side.

For more information, see [T4 Page Builder](https://www.joomlart.com/documentation/t4-page-builder/getting-started) official documentation.

{{< alert title="Note" color="primary" >}}With T4 Page Builder you can easily customize the static content. You cannot customize content coming from a Joomla module.{{< /alert >}}

### Customizations with Joomla modules

API Portal uses Joomla modules to render dynamic content (APIs, Applications, Users). Each module provides configuration which gives you control over the content rendered by the module.
You can see what configuration options a module provides by clicking **Content > Site Modules**, and opening a module.

Watch this video to learn more about applying your customizations and styling to the new T4 Template: {{< youtube EwnpLoCr-4s >}}

## Customize your logo

Change the API Portal site logo using the Joomla! Media Manager.

### Upload your image file

1. In Joomla! Administrator Interface (JAI), click **Content > Media**.
2. Select the place where you want to upload the image. For example: **com_apiportal** folder.
3. Upload the image file you want to use, and select **Save**.

### Link the logo to your template styles in Purity III template

To link your logo to template:

1. In JAI, click **System > Site Templates Styles**. A list of template styles is displayed.
2. Click on template style.
3. Go to the **Theme** tab, and click **Select** from **Logo Image**.
4. Navigate to the folder where the image was uploaded.
5. Select your logo from the list of the available image files, and click **Insert**.

    Files in **SVG** format are not listed. In that case, you must enter the path to that image in **Image URL**. The path must start with the `images/` segment. For example, `images/path-to-logo/logo-filename.svg`.

6. Click **Save**.

### Link the logo to your template styles in T4 template

To link your logo to template:

1. In JAI, click **System > Site Templates Styles**. A list of template styles is displayed.
2. Click on template style.
3. Click on **Site settings** from the sidebar menu.
4. Clone the selected site settings. Edit the cloned site settings.
5. Click **Select** button from the **Logo image** field.
6. Save the site settings.
7. Save the template style.

{{< alert title="Note" color="primary" >}}You must repeat this procedure to apply your logo to all your templates.{{< /alert >}}

## Customize standard footer

You can customize API Portal standard footer content using the following modules: Footer, Logo - Footer, Legal Menu - Footer.

1. In the JAI, click **System > Site Modules**.
2. Click **New** to create a new module.
3. From the list of module types, click **Custom**.
4. From the right-side menu, select `Hide` on the **Show title** option.
5. Set position:
    * for **Legal Menu - Footer** module to **footnav-1**.
    * for **Logo - Footer** to **footer-logo**.
    * for **Footer** module to **footer**.
6. Apply your desired changes.
7. Click **Save**.

## Customize the 404 error page

Customize a `404` error page for your API Portal.

### Duplicate the template

Duplicate the current template to avoid losing your changes when you upgrade API Portal.

1. In JAI, click **System** in the left sidebar.
2. Under **Templates** click **Site Templates**, and click the **Purity_III Details and Files** template.
3. Click **Copy Template**, add a name to the template, and click **Copy Template**.
4. Click **Save**, then click **Close**.

### Customize 404 page

Customize the message for your error page.

1. In JAI, from the list of templates, click your newly created template.
2. On the **Editor** tab, click **error.php** to edit this file.
3. Customize the line describing the 404 page.
4. Click **Save & Close** to save your changes.
5. Click **Close** to leave the template page.

### Assign your template as default for all pages

Assign your new template as the default template for API Portal pages.

1. In JAI, click **System** in the left sidebar.
2. Under **Templates**, click **Site Templates Styles** and click to open the newly created style for your template.
3. Click the **Theme** tab, and select **Axway** for **Theme**.
4. Click the **Layout** tab, and select **Blog** for **Position & Responsive Configuration**.
5. Click **Less to CSS**.
6. Click **Save**, then click **Close**.
7. In the **Default** column, mark this style as default.

### Assign your template as default for the Home page

Create a new style and assign it to the Home page.

1. Select the checkbox next to an existent customized style and press **Duplicate**.
2. Click to open the style.
3. In **Style Name**, add a name related to homepage.
4. Click the **Layout** tab, and select **apiportal-homepage** for **Position & Responsive Configuration**.
5. Click the **Assignment** tab, and select only **Home**.
6. Click **Save**, then click **Close**.

## Configure terms and conditions text

To modify the API Portal Terms and Conditions content, edit the following file:

```
/opt/axway/apiportal/htdoc/components/com_apiportal/views/terms/tmpl/default.php
```

## Enable the T4 template

API Portal version [November 2022](/docs/apim_relnotes/20221130_apip_relnotes/) ships with the [T4 template](https://www.joomlart.com/t4-framework). However, if you are upgrading from previous versions to the *November 22* release of API Portal and wish to adopt this template, there are some manual steps you must take to configure menu items, and apply your customizations and styling to the new T4 template.

Follow the steps below to configure menu items in the T4 template:  

1. In JAI, click **System > Site Templates Styles** under the **Templates** section, and in the **Default** column, select **T4 - Default**.

   ![API Portal set default T4 template style](/Images/APIPortal/portal_t4_default_template.png)

2. Click **Menus > Main Menu T4** and assign the home page by clicking **Home** icon under the **Home** column, then select the checkboxes for all menu items and click **... Actions > Publish**.

   ![API Portal set T4 home page](/Images/APIPortal/portal_t4_homepage.png)

3. Click **Menus > Manage > Main Menu** and change the menu name from *mainmenu* to, for example, *mainmenu-t3*.
4. Click **Menus > Main Menu** and select the checkboxes for all menu items,  then click **... Actions > Unpublish**.
5. Click **Menus > Manage > Main Menu T4** and change the menu name from *mainmenu-t4* to *mainmenu*.
6. Click **Menus > Manage > User Menu T4** and change the menu name from *user-menu-t4* to *user-menu*.
7. Click **Menus > User Menu T4**, select the checkboxes for all menu items and click **... Actions > Publish**.
8. (Optional) To preserve URLs format, click all menu items under both **Menus > User Menu T4** and **Menus > Main Menu T4** and remove *-t4* prefix from aliases.

Watch this video to learn more about enabling T4 Template after upgrade:
{{< youtube QNmU_CrE1Ic >}}
