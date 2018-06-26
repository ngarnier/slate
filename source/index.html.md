---
title: Documentation for MJML - The Responsive Email Framework

language_tabs:
  - html : MJML

toc_footers:
  - <a href='https://github.com/mjmlio/mjml'>Fork me on Github</a>
  - <a href='https://github.com/mjmlio/mjml/issues'>Submit an Issue</a>
  - MJML v4.0.2

search: true
---


# MJML Guides

MJML is a markup language designed to reduce the pain of coding a responsive email. Its semantic syntax makes it easy and straightforward and its rich standard components library speeds up your development time and lightens your email codebase. MJML’s open-source engine generates high quality responsive HTML compliant with best practices.

## Overview

MJML rolls up all of what Mailjet has learned about HTML email design over the past few years and abstracts the whole layer of complexity related to responsive email design.

Get your speed and productivity boosted with MJML’s semantic syntax. Say goodbye to endless HTML table nesting or email client specific CSS. Building a responsive email is super easy with tags such as `<mj-section>` and `<mj-column>`.

MJML has been designed with responsiveness in mind. The abstraction it offers guarantee you to always be up-to-date with the industry practices and responsive. Email clients update their specs and requirements regularly, but we geek about that stuff - we’ll stay on top of it so you can spend less time reading up on latest email client updates and more time designing beautiful email.

``` html

<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-text>Hi sexy!</mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>

```
<p align="center">
  <br />
  <br />
  <br />
  <a href="/try-it-live/intro"><img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" /></a>
</p>


## mjml

A MJML document starts with a `<mjml>` tag, it can contain only `mj-head` and `mj-body` tags. Both have the same purpose of `head` and `body` in a HTML document.

## mj-head

mj-head contains everything related to the document such as style and meta elements. It supports custom head elements and can be registered through `registerMJHeadElement(<string> name, <function> handler)` api from `mjml-core`, it acts as a pre-render hook.


## mj-body

mj-body contains everything related to the content of your email. It supports custom elements too and can be registered either through `registerMJElement(<MJMLElement> class)` api from `mjml-core` or via a `.mjmlconfig` file. Non-known element from `mjml-core` are simply ignored. Note that `mj-body` should have only one root element due to how React works.


## mj-include

The mjml-core package allows you to include external mjml files to build your email template.

```xml
<!-- header.mjml -->
<mj-section>
  <mj-column>
    <mj-text>This is a header</mj-text>
  </mj-column>
</mj-section>
```

You can wrap your external mjml files inside the default `mjml > mj-body`
tags to make it easier to preview outside the main template


```xml
<!-- main.mjml -->
<mjml>
  <mj-body>
    <mj-include path="./header" /> <!-- or 'header.mjml' -->
  </mj-body>
</mjml>
```

The MJML engine will then replace your included files before starting the rendering process

<aside class="notice">
Note that the file must be a file with a `.mjml` extension
</aside>

# Installation

You can install MJML with NPM to use it with NodeJS or the Command Line Interface. If you're not sure what those are, head over to <a href="#usage">Usage</a> for other ways to use MJML.
 
```bash
npm install mjml
```

# Development

To work on MJML, make changes and create merge requests, download and install [yarn](https://yarnpkg.com/lang/en/docs/install/) for easy development.

```bash
git clone https://github.com/mjmlio/mjml.git && cd mjml
yarn 
yarn build
```

You can also run `yarn build:watch` to rebuild the package as you code.

# Usage

## Online

Don't want to install anything? Use the free online editor!

<p align="center">
  <a href="http://mjml.io/try-it-live" target="_blank"><img src="https://cloud.githubusercontent.com/assets/6558790/12195421/58a40618-b5f7-11e5-9ed3-80463874ab14.png" alt="try it live" width="75%"></a>
</p>
<br>

## Applications and plugins

MJML comes with an ecosystem of tools and plugins, check out:
* The [MJML App](https://mjmlio.github.io/mjml-app/) (MJML is included)
* [Visual Studio Code plugin](https://github.com/attilabuti/vscode-mjml) (MJML is included)
* [Atom plugin](https://atom.io/users/mjmlio) (MJML needs to be installed separately)
* [Sublime Text plugin](https://packagecontrol.io/packages/MJML-syntax) (MJML needs to be installed separately)

For more tools, check the [Community](https://mjml.io/community) page.

## Command line interface

> Compiles the file and outputs the HTML generated in `output.html`

```bash
mjml input.mjml -o output.html
```

You can pass optional `arguments` to the CLI and combine them.

argument | description | default value
---------|--------|--------------
`mjml -m [input]` | Migrates a v3 MJML file to the v4 syntax | NA
`mjml [input] -o [output]` | Writes the output to [output] | NA
`mjml [input] -s` | Writes the output to `stdout` | NA
`mjml -w [input]` | Watches the changes made to [input] (file or folder) | NA
`mjml [input] --config.beautify` | Beautifies the output (`true` or `false`) | true
`mjml [input] --config.minify` | Minifies the output (`true` or `false`) | false

## Inside Node.js

```javascript
import mjml2html from 'mjml'

/*
  Compile an mjml string
*/
const htmlOutput = mjml2html(`
  <mjml>
    <mj-body>
      <mj-section>
        <mj-column>
          <mj-text>
            Hello World!
          </mj-text>
        </mj-column>
      </mj-section>
    </mj-body>
  </mjml>
`, options)


/*
  Print the responsive HTML generated and MJML errors if any
*/
console.log(htmlOutput)
```

You can pass optional `options` as an object to the `mjml2html` function:

option   | unit   | description  | default value
-------------|--------|--------------|---------------
fonts  | object | Default fonts imported in the HTML rendered by HTML | See in [index.js](https://github.com/mjmlio/mjml/blob/master/packages/mjml-core/src/index.js#L36-L44)
keepComments | boolean | Option to keep comments in the HTML output | true 
beautify | boolean | Option to beautify the HTML output | false
minify | boolean | Option to minify the HTML output | false
validationLevel | string | Available values for the [validator](https://github.com/mjmlio/mjml/tree/master/packages/mjml-validator#validating-mjml): 'strict', 'soft', 'skip'  | 'soft'
filePath | boolean | Option to beautify the HTML output | false

## API

A free-to-use MJML API is available to make it easy to integrate MJML in your application. Head over [here](https://mjml.io/api) to learn more about the API.

# Getting Started
This is a responsive email

<p align="center">
  <img width="300px" src="https://cloud.githubusercontent.com/assets/6558790/12751054/322b2c8c-c9bb-11e5-98b9-942f6ea4d585.png" alt="layout">
</p>

Like a regular HTML template, we can split this one into different parts to fit in a grid.

The body of your email, represented by the `mj-body` tag contains the entire content of your document:

<p align="center">
  <img width="300px" src="https://cloud.githubusercontent.com/assets/6558790/12751043/1fd499c4-c9bb-11e5-828f-e0e6e18180b8.png" alt="body">
</p>

From here, you can first define your sections:

<p align="center">
  <img width="300px" src="https://cloud.githubusercontent.com/assets/6558790/12751042/1fd191b6-c9bb-11e5-9450-cc15acec72b4.png" alt="sections">
</p>

Inside any section, there should be columns (even if you need only one column). Columns are what makes MJML responsive.

<p align="center">
  <img width="300px" src="https://cloud.githubusercontent.com/assets/6558790/12751041/1fd112d6-c9bb-11e5-97e7-d9c93c743c4d.png" alt="columns">
</p>

Below, you'll find some basic rules of MJML to keep in mind for later. We'll remind them when useful but better start learning them early on.

## Column sizing

### Auto sizing

The default behavior of the MJML translation engine is to divide the section space (600px by default, but it can be changed with the `width` attribute on `mj-body`) in as many columns as you declare.

<aside class="warning">
  Any mj-element included in a column will have a width equivalent to 100% of this column's width.
</aside>

Let's take the following layout to illustrate this:
```html
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <!-- First column content -->
      </mj-column>
      <mj-column>
        <!-- Second column content -->
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

Since the first section defines only 2 columns, the engine will translate that in a layout where each column takes 50% of the total space (300px each). If we add a third one, it goes down to 33%, and with a fourth one to 25%.

### Manual sizing
You can also manually set the size of your columns, in pixels or percentage, by using the `width` attribute on `mj-column`.

Let's take the following layout to illustrate this:
```html
<mjml>
  <mj-body>
    <mj-section>
      <mj-column width="200px">
        <!-- First column content -->
      </mj-column>
      <mj-column width="400px">
        <!-- Second column content -->
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

## Nesting

```html
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <!-- Column content -->
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

# Basic layout example

In this section, you're going to learn how to code a basic email template using MJML.

Here is the final render we want to end with:

<p align="center">
  <a href="http://mjml.io/try-it-live/templates/hello-world"><img width="350px" src="https://cloud.githubusercontent.com/assets/6558790/12779864/d9c20556-ca6a-11e5-9007-d40ac89c5088.png" alt="sexy"></a>
</p>

<p align="center">
  <a href="/try-it-live/templates/basic"><img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" /></a>
</p>

Looks cool, right?

## Sections

``` html
<mjml>
  <mj-body>

    <!-- Company Header -->
    <mj-section background-color="#f0f0f0"></mj-section>

    <!-- Image Header -->
    <mj-section background-color="#f0f0f0"></mj-section>

    <!-- Introduction Text -->
    <mj-section background-color="#fafafa"></mj-section>

    <!-- 2 columns section -->
    <mj-section background-color="white"></mj-section>

    <!-- Icons -->
    <mj-section background-color="#fbfbfb"></mj-section>

    <!-- Social icons -->
    <mj-section background-color="#f0f0f0"></mj-section>

  </mj-body>
</mjml>
```
First, we will implement the skeleton which are the sections. Here, our email is going to be divided into 6 sections.

## Company Header

``` html

<!-- Company Header -->
<mj-section background-color="#f0f0f0">
  <mj-column>
    <mj-text  font-style="italic"
              font-size="20"
              color="#626262">
      My Company
    </mj-text>
  </mj-column>
</mj-section>

```
The first section of the email consists in a centered banner, containing only the company name. The following markup is the MJML representation of the layout we want to obtain.

<aside class="notice">
Remember everything has to be contained in one column.
</aside>
The text padding represents the inner space around the content within the `mj-text` element.

## Image Header

``` html

<!-- Image Header -->
  <mj-section background-url="http://1.bp.blogspot.com/-TPrfhxbYpDY/Uh3Refzk02I/AAAAAAAALw8/5sUJ0UUGYuw/s1600/New+York+in+The+1960's+-+70's+(2).jpg"
              background-size="cover"
              background-repeat="no-repeat">

    <mj-column width="600">

		  <mj-text  align="center"
                color="#fff"
                font-size="40"
                font-family="Helvetica Neue">Slogan here</mj-text>

      <mj-button background-color="#F63A4D"
                 href="#">
      	Promotion
      </mj-button>

    </mj-column>

  </mj-section>

```
Next comes a section with a background image and a block of text (representing the company slogan) and a button pointing to a page listing all the company promotions.

To add the image header, you will have to replace the section's background-color by a background-url.
Similarly to the first header, you will have to center the text both vertically and horizontally.
The padding remains the same.
The button `href` sets the button location.
In order to have the background rendered full-width in the column, set the column width to 600px with `width="600"`.

## Introduction Text

``` html

<!-- Intro text -->
  <mj-section background-color="#fafafa">
    	<mj-column width="400">

          <mj-text font-style="italic"
                   font-size="20"
                   font-family="Helvetica Neue"
                   color="#626262">My Awesome Text</mj-text>

      		<mj-text color="#525252">
          		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin rutrum enim eget magna efficitur, eu semper augue semper. Aliquam erat volutpat. Cras id dui lectus. Vestibulum sed finibus lectus, sit amet suscipit nibh. Proin nec commodo purus. Sed eget nulla elit. Nulla aliquet mollis faucibus.
          </mj-text>

        	<mj-button background-color="#F45E43"
                     href="#">Learn more</mj-button>

    </mj-column>
  </mj-section>

```

The introduction text will consist of a title, a main text and a button.
The title is a regular `mj-text` that can be customized.

## 2 Columns Section

``` html

<!-- Side image -->
<mj-section background-color="white">

  <!-- Left image -->
  <mj-column>
    <mj-image width="200"
              src="https://designspell.files.wordpress.com/2012/01/sciolino-paris-bw.jpg" />
  </mj-column>

  <!-- right paragraph -->
  <mj-column>
    <mj-text font-style="italic"
             font-size="20"
             font-family="Helvetica Neue"
             color="#626262">
        Find amazing places
      </mj-text>

      <mj-text color="#525252">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin rutrum enim eget magna efficitur, eu semper augue semper. Aliquam erat volutpat. Cras id dui lectus. Vestibulum sed finibus lectus.</mj-text>

  </mj-column>
</mj-section>

```

This sections is made up of 2 columns. One containing an image, the other one containing a text.
For the image part, note that when a tag does not have any child, you can use the XML self-closing tag syntax:
`<mj-image />`

For the text part, you are going to need two `<mj-text>`s like above. One with a title format, and the other one as a regular text.

## Icons

``` html
<!-- Icons -->
<mj-section background-color="#fbfbfb">
  <mj-column>
    <mj-image width="100" src="http://191n.mj.am/img/191n/3s/x0l.png" />
  </mj-column>
  <mj-column>
    <mj-image width="100" src="http://191n.mj.am/img/191n/3s/x01.png" />
  </mj-column>
  <mj-column>
    <mj-image width="100" src="http://191n.mj.am/img/191n/3s/x0s.png" />
  </mj-column>
</mj-section>
```
This section is a 3-columns-based section. Please notice you can make the padding vary to change the space around the images.


## Social Icons

``` html

<mj-section background-color="#e7e7e7">
  <mj-column>
    <mj-social>
      <mj-social-element name="facebook" />
    </mj-social>
  </mj-column>
</mj-section>

```
The MJML standard components library comes with a `mj-social` component. By default, every social network is enabled. To disable some of them, just use their names as an attribute with a `false` value. Here, we're going to use `facebook` only.

# Components

Components are the core of MJML. A component is an abstraction of a more complex email-responsive HTML layout. It exposes attributes, enabling you to interact with the final component visual aspect.

MJML comes out of the box with a set of standard components to help you build easily your first templates without having to reinvent the wheel.

For instance, the `mj-button` components is, on the inside, a complex HTML layout:

``` html

<!-- MJML -->
<mj-button href="#">
    Hello There!
</mj-button>

<!-- HTML -->
<table cellpadding="0" cellspacing="0" style="border:none;border-radius:3px;" align="center">
	<tbody>
		<tr>
			<td style="background-color:#414141;border-radius:3px;color:#ffffff;cursor:auto;" align="center" valign="middle" bgcolor="#414141">
				<a class="mj-content" href="#" style="display:inline-block;text-decoration:none;background-color:#414141;border:1px solid #414141;border-radius:3px;color:#ffffff;font-size:13px;font-weight:bold;padding:15px 30px;" target="_blank">
					Hello There!
				</a>
			</td>
		</tr>
	</tbody>
</table>
```

# Standard Head components

Head components ease your development process, enabling you to import fonts, define default styles or create classes for MJML components among others.

## mjml-attributes

This tag allows you to modify default attributes on a `mj-tag` and add `mj-class` to them.

 ```xml
<mjml>
  <mj-head>
    <mj-attributes>
      <mj-text padding="0" />
      <mj-class name="blue" color="blue" />
      <mj-class name="big" font-size="20px" />
      <mj-all font-family="Arial" />
    </mj-attributes>
  </mj-head>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-text mj-class="blue big">
          Hello World!
        </mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
 ```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/head-attributes">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

<aside class="notice">
  You can use mj-all to set default attributes for every components inside your MJML document
</aside>

<aside class="notice">
  Note that the apply order of attributes is: inline attributes, then classes, then default mj-attributes and then defaultMJMLDefinition
</aside>

## mjml-breakpoint
This tag allows you to control on which breakpoint the layout should go desktop/mobile.

```xml
<mjml>
  <mj-head>
    <mj-breakpoint width="320px" />
  </mj-head>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-text>
          Hello World!
        </mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/head-font">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>


attribute            | unit          | description                    | default value
---------------------|---------------|--------------------------------|---------------
width                | px            | breakpoint's value             | n/a

## mjml-font

This tag allows you to import fonts if used in your MJML document

 ```xml
 <mjml>
   <mj-head>
     <mj-font name="Raleway" href="https://fonts.googleapis.com/css?family=Raleway" />
   </mj-head>
   <mj-body>
     <mj-section>
       <mj-column>
         <mj-text font-family="Raleway, Arial">
           Hello World!
         </mj-text>
       </mj-column>
      </mj-section>
   </mj-body>
 </mjml>
 ```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/head-font">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>


attribute            | unit          | description                    | default value
---------------------|---------------|--------------------------------|---------------
href                 | string        | url of the font                | n/a
name                 | string        | name of the font               | n/a

## mjml-preview

This tag allows you to set the preview that will be displayed in the inbox of the recipient.

 ```xml
<mjml>
  <mj-head>
    <mj-preview>Hello MJML</mj-preview>
  </mj-head>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-text>
          Hello World!           
        </mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
 ```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/head-preview">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

`mj-preview` doesn't support any attribute.

## mjml-style

This tag allows you to set CSS styles that will be applied to the <b>HTML</b> in your MJML document as well as the HTML outputted. The CSS styles will be added to the head of the rendered HTML by default, but can also be inlined by using the `inline="inline"` attribute.

  ```xml
<mjml>
  <mj-head>
    <mj-style>
      @media all and (max-width: 480px) {
        div[style*="color:#F45e46;"] {
          text-align: center !important
        }
      }
    </mj-style>
    <mj-style inline="inline">
      .link-nostyle {
        color: inherit;
        text-decoration: none
      }
    </mj-style>
  </mj-head>
  <mj-body>
    <mj-section >
      <mj-column>
        <mj-image width="100" src="/assets/img/logo-small.png"></mj-image>

        <mj-divider border-color="#F45E43"></mj-divider>

        <mj-text font-size="20px" color="#F45e46" font-family="helvetica">
          Hello <a href="https://mjml.io" class="link-nostyle">World</a>
        </mj-text>

      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
   ```

  <p align="center">
    <a href="https://mjml.io/try-it-live/components/head-style">
      <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
    </a>
  </p>
  
  attribute            | unit          | description                         | default value
  ---------------------|---------------|-------------------------------------|---------------
  inline               | string        | set to "inline" to inline styles    | n/a

## mjml-title

This tag allows you to set the title of an MJML document

 ```xml
<mjml>
  <mj-head>
    <mj-title>Hello MJML</mj-title>
  </mj-head>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-text>
          Hello World!
        </mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
 ```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/head-title">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

# Standard Body components

MJML comes out of the box with a set of standard components to help you build easily your first templates without having to reinvent the wheel.

## mjml-accordion

<p align="center">
  <img src="http://i.imgur.com/C4S9MVc.gif" alt="accordion" />
</p>

`mjml-accordion` is an interactive MJML component to stack content in tabs, so the information is collapsed and only the titles are visible. Readers can interact by clicking on the tabs to reveal the content, providing a great experience on mobile devices where space is scarce.

```xml
<mjml>
  <mj-head>
    <mj-attributes>
      <mj-accordion border="none" padding="1px" />
      <mj-accordion-element icon-wrapped-url="http://i.imgur.com/Xvw0vjq.png" icon-unwrapped-url="http://i.imgur.com/KKHenWa.png" icon-height="24px" icon-width="24px" />
      <mj-accordion-title font-family="Roboto, Open Sans, Helvetica, Arial, sans-serif" background-color="#fff" color="#031017" padding="15px" font-size="18px" />
      <mj-accordion-text font-family="Open Sans, Helvetica, Arial, sans-serif" background-color="#fafafa" padding="15px" color="#505050" font-size="14px" />
    </mj-attributes>
  </mj-head>

  <mj-body>
    <mj-section padding="20px" background-color="#ffffff">
      <mj-column background-color="#dededd">
        <mj-accordion>
          <mj-accordion-element>
            <mj-accordion-title>Why use an accordion?</mj-accordion-title>
            <mj-accordion-text>
              <span style="line-height:20px">
                Because emails with a lot of content are most of the time a very bad experience on mobile, mj-accordion comes handy when you want to deliver a lot of information in a concise way.
              </span>
            </mj-accordion-text>
          </mj-accordion-element>
          <mj-accordion-element>
            <mj-accordion-title>How it works</mj-accordion-title>
            <mj-accordion-text>
              <span style="line-height:20px">
                Content is stacked into tabs and users can expand them at will. If responsive styles are not supported (mostly on desktop clients), tabs are then expanded and your content is readable at once.
              </span>
            </mj-accordion-text>
          </mj-accordion-element>
        </mj-accordion>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/accordion">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="sexy" />
  </a>
</p>

<aside class="notice">
Every attribute in `mj-accordion` are applied to `mj-accordion-element` unless you overide them on `mj-accordion-element`
</aside>


attribute | unit | description | default value
----------|------|-------------|---------------
css-class | string | class name, added to the root HTML element created | n/a
container-background-color | n/a | background-color of the cell | n/a,
border | n/a | border | n/a
font-family | n/a | font | Ubuntu, Helvetica, Arial, sans-serif
icon-align | n/a | icon alignment | middle
icon-wrapped-url | n/a | icon when accordion is wrapped | http://i.imgur.com/bIXv1bk.png
icon-wrapped-alt | n/a | alt text when accordion is wrapped | +
icon-unwrapped-url | n/a | icon when accordion is unwrapped | http://i.imgur.com/w4uTygT.png
icon-unwrapped-alt | n/a | alt text when accordion is unwrapped | -
icon-position | n/a | display icon left or right | right
icon-height | px | icon width | 32px
icon-width | px | icon height | 32px
padding-bottom | px | padding bottom | n/a
padding-left | px | padding left | n/a
padding-right | px | padding right | n/a
padding-top | px | padding top | n/a
padding | px | padding | 10px 25px

### mjml-accordion-element

This component enables you to create a accordion pane

attribute | unit | description | default value
----------|------|-------------|---------------
background-color | n/a | background color | n/a
font-family | n/a | font | Ubuntu, Helvetica, Arial, sans-serif
icon-align | n/a | icon alignment | middle
icon-wrapped-url | n/a | icon when accordion is wrapped | http://i.imgur.com/bIXv1bk.png
icon-wrapped-alt | n/a | alt text when accordion is wrapped | +
icon-unwrapped-url | n/a | icon when accordion is unwrapped | http://i.imgur.com/w4uTygT.png
icon-unwrapped-alt | n/a | alt text when accordion is unwrapped | -
icon-position | n/a | display icon left or right | right
icon-height | n/a | icon width | 32px
icon-width | n/a | icon height | 32px
css-class | string | class name, added to the root HTML element created | n/a

### mjml-accordion-title

This component enables you to add and style a title to your accordion

attribute | unit | description | default value
----------|------|-------------|---------------
background-color | n/a | background color | n/a
color | n/a | text color | n/a
font-family | n/a | font family | Ubuntu, Helvetica, Arial, sans-serif
font-size | px | font size | 13px
padding-bottom | px | padding bottom | n/a
padding-left | px | padding left | n/a
padding-right | px | padding right | n/a
padding-top | px | padding top | n/a
padding | px | padding | 16px
css-class | string | class name, added to the root HTML element created | n/a

### mjml-accordion-text

This component enables you to add and style a text to your accordion

attribute | unit | description | default value
----------|------|-------------|---------------
background-color | n/a | background color | n/a
color | n/a | text color | n/a
font-family | n/a | font family | Ubuntu, Helvetica, Arial, sans-serif
font-size | px | font size | 13px
padding-bottom | px | padding bottom | n/a
padding-left | px | padding left | n/a
padding-right | px | padding right | n/a
padding-top | px | padding top | n/a
padding | px | padding | 16px
css-class | string | class name, added to the root HTML element created | n/a

## mjml-body

This is the starting point of your email.

```xml
<mjml>
  <mj-body>
    <!-- Your email goes here -->
  </mj-body>
</mjml>
```

<p align="center">
  <a target="_blank" href="https://mjml.io/try-it-live/components/body">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

<aside class="notice">
  mj-body replaces the couple mj-body and mj-container of MJML v3.
</aside>

attribute            | unit          | description                    | default value
---------------------|---------------|--------------------------------|---------------
width                | px            | email's width                  | 600px
background-color     | color formats | the general background color   | n/a
css-class            | string        | class name, added to the root HTML element created | n/a

## mjml-button

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/6558790/12751346/fd993192-c9bc-11e5-8c91-37d616bf5874.png" alt="desktop" width="150px" />
</p>

Displays a customizable button.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-button font-family="Helvetica" background-color="#f45e43" color="white">
          Don't click me!
         </mj-button>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/button">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

attribute                   | unit        | description                                      | default value
----------------------------|-------------|--------------------------------------------------|---------------------
background-color            | color       | button background-color                          | #414141
container-background-color  | color       | button container background color                | n/a
border                      | string      | css border format                                | none
border-bottom               | string      | css border format                                | n/a
border-left                 | string      | css border format                                | n/a
border-right                | string      | css border format                                | n/a
border-top                  | string      | css border format                                | n/a
border-radius               | px          | border radius                                    | 3px
font-style                  | string      | normal/italic/oblique                            | n/a
font-size                   | px          | text size                                        | 13px
font-weight                 | number      | text thickness                                   | normal
font-family                 | string      | font name                                        | Ubuntu, Helvetica, Arial, sans-serif
color                       | color       | text color                                       | #ffffff
text-align                  | string      | text-align button content                        | none
text-decoration             | string      | underline/overline/none                          | none
text-transform              | string      | capitalize/uppercase/lowercase                   | none
align                       | string      | horizontal alignment                             | center
vertical-align              | string      | vertical alignment                               | middle
line-height                 | px/%/none   | line-height on link                              | 120%
href                        | link        | link to be triggered when the button is clicked  | n/a
rel                         | string      | specify the rel attribute for the button link    | n/a
target                      | string      | specify the target attribute for the button link | \_blank
inner-padding               | px          | inner button padding                             | 10px 25px
padding                     | px          | supports up to 4 parameters                      | 10px 25px
padding-top                 | px          | top offset                                       | n/a
padding-bottom              | px          | bottom offset                                    | n/a
padding-left                | px          | left offset                                      | n/a
padding-right               | px          | right offset                                     | n/a
width                       | px          | button width                                     | n/a
height                      | px          | button height                                    | n/a
css-class                   | string      | class name, added to the root HTML element created | n/a

## mjml-carousel

<p align="center">
  <img src="http://i.imgur.com/wHqIzgd.gif" alt="desktop" />
</p>

`mjml-carousel` displays a gallery of images or "carousel". Readers can interact by hovering and clicking on thumbnails depending on the email client they use.

This component enables you to set the styles of the carousel elements.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-carousel>
          <mj-carousel-image src="https://www.mailjet.com/wp-content/uploads/2016/11/ecommerce-guide.jpg" />
          <mj-carousel-image src="https://www.mailjet.com/wp-content/uploads/2016/09/3@1x.png" />
          <mj-carousel-image src="https://www.mailjet.com/wp-content/uploads/2016/09/1@1x.png" />
        </mj-carousel>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/carousel">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="sexy" />
  </a>
</p>


attribute | unit | description | default value
----------|------|-------------|---------------
align | string | horizontal alignment | center
border-radius | px | border radius | n/a
background-color | string | column background color | none
thumbnails | String | display or not the thumbnails (visible | hidden)
tb-border | css border format | border of the thumbnails | none
tb-border-radius | px | border-radius of the thumbnails | none
tb-hover-border-color | string | css border color of the hovered thumbnail | none
tb-selected-border-color | string | css border color of the selected thumbnail | none
tb-width | px | thumbnail width | null
left-icon | url | icon on the left of the main image | https://mjml.io/assets/img/left-arrow.png
right-icon | url | icon on the right of the main image | https://mjml.io/assets/img/right-arrow.png
icon-width | px | width of the icons on left and right of the main image | 44px
css-class | string | class name, added to the root HTML element created | n/a

### mjml-carousel-image

This component enables you to add and style the images in the carousel.

attribute | unit | description | default value
----------|------|-------------|---------------
src | url | image source | n/a
thumbnails-src | url | image source to have a thumbnail different than the image it's linked to | null
href | url | link to redirect to on click | n/a
target | string | link target on click | \_blank
rel | string | specify the rel attribute | n/a
alt | string | image description | n/a
title | string | tooltip & accessibility | n/a
css-class | string | class name, added to the root HTML element created | n/a

## mjml-column

Columns enable you to horizontally organize the content within your sections. They must be located under `mj-section` tags in order to be considered by the engine.
To be responsive, columns are expressed in terms of percentage.

Every single column has to contain something because they are responsive containers, and will be vertically stacked on a mobile view. Any standard component, or component that you have defined and registered, can be placed within a column – except `mj-column` or `mj-section` elements.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <!-- Your first column --> 
      </mj-column>
      <mj-column>
        <!-- Your second column -->
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/column">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

<aside class="notice">
  Columns are meant to be used as a container for your content. They must not be used as offset. Any mj-element included in a column will have a width equivalent to 100% of this column's width.
</aside>

<aside class="warning">
  Columns cannot be nested into columns, and sections cannot be nested into columns as well.
</aside>

attribute           | unit        | description                    | default attributes
--------------------|-------------|--------------------------------|--------------------------------------
background-color    | string      | background color for a column  | n/a
border              | string      | css border format              | none
border-bottom       | string      | css border format              | n/a
border-left         | string      | css border format              | n/a
border-right        | string      | css border format              | n/a
border-top          | string      | css border format              | n/a
border-radius       | px          | border radius                  | n/a
width               | percent/px  | column width                   | (100 / number of columns in section)%
vertical-align      | string      | middle/top/bottom              | top
padding             | px          | supports up to 4 parameters    | 20px 0
padding-top         | px          | section top offset             | n/a
padding-bottom      | px          | section bottom offset          | n/a
padding-left        | px          | section left offset            | n/a
padding-right       | px          | section right offset           | n/a
css-class           | string      | class name, added to the root HTML element created | n/a

## mjml-divider

Displays a horizontal divider that can be customized like a HTML border.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-divider border-width="1px" border-style="dashed" border-color="lightgrey" />
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/divider">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

attribute                   | unit        | description                    | default value
----------------------------|-------------|--------------------------------|------------------------------
border-color                | color       | divider color                  | #000000
border-style                | string      | dashed/dotted/solid            | solid
border-width                | px          | divider's border width         | 4px
width                       | px/percent  | divider width                  | 100%
container-background-color  | color       | inner element background color | n/a
padding                     | px          | supports up to 4 parameters    | 10px 25px
padding-top                 | px          | top offset                     | n/a
padding-bottom              | px          | bottom offset                  | n/a
padding-left                | px          | left offset                    | n/a
padding-right               | px          | right offset                   | n/a
css-class                   | string      | class name, added to the root HTML element created | n/a

## mjml-group


<p align="center">
  Desktop<br />
  <img src="https://cloud.githubusercontent.com/assets/570317/15677458/a6ad2c1c-274a-11e6-8fdf-6853d748ef27.png" />
</p>

<p align="center">
  Mobile<br />
  <img src="https://cloud.githubusercontent.com/assets/570317/15677396/6bb62708-274a-11e6-8c59-0d8b3944a2ae.png" />
</p>

mj-group allows you to prevent columns from stacking on mobile. To do so, wrap the columns inside a `mj-group` tag, so they'll stay side by side on mobile.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-group>
        <mj-column>
          <mj-image width="137px" height="185px" padding="0"    src="https://mjml.io/assets/img/easy-and-quick.png" />
          <mj-text align="center">
            <h2>Easy and quick</h2>
            <p>Write less code, save time and code more efficiently with MJML’s semantic syntax.</p>
          </mj-text>
        </mj-column>
        <mj-column>
          <mj-image width="166px" height="185px" padding="0" src="https://mjml.io/assets/img/responsive.png" />
          <mj-text align="center">
            <h2>Responsive</h2>
            <p>MJML is responsive by design on most-popular email clients, even Outlook.</p>
          </mj-text>
        </mj-column>
      </mj-group>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/group"><img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" /></a>
</p>

<aside class="notice">
  Column inside a group must have a width in percentage, not in pixel
</aside>


<aside class="notice">
  You can have both column and group inside a Section
</aside>

<aside class="notice">
  <b>iOS 9 Issue:</b> If you use a HTML beautifier for MJML output, iOS9 will render your columns inside a mj-group as stacked. On the output HTML, remove the <b>blank space</b> between the two columns inside a mj-group.
</aside>


attribute           | unit        | description                    | default attributes
--------------------|-------------|--------------------------------|--------------------------------------
width               | percent/px  | group width                    | (100 / number of sibling in section)%
vertical-align      | string      | middle/top/bottom              | top
background-color    | string      | background color for a group   | n/a
css-class           | string      | class name, added to the root HTML element created | n/a

## mjml-hero

Display a section with a background image and some content inside (mj-text, mj-button, mj-image ...) wrapped in mj-hero-content component

Fixed height  

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1830348/15354833/bfe7faaa-1cef-11e6-8d38-15e8951b6636.png" />
</p>

```xml
<mjml>
  <mj-body>
    <mj-hero
      mode="fixed-height"
      height="469px"
      width="100%"
      background-width="600px"
      background-height="469px"
      background-url="https://cloud.githubusercontent.com/assets/1830348/15354890/1442159a-1cf0-11e6-92b1-b861dadf1750.jpg"
      background-color="#2a3448"
      padding="100px 0px">
      <!-- To add content like mj-image, mj-text, mj-button ... use the mj-hero-content component -->
      <mj-text
        padding="20px"
        color="#ffffff"
        font-family="Helvetica"
        align="center"
        font-size="45"
        line-height="45px"
        font-weight="900">
        GO TO SPACE
      </mj-text>
      <mj-button href="https://mjml.io/" align="center">
        ORDER YOUR TICKET NOW
      </mj-button>
    </mj-hero>
  </mj-body>
</mjml>
 ```

 <p align="center">
   <a href="https://mjml.io/try-it-live/components/hero">
     <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
   </a>
 </p>

Fluid height

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1830348/15354867/fc2f404a-1cef-11e6-92ac-92de9e438210.png" />
</p>

```xml
<mjml>
  <mj-body>
    <mj-hero
      mode="fluid-height"
      background-width="600px"
      background-height="469px"
      background-url="https://cloud.githubusercontent.com/assets/1830348/15354890/1442159a-1cf0-11e6-92b1-b861dadf1750.jpg"
      background-color="#2a3448"
      padding="100px 0px"
      width="100%">
      <!-- To add content like mj-image, mj-text, mj-button ... use the mj-hero-content component -->
      <mj-text
        padding="20px"
        color="#ffffff"
        font-family="Helvetica"
        align="center"
        font-size="45"
        line-height="45px"
        font-weight="900">
        GO TO SPACE
      </mj-text>
      <mj-button href="https://mjml.io/" align="center">
        ORDER YOUR TICKET NOW
      </mj-button>
    </mj-hero>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/hero/1">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

<aside class="notice">
  The height attribute is required only for the fixed-height mode
</aside>

<aside class="notice">
  <span style="font-weight:bold;">The background position does not work in fluid-height mode on outlook.com</span>
</aside>

<aside class="notice">
For better result we encourage you to use a background image width equal to the hero container width and always specify a fallback background color, in case the user email client does not support background images.
</aside>

<aside class="notice">
  Please keep the hero container height below the image height. When the hero container height - both in fixed or fluid modes - is greater than the background image height, we can’t guarantee a perfect rendering in all supported email clients
</aside>

attribute           | unit                                | description                                                          | default value
--------------------|-------------------------------------|----------------------------------------------------------------------|--------------
width               | px                                  | hero container width                                                 | parent element width
mode                | fluid-height/fixed-height           | choose if the height is fixed based on the height attribute or fluid | fluid-height
height              | px                                  | hero section height (required for fixed-height mode)                 | 0px
background-width    | px                                  | width of the image used                                              | 0px
background-height   | px                                  | height of the image used                                             | 0px
background-url      | url                                 | absolute background url                                              | n/a
background-color    | color                               | hero background color                                                | #ffffff
background-position | top/center/bottom left/center/right | background image position                                            | center center
padding             | px                                  | supports up to 4 parameters                                          | 0px
padding-top         | px                                  | top offset                                                           | 0px
padding-right       | px                                  | right offset                                                         | 0px
padding-left        | px                                  | left offset                                                          | 0px
padding-bottom      | px                                  | bottom offset                                                        | 0px
vertical-align      | top/middle/bottom                   | content vertical alignment                                           | top
css-class | string | class name, added to the root HTML element created | n/a

## mjml-image

Displays a responsive image in your email. It is similar to the HTML `<img />` tag.
Note that if no width is provided, the image will use the parent column width.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-image width="300" src="http://www.online-image-editor.com//styles/2014/images/example_image.png" />
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/image">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>


attribute                     | unit          | description                    | default value
------------------------------|---------------|--------------------------------|-----------------------------
padding                       | px            | supports up to 4 parameters    | 10px 25px
padding-top                   | px            | top offset                     | n/a
padding-bottom                | px            | bottom offset                  | n/a
padding-left                  | px            | left offset                    | n/a
padding-right                 | px            | right offset                   | n/a
container-background-color    | color         | inner element background color | n/a
border                        | string        | css border definition          | none
border-radius                 | px            | border radius                  | n/a
width                         | px            | image width                    | 100%
height                        | px            | image height                   | auto
src                           | url           | image source                   | n/a
srcset                        | url & width   | enables to set a different image source based on the viewport | n/a
href                          | url           | link to redirect to on click   | n/a
target                        | string        | link target on click           | \_blank
rel                           | string        | specify the rel attribute      | n/a
alt                           | string        | image description              | n/a
align                         | position      | image alignment                | center
title                         | string        | tooltip & accessibility        | n/a
css-class                     | string        | class name, added to the root HTML element created | n/a

## mjml-navbar

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1830348/15317906/d6cef510-1c23-11e6-83d7-31e4e4f8ba2a.png" width="800px" />
</p>

Displays a menu for navigation with an optional hamburger mode for mobile devices.

```xml
<mjml>
  <mj-body>
    <mj-section background-color="#ef6451">
      <mj-column>
        <mj-navbar base-url="https://mjml.io" hamburger="hamburger" ico-color="#ffffff">
            <mj-navbar-link href="/gettings-started-onboard" color="#ffffff">Getting started</mj-navbar-link>
            <mj-navbar-link href="/try-it-live" color="#ffffff">Try it live</mj-navbar-link>
            <mj-navbar-link href="/templates" color="#ffffff">Templates</mj-navbar-link>
            <mj-navbar-link href="/components" color="#ffffff">Components</mj-navbar-link>
        </mj-navbar>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a target="_blank" href="https://mjml.io/try-it-live/components/navbar">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

### mjml-navbar

Individual links of the menu should we wrapped inside mj-navbar.


Standard Desktop:

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1830348/15317906/d6cef510-1c23-11e6-83d7-31e4e4f8ba2a.png" width="800px" />
</p>

Standard Mobile:

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1830348/15317917/e514d0a4-1c23-11e6-8e5a-c23da9ac1d4e.png" width="318px" />
</p>

Mode hamburger enabled:

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1830348/15317922/f01c5c24-1c23-11e6-9b0c-95b0602da260.gif" width="309px" />
</p>

<aside class="notice">
  The "hamburger" feature only work on mobile device with all iOS mail client, for others mail clients the render is performed on an normal way, the links are displayed inline and the hamburger is not visible.
</aside>

<aside class="notice">
  All the attributes prefixed with <code>ico-</code> help to customize the hamburger icon. They only work with the hamburger mode enabled.
</aside>

attribute                   | unit               | description                                                                                      | default value
----------------------------|--------------------|--------------------------------------------------------------------------------------------------|-----------------
base url                    | string             | base url for children components                                                                 | n/a
hamburger                   | string             | activate the hamburger navigation on mobile if the value is hamburger                            | n/a
align                       | string             | align content left/center/right                                                                  | center
ico-open                    | ASCII code decimal | char code for a custom open icon (hamburger mode required)                                       | 9776
ico-close                   | ASCII code decimal | char code for a custom close icon (hamburger mode required)                                      | 8855
ico-padding                 | px                 | hamburger icon padding, supports up to 4 parameters (hamburger mode required)                    | 10px
ico-padding-top             | px                 | hamburger icon top offset (hamburger mode required)                                              | 10px
ico-padding-right           | px                 | hamburger icon right offset (hamburger mode required)                                            | 10px
ico-padding-bottom          | px                 | hamburger icon bottom offset (hamburger mode required)                                           | 10px
ico-padding-left            | px                 | hamburger icon left offset (hamburger mode required)                                             | 10px
ico-align                   | string             | hamburger icon alignment, left/center/right (hamburger mode required)                            | center
ico-color                   | color format       | hamburger icon color (hamburger mode required)                                                   | #000000
ico-font-size               | px                 | hamburger icon size (hamburger mode required)                                                    | 30px
ico-font-family             | string             | hamburger icon font (only on hamburger mode)                                                     | Ubuntu, Helvetica, Arial, sans-serif
ico-text-transform          | string             | hamburger icon text transformation none/capitalize/uppercase/lowercase (hamburger mode required) | none
ico-text-decoration         | string             | hamburger icon text decoration none/underline/overline/line-through (hamburger mode required)    | none
ico-line-height             | px                 | hamburger icon line height (hamburger mode required)                                             | 30px


### mjml-navbar-link


This component should be used to display an individual link in the navbar.

<aside class="notice">
  The mj-navbar-link component must be used inside a mj-navbar component only.
</aside>

attribute        | unit          | description                           | default value
-----------------|---------------|---------------------------------------|------------------------------
color            | color         | text color                            | #000000
font-family      | string        | font                                  | Ubuntu, Helvetica, Arial, sans-serif
font-size        | px            | text size                             | 13px
font-style       | string        | normal/italic/oblique                 | n/a
font-weight      | number        | text thickness                        | n/a
line-height      | px            | space between the lines               | 22px
text-decoration  | string        | underline/overline/none               | n/a
text-transform   | string        | capitalize/uppercase/lowercase/none   | uppercase
padding          | px            | supports up to 4 parameters           | 10px 25px
padding-top      | px            | top offset                            | n/a
padding-bottom   | px            | bottom offset                         | n/a
padding-left     | px            | left offset                           | n/a
padding-right    | px            | right offset                          | n/a
rel              | string        | specify the rel attribute             | n/a
href             | string        | link to redirect to on click          | n/a
target           | string        | link target on click                  | n/a

## mjml-raw

Displays raw HTML that is not going to be parsed by the MJML engine. Anything left inside this tag should be raw, responsive HTML.

```xml
<mjml>
  <mj-body>
    <mj-raw>
      <!-- Your content goes here -->
    </mj-raw>
  </mj-body>
</mjml>
```

<p align="center">
  <a target="_blank" href="https://mjml.io/try-it-live/components/raw">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

## mjml-section

Sections are intended to be used as rows within your email.
They will be used to structure the layout.

```xml
<mjml>
  <mj-body>
    <mj-section full-width="full-width" background-color="red">
      <!-- Your columns go here -->
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/section">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

The `full-width` property will be used to manage the background width.
By default, it will be 600px. With the `full-width` property on, it will be
changed to 100%.

<aside class="notice">
  <b>Inverting the order in which columns display:</b> set the `direction` attribute to `rtl` to change the order in which columns display on desktop. Because MJML is mobile-first, structure the columns in the <b>order you want them to stack on mobile</b>, and use `direction` to change the order they display <b>on desktop</b>.
</aside>

<aside class="warning">
  Sections cannot be nested into sections. Also, any content in a section should also be wrapped in a column.
</aside>

attribute           | unit        | description                    | default value
--------------------|-------------|--------------------------------|---------------
full-width          | string      | make the section full-width    | n/a
border              | string      | css border format              | none
border-bottom       | string      | css border format              | n/a
border-left         | string      | css border format              | n/a
border-right        | string      | css border format              | n/a
border-top          | string      | css border format              | n/a
border-radius       | px          | border radius                  | n/a
background-color    | color       | section color                  | n/a
background-url      | url         | background url                 | n/a
background-repeat   | string      | css background repeat          | repeat
background-size     | percent/px  | css background size            | auto
vertical-align      | string      | css vertical-align             | top
text-align          | string      | css text-align                 | center
padding             | px          | supports up to 4 parameters    | 20px 0
padding-top         | px          | section top offset             | n/a
padding-bottom      | px          | section bottom offset          | n/a
padding-left        | px          | section left offset            | n/a
padding-right       | px          | section right offset           | n/a
direction           | string      | ltr / rtl                      | ltr
css-class           | string      | class name, added to the root HTML element created | n/a

## mjml-social

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/6558790/12751360/0c78ce48-c9bd-11e5-98ca-4a2ac9e6341b.png" alt="desktop" style="width: 250px;"/>
</p>

Displays calls-to-action for various social networks with their associated logo. You can add social networks with the `mj-social-element` tag.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-social font-size="15px" icon-size="30px" mode="horizontal">
          <mj-social-element name="facebook" href="https://mjml.io/" background-color="#4d4d4d">
            Facebook
          </mj-social-element>
          <mj-social-element name="google" href="https://mjml.io/" background-color="#4d4d4d">
            Google
          </mj-social-element>
          <mj-social-element  name="instagram" href="https://mjml.io/" background-color="#4d4d4d">
            Instagram
          </mj-social-element>
        </mj-social>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<aside class="notice">
  You can add any unsupported network like this:

```xml
    <mj-social-element href="url" background-color="#FF00FF" src="path-to-your-icon">
      Optional label
    </mj-social-element>
```
</aside>

<p align="center">
  <a href="https://mjml.io/try-it-live/components/social">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

<!--
<aside class="notice">
  Note that you can disable default sharing option by adding <code class="prettyprint">:url</code> on any social network.
  Example: <code class="prettyprint">&lt;mj-social display="facebook" /&gt;</code> will render <code class="prettyprint">https://www.facebook.com/sharer/sharer.php?u=[[facebook-href]]</code> url, and <code class="prettyprint">&lt;mj-social display="facebook:url" /&gt;</code> will render <code class="prettyprint">[[facebook-href]]</code> url
</aside>
-->


attribute                   | unit        | description                   | default value
----------------------------|-------------|-------------------------------|---------------------------
border-radius               | px          | border radius                 | 3px
font-family                 | string      | font name                     | Ubuntu, Helvetica, Arial, sans-serif
font-size                   | px/em       | font size                     | 13px
icon-size                   | percent/px  | icon size                     | 20px
line-height                 | percent/px  | space between lines           | 22px
mode                        | string      | vertical/horizontal           | horizontal
text-decoration             | string      | underline/overline/none       | none
align                       | string      | left/right/center             | center
color                       | color       | text color                    | #333333
inner-padding               | px          | social network surrounding padding                 | 4px
padding                     | px          | supports up to 4 parameters                       | 10px 25px
padding-top                 | px          | top offset                         | n/a
padding-bottom              | px          | bottom offset                    | n/a
padding-left                | px          | left offset                      | n/a
padding-right               | px          | right offset                       | n/a
container-background-color  | color       | inner element background color                     | n/a

### mj-social-element

This component enables you to display a given social network inside `mj-social`.  
Note that default icons are transparent, which allows `background-color` to actually be the icon color.

attribute                   | unit        | description                   | default value
----------------------------|-------------|-------------------------------|---------------------------
border-radius               | px          | border radius                 | 3px
href                        | url         | button redirection url        | [[SHORT_PERMALINK]]
target                      | string      | link target                   | \_blank
background-color            | color       | icon color                    | Each social `name` has its own default
font-family                 | string      | font name                     | Ubuntu, Helvetica, Arial, sans-serif
font-size                   | px/em       | font size                     | 13px
icon-size                   | percent/px  | icon size                     | 20px
line-height                 | percent/px  | space between lines           | 22px
mode                        | string      | vertical/horizontal           | horizontal
text-decoration             | string      | underline/overline/none       | none
text-mode                   | string      | display social network name   | true
align                       | string      | left/right/center             | center
color                       | color       | text color                    | #333333
name                        | string      | `facebook google instagram pinterest linkedin twitter` | N/A
src                         | url         | image source                  | Each social `name` has its own default
padding                     | px          | supports up to 4 parameters                       | 10px 25px
padding-top                 | px          | top offset                         | n/a
padding-bottom              | px          | bottom offset                    | n/a
padding-left                | px          | left offset                      | n/a
padding-right               | px          | right offset                       | n/a
target                      | string      | usual html link target              | \_blank

## mjml-spacer

Displays a blank space.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-text>A first line of text</mj-text>
        <mj-spacer height="50px" />
        <mj-text>A second line of text</mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/spacer">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

attribute                   | unit        | description                    | default value
----------------------------|-------------|--------------------------------|------------------------------
height                      | px          | spacer height                  | 20px
css-class                   | string      | class name, added to the root HTML element created | n/a

## mjml-table

This tag allows you to display table and filled it with data. It only accepts plain HTML.

```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-table>
          <tr style="border-bottom:1px solid #ecedee;text-align:left;padding:15px 0;">
            <th style="padding: 0 15px 0 0;">Year</th>
            <th style="padding: 0 15px;">Language</th>
            <th style="padding: 0 0 0 15px;">Inspired from</th>
          </tr>
          <tr>
            <td style="padding: 0 15px 0 0;">1995</td>
            <td style="padding: 0 15px;">PHP</td>
            <td style="padding: 0 0 0 15px;">C, Shell Unix</td>
          </tr>
          <tr>
            <td style="padding: 0 15px 0 0;">1995</td>
            <td style="padding: 0 15px;">JavaScript</td>
            <td style="padding: 0 0 0 15px;">Scheme, Self</td>
          </tr>
        </mj-table>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/table">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

attribute                   | unit                        | description                    | default value
----------------------------|-----------------------------|------------------------------- |--------------
color                       | color                       | text header & footer color     | #000
cellpadding                 | pixels                      | space between cells            | n/a
cellspacing                 | pixels                      | space between cell and border  | n/a
font-family                 | string                      | font name                      | Ubuntu, Helvetica, Arial, sans-serif
font-size                   | px/em                       | font size                      | 13px
line-height                 | percent/px                  | space between lines            | 22px
container-background-color  | color                       | inner element background color | n/a
padding                     | px                          | supports up to 4 parameters    | 10px 25px
padding-top                 | px                          | top offset                     | n/a
padding-bottom              | px                          | bottom offset                  | n/a
padding-left                | px                          | left offset                    | n/a
padding-right               | px                          | right offset                   | n/a
width                       | percent/px                  | table width                    | 100%
table-layout                | auto/fixed/initial/inherit  | sets the table layout.         | auto

## mjml-text

This tag allows you to display text in your email.

 ```xml
<mjml>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-text>
          <h1>
            Hey Title!
          </h1>
        </mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
 ```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/text">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

<aside class="notice">
  `MjText` can contain any HTML tag with any attributes. Don't forget to encode special characters to avoid unexpected behaviour from MJML's parser
</aside>

 attribute                    | unit          | description                                 | default value
------------------------------|---------------|---------------------------------------------|-------------------------------------
 color                        | color         | text color                                  | #000000
 font-family                  | string        | font                                        | Ubuntu, Helvetica, Arial, sans-serif
 font-size                    | px            | text size                                   | 13px
 font-style                   | string        | normal/italic/oblique                       | n/a
 font-weight                  | number        | text thickness                              | n/a
 line-height                  | px            | space between the lines                     | 22px
 letter-spacing               | px            | letter spacing                              | none
 height                       | px            | The height of the element                   | n/a
 text-decoration              | string        | underline/overline/line-through/none        | n/a
 text-transform               | string        | uppercase/lowercase/capitalize              | n/a
 align                        | string        | left/right/center/justify                   | left
 container-background-color   | color         | inner element background color              | n/a
 padding                      | px            | supports up to 4 parameters                 | 10px 25px
 padding-top                  | px            | top offset                                  | n/a
 padding-bottom               | px            | bottom offset                               | n/a
 padding-left                 | px            | left offset                                 | n/a
 padding-right                | px            | right offset                                | n/a
 css-class                    | string        | class name, added to the root HTML element created | n/a

## mjml-wrapper

<p align="center">
  <img src="http://i.imgur.com/6YKq83B.png" alt="wrapper" />
</p>

Wrapper enables to wrap multiple sections together. It's especially useful to achieve nested layouts with shared border or background images across sections.

```xml
<mjml>
  <mj-body>
    <mj-wrapper border="1px solid #000000" padding="50px 30px">
      <mj-section border-top="1px solid #aaaaaa" border-left="1px solid #aaaaaa" border-right="1px solid #aaaaaa" padding="20px">
        <mj-column>
          <mj-image padding="0" src="https://placeholdit.imgix.net/~text?&w=350&h=150" />
        </mj-column>
      </mj-section>
      <mj-section border-left="1px solid #aaaaaa" border-right="1px solid #aaaaaa" padding="20px" border-bottom="1px solid #aaaaaa">
        <mj-column border="1px solid #dddddd">
          <mj-text padding="20px"> First line of text </mj-text>
          <mj-divider border-width="1px" border-style="dashed" border-color="lightgrey" padding="0 20px" />
          <mj-text padding="20px"> Second line of text </mj-text>
        </mj-column>
      </mj-section>
    </mj-wrapper>
  </mj-body>
</mjml>
```

<p align="center">
  <a href="https://mjml.io/try-it-live/components/wrapper">
    <img width="100px" src="https://mjml.io/assets/img/svg/TRYITLIVE.svg" alt="try it live" />
  </a>
</p>

The `full-width` property will be used to manage the background width.
By default, it will be 600px. With the `full-width` property on, it will be
changed to 100%.

<aside class="notice">
  You can't nest a full-width section inside a full-width wrapper, section will act as a non-full-width section.
</aside>

<aside class="notice">
  If you're using a background-url on a `mj-wrapper` then do not add one into a section within the mj-wrapper. Outlook Desktop doesn't support nested VML, so it will most likely break your email.
</aside>


attribute           | unit        | description                    | default value
--------------------|-------------|--------------------------------|---------------
full-width          | string      | make the wrapper full-width    | n/a
border              | string      | css border format              | none
border-bottom       | string      | css border format              | n/a
border-left         | string      | css border format              | n/a
border-right        | string      | css border format              | n/a
border-top          | string      | css border format              | n/a
border-radius       | px          | border radius                  | n/a
background-color    | color       | section color                  | n/a
background-url      | url         | background url                 | n/a
background-repeat   | string      | css background repeat          | repeat
background-size     | percent/px  | css background size            | auto
vertical-align      | string      | css vertical-align             | top
text-align          | string      | css text-align                 | center
padding             | px          | supports up to 4 parameters    | 20px 0
padding-top         | px          | section top offset             | n/a
padding-bottom      | px          | section bottom offset          | n/a
padding-left        | px          | section left offset            | n/a
padding-right       | px          | section right offset           | n/a
css-class           | string      | class name, added to the root HTML element created | n/a

# Community components

In addition to the standard components available in MJML, our awesome community is contributing by creating their own components.

To use a community component, proceed as follows:

* Install MJML locally with `npm install mjml` in a folder
* Install the community component with `npm install {component-name}` in the same folder
* Create a `.mjmlconfig` file in the same folder with:

```
{
  "packages": [
    "./node_modules/component-name/path-to-js-file"
  ]
}
```

Finally, you can now use the component in a MJML file, for example `index.mjml`, and run MJML locally in your terminal (make sure to be in the folder where you installed MJML and the community component): `./node_modules/.bin/mjml index.mjml`.

## mjml-chart

Thanks to [image-charts](https://image-charts.com/) for their contribution with this component. It's available on [Github](https://github.com/image-charts/mjml-charts) and [NPM](https://www.npmjs.com/package/mjml-chart).

<p align="center">
  <img src="https://puu.sh/tjIVp/cd01defdac.png" alt="mjml-charts" />
</p>

Displays charts as images in your email.

# Validating MJML

MJML provides a validation layer that helps you building your email. It can detect if you misplaced or mispelled a MJML component, or if you used any unauthorised attribute on a specific component. It supports 3 levels of validation:

* `skip`: your document is rendered without going through validation
* `soft`: your document is going through validation and is rendered, even if it has errors
* `strict`: your document is going through validation and is not rendered if it has any error

By default, the level is set to `soft`.

## In CLI

When using the `mjml` command line, you can add the option `-l` or `--level` with the validation level you want.

> Validates the file without rendering it

```bash
mjml --validate template.mjml
```

> Sets the validation level to `skip` (so that the file is not validated) and renders the file

```bash
mjml -l skip -r template.mjml
```

## In Javascript

In Javascript, you can provide the level through the `options` parameters on `MJMLRenderer`. Ex: `new MJMLRenderer(inputMJML, { level: strict })`

`strict` will raise a `MJMLValidationError` exception. This object has 2 methods:
* `getErrors` returns an array of objects with `line`, `message`, `tagName` as well as a `formattedMessage` which contains the `line`, `message` and `tagName` concatenated in a sentence.
* `getMessages` returns an array of `formattedMessage`.

When using `soft`, no exception will be raised. You can get the errors using the object returned by the `render` method `errors`. It is the same object returned by `getErrors` on strict mode.

### Use of .mjmlconfig file
If not exists, add a .mjmlconfig file at the root of your project (where you execute the mjml command).
Add the following key to the json:

```json
{
    ...
    "validators": [
        "validateTag",
        "validateAttribute",
        "validChildren",
        "./validators/ColumnCount.js",
    ]
}
```

`"validateTag"`, `"validateAttribute"` and `"validChildren"` are the default validation rules.
If you want to add custom rules, you can add the path to the file where the validtion function resides.

# Creating a Component

One of the great advantages of MJML is that it's component-based. Components abstract complex patterns and can easily be reused. In addition to the standard library of components, it is also possible to create your own components!

We will soon publish a step-by-step guide to explain how to create a custom component with MJML 4. Meanwhile, you can find a guide on how to create a custom component for MJML 3 [here](https://medium.com/mjml-making-responsive-email-easy/tutorial-creating-your-own-mjml-component-d3a236ab7093#.pz0ebb537) (note that it won't be compatible with MJML 4).

# Tooling

In order to provide you with the best experience with MJML and help you use it more efficiently, we've developed some tools to integrate it seamlessly in your development workflow:

## Atom language plugin
[Atom](https://atom.io) is a powerful text editor originally released by [Github](https://github.com). This package provides autocompletion and syntax highlighting for MJML. It is available [on Github](https://github.com/mjmlio/language-mjml) and through the [Atom Package Manager (APM)](https://atom.io/packages/language-mjml).

## Atom linter
In addition to the language plugin, a linter is available to highlight errors in MJML. The linter is available [on Github](https://github.com/mjmlio/atom-linter-mjml) and through the [Atom Package Manager (APM)](https://atom.io/packages/linter-mjml).

## Sublime Text
[Sublime Text](https://www.sublimetext.com/) is a powerful text editor. We're providing you with a package to color MJML tags. It is available [on Github](https://github.com/mjmlio/mjml-syntax) and through the [Sublime Package Control](https://packagecontrol.io/packages/MJML-syntax).

## Gulp
Gulp is a tool designed to help you automate and enhance your workflow. Our plugin enables you to plug the MJML translation engine into your workflow, helping you to streamline your development workflow. It is available here on [Github](https://github.com/mjmlio/gulp-mjml)

## Contribute to the MJML ecosystem
The MJML ecosystem is still young and we're also counting on your help to help us make it grow and provide its community with even more awesome tools, always aiming to making development with MJML an efficient and fun process!

Getting involved is really easy and our [roadmap is open](https://github.com/mjmlio/mjml/projects/1). If you want to contribute, feel free to [open an issue](https://github.com/mjmlio/mjml/issues) or [submit a pull-request](https://github.com/mjmlio/mjml/pulls)!
