# Aucor Coding Guidelines

This is the Aucor way of writing and formatting code. By following these guidelines you will write better code that will be easy to read. We have history in both WordPress and Drupal so our ways are relaxed combination of both.

When there is discipline in writing and formatting code, our freedom to operate will increase. To create code that other people can take and extend will give you freedom from your old code. To understand your peers' code will give you freedom to participate.

> Discipline equals freedom. – Jocko Willink

## Table of contents

1. [Who keeps your code clean?](#1-who-keeps-your-code-clean)
    1. [You](#11-you)
    2. [Editorconfig](#12-editorconfig)
    3. [PHP (PHPCS)](#13-php-phpcs)
    4. [Styles (SASS)](#14-styles-sass)
    5. [JS (JSHint)](#15-js-jshint)
2. [Configuring tools](#2-configuring-tools)
    1. [Setup Editorconfig](#21-setup-editorconfig)
    2. [Setup PHPCS](#22-setup-phpcs)
3. [PHP](#3-php)
    1. [Naming conventions](#31-naming-conventions)
    2. [Documentation](#32-documentation)
    3. [Whitespace](#33-whitespace)
    4. [Embedding PHP in HTML](#34-embedding-php-in-html)
    5. [Quotes](#35-quotes)
    6. [Braces](#36-braces)
    7. [Conditions](#37-conditions)
    8. [Example](#38-example)
4. [SASS](#4-sass)
    1. [Selectors](#41-selectors)
    2. [Documentation](#42-documentation)
    3. [SASS functions](#43-sass-functions)
    4. [8-point grid](#44-8-point-grid)
    5. [Braces](#45-braces)
    6. [Example](#46-example)
5. [HTML](#5-html)
    1. [Naming conventions](#51-naming-conventions)
    2. [Documentation](#52-documentation)
    3. [Elements](#53-elements)
    4. [Accessibility](#54-accessibility)
    5. [Example](#55-example)
6. [JS](#6-js)

## 1. Who keeps your code clean?

There's a few of tools to do this job as there is no one-size-fits-all solution for different languages.

### 1.1 You

You are mainly resposible of keeping your code clean and easy to read. There are bunch of automations to help you, but they can only detect some things.

### 1.2 Editorconfig

`First time setup: Install PHPCS and plugin to text editor`

Editorconfig automatically configures your code editor to project's settings. For example [aucor-starter](https://github.com/aucor/aucor-starter) includes this file so when you have [the plugin installed in your text editor](http://editorconfig.org/#download) you are good to go.

This is the content of `.editorconfig` file:

```
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

### 1.3 PHP (PHPCS)

`First time setup: Install PHPCS and plugin to text editor`

PHPCS (PHP_CodeSniffer) is a command line tool / text editor plugin that will check syntax and formatting of PHP code either on every save or once for whole project, directory or file. PHPCS has also tools to automatically fix some errors. PHPCS rules live on project's `phpcs.xml` file that lists which rules it includes.

Instruction how to install PHPCS can be found on chapter 2 and PHP guidelines on chapter 3.

### 1.4 Styles (SASS)

`First time setup: -`

Styles are written in [SASS](http://sass-lang.com/) that extends CSS capabilities. SASS files are compiled back to CSS ([Gulp does this](https://github.com/aucor/aucor-starter#32-workflow)). During this compilation you will get a tiny syntax check that will fail if your SASS is not valid or files do not exist.

There's not really many good tools for checking the formatting so you'll have to follow guidelines from chapter 4 yourself.

### 1.5 JS (JSHint)

`First time setup: -`

Javascript is part of Gulp's build process so the syntax check happens when Gulp compiles files. The tool for the job is JSHint and its rules live in `.jscsrc`. JSHint has also a few other files. You can ignore some files from syntax check by adding it to `.jshintignore`. JSHint configuration lives in `.jshintrc`.

JSHint gives warnings for potentially bad syntax in command line when Gulp is running and you save JS files.

Find JS guidelines in chapter 6.

## 2. Configuring tools

### 2.1 Setup Editorconfig

Install [a plugin to your text editor](http://editorconfig.org/#download). That's it.

### 2.2 Setup PHPCS

#### 2.2.1 Install PHPCS

First you need to install PHPCS with Homebrew. If you are missing Homebrew, [here's the instructions for installing it](https://brew.sh/). (If you are not using MacOS, there are other ways).

##### Install homebrew-php

```
brew tap homebrew/dupes
brew tap josegonzalez/homebrew-php
brew install PHP71 (or other version of your choice)
```

##### Install php-code-sniffer

```
brew install php-code-sniffer
brew install phpcs
```

#### 2.2.2 Create empty phpcs.xml

PHPCS will use ruleset from project and it will go up the directory as long as it will find a ruleset. Some text editor plugins will fallback to a premade standard if ruleset is not found. For this reason, we can create an empty ruleset for your development root to disable this. So if the project has no standard, it won't check the formatting.

Create `phpcs.xml` for your development directory (for example `/htdocs/`):

```xml
<?xml version="1.0"?>
<ruleset name="No Standards">
  <description>Skip</description>
</ruleset>

```

#### 2.2.3 Add PHPCS plugin for your text editor

##### Sublime Text

Open `Package Control` and install package `Phpcs`.

Go to "Sublime Text" > Preferences > Package Settings > PHP Code Sniffer > Settings - User

Add following settings:
```
{
  // path to the php executable.
  "phpcs_php_path": "/usr/local/bin/phpcs",

  // project based PHPCS
  "phpcs_additional_args": {
    "-n": ""
  },
}
```

Open some PHP file from project. Open package manager with `Cmd + Shift + P` and select `Php Code Sniffer: Turn Execute On Save On`.

Now the code is checked every time you save. If project has `phpcs.xml`, Sublime Text will automatically use it.

##### Atom

There is atom-phpcs. [Check it out and tell how it works.](https://github.com/bpearson/atom-phpcs)

##### CLI

PHPCS can be used in command line without any fuss. [PHPCS list of commands.](https://pear.php.net/manual/en/package.php.php-codesniffer.usage.php)

## 3. PHP

### 3.1 Naming conventions

**Rule: Use English always if possible.**

`Enforced: -`

```php
✅ aucor_get_svg();
✅ $svg_title;

❌ aucor_hae_ikoni();
❌ $ikoni_otsikko;
```

**Rule: Use lowercase letters and underscores in variable and function names.**

`Enforced: -`

```php
✅ aucor_get_svg();
✅ $svg_title;

❌ aucorGetSvg();
❌ AUCORGETSVG();
❌ $svgtitle;
❌ $SvgTitle;
```

**Rule: Prefix your functions to avoid collitions with WordPress or plugins.**

`Enforced: -`

```php
✅ function aucor_get_svg();

❌ function get_svg();
```

**Rule: Constants should be in all upper-case with underscores separating words.**

`Enforced: PHPCS (Generic.NamingConventions.UpperCaseConstantName)`

```php
✅ define('SITE_LANGUAGE', 'fi');

❌ define('SiteLanguage', 'fi');
❌ define('site_langauge', 'fi');
```

**Rule: Use lowercase for default PHP constants.**

`Enforced: PHPCS (Generic.PHP.LowerCaseConstant)`

```php
✅ true
✅ false
✅ null

❌ TRUE
❌ FALSE
❌ NULL
```

**Rule: Function keywords should be lowercase.**

`Enforced: PHPCS (Squiz.Functions.LowercaseFunctionKeywords)`

```php
✅ public function aucor_get_svg()

❌ PUBLIC FUNCTION aucor_get_svg()
```

**Rule: Built-in PHP functions should be lowercase.**

`Enforced: PHPCS (Squiz.PHP.LowercasePHPFunctions)`

```php
✅ echo '🍏';
✅ empty($arr);

❌ ECHO '🍏';
❌ EMPTY($arr);
```

### 3.2 Documentation

**Rule: Every function should have at least small description.**

`Enforced: -`

```php
✅
/**
 * Get HTML SVG markup from theme's SVG sprite
 */
function aucor_get_svg($id, $args)

❌
function mystery_function($secret)
```

**Rule: Documention is grouped with title, description and @groups.**

`Enforced: PHPCS (Generic.Commenting.DocComment)`

```php
✅
/**
 * Get HTML SVG markup from theme's SVG sprite
 */
function aucor_get_svg($id, $args)

✅
/**
 * Lorem ipsum
 *
 * Dolor sit amet integer omit nomen donec.
 *
 * @example lorem_ipsum('amor fati', $post_id)
 *
 * @param string $lorem acta non verba
 * @param int    $donec dolor sit amet
 *
 * @return int lorem ipsum dolor
 */
function lorem_ipsum($lorem, $donec)

✅
/**
 * Lorem ipsum
 *
 * @return int lorem ipsum dolor
 */
function lorem_ipsum()

❌
/**
 * Lorem ipsum
 * Dolor sit amet integer omit nomen donec.
 * @example lorem_ipsum('amor fati', $post_id)
 * @param string $lorem acta non verba
 * @param int $donec dolor sit amet
 * @return int lorem ipsum dolor
 */
function lorem_ipsum($lorem, $donec)

❌
/** Get HTML SVG markup from theme's SVG sprite */
function aucor_get_svg($id, $args)
```

**Rule: Line comments should start with lowercase letter and be just one sentence. Use code blocks for longer comments.**

`Enforced: -`

```php
✅
// this is a short notice

✅
/**
 * Sometimes you have to explain things longer. You can make line breaks when
 * it seems natural as text editor won't do it for you.
 */

❌
//I like to capitalize things.

❌
// I need to explain this very thorough. I'm going on and on. I should have used code block but here I still go. This comment is so long that it will break to another line or give you nice old scroll bar for your text editor.
```

**Rule: Make asterisks (\*) aligned and leave 1 space before content.**

`Enforced: PHPCS (Squiz.Commenting.DocCommentAlignment)`

```php
✅
/**
 * Get HTML SVG markup from theme's SVG sprite
 */

❌
/**
* Get HTML SVG markup from theme's SVG sprite
*/

❌
/**
 *Get HTML SVG markup from theme's SVG sprite
 */
```

### 3.3 Whitespace

**Rule: No extra spaces everywhere aka WordPress spacing.**

`Enforced: -`

```php
✅ if (!empty($str))
✅ function lorem_ipsum($acta, $non, $verba)
✅ add_action('login_head', 'aucor_starter_favicons');

❌ if( !empty( $str ) )
❌ function lorem_ipsum( $acta, $non, $verba )
❌ add_action( 'login_head', 'aucor_starter_favicons' );
```

**Rule: Indent with spaces, 2 at a time.**

`Enforced: PHPCS (Generic.WhiteSpace.ScopeIndent) + .editorconfig (indent_style + indent_size)`

```php
✅  $example; // 2 spaces
✅    $example; // 4 spaces (you can go over if it's clearer that way)

❌	$example; // 1 tab
```

Too little indentation is error as well!

**Rule: No whitespace at the end of each line of code.**

`Enforced: PHPCS (Squiz.WhiteSpace.SuperfluousWhitespace) + .editorconfig (trim_trailing_whitespace)`

```php
✅ echo '🍏';

❌ echo '🍏';          
```

**Rule: All files should end with a new line.**

`Enforced: PHPCS (Generic.Files.EndFileNewline) + .editorconfig (insert_final_newline)`

**Rule: No whitespace before semicolon.**

`Enforced: PHPCS (Squiz.WhiteSpace.SemicolonSpacing)`

```php
✅ echo '🍏';

❌ echo '🍏'  ;
```

**Rule: Separate function arguments with space.**

`Enforced: PHPCS (Generic.Functions.FunctionCallArgumentSpacing)`

```php
✅ function lorem_ipsum($acta, $non, $verba)

❌ function lorem_ipsum($acta,$non,$verba)
```

### 3.4 Embedding PHP in HTML

**Rule: When embedding multi-line PHP snippets within a HTML block, the PHP open and close tags must be on a line by themselves.**

`Enforced: PHPCS (Squiz.PHP.EmbeddedPhp)`

```php
✅
<?php
  $url = get_permalink();
  $title = get_the_title();
?>

❌
<?php $url = get_permalink();
$title = get_the_title(); ?>

❌
<?php }
else {
?>
```

**Rule: Avoid echoing HTML markup if possible. It's very hard to read.**

`Enforced: -`

```html
✅
<article>
  <h1><?php the_title(); ?></h1>
  <?php the_content(); ?>
  <a href="<?php the_permalink(); ?>"><?php pll_e('Lue lisää'); ?></a>
</article>

❌
<?php echo '<article><h1>'.get_the_title().'</h1>'.get_the_content().'<a href="'.get_permalink().'">.pll__('Lue lisää').'</a></article>'; ?>
```

**Rule: Never use shorthand PHP start tags. Always use full PHP tags.**

`Enforced: PHPCS (Generic.PHP.DisallowShortOpenTag + Generic.PHP.DisallowAlternativePHPTags)`

```php
✅ <?php $url = get_permalink(); ?>

❌ <?= $url = get_permalink(); ?>
```

**Rule: Don't put closing PHP tag at the end of a file, leave it open.**

`Enforced: PHPCS (PSR3.Files.ClosingTag)`

File should never end with `?>`.

### 3.5 Quotes

**Rule: Use single and double quotes when appropriate. If you're not evaluating anything in the string, use single quotes.**

`Enforced: PHPCS (Squiz.Strings.DoubleQuoteUsage)`

```php
✅ echo 'lorem ipsum';
✅ echo "lorem ipsum \n"; // escaping requires double quotes
✅ echo "name: $name"; // variables require double quotes but please don't do it like this

❌ echo "lorem ipsum"; // no need to use double quotes
```

### 3.6 Braces

**Rule: Class opening braces should be on the same line as the statement.**

`Enforced: PHPCS (Squiz.ControlStructures.ControlSignature)`

```php
✅
class My_Class() {

✅
function my_function() {

❌
class My_Class()
{

❌
function my_function()
{
```

**Rule: Braces shall be used for all blocks, even when they are not required.**

`Enforced: PHPCS (Generic.Classes.OpeningBraceSameLine)`

```php
✅
if ($has_link) {
  echo $link;
}

❌
if ($has_link)
  echo $link;
```

### 3.7 Conditions

**Rule: Add 1 space after conditional keywords.**

`Enforced: PHPCS (Generic.Functions.FunctionCallArgumentSpacing)`

```php
✅
if () {

} else {
 
}

❌
if() {

}else{

}
```

**Rule: Use elseif, not else if.**

`Enforced: PHPCS (PSR3.ControlStructures.ElseIfDeclaration)`

```php
✅ } elseif () {

❌ } else if () {
```

### 3.8 Example

Here's a few longer examples to help you get hang of it.

**✅ Example A: aucor-starter hide-users.php**

```php
<?php
/**
 * Hide users' identities
 *
 * @package aucor_starter
 */

/**
 * Rename users to sitename (only front-end)
 *
 * @param string $name the name of the author
 *
 * @return string name of the author
 */
function aucor_starter_rename_authors($name) {

  if (is_admin()) {
    return $name;
  }

  return get_bloginfo('name');

}
add_filter('the_author', 'aucor_starter_rename_authors', 100);
add_filter('the_modified_author', 'aucor_starter_rename_authors', 100);

/**
 * Link user to front page
 *
 * @param string $url link to author archive
 *
 * @return string link to site url
 */
function aucor_starter_author_link_to_front_page($url) {

  return get_site_url();

}
add_filter('get_the_author_link', 'aucor_starter_author_link_to_front_page', 100);

/**
 * Disable users from REST API
 *
 * @param array $endpoints registered routes
 *
 * @return array registered routes
 */
function aucor_starter_disable_user_endpoints($endpoints) {

  // disable list of users
  if (isset($endpoints['/wp/v2/users'])) {
    unset($endpoints['/wp/v2/users']);
  }

  // disable single user
  if (isset($endpoints['/wp/v2/users/(?P<id>[\d]+)'])) {
    unset($endpoints['/wp/v2/users/(?P<id>[\d]+)']);
  }

  return $endpoints;

}
add_filter('rest_endpoints', 'aucor_starter_disable_user_endpoints', 1000);
```

**✅ Example B: aucor-lead-paragraph**

```php
/**
 * Class: Aucor_Lead_Paragraph
 */
class Aucor_Lead_Paragraph {

  // internal vars
  private $meta_key   = 'lead';
  private $nonce_key  = 'aucor_lead_paragraph_nonce';

  // configurable vars
  private $use_soft_limit;
  private $use_in_excerpts;
  private $char_limit;
  private $auto_prepend_lead_paragraph;

  /**
   * Constructor
   */
  public function __construct() {

    // configure character limit (default: 280)
    $this->char_limit = apply_filters('aucor_lead_pargraph_character_limit', 280);

    // use soft or hard character limit
    $this->use_soft_limit = apply_filters('aucor_lead_pargraph_use_soft_character_limit', true);

    // load textdomain
    if (is_admin()) {
      load_plugin_textdomain('aucor-lead-paragraph', false, basename(dirname(__FILE__)) . '/languages');
    }

    // add meta box when needed
    add_action('add_meta_boxes', array($this, 'plugin_add_meta_boxes'));

    // print meta box below title
    add_action('edit_form_after_title', array($this, 'plugin_edit_form_after_title'));

    // handle value save
    add_action('save_post', array($this, 'plugin_meta_save'));

    // maybe add the lead paragraph before content
    $this->auto_prepend_lead_paragraph = apply_filters('aucor_lead_paragraph_auto_prepend', true);
    if ($this->auto_prepend_lead_paragraph) {
      add_filter('the_content', array($this, 'plugin_the_content'));
    }

    // maybe use lead paragraph as excerpt if it makes sense
    $this->use_in_excerpts = apply_filters('aucor_lead_paragraph_use_in_excerpts', true);
    if ($this->use_in_excerpts) {
      add_filter('get_the_excerpt', array($this, 'plugin_get_the_excerpt'));
    }

    // include lead to REST API
    add_action('rest_api_init', array($this, 'append_lead_to_rest_api'));

  }

  /**
   * Get lead paragraph
   *
   * @param int $post_id the ID of post
   *
   * @return string plain lead paragraph content without HTML markup
   */
  public function get_lead_paragraph($post_id = null) {

    if (empty($post_id)) {
      $post_id = get_the_ID();
    }

    return get_post_meta($post_id, $this->meta_key, true);

  }

  /**
   * Get lead paragraph with HTML markup
   *
   * @param int $post_id the ID of post
   *
   * @return string lead paragraph with HTML markup
   */
  public function get_lead_paragraph_html($post_id = null) {

    $stored_lead_paragraph = $this->get_lead_paragraph($post_id);

    if (empty($stored_lead_paragraph)) {
      return '';
    }

    return '<p class="lead" itemprop="description">' . esc_html($stored_lead_paragraph) . '</p>';

  }

...
```

## 4. SASS

### 4.1 Selectors

**Rule: Generally avoid styling bare elements – it's very risky.**

Don't apply styles to basic HTML elements if you don't know what you are doing.

```sass
✅
.primary-menu li {
  display: flex;
}

❌
li {
  display: flex;
}
```

**Rule: Be only as specific as you need.**

We get it, nesting things is fun. But it also leads to overly specific rules that may need `!important` later on and the code will be hard to re-use.

```sass
✅
.person {
  .contact-info {

  }
  .phone {

  }
  .phone-icon {

  }
}

❌
.person {
  .contact-info {
      .phone {
        .phone-icon {

       }
    }
  }
}
```

**Rule: Avoid `!important` if you can.**

The `!important` is just a shortcut to be more specific but you can often get over this by making the selector more specific (longer). Using `!important` is a short lived ease as there is no `!importanter`.

### 4.2 Documentation

Styles don't require tons of documentation. There are a few cases when you want to add some documentation:

**Rule: Start file with name.**

```sass
✅
/* ==========================================================================
  Templates - Page
========================================================================== */
```

**Rule: No magic numbers – explain weird values.**

```sass
✅ width: 120%; // stretch to outer container (1200px / 1000px)

❌ width: 120%;
```

### 4.3 SASS functions

**Rule: Avoid repeating colors and values – use variables.**

```sass
✅ color: $pink;

❌ color: #C82986;
```

**Rule: Create mixins for repeating snippets.**

```sass
✅
.button-menu {
  @include button-reset;
}

❌
.button-menu {
  border: 0;
  background: none;
  border-radius: 0;
  ... // resetting button styles in many places
}
```

**Rule: Avoid `@extend` if you can.**

The `@extend` command is risky command if you don't know what you are doing. [Read more on why @extend is bad.](https://tiffanybbrown.com/2017/03/dont-use-extend-sass/index.html)

### 4.4 8-point grid

**Rule: Size of elements should be multiply of 0.5 rem.**

In 8-point grid you try to size everything by multiply of 8 points like 8px, 16px, 24px... So there generally shouldn't be elements that are 7px or 10px. With rem units this is done with 0.5rem, 1rem, 1.5rem... This adds harmony and consistency to UI. [Read more about 8-point grid.](https://builttoadapt.io/intro-to-the-8-point-grid-system-d2573cde8632)

```sass
✅ padding: 1rem;
✅ font-size 1.5rem;

❌ padding: 12px; // correct if the element will be in grid
❌ font-size: .9735rem; // correct if the element will be in grid
```

### 4.5 Values

**Rule: Use relative units as often as possible.**

```sass
✅ padding: 1rem;
✅ line-height: 1.5;
✅ width: 50%;

❌ padding: 16px;
❌ line-height: 24px;
❌ width: 500px;
```

### 4.6 Braces

**Rule: Braces go to same line as selector.**

```sass
✅
.person {

❌
.person
{
```

### 4.7 Example

**✅ Example A: Simple nested class.**

```sass
.menu-social-items {
  @include list-reset;
  li {
    display: inline-block;
  }
  svg {
    width: 1rem;
    height: 1rem;
    margin-right: .5rem;
  }
  .menu-item-label {
    @include visuallyhidden; // show titles only to screen-readers
  }
}
```

## 5. HTML

### 5.1 Naming conventions

**Rule: Use kebab-case for class and attribute names.**

```html
✅ <span class="phone-number">

❌ <span class="phoneNumber">
❌ <span class="phone_number">
```

**Rule: Name values from least specific to most specific.**

```html
✅ <span class="event-date-start">
✅ <span class="event-start-date">

❌ <span class="start-date-event">
❌ <span class="date-event">
```

### 5.2 Documentation

**Rule: HTML comments should be usually avoided.**

HTML comments are send with the document unless server/WordPress minifies HTML. This is unnecessary info and comments can include some embarassing text.

Exceptions are marking end of large containers where these comments can be helpful but not any way necessary.

```html
✅ (none)
✅ <!-- .post -->

❌ <!-- Is this working? -->
```

### 5.3 Elements

**Rule: If it's a link, it should be `<a>`.**
```html
✅ <a href="/news">Click me</a>

❌ <span data-href="/news">Click me</span> <!-- JS magic -->
```

**Rule: If it's a button and not a link, it should be `<button>`.**

```html
✅ <button class="next">Next</button>

❌ <span class="next">Next</span> <!-- JS magic -->
```

### 5.4 Accessibility

**Rule: Study WCAG standards for accessibility.**

[WCAG 2.0](https://www.w3.org/TR/WCAG20/) has the best practices for accessibility. Apply where you can.

**Rule: Always have alt attribute for images, even an empty one.**

```html
✅ <img alt="Description" src="image.png" />
✅ <img alt="" src="image.png" />

❌ <img src="image.png" />
```

**Rule: No buttons without text. Use at least invisible text.**

```html
✅ <button>Open menu</button>
✅ <button><img alt="" src="hamburger.svg" /><span class="screen-reader-text">Open menu</span></button>

❌ <button><img alt="" src="hamburger.svg" /></button>
```

## 5.5 Example

**✅ Example A: Simple article markup with HTML comments.**

```html
<article id="post-<?php the_ID(); ?>" <?php post_class(); ?>>

  <header class="entry-header">
    <?php the_title('<h1 class="entry-title">', '</h1>'); ?>
  </header><!-- .entry-header -->

  <div class="entry-content">
    <?php the_content(); ?>
  </div><!-- .entry-content -->

  <footer class="entry-footer">
  </footer><!-- .entry-footer -->

</article><!-- #post-## -->
```

## 6. JS

JS guidelines are work in progress.

