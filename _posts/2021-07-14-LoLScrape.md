---
title: "Scraping e análise de dados de LoL"
date: 2021-07-14
tags: jupyter-notebook python pandas
---
Objetivo: Realizar scraping  para obter dados dos campeões do jogo LoL.

Utilização de BeautifulSoup e python para realizar data scraping do site de fandom do jogo LoL e analizar o tamanho das descrições de habilidades ao longo do tempo.
<!--more-->

<html>
<head><meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>unt</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>




<style type="text/css">
    pre { line-height: 125%; }
td.linenos .normal { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
span.linenos { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
td.linenos .special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>



<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/*
 * Webkit scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar,
[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-corner {
  background: var(--jp-scrollbar-background-color);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-thumb {
  background: rgb(var(--jp-scrollbar-thumb-color));
  border: var(--jp-scrollbar-thumb-margin) solid transparent;
  background-clip: content-box;
  border-radius: var(--jp-scrollbar-thumb-radius);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-track:horizontal {
  border-left: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
  border-right: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-track:vertical {
  border-top: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
  border-bottom: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar */

[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar::-webkit-scrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar::-webkit-scrollbar,
[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-corner,
[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-corner {
  background-color: transparent;
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-thumb,
[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
  border: var(--jp-scrollbar-thumb-margin) solid transparent;
  background-clip: content-box;
  border-radius: var(--jp-scrollbar-thumb-radius);
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-track:horizontal {
  border-left: var(--jp-scrollbar-endpad) solid transparent;
  border-right: var(--jp-scrollbar-endpad) solid transparent;
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-track:vertical {
  border-top: var(--jp-scrollbar-endpad) solid transparent;
  border-bottom: var(--jp-scrollbar-endpad) solid transparent;
}

/*
 * Phosphor
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-Widget, /* </DEPRECATED> */
.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  cursor: default;
}


/* <DEPRECATED> */ .p-Widget.p-mod-hidden, /* </DEPRECATED> */
.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-CommandPalette, /* </DEPRECATED> */
.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-CommandPalette-search, /* </DEPRECATED> */
.lm-CommandPalette-search {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-content, /* </DEPRECATED> */
.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}


/* <DEPRECATED> */ .p-CommandPalette-header, /* </DEPRECATED> */
.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}


/* <DEPRECATED> */ .p-CommandPalette-item, /* </DEPRECATED> */
.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}


/* <DEPRECATED> */ .p-CommandPalette-itemIcon, /* </DEPRECATED> */
.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-itemContent, /* </DEPRECATED> */
.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}


/* <DEPRECATED> */ .p-CommandPalette-itemShortcut, /* </DEPRECATED> */
.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-itemLabel, /* </DEPRECATED> */
.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-DockPanel, /* </DEPRECATED> */
.lm-DockPanel {
  z-index: 0;
}


/* <DEPRECATED> */ .p-DockPanel-widget, /* </DEPRECATED> */
.lm-DockPanel-widget {
  z-index: 0;
}


/* <DEPRECATED> */ .p-DockPanel-tabBar, /* </DEPRECATED> */
.lm-DockPanel-tabBar {
  z-index: 1;
}


/* <DEPRECATED> */ .p-DockPanel-handle, /* </DEPRECATED> */
.lm-DockPanel-handle {
  z-index: 2;
}


/* <DEPRECATED> */ .p-DockPanel-handle.p-mod-hidden, /* </DEPRECATED> */
.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-DockPanel-handle:after, /* </DEPRECATED> */
.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='horizontal'],
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='vertical'],
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='horizontal']:after,
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='vertical']:after,
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}


/* <DEPRECATED> */ .p-DockPanel-overlay, /* </DEPRECATED> */
.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}


/* <DEPRECATED> */ .p-DockPanel-overlay.p-mod-hidden, /* </DEPRECATED> */
.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-Menu, /* </DEPRECATED> */
.lm-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-Menu-content, /* </DEPRECATED> */
.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}


/* <DEPRECATED> */ .p-Menu-item, /* </DEPRECATED> */
.lm-Menu-item {
  display: table-row;
}


/* <DEPRECATED> */
.p-Menu-item.p-mod-hidden,
.p-Menu-item.p-mod-collapsed,
/* </DEPRECATED> */
.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}


/* <DEPRECATED> */
.p-Menu-itemIcon,
.p-Menu-itemSubmenuIcon,
/* </DEPRECATED> */
.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}


/* <DEPRECATED> */ .p-Menu-itemLabel, /* </DEPRECATED> */
.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}


/* <DEPRECATED> */ .p-Menu-itemShortcut, /* </DEPRECATED> */
.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-MenuBar, /* </DEPRECATED> */
.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-MenuBar-content, /* </DEPRECATED> */
.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}


/* <DEPRECATED> */ .p--MenuBar-item, /* </DEPRECATED> */
.lm-MenuBar-item {
  box-sizing: border-box;
}


/* <DEPRECATED> */
.p-MenuBar-itemIcon,
.p-MenuBar-itemLabel,
/* </DEPRECATED> */
.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-ScrollBar, /* </DEPRECATED> */
.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */
.p-ScrollBar[data-orientation='horizontal'],
/* </DEPRECATED> */
.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}


/* <DEPRECATED> */
.p-ScrollBar[data-orientation='vertical'],
/* </DEPRECATED> */
.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}


/* <DEPRECATED> */ .p-ScrollBar-button, /* </DEPRECATED> */
.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-ScrollBar-track, /* </DEPRECATED> */
.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}


/* <DEPRECATED> */ .p-ScrollBar-thumb, /* </DEPRECATED> */
.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-SplitPanel-child, /* </DEPRECATED> */
.lm-SplitPanel-child {
  z-index: 0;
}


/* <DEPRECATED> */ .p-SplitPanel-handle, /* </DEPRECATED> */
.lm-SplitPanel-handle {
  z-index: 1;
}


/* <DEPRECATED> */ .p-SplitPanel-handle.p-mod-hidden, /* </DEPRECATED> */
.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-SplitPanel-handle:after, /* </DEPRECATED> */
.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle:after,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle:after,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-TabBar, /* </DEPRECATED> */
.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-TabBar[data-orientation='horizontal'], /* </DEPRECATED> */
.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
}


/* <DEPRECATED> */ .p-TabBar[data-orientation='vertical'], /* </DEPRECATED> */
.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
}


/* <DEPRECATED> */ .p-TabBar-content, /* </DEPRECATED> */
.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}


/* <DEPRECATED> */
.p-TabBar[data-orientation='horizontal'] > .p-TabBar-content,
/* </DEPRECATED> */
.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}


/* <DEPRECATED> */
.p-TabBar[data-orientation='vertical'] > .p-TabBar-content,
/* </DEPRECATED> */
.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}


/* <DEPRECATED> */ .p-TabBar-tab, /* </DEPRECATED> */
.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
}


/* <DEPRECATED> */
.p-TabBar-tabIcon,
.p-TabBar-tabCloseIcon,
/* </DEPRECATED> */
.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-TabBar-tabLabel, /* </DEPRECATED> */
.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}


/* <DEPRECATED> */ .p-TabBar-tab.p-mod-hidden, /* </DEPRECATED> */
.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-TabBar.p-mod-dragging .p-TabBar-tab, /* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab,
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab,
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-TabPanel-tabBar, /* </DEPRECATED> */
.lm-TabPanel-tabBar {
  z-index: 1;
}


/* <DEPRECATED> */ .p-TabPanel-stackedPanel, /* </DEPRECATED> */
.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

@charset "UTF-8";
/*!

Copyright 2015-present Palantir Technologies, Inc. All rights reserved.
Licensed under the Apache License, Version 2.0.

*/
html{
  -webkit-box-sizing:border-box;
          box-sizing:border-box; }

*,
*::before,
*::after{
  -webkit-box-sizing:inherit;
          box-sizing:inherit; }

body{
  text-transform:none;
  line-height:1.28581;
  letter-spacing:0;
  font-size:14px;
  font-weight:400;
  color:#182026;
  font-family:-apple-system, "BlinkMacSystemFont", "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Open Sans", "Helvetica Neue", "Icons16", sans-serif; }

p{
  margin-top:0;
  margin-bottom:10px; }

small{
  font-size:12px; }

strong{
  font-weight:600; }

::-moz-selection{
  background:rgba(125, 188, 255, 0.6); }

::selection{
  background:rgba(125, 188, 255, 0.6); }
.bp3-heading{
  color:#182026;
  font-weight:600;
  margin:0 0 10px;
  padding:0; }
  .bp3-dark .bp3-heading{
    color:#f5f8fa; }

h1.bp3-heading, .bp3-running-text h1{
  line-height:40px;
  font-size:36px; }

h2.bp3-heading, .bp3-running-text h2{
  line-height:32px;
  font-size:28px; }

h3.bp3-heading, .bp3-running-text h3{
  line-height:25px;
  font-size:22px; }

h4.bp3-heading, .bp3-running-text h4{
  line-height:21px;
  font-size:18px; }

h5.bp3-heading, .bp3-running-text h5{
  line-height:19px;
  font-size:16px; }

h6.bp3-heading, .bp3-running-text h6{
  line-height:16px;
  font-size:14px; }
.bp3-ui-text{
  text-transform:none;
  line-height:1.28581;
  letter-spacing:0;
  font-size:14px;
  font-weight:400; }

.bp3-monospace-text{
  text-transform:none;
  font-family:monospace; }

.bp3-text-muted{
  color:#5c7080; }
  .bp3-dark .bp3-text-muted{
    color:#a7b6c2; }

.bp3-text-disabled{
  color:rgba(92, 112, 128, 0.6); }
  .bp3-dark .bp3-text-disabled{
    color:rgba(167, 182, 194, 0.6); }

.bp3-text-overflow-ellipsis{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal; }
.bp3-running-text{
  line-height:1.5;
  font-size:14px; }
  .bp3-running-text h1{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h1{
      color:#f5f8fa; }
  .bp3-running-text h2{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h2{
      color:#f5f8fa; }
  .bp3-running-text h3{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h3{
      color:#f5f8fa; }
  .bp3-running-text h4{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h4{
      color:#f5f8fa; }
  .bp3-running-text h5{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h5{
      color:#f5f8fa; }
  .bp3-running-text h6{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h6{
      color:#f5f8fa; }
  .bp3-running-text hr{
    margin:20px 0;
    border:none;
    border-bottom:1px solid rgba(16, 22, 26, 0.15); }
    .bp3-dark .bp3-running-text hr{
      border-color:rgba(255, 255, 255, 0.15); }
  .bp3-running-text p{
    margin:0 0 10px;
    padding:0; }

.bp3-text-large{
  font-size:16px; }

.bp3-text-small{
  font-size:12px; }
a{
  text-decoration:none;
  color:#106ba3; }
  a:hover{
    cursor:pointer;
    text-decoration:underline;
    color:#106ba3; }
  a .bp3-icon, a .bp3-icon-standard, a .bp3-icon-large{
    color:inherit; }
  a code,
  .bp3-dark a code{
    color:inherit; }
  .bp3-dark a,
  .bp3-dark a:hover{
    color:#48aff0; }
    .bp3-dark a .bp3-icon, .bp3-dark a .bp3-icon-standard, .bp3-dark a .bp3-icon-large,
    .bp3-dark a:hover .bp3-icon,
    .bp3-dark a:hover .bp3-icon-standard,
    .bp3-dark a:hover .bp3-icon-large{
      color:inherit; }
.bp3-running-text code, .bp3-code{
  text-transform:none;
  font-family:monospace;
  border-radius:3px;
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2);
  background:rgba(255, 255, 255, 0.7);
  padding:2px 5px;
  color:#5c7080;
  font-size:smaller; }
  .bp3-dark .bp3-running-text code, .bp3-running-text .bp3-dark code, .bp3-dark .bp3-code{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#a7b6c2; }
  .bp3-running-text a > code, a > .bp3-code{
    color:#137cbd; }
    .bp3-dark .bp3-running-text a > code, .bp3-running-text .bp3-dark a > code, .bp3-dark a > .bp3-code{
      color:inherit; }

.bp3-running-text pre, .bp3-code-block{
  text-transform:none;
  font-family:monospace;
  display:block;
  margin:10px 0;
  border-radius:3px;
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
  background:rgba(255, 255, 255, 0.7);
  padding:13px 15px 12px;
  line-height:1.4;
  color:#182026;
  font-size:13px;
  word-break:break-all;
  word-wrap:break-word; }
  .bp3-dark .bp3-running-text pre, .bp3-running-text .bp3-dark pre, .bp3-dark .bp3-code-block{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#f5f8fa; }
  .bp3-running-text pre > code, .bp3-code-block > code{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:none;
    padding:0;
    color:inherit;
    font-size:inherit; }

.bp3-running-text kbd, .bp3-key{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  background:#ffffff;
  min-width:24px;
  height:24px;
  padding:3px 6px;
  vertical-align:middle;
  line-height:24px;
  color:#5c7080;
  font-family:inherit;
  font-size:12px; }
  .bp3-running-text kbd .bp3-icon, .bp3-key .bp3-icon, .bp3-running-text kbd .bp3-icon-standard, .bp3-key .bp3-icon-standard, .bp3-running-text kbd .bp3-icon-large, .bp3-key .bp3-icon-large{
    margin-right:5px; }
  .bp3-dark .bp3-running-text kbd, .bp3-running-text .bp3-dark kbd, .bp3-dark .bp3-key{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
    background:#394b59;
    color:#a7b6c2; }
.bp3-running-text blockquote, .bp3-blockquote{
  margin:0 0 10px;
  border-left:solid 4px rgba(167, 182, 194, 0.5);
  padding:0 20px; }
  .bp3-dark .bp3-running-text blockquote, .bp3-running-text .bp3-dark blockquote, .bp3-dark .bp3-blockquote{
    border-color:rgba(115, 134, 148, 0.5); }
.bp3-running-text ul,
.bp3-running-text ol, .bp3-list{
  margin:10px 0;
  padding-left:30px; }
  .bp3-running-text ul li:not(:last-child), .bp3-running-text ol li:not(:last-child), .bp3-list li:not(:last-child){
    margin-bottom:5px; }
  .bp3-running-text ul ol, .bp3-running-text ol ol, .bp3-list ol,
  .bp3-running-text ul ul,
  .bp3-running-text ol ul,
  .bp3-list ul{
    margin-top:5px; }

.bp3-list-unstyled{
  margin:0;
  padding:0;
  list-style:none; }
  .bp3-list-unstyled li{
    padding:0; }
.bp3-rtl{
  text-align:right; }

.bp3-dark{
  color:#f5f8fa; }

:focus{
  outline:rgba(19, 124, 189, 0.6) auto 2px;
  outline-offset:2px;
  -moz-outline-radius:6px; }

.bp3-focus-disabled :focus{
  outline:none !important; }
  .bp3-focus-disabled :focus ~ .bp3-control-indicator{
    outline:none !important; }

.bp3-alert{
  max-width:400px;
  padding:20px; }

.bp3-alert-body{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex; }
  .bp3-alert-body .bp3-icon{
    margin-top:0;
    margin-right:20px;
    font-size:40px; }

.bp3-alert-footer{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:reverse;
      -ms-flex-direction:row-reverse;
          flex-direction:row-reverse;
  margin-top:10px; }
  .bp3-alert-footer .bp3-button{
    margin-left:10px; }
.bp3-breadcrumbs{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-wrap:wrap;
      flex-wrap:wrap;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  margin:0;
  cursor:default;
  height:30px;
  padding:0;
  list-style:none; }
  .bp3-breadcrumbs > li{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center; }
    .bp3-breadcrumbs > li::after{
      display:block;
      margin:0 5px;
      background:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M10.71 7.29l-4-4a1.003 1.003 0 0 0-1.42 1.42L8.59 8 5.3 11.29c-.19.18-.3.43-.3.71a1.003 1.003 0 0 0 1.71.71l4-4c.18-.18.29-.43.29-.71 0-.28-.11-.53-.29-.71z' fill='%235C7080'/%3e%3c/svg%3e");
      width:16px;
      height:16px;
      content:""; }
    .bp3-breadcrumbs > li:last-of-type::after{
      display:none; }

.bp3-breadcrumb,
.bp3-breadcrumb-current,
.bp3-breadcrumbs-collapsed{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  font-size:16px; }

.bp3-breadcrumb,
.bp3-breadcrumbs-collapsed{
  color:#5c7080; }

.bp3-breadcrumb:hover{
  text-decoration:none; }

.bp3-breadcrumb.bp3-disabled{
  cursor:not-allowed;
  color:rgba(92, 112, 128, 0.6); }

.bp3-breadcrumb .bp3-icon{
  margin-right:5px; }

.bp3-breadcrumb-current{
  color:inherit;
  font-weight:600; }
  .bp3-breadcrumb-current .bp3-input{
    vertical-align:baseline;
    font-size:inherit;
    font-weight:inherit; }

.bp3-breadcrumbs-collapsed{
  margin-right:2px;
  border:none;
  border-radius:3px;
  background:#ced9e0;
  cursor:pointer;
  padding:1px 5px;
  vertical-align:text-bottom; }
  .bp3-breadcrumbs-collapsed::before{
    display:block;
    background:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cg fill='%235C7080'%3e%3ccircle cx='2' cy='8.03' r='2'/%3e%3ccircle cx='14' cy='8.03' r='2'/%3e%3ccircle cx='8' cy='8.03' r='2'/%3e%3c/g%3e%3c/svg%3e") center no-repeat;
    width:16px;
    height:16px;
    content:""; }
  .bp3-breadcrumbs-collapsed:hover{
    background:#bfccd6;
    text-decoration:none;
    color:#182026; }

.bp3-dark .bp3-breadcrumb,
.bp3-dark .bp3-breadcrumbs-collapsed{
  color:#a7b6c2; }

.bp3-dark .bp3-breadcrumbs > li::after{
  color:#a7b6c2; }

.bp3-dark .bp3-breadcrumb.bp3-disabled{
  color:rgba(167, 182, 194, 0.6); }

.bp3-dark .bp3-breadcrumb-current{
  color:#f5f8fa; }

.bp3-dark .bp3-breadcrumbs-collapsed{
  background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-breadcrumbs-collapsed:hover{
    background:rgba(16, 22, 26, 0.6);
    color:#f5f8fa; }
.bp3-button{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  border:none;
  border-radius:3px;
  cursor:pointer;
  padding:5px 10px;
  vertical-align:middle;
  text-align:left;
  font-size:14px;
  min-width:30px;
  min-height:30px; }
  .bp3-button > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-button > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-button::before,
  .bp3-button > *{
    margin-right:7px; }
  .bp3-button:empty::before,
  .bp3-button > :last-child{
    margin-right:0; }
  .bp3-button:empty{
    padding:0 !important; }
  .bp3-button:disabled, .bp3-button.bp3-disabled{
    cursor:not-allowed; }
  .bp3-button.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-button.bp3-align-right,
  .bp3-align-right .bp3-button{
    text-align:right; }
  .bp3-button.bp3-align-left,
  .bp3-align-left .bp3-button{
    text-align:left; }
  .bp3-button:not([class*="bp3-intent-"]){
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    color:#182026; }
    .bp3-button:not([class*="bp3-intent-"]):hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
      background-clip:padding-box;
      background-color:#ebf1f5; }
    .bp3-button:not([class*="bp3-intent-"]):active, .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#d8e1e8;
      background-image:none; }
    .bp3-button:not([class*="bp3-intent-"]):disabled, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled{
      outline:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(206, 217, 224, 0.5);
      background-image:none;
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6); }
      .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active, .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active:hover, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active:hover{
        background:rgba(206, 217, 224, 0.7); }
  .bp3-button.bp3-intent-primary{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
    .bp3-button.bp3-intent-primary:hover, .bp3-button.bp3-intent-primary:active, .bp3-button.bp3-intent-primary.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-primary:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
      background-color:#106ba3; }
    .bp3-button.bp3-intent-primary:active, .bp3-button.bp3-intent-primary.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#0e5a8a;
      background-image:none; }
    .bp3-button.bp3-intent-primary:disabled, .bp3-button.bp3-intent-primary.bp3-disabled{
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(19, 124, 189, 0.5);
      background-image:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-success{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#0f9960;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
    .bp3-button.bp3-intent-success:hover, .bp3-button.bp3-intent-success:active, .bp3-button.bp3-intent-success.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-success:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
      background-color:#0d8050; }
    .bp3-button.bp3-intent-success:active, .bp3-button.bp3-intent-success.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#0a6640;
      background-image:none; }
    .bp3-button.bp3-intent-success:disabled, .bp3-button.bp3-intent-success.bp3-disabled{
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(15, 153, 96, 0.5);
      background-image:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-warning{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#d9822b;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
    .bp3-button.bp3-intent-warning:hover, .bp3-button.bp3-intent-warning:active, .bp3-button.bp3-intent-warning.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-warning:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
      background-color:#bf7326; }
    .bp3-button.bp3-intent-warning:active, .bp3-button.bp3-intent-warning.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#a66321;
      background-image:none; }
    .bp3-button.bp3-intent-warning:disabled, .bp3-button.bp3-intent-warning.bp3-disabled{
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(217, 130, 43, 0.5);
      background-image:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-danger{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#db3737;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
    .bp3-button.bp3-intent-danger:hover, .bp3-button.bp3-intent-danger:active, .bp3-button.bp3-intent-danger.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-danger:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
      background-color:#c23030; }
    .bp3-button.bp3-intent-danger:active, .bp3-button.bp3-intent-danger.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#a82a2a;
      background-image:none; }
    .bp3-button.bp3-intent-danger:disabled, .bp3-button.bp3-intent-danger.bp3-disabled{
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(219, 55, 55, 0.5);
      background-image:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button[class*="bp3-intent-"] .bp3-button-spinner .bp3-spinner-head{
    stroke:#ffffff; }
  .bp3-button.bp3-large,
  .bp3-large .bp3-button{
    min-width:40px;
    min-height:40px;
    padding:5px 15px;
    font-size:16px; }
    .bp3-button.bp3-large::before,
    .bp3-button.bp3-large > *,
    .bp3-large .bp3-button::before,
    .bp3-large .bp3-button > *{
      margin-right:10px; }
    .bp3-button.bp3-large:empty::before,
    .bp3-button.bp3-large > :last-child,
    .bp3-large .bp3-button:empty::before,
    .bp3-large .bp3-button > :last-child{
      margin-right:0; }
  .bp3-button.bp3-small,
  .bp3-small .bp3-button{
    min-width:24px;
    min-height:24px;
    padding:0 7px; }
  .bp3-button.bp3-loading{
    position:relative; }
    .bp3-button.bp3-loading[class*="bp3-icon-"]::before{
      visibility:hidden; }
    .bp3-button.bp3-loading .bp3-button-spinner{
      position:absolute;
      margin:0; }
    .bp3-button.bp3-loading > :not(.bp3-button-spinner){
      visibility:hidden; }
  .bp3-button[class*="bp3-icon-"]::before{
    line-height:1;
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-weight:400;
    font-style:normal;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    color:#5c7080; }
  .bp3-button .bp3-icon, .bp3-button .bp3-icon-standard, .bp3-button .bp3-icon-large{
    color:#5c7080; }
    .bp3-button .bp3-icon.bp3-align-right, .bp3-button .bp3-icon-standard.bp3-align-right, .bp3-button .bp3-icon-large.bp3-align-right{
      margin-left:7px; }
  .bp3-button .bp3-icon:first-child:last-child,
  .bp3-button .bp3-spinner + .bp3-icon:last-child{
    margin:0 -7px; }
  .bp3-dark .bp3-button:not([class*="bp3-intent-"]){
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#394b59;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
    color:#f5f8fa; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):hover, .bp3-dark .bp3-button:not([class*="bp3-intent-"]):active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      color:#f5f8fa; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):hover{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#30404d; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#202b33;
      background-image:none; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):disabled, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(57, 75, 89, 0.5);
      background-image:none;
      color:rgba(167, 182, 194, 0.6); }
      .bp3-dark .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active{
        background:rgba(57, 75, 89, 0.7); }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-button-spinner .bp3-spinner-head{
      background:rgba(16, 22, 26, 0.5);
      stroke:#8a9ba8; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"])[class*="bp3-icon-"]::before{
      color:#a7b6c2; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon, .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon-standard, .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon-large{
      color:#a7b6c2; }
  .bp3-dark .bp3-button[class*="bp3-intent-"]{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:hover{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:active, .bp3-dark .bp3-button[class*="bp3-intent-"].bp3-active{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:disabled, .bp3-dark .bp3-button[class*="bp3-intent-"].bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background-image:none;
      color:rgba(255, 255, 255, 0.3); }
    .bp3-dark .bp3-button[class*="bp3-intent-"] .bp3-button-spinner .bp3-spinner-head{
      stroke:#8a9ba8; }
  .bp3-button:disabled::before,
  .bp3-button:disabled .bp3-icon, .bp3-button:disabled .bp3-icon-standard, .bp3-button:disabled .bp3-icon-large, .bp3-button.bp3-disabled::before,
  .bp3-button.bp3-disabled .bp3-icon, .bp3-button.bp3-disabled .bp3-icon-standard, .bp3-button.bp3-disabled .bp3-icon-large, .bp3-button[class*="bp3-intent-"]::before,
  .bp3-button[class*="bp3-intent-"] .bp3-icon, .bp3-button[class*="bp3-intent-"] .bp3-icon-standard, .bp3-button[class*="bp3-intent-"] .bp3-icon-large{
    color:inherit !important; }
  .bp3-button.bp3-minimal{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:none; }
    .bp3-button.bp3-minimal:hover{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(167, 182, 194, 0.3);
      text-decoration:none;
      color:#182026; }
    .bp3-button.bp3-minimal:active, .bp3-button.bp3-minimal.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(115, 134, 148, 0.3);
      color:#182026; }
    .bp3-button.bp3-minimal:disabled, .bp3-button.bp3-minimal:disabled:hover, .bp3-button.bp3-minimal.bp3-disabled, .bp3-button.bp3-minimal.bp3-disabled:hover{
      background:none;
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6); }
      .bp3-button.bp3-minimal:disabled.bp3-active, .bp3-button.bp3-minimal:disabled:hover.bp3-active, .bp3-button.bp3-minimal.bp3-disabled.bp3-active, .bp3-button.bp3-minimal.bp3-disabled:hover.bp3-active{
        background:rgba(115, 134, 148, 0.3); }
    .bp3-dark .bp3-button.bp3-minimal{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:inherit; }
      .bp3-dark .bp3-button.bp3-minimal:hover, .bp3-dark .bp3-button.bp3-minimal:active, .bp3-dark .bp3-button.bp3-minimal.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none; }
      .bp3-dark .bp3-button.bp3-minimal:hover{
        background:rgba(138, 155, 168, 0.15); }
      .bp3-dark .bp3-button.bp3-minimal:active, .bp3-dark .bp3-button.bp3-minimal.bp3-active{
        background:rgba(138, 155, 168, 0.3);
        color:#f5f8fa; }
      .bp3-dark .bp3-button.bp3-minimal:disabled, .bp3-dark .bp3-button.bp3-minimal:disabled:hover, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled:hover{
        background:none;
        cursor:not-allowed;
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-button.bp3-minimal:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal:disabled:hover.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled:hover.bp3-active{
          background:rgba(138, 155, 168, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-primary{
      color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:hover, .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.15);
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:disabled, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(16, 107, 163, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-primary:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
        stroke:#106ba3; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary{
        color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:hover{
          background:rgba(19, 124, 189, 0.2);
          color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
          background:rgba(19, 124, 189, 0.3);
          color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled{
          background:none;
          color:rgba(72, 175, 240, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled.bp3-active{
            background:rgba(19, 124, 189, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-success{
      color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:hover, .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.15);
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:disabled, .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(13, 128, 80, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-success:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
        stroke:#0d8050; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success{
        color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:hover{
          background:rgba(15, 153, 96, 0.2);
          color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
          background:rgba(15, 153, 96, 0.3);
          color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled{
          background:none;
          color:rgba(61, 204, 145, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled.bp3-active{
            background:rgba(15, 153, 96, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-warning{
      color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:hover, .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.15);
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:disabled, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(191, 115, 38, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-warning:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
        stroke:#bf7326; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning{
        color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:hover{
          background:rgba(217, 130, 43, 0.2);
          color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
          background:rgba(217, 130, 43, 0.3);
          color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled{
          background:none;
          color:rgba(255, 179, 102, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled.bp3-active{
            background:rgba(217, 130, 43, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-danger{
      color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:hover, .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.15);
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:disabled, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(194, 48, 48, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-danger:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
        stroke:#c23030; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger{
        color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:hover{
          background:rgba(219, 55, 55, 0.2);
          color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
          background:rgba(219, 55, 55, 0.3);
          color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled{
          background:none;
          color:rgba(255, 115, 115, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled.bp3-active{
            background:rgba(219, 55, 55, 0.3); }

a.bp3-button{
  text-align:center;
  text-decoration:none;
  -webkit-transition:none;
  transition:none; }
  a.bp3-button, a.bp3-button:hover, a.bp3-button:active{
    color:#182026; }
  a.bp3-button.bp3-disabled{
    color:rgba(92, 112, 128, 0.6); }

.bp3-button-text{
  -webkit-box-flex:0;
      -ms-flex:0 1 auto;
          flex:0 1 auto; }

.bp3-button.bp3-align-left .bp3-button-text, .bp3-button.bp3-align-right .bp3-button-text,
.bp3-button-group.bp3-align-left .bp3-button-text,
.bp3-button-group.bp3-align-right .bp3-button-text{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto; }
.bp3-button-group{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex; }
  .bp3-button-group .bp3-button{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    position:relative;
    z-index:4; }
    .bp3-button-group .bp3-button:focus{
      z-index:5; }
    .bp3-button-group .bp3-button:hover{
      z-index:6; }
    .bp3-button-group .bp3-button:active, .bp3-button-group .bp3-button.bp3-active{
      z-index:7; }
    .bp3-button-group .bp3-button:disabled, .bp3-button-group .bp3-button.bp3-disabled{
      z-index:3; }
    .bp3-button-group .bp3-button[class*="bp3-intent-"]{
      z-index:9; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:focus{
        z-index:10; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:hover{
        z-index:11; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:active, .bp3-button-group .bp3-button[class*="bp3-intent-"].bp3-active{
        z-index:12; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:disabled, .bp3-button-group .bp3-button[class*="bp3-intent-"].bp3-disabled{
        z-index:8; }
  .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:first-child) .bp3-button,
  .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:first-child){
    border-top-left-radius:0;
    border-bottom-left-radius:0; }
  .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:last-child){
    margin-right:-1px;
    border-top-right-radius:0;
    border-bottom-right-radius:0; }
  .bp3-button-group.bp3-minimal .bp3-button{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:none; }
    .bp3-button-group.bp3-minimal .bp3-button:hover{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(167, 182, 194, 0.3);
      text-decoration:none;
      color:#182026; }
    .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(115, 134, 148, 0.3);
      color:#182026; }
    .bp3-button-group.bp3-minimal .bp3-button:disabled, .bp3-button-group.bp3-minimal .bp3-button:disabled:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover{
      background:none;
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6); }
      .bp3-button-group.bp3-minimal .bp3-button:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button:disabled:hover.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover.bp3-active{
        background:rgba(115, 134, 148, 0.3); }
    .bp3-dark .bp3-button-group.bp3-minimal .bp3-button{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:inherit; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:hover, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:hover{
        background:rgba(138, 155, 168, 0.15); }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
        background:rgba(138, 155, 168, 0.3);
        color:#f5f8fa; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled:hover, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover{
        background:none;
        cursor:not-allowed;
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled:hover.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover.bp3-active{
          background:rgba(138, 155, 168, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary{
      color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.15);
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(16, 107, 163, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
        stroke:#106ba3; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary{
        color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover{
          background:rgba(19, 124, 189, 0.2);
          color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
          background:rgba(19, 124, 189, 0.3);
          color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled{
          background:none;
          color:rgba(72, 175, 240, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled.bp3-active{
            background:rgba(19, 124, 189, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success{
      color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.15);
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(13, 128, 80, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
        stroke:#0d8050; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success{
        color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover{
          background:rgba(15, 153, 96, 0.2);
          color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
          background:rgba(15, 153, 96, 0.3);
          color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled{
          background:none;
          color:rgba(61, 204, 145, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled.bp3-active{
            background:rgba(15, 153, 96, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning{
      color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.15);
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(191, 115, 38, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
        stroke:#bf7326; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning{
        color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover{
          background:rgba(217, 130, 43, 0.2);
          color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
          background:rgba(217, 130, 43, 0.3);
          color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled{
          background:none;
          color:rgba(255, 179, 102, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled.bp3-active{
            background:rgba(217, 130, 43, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger{
      color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.15);
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(194, 48, 48, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
        stroke:#c23030; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger{
        color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover{
          background:rgba(219, 55, 55, 0.2);
          color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
          background:rgba(219, 55, 55, 0.3);
          color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled{
          background:none;
          color:rgba(255, 115, 115, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled.bp3-active{
            background:rgba(219, 55, 55, 0.3); }
  .bp3-button-group .bp3-popover-wrapper,
  .bp3-button-group .bp3-popover-target{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-button-group.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-button-group .bp3-button.bp3-fill,
  .bp3-button-group.bp3-fill .bp3-button:not(.bp3-fixed){
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-button-group.bp3-vertical{
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column;
    -webkit-box-align:stretch;
        -ms-flex-align:stretch;
            align-items:stretch;
    vertical-align:top; }
    .bp3-button-group.bp3-vertical.bp3-fill{
      width:unset;
      height:100%; }
    .bp3-button-group.bp3-vertical .bp3-button{
      margin-right:0 !important;
      width:100%; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:first-child .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:first-child{
      border-radius:3px 3px 0 0; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:last-child .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:last-child{
      border-radius:0 0 3px 3px; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:not(:last-child){
      margin-bottom:-1px; }
  .bp3-button-group.bp3-align-left .bp3-button{
    text-align:left; }
  .bp3-dark .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-dark .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:last-child){
    margin-right:1px; }
  .bp3-dark .bp3-button-group.bp3-vertical > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-dark .bp3-button-group.bp3-vertical > .bp3-button:not(:last-child){
    margin-bottom:1px; }
.bp3-callout{
  line-height:1.5;
  font-size:14px;
  position:relative;
  border-radius:3px;
  background-color:rgba(138, 155, 168, 0.15);
  width:100%;
  padding:10px 12px 9px; }
  .bp3-callout[class*="bp3-icon-"]{
    padding-left:40px; }
    .bp3-callout[class*="bp3-icon-"]::before{
      line-height:1;
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-weight:400;
      font-style:normal;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased;
      position:absolute;
      top:10px;
      left:10px;
      color:#5c7080; }
  .bp3-callout.bp3-callout-icon{
    padding-left:40px; }
    .bp3-callout.bp3-callout-icon > .bp3-icon:first-child{
      position:absolute;
      top:10px;
      left:10px;
      color:#5c7080; }
  .bp3-callout .bp3-heading{
    margin-top:0;
    margin-bottom:5px;
    line-height:20px; }
    .bp3-callout .bp3-heading:last-child{
      margin-bottom:0; }
  .bp3-dark .bp3-callout{
    background-color:rgba(138, 155, 168, 0.2); }
    .bp3-dark .bp3-callout[class*="bp3-icon-"]::before{
      color:#a7b6c2; }
  .bp3-callout.bp3-intent-primary{
    background-color:rgba(19, 124, 189, 0.15); }
    .bp3-callout.bp3-intent-primary[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-primary > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-primary .bp3-heading{
      color:#106ba3; }
    .bp3-dark .bp3-callout.bp3-intent-primary{
      background-color:rgba(19, 124, 189, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-primary[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-primary > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-primary .bp3-heading{
        color:#48aff0; }
  .bp3-callout.bp3-intent-success{
    background-color:rgba(15, 153, 96, 0.15); }
    .bp3-callout.bp3-intent-success[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-success > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-success .bp3-heading{
      color:#0d8050; }
    .bp3-dark .bp3-callout.bp3-intent-success{
      background-color:rgba(15, 153, 96, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-success[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-success > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-success .bp3-heading{
        color:#3dcc91; }
  .bp3-callout.bp3-intent-warning{
    background-color:rgba(217, 130, 43, 0.15); }
    .bp3-callout.bp3-intent-warning[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-warning > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-warning .bp3-heading{
      color:#bf7326; }
    .bp3-dark .bp3-callout.bp3-intent-warning{
      background-color:rgba(217, 130, 43, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-warning[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-warning > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-warning .bp3-heading{
        color:#ffb366; }
  .bp3-callout.bp3-intent-danger{
    background-color:rgba(219, 55, 55, 0.15); }
    .bp3-callout.bp3-intent-danger[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-danger > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-danger .bp3-heading{
      color:#c23030; }
    .bp3-dark .bp3-callout.bp3-intent-danger{
      background-color:rgba(219, 55, 55, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-danger[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-danger > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-danger .bp3-heading{
        color:#ff7373; }
  .bp3-running-text .bp3-callout{
    margin:20px 0; }
.bp3-card{
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
  background-color:#ffffff;
  padding:20px;
  -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-card.bp3-dark,
  .bp3-dark .bp3-card{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
    background-color:#30404d; }

.bp3-elevation-0{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0); }
  .bp3-elevation-0.bp3-dark,
  .bp3-dark .bp3-elevation-0{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0); }

.bp3-elevation-1{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-1.bp3-dark,
  .bp3-dark .bp3-elevation-1{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-elevation-2{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 1px 1px rgba(16, 22, 26, 0.2), 0 2px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 1px 1px rgba(16, 22, 26, 0.2), 0 2px 6px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-2.bp3-dark,
  .bp3-dark .bp3-elevation-2{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.4), 0 2px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.4), 0 2px 6px rgba(16, 22, 26, 0.4); }

.bp3-elevation-3{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-3.bp3-dark,
  .bp3-dark .bp3-elevation-3{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }

.bp3-elevation-4{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-4.bp3-dark,
  .bp3-dark .bp3-elevation-4{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4); }

.bp3-card.bp3-interactive:hover{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  cursor:pointer; }
  .bp3-card.bp3-interactive:hover.bp3-dark,
  .bp3-dark .bp3-card.bp3-interactive:hover{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }

.bp3-card.bp3-interactive:active{
  opacity:0.9;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  -webkit-transition-duration:0;
          transition-duration:0; }
  .bp3-card.bp3-interactive:active.bp3-dark,
  .bp3-dark .bp3-card.bp3-interactive:active{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-collapse{
  height:0;
  overflow-y:hidden;
  -webkit-transition:height 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:height 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-collapse .bp3-collapse-body{
    -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-collapse .bp3-collapse-body[aria-hidden="true"]{
      display:none; }

.bp3-context-menu .bp3-popover-target{
  display:block; }

.bp3-context-menu-popover-target{
  position:fixed; }

.bp3-divider{
  margin:5px;
  border-right:1px solid rgba(16, 22, 26, 0.15);
  border-bottom:1px solid rgba(16, 22, 26, 0.15); }
  .bp3-dark .bp3-divider{
    border-color:rgba(16, 22, 26, 0.4); }
.bp3-dialog-container{
  opacity:1;
  -webkit-transform:scale(1);
          transform:scale(1);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  width:100%;
  min-height:100%;
  pointer-events:none;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-dialog-container.bp3-overlay-enter > .bp3-dialog, .bp3-dialog-container.bp3-overlay-appear > .bp3-dialog{
    opacity:0;
    -webkit-transform:scale(0.5);
            transform:scale(0.5); }
  .bp3-dialog-container.bp3-overlay-enter-active > .bp3-dialog, .bp3-dialog-container.bp3-overlay-appear-active > .bp3-dialog{
    opacity:1;
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-property:opacity, -webkit-transform;
    transition-property:opacity, -webkit-transform;
    transition-property:opacity, transform;
    transition-property:opacity, transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-dialog-container.bp3-overlay-exit > .bp3-dialog{
    opacity:1;
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-dialog-container.bp3-overlay-exit-active > .bp3-dialog{
    opacity:0;
    -webkit-transform:scale(0.5);
            transform:scale(0.5);
    -webkit-transition-property:opacity, -webkit-transform;
    transition-property:opacity, -webkit-transform;
    transition-property:opacity, transform;
    transition-property:opacity, transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }

.bp3-dialog{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:30px 0;
  border-radius:6px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  background:#ebf1f5;
  width:500px;
  padding-bottom:20px;
  pointer-events:all;
  -webkit-user-select:text;
     -moz-user-select:text;
      -ms-user-select:text;
          user-select:text; }
  .bp3-dialog:focus{
    outline:0; }
  .bp3-dialog.bp3-dark,
  .bp3-dark .bp3-dialog{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
    background:#293742;
    color:#f5f8fa; }

.bp3-dialog-header{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  border-radius:6px 6px 0 0;
  -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
  background:#ffffff;
  min-height:40px;
  padding-right:5px;
  padding-left:20px; }
  .bp3-dialog-header .bp3-icon-large,
  .bp3-dialog-header .bp3-icon{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    margin-right:10px;
    color:#5c7080; }
  .bp3-dialog-header .bp3-heading{
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    margin:0;
    line-height:inherit; }
    .bp3-dialog-header .bp3-heading:last-child{
      margin-right:20px; }
  .bp3-dark .bp3-dialog-header{
    -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:0 1px 0 rgba(16, 22, 26, 0.4);
    background:#30404d; }
    .bp3-dark .bp3-dialog-header .bp3-icon-large,
    .bp3-dark .bp3-dialog-header .bp3-icon{
      color:#a7b6c2; }

.bp3-dialog-body{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  margin:20px;
  line-height:18px; }

.bp3-dialog-footer{
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  margin:0 20px; }

.bp3-dialog-footer-actions{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-pack:end;
      -ms-flex-pack:end;
          justify-content:flex-end; }
  .bp3-dialog-footer-actions .bp3-button{
    margin-left:10px; }
.bp3-drawer{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:0;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  background:#ffffff;
  padding:0; }
  .bp3-drawer:focus{
    outline:0; }
  .bp3-drawer.bp3-position-top{
    top:0;
    right:0;
    left:0;
    height:50%; }
    .bp3-drawer.bp3-position-top.bp3-overlay-enter, .bp3-drawer.bp3-position-top.bp3-overlay-appear{
      -webkit-transform:translateY(-100%);
              transform:translateY(-100%); }
    .bp3-drawer.bp3-position-top.bp3-overlay-enter-active, .bp3-drawer.bp3-position-top.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer.bp3-position-top.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer.bp3-position-top.bp3-overlay-exit-active{
      -webkit-transform:translateY(-100%);
              transform:translateY(-100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer.bp3-position-bottom{
    right:0;
    bottom:0;
    left:0;
    height:50%; }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-enter, .bp3-drawer.bp3-position-bottom.bp3-overlay-appear{
      -webkit-transform:translateY(100%);
              transform:translateY(100%); }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-enter-active, .bp3-drawer.bp3-position-bottom.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-exit-active{
      -webkit-transform:translateY(100%);
              transform:translateY(100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer.bp3-position-left{
    top:0;
    bottom:0;
    left:0;
    width:50%; }
    .bp3-drawer.bp3-position-left.bp3-overlay-enter, .bp3-drawer.bp3-position-left.bp3-overlay-appear{
      -webkit-transform:translateX(-100%);
              transform:translateX(-100%); }
    .bp3-drawer.bp3-position-left.bp3-overlay-enter-active, .bp3-drawer.bp3-position-left.bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer.bp3-position-left.bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer.bp3-position-left.bp3-overlay-exit-active{
      -webkit-transform:translateX(-100%);
              transform:translateX(-100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer.bp3-position-right{
    top:0;
    right:0;
    bottom:0;
    width:50%; }
    .bp3-drawer.bp3-position-right.bp3-overlay-enter, .bp3-drawer.bp3-position-right.bp3-overlay-appear{
      -webkit-transform:translateX(100%);
              transform:translateX(100%); }
    .bp3-drawer.bp3-position-right.bp3-overlay-enter-active, .bp3-drawer.bp3-position-right.bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer.bp3-position-right.bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer.bp3-position-right.bp3-overlay-exit-active{
      -webkit-transform:translateX(100%);
              transform:translateX(100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
  .bp3-position-right):not(.bp3-vertical){
    top:0;
    right:0;
    bottom:0;
    width:50%; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-enter, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-appear{
      -webkit-transform:translateX(100%);
              transform:translateX(100%); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-enter-active, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-exit-active{
      -webkit-transform:translateX(100%);
              transform:translateX(100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
  .bp3-position-right).bp3-vertical{
    right:0;
    bottom:0;
    left:0;
    height:50%; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-enter, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-appear{
      -webkit-transform:translateY(100%);
              transform:translateY(100%); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-enter-active, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-exit-active{
      -webkit-transform:translateY(100%);
              transform:translateY(100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer.bp3-dark,
  .bp3-dark .bp3-drawer{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
    background:#30404d;
    color:#f5f8fa; }

.bp3-drawer-header{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  position:relative;
  border-radius:0;
  -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
  min-height:40px;
  padding:5px;
  padding-left:20px; }
  .bp3-drawer-header .bp3-icon-large,
  .bp3-drawer-header .bp3-icon{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    margin-right:10px;
    color:#5c7080; }
  .bp3-drawer-header .bp3-heading{
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    margin:0;
    line-height:inherit; }
    .bp3-drawer-header .bp3-heading:last-child{
      margin-right:20px; }
  .bp3-dark .bp3-drawer-header{
    -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:0 1px 0 rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-drawer-header .bp3-icon-large,
    .bp3-dark .bp3-drawer-header .bp3-icon{
      color:#a7b6c2; }

.bp3-drawer-body{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  overflow:auto;
  line-height:18px; }

.bp3-drawer-footer{
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  position:relative;
  -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
  padding:10px 20px; }
  .bp3-dark .bp3-drawer-footer{
    -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.4); }
.bp3-editable-text{
  display:inline-block;
  position:relative;
  cursor:text;
  max-width:100%;
  vertical-align:top;
  white-space:nowrap; }
  .bp3-editable-text::before{
    position:absolute;
    top:-3px;
    right:-3px;
    bottom:-3px;
    left:-3px;
    border-radius:3px;
    content:"";
    -webkit-transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-editable-text:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-editable-text.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
    background-color:#ffffff; }
  .bp3-editable-text.bp3-disabled::before{
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-editable-text.bp3-intent-primary .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-primary .bp3-editable-text-content{
    color:#137cbd; }
  .bp3-editable-text.bp3-intent-primary:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(19, 124, 189, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(19, 124, 189, 0.4); }
  .bp3-editable-text.bp3-intent-primary.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-success .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-success .bp3-editable-text-content{
    color:#0f9960; }
  .bp3-editable-text.bp3-intent-success:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px rgba(15, 153, 96, 0.4);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px rgba(15, 153, 96, 0.4); }
  .bp3-editable-text.bp3-intent-success.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-warning .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-warning .bp3-editable-text-content{
    color:#d9822b; }
  .bp3-editable-text.bp3-intent-warning:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px rgba(217, 130, 43, 0.4);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px rgba(217, 130, 43, 0.4); }
  .bp3-editable-text.bp3-intent-warning.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-danger .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-danger .bp3-editable-text-content{
    color:#db3737; }
  .bp3-editable-text.bp3-intent-danger:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px rgba(219, 55, 55, 0.4);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px rgba(219, 55, 55, 0.4); }
  .bp3-editable-text.bp3-intent-danger.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-editable-text:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(255, 255, 255, 0.15);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(255, 255, 255, 0.15); }
  .bp3-dark .bp3-editable-text.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background-color:rgba(16, 22, 26, 0.3); }
  .bp3-dark .bp3-editable-text.bp3-disabled::before{
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-dark .bp3-editable-text.bp3-intent-primary .bp3-editable-text-content{
    color:#48aff0; }
  .bp3-dark .bp3-editable-text.bp3-intent-primary:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(72, 175, 240, 0), 0 0 0 0 rgba(72, 175, 240, 0), inset 0 0 0 1px rgba(72, 175, 240, 0.4);
            box-shadow:0 0 0 0 rgba(72, 175, 240, 0), 0 0 0 0 rgba(72, 175, 240, 0), inset 0 0 0 1px rgba(72, 175, 240, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-primary.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #48aff0, 0 0 0 3px rgba(72, 175, 240, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #48aff0, 0 0 0 3px rgba(72, 175, 240, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-success .bp3-editable-text-content{
    color:#3dcc91; }
  .bp3-dark .bp3-editable-text.bp3-intent-success:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(61, 204, 145, 0), 0 0 0 0 rgba(61, 204, 145, 0), inset 0 0 0 1px rgba(61, 204, 145, 0.4);
            box-shadow:0 0 0 0 rgba(61, 204, 145, 0), 0 0 0 0 rgba(61, 204, 145, 0), inset 0 0 0 1px rgba(61, 204, 145, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-success.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #3dcc91, 0 0 0 3px rgba(61, 204, 145, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #3dcc91, 0 0 0 3px rgba(61, 204, 145, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-warning .bp3-editable-text-content{
    color:#ffb366; }
  .bp3-dark .bp3-editable-text.bp3-intent-warning:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(255, 179, 102, 0), 0 0 0 0 rgba(255, 179, 102, 0), inset 0 0 0 1px rgba(255, 179, 102, 0.4);
            box-shadow:0 0 0 0 rgba(255, 179, 102, 0), 0 0 0 0 rgba(255, 179, 102, 0), inset 0 0 0 1px rgba(255, 179, 102, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-warning.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #ffb366, 0 0 0 3px rgba(255, 179, 102, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #ffb366, 0 0 0 3px rgba(255, 179, 102, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-danger .bp3-editable-text-content{
    color:#ff7373; }
  .bp3-dark .bp3-editable-text.bp3-intent-danger:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(255, 115, 115, 0), 0 0 0 0 rgba(255, 115, 115, 0), inset 0 0 0 1px rgba(255, 115, 115, 0.4);
            box-shadow:0 0 0 0 rgba(255, 115, 115, 0), 0 0 0 0 rgba(255, 115, 115, 0), inset 0 0 0 1px rgba(255, 115, 115, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-danger.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #ff7373, 0 0 0 3px rgba(255, 115, 115, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #ff7373, 0 0 0 3px rgba(255, 115, 115, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-editable-text-input,
.bp3-editable-text-content{
  display:inherit;
  position:relative;
  min-width:inherit;
  max-width:inherit;
  vertical-align:top;
  text-transform:inherit;
  letter-spacing:inherit;
  color:inherit;
  font:inherit;
  resize:none; }

.bp3-editable-text-input{
  border:none;
  -webkit-box-shadow:none;
          box-shadow:none;
  background:none;
  width:100%;
  padding:0;
  white-space:pre-wrap; }
  .bp3-editable-text-input::-webkit-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input::-moz-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input:-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input::-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input::placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input:focus{
    outline:none; }
  .bp3-editable-text-input::-ms-clear{
    display:none; }

.bp3-editable-text-content{
  overflow:hidden;
  padding-right:2px;
  text-overflow:ellipsis;
  white-space:pre; }
  .bp3-editable-text-editing > .bp3-editable-text-content{
    position:absolute;
    left:0;
    visibility:hidden; }
  .bp3-editable-text-placeholder > .bp3-editable-text-content{
    color:rgba(92, 112, 128, 0.6); }
    .bp3-dark .bp3-editable-text-placeholder > .bp3-editable-text-content{
      color:rgba(167, 182, 194, 0.6); }

.bp3-editable-text.bp3-multiline{
  display:block; }
  .bp3-editable-text.bp3-multiline .bp3-editable-text-content{
    overflow:auto;
    white-space:pre-wrap;
    word-wrap:break-word; }
.bp3-control-group{
  -webkit-transform:translateZ(0);
          transform:translateZ(0);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:stretch;
      -ms-flex-align:stretch;
          align-items:stretch; }
  .bp3-control-group > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-control-group > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-control-group .bp3-button,
  .bp3-control-group .bp3-html-select,
  .bp3-control-group .bp3-input,
  .bp3-control-group .bp3-select{
    position:relative; }
  .bp3-control-group .bp3-input{
    z-index:2;
    border-radius:inherit; }
    .bp3-control-group .bp3-input:focus{
      z-index:14;
      border-radius:3px; }
    .bp3-control-group .bp3-input[class*="bp3-intent"]{
      z-index:13; }
      .bp3-control-group .bp3-input[class*="bp3-intent"]:focus{
        z-index:15; }
    .bp3-control-group .bp3-input[readonly], .bp3-control-group .bp3-input:disabled, .bp3-control-group .bp3-input.bp3-disabled{
      z-index:1; }
  .bp3-control-group .bp3-input-group[class*="bp3-intent"] .bp3-input{
    z-index:13; }
    .bp3-control-group .bp3-input-group[class*="bp3-intent"] .bp3-input:focus{
      z-index:15; }
  .bp3-control-group .bp3-button,
  .bp3-control-group .bp3-html-select select,
  .bp3-control-group .bp3-select select{
    -webkit-transform:translateZ(0);
            transform:translateZ(0);
    z-index:4;
    border-radius:inherit; }
    .bp3-control-group .bp3-button:focus,
    .bp3-control-group .bp3-html-select select:focus,
    .bp3-control-group .bp3-select select:focus{
      z-index:5; }
    .bp3-control-group .bp3-button:hover,
    .bp3-control-group .bp3-html-select select:hover,
    .bp3-control-group .bp3-select select:hover{
      z-index:6; }
    .bp3-control-group .bp3-button:active,
    .bp3-control-group .bp3-html-select select:active,
    .bp3-control-group .bp3-select select:active{
      z-index:7; }
    .bp3-control-group .bp3-button[readonly], .bp3-control-group .bp3-button:disabled, .bp3-control-group .bp3-button.bp3-disabled,
    .bp3-control-group .bp3-html-select select[readonly],
    .bp3-control-group .bp3-html-select select:disabled,
    .bp3-control-group .bp3-html-select select.bp3-disabled,
    .bp3-control-group .bp3-select select[readonly],
    .bp3-control-group .bp3-select select:disabled,
    .bp3-control-group .bp3-select select.bp3-disabled{
      z-index:3; }
    .bp3-control-group .bp3-button[class*="bp3-intent"],
    .bp3-control-group .bp3-html-select select[class*="bp3-intent"],
    .bp3-control-group .bp3-select select[class*="bp3-intent"]{
      z-index:9; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:focus,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:focus,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:focus{
        z-index:10; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:hover,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:hover,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:hover{
        z-index:11; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:active,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:active,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:active{
        z-index:12; }
      .bp3-control-group .bp3-button[class*="bp3-intent"][readonly], .bp3-control-group .bp3-button[class*="bp3-intent"]:disabled, .bp3-control-group .bp3-button[class*="bp3-intent"].bp3-disabled,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"][readonly],
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:disabled,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"].bp3-disabled,
      .bp3-control-group .bp3-select select[class*="bp3-intent"][readonly],
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:disabled,
      .bp3-control-group .bp3-select select[class*="bp3-intent"].bp3-disabled{
        z-index:8; }
  .bp3-control-group .bp3-input-group > .bp3-icon,
  .bp3-control-group .bp3-input-group > .bp3-button,
  .bp3-control-group .bp3-input-group > .bp3-input-action{
    z-index:16; }
  .bp3-control-group .bp3-select::after,
  .bp3-control-group .bp3-html-select::after,
  .bp3-control-group .bp3-select > .bp3-icon,
  .bp3-control-group .bp3-html-select > .bp3-icon{
    z-index:17; }
  .bp3-control-group:not(.bp3-vertical) > *{
    margin-right:-1px; }
  .bp3-dark .bp3-control-group:not(.bp3-vertical) > *{
    margin-right:0; }
  .bp3-dark .bp3-control-group:not(.bp3-vertical) > .bp3-button + .bp3-button{
    margin-left:1px; }
  .bp3-control-group .bp3-popover-wrapper,
  .bp3-control-group .bp3-popover-target{
    border-radius:inherit; }
  .bp3-control-group > :first-child{
    border-radius:3px 0 0 3px; }
  .bp3-control-group > :last-child{
    margin-right:0;
    border-radius:0 3px 3px 0; }
  .bp3-control-group > :only-child{
    margin-right:0;
    border-radius:3px; }
  .bp3-control-group .bp3-input-group .bp3-button{
    border-radius:3px; }
  .bp3-control-group > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-control-group.bp3-fill > *:not(.bp3-fixed){
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-control-group.bp3-vertical{
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column; }
    .bp3-control-group.bp3-vertical > *{
      margin-top:-1px; }
    .bp3-control-group.bp3-vertical > :first-child{
      margin-top:0;
      border-radius:3px 3px 0 0; }
    .bp3-control-group.bp3-vertical > :last-child{
      border-radius:0 0 3px 3px; }
.bp3-control{
  display:block;
  position:relative;
  margin-bottom:10px;
  cursor:pointer;
  text-transform:none; }
  .bp3-control input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
  .bp3-control:hover input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#106ba3; }
  .bp3-control input:not(:disabled):active:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background:#0e5a8a; }
  .bp3-control input:disabled:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(19, 124, 189, 0.5); }
  .bp3-dark .bp3-control input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control:hover input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#106ba3; }
  .bp3-dark .bp3-control input:not(:disabled):active:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#0e5a8a; }
  .bp3-dark .bp3-control input:disabled:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(14, 90, 138, 0.5); }
  .bp3-control:not(.bp3-align-right){
    padding-left:26px; }
    .bp3-control:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-26px; }
  .bp3-control.bp3-align-right{
    padding-right:26px; }
    .bp3-control.bp3-align-right .bp3-control-indicator{
      margin-right:-26px; }
  .bp3-control.bp3-disabled{
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-control.bp3-inline{
    display:inline-block;
    margin-right:20px; }
  .bp3-control input{
    position:absolute;
    top:0;
    left:0;
    opacity:0;
    z-index:-1; }
  .bp3-control .bp3-control-indicator{
    display:inline-block;
    position:relative;
    margin-top:-3px;
    margin-right:10px;
    border:none;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    cursor:pointer;
    width:1em;
    height:1em;
    vertical-align:middle;
    font-size:16px;
    -webkit-user-select:none;
       -moz-user-select:none;
        -ms-user-select:none;
            user-select:none; }
    .bp3-control .bp3-control-indicator::before{
      display:block;
      width:1em;
      height:1em;
      content:""; }
  .bp3-control:hover .bp3-control-indicator{
    background-color:#ebf1f5; }
  .bp3-control input:not(:disabled):active ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background:#d8e1e8; }
  .bp3-control input:disabled ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(206, 217, 224, 0.5);
    cursor:not-allowed; }
  .bp3-control input:focus ~ .bp3-control-indicator{
    outline:rgba(19, 124, 189, 0.6) auto 2px;
    outline-offset:2px;
    -moz-outline-radius:6px; }
  .bp3-control.bp3-align-right .bp3-control-indicator{
    float:right;
    margin-top:1px;
    margin-left:10px; }
  .bp3-control.bp3-large{
    font-size:16px; }
    .bp3-control.bp3-large:not(.bp3-align-right){
      padding-left:30px; }
      .bp3-control.bp3-large:not(.bp3-align-right) .bp3-control-indicator{
        margin-left:-30px; }
    .bp3-control.bp3-large.bp3-align-right{
      padding-right:30px; }
      .bp3-control.bp3-large.bp3-align-right .bp3-control-indicator{
        margin-right:-30px; }
    .bp3-control.bp3-large .bp3-control-indicator{
      font-size:20px; }
    .bp3-control.bp3-large.bp3-align-right .bp3-control-indicator{
      margin-top:0; }
  .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
  .bp3-control.bp3-checkbox:hover input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#106ba3; }
  .bp3-control.bp3-checkbox input:not(:disabled):active:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background:#0e5a8a; }
  .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(19, 124, 189, 0.5); }
  .bp3-dark .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-checkbox:hover input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#106ba3; }
  .bp3-dark .bp3-control.bp3-checkbox input:not(:disabled):active:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#0e5a8a; }
  .bp3-dark .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(14, 90, 138, 0.5); }
  .bp3-control.bp3-checkbox .bp3-control-indicator{
    border-radius:3px; }
  .bp3-control.bp3-checkbox input:checked ~ .bp3-control-indicator::before{
    background-image:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M12 5c-.28 0-.53.11-.71.29L7 9.59l-2.29-2.3a1.003 1.003 0 0 0-1.42 1.42l3 3c.18.18.43.29.71.29s.53-.11.71-.29l5-5A1.003 1.003 0 0 0 12 5z' fill='white'/%3e%3c/svg%3e"); }
  .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator::before{
    background-image:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M11 7H5c-.55 0-1 .45-1 1s.45 1 1 1h6c.55 0 1-.45 1-1s-.45-1-1-1z' fill='white'/%3e%3c/svg%3e"); }
  .bp3-control.bp3-radio .bp3-control-indicator{
    border-radius:50%; }
  .bp3-control.bp3-radio input:checked ~ .bp3-control-indicator::before{
    background-image:radial-gradient(#ffffff, #ffffff 28%, transparent 32%); }
  .bp3-control.bp3-radio input:checked:disabled ~ .bp3-control-indicator::before{
    opacity:0.5; }
  .bp3-control.bp3-radio input:focus ~ .bp3-control-indicator{
    -moz-outline-radius:16px; }
  .bp3-control.bp3-switch input ~ .bp3-control-indicator{
    background:rgba(167, 182, 194, 0.5); }
  .bp3-control.bp3-switch:hover input ~ .bp3-control-indicator{
    background:rgba(115, 134, 148, 0.5); }
  .bp3-control.bp3-switch input:not(:disabled):active ~ .bp3-control-indicator{
    background:rgba(92, 112, 128, 0.5); }
  .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator{
    background:rgba(206, 217, 224, 0.5); }
    .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator::before{
      background:rgba(255, 255, 255, 0.8); }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator{
    background:#137cbd; }
  .bp3-control.bp3-switch:hover input:checked ~ .bp3-control-indicator{
    background:#106ba3; }
  .bp3-control.bp3-switch input:checked:not(:disabled):active ~ .bp3-control-indicator{
    background:#0e5a8a; }
  .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator{
    background:rgba(19, 124, 189, 0.5); }
    .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator::before{
      background:rgba(255, 255, 255, 0.8); }
  .bp3-control.bp3-switch:not(.bp3-align-right){
    padding-left:38px; }
    .bp3-control.bp3-switch:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-38px; }
  .bp3-control.bp3-switch.bp3-align-right{
    padding-right:38px; }
    .bp3-control.bp3-switch.bp3-align-right .bp3-control-indicator{
      margin-right:-38px; }
  .bp3-control.bp3-switch .bp3-control-indicator{
    border:none;
    border-radius:1.75em;
    -webkit-box-shadow:none !important;
            box-shadow:none !important;
    width:auto;
    min-width:1.75em;
    -webkit-transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-control.bp3-switch .bp3-control-indicator::before{
      position:absolute;
      left:0;
      margin:2px;
      border-radius:50%;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
      background:#ffffff;
      width:calc(1em - 4px);
      height:calc(1em - 4px);
      -webkit-transition:left 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
      transition:left 100ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator::before{
    left:calc(100% - 1em); }
  .bp3-control.bp3-switch.bp3-large:not(.bp3-align-right){
    padding-left:45px; }
    .bp3-control.bp3-switch.bp3-large:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-45px; }
  .bp3-control.bp3-switch.bp3-large.bp3-align-right{
    padding-right:45px; }
    .bp3-control.bp3-switch.bp3-large.bp3-align-right .bp3-control-indicator{
      margin-right:-45px; }
  .bp3-dark .bp3-control.bp3-switch input ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.5); }
  .bp3-dark .bp3-control.bp3-switch:hover input ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.7); }
  .bp3-dark .bp3-control.bp3-switch input:not(:disabled):active ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.9); }
  .bp3-dark .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator{
    background:rgba(57, 75, 89, 0.5); }
    .bp3-dark .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator::before{
      background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator{
    background:#137cbd; }
  .bp3-dark .bp3-control.bp3-switch:hover input:checked ~ .bp3-control-indicator{
    background:#106ba3; }
  .bp3-dark .bp3-control.bp3-switch input:checked:not(:disabled):active ~ .bp3-control-indicator{
    background:#0e5a8a; }
  .bp3-dark .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator{
    background:rgba(14, 90, 138, 0.5); }
    .bp3-dark .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator::before{
      background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-switch .bp3-control-indicator::before{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background:#394b59; }
  .bp3-dark .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator::before{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-control.bp3-switch .bp3-switch-inner-text{
    text-align:center;
    font-size:0.7em; }
  .bp3-control.bp3-switch .bp3-control-indicator-child:first-child{
    visibility:hidden;
    margin-right:1.2em;
    margin-left:0.5em;
    line-height:0; }
  .bp3-control.bp3-switch .bp3-control-indicator-child:last-child{
    visibility:visible;
    margin-right:0.5em;
    margin-left:1.2em;
    line-height:1em; }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator .bp3-control-indicator-child:first-child{
    visibility:visible;
    line-height:1em; }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator .bp3-control-indicator-child:last-child{
    visibility:hidden;
    line-height:0; }
  .bp3-dark .bp3-control{
    color:#f5f8fa; }
    .bp3-dark .bp3-control.bp3-disabled{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-control .bp3-control-indicator{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#394b59;
      background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
      background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0)); }
    .bp3-dark .bp3-control:hover .bp3-control-indicator{
      background-color:#30404d; }
    .bp3-dark .bp3-control input:not(:disabled):active ~ .bp3-control-indicator{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background:#202b33; }
    .bp3-dark .bp3-control input:disabled ~ .bp3-control-indicator{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(57, 75, 89, 0.5);
      cursor:not-allowed; }
    .bp3-dark .bp3-control.bp3-checkbox input:disabled:checked ~ .bp3-control-indicator, .bp3-dark .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
      color:rgba(167, 182, 194, 0.6); }
.bp3-file-input{
  display:inline-block;
  position:relative;
  cursor:pointer;
  height:30px; }
  .bp3-file-input input{
    opacity:0;
    margin:0;
    min-width:200px; }
    .bp3-file-input input:disabled + .bp3-file-upload-input,
    .bp3-file-input input.bp3-disabled + .bp3-file-upload-input{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(206, 217, 224, 0.5);
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6);
      resize:none; }
      .bp3-file-input input:disabled + .bp3-file-upload-input::after,
      .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after{
        outline:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        background-color:rgba(206, 217, 224, 0.5);
        background-image:none;
        cursor:not-allowed;
        color:rgba(92, 112, 128, 0.6); }
        .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active, .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active:hover,
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active,
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active:hover{
          background:rgba(206, 217, 224, 0.7); }
      .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input, .bp3-dark
      .bp3-file-input input.bp3-disabled + .bp3-file-upload-input{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:rgba(57, 75, 89, 0.5);
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input::after, .bp3-dark
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after{
          -webkit-box-shadow:none;
                  box-shadow:none;
          background-color:rgba(57, 75, 89, 0.5);
          background-image:none;
          color:rgba(167, 182, 194, 0.6); }
          .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active, .bp3-dark
          .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active{
            background:rgba(57, 75, 89, 0.7); }
  .bp3-file-input.bp3-file-input-has-selection .bp3-file-upload-input{
    color:#182026; }
  .bp3-dark .bp3-file-input.bp3-file-input-has-selection .bp3-file-upload-input{
    color:#f5f8fa; }
  .bp3-file-input.bp3-fill{
    width:100%; }
  .bp3-file-input.bp3-large,
  .bp3-large .bp3-file-input{
    height:40px; }
  .bp3-file-input .bp3-file-upload-input-custom-text::after{
    content:attr(bp3-button-text); }

.bp3-file-upload-input{
  outline:none;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
  background:#ffffff;
  height:30px;
  padding:0 10px;
  vertical-align:middle;
  line-height:30px;
  color:#182026;
  font-size:14px;
  font-weight:400;
  -webkit-transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  -webkit-appearance:none;
     -moz-appearance:none;
          appearance:none;
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  position:absolute;
  top:0;
  right:0;
  left:0;
  padding-right:80px;
  color:rgba(92, 112, 128, 0.6);
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-file-upload-input::-webkit-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input::-moz-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input:-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input::-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input::placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input:focus, .bp3-file-upload-input.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-file-upload-input[type="search"], .bp3-file-upload-input.bp3-round{
    border-radius:30px;
    -webkit-box-sizing:border-box;
            box-sizing:border-box;
    padding-left:10px; }
  .bp3-file-upload-input[readonly]{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-file-upload-input:disabled, .bp3-file-upload-input.bp3-disabled{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(206, 217, 224, 0.5);
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6);
    resize:none; }
  .bp3-file-upload-input::after{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    color:#182026;
    min-width:24px;
    min-height:24px;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    position:absolute;
    top:0;
    right:0;
    margin:3px;
    border-radius:3px;
    width:70px;
    text-align:center;
    line-height:24px;
    content:"Browse"; }
    .bp3-file-upload-input::after:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
      background-clip:padding-box;
      background-color:#ebf1f5; }
    .bp3-file-upload-input::after:active, .bp3-file-upload-input::after.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#d8e1e8;
      background-image:none; }
    .bp3-file-upload-input::after:disabled, .bp3-file-upload-input::after.bp3-disabled{
      outline:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(206, 217, 224, 0.5);
      background-image:none;
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6); }
      .bp3-file-upload-input::after:disabled.bp3-active, .bp3-file-upload-input::after:disabled.bp3-active:hover, .bp3-file-upload-input::after.bp3-disabled.bp3-active, .bp3-file-upload-input::after.bp3-disabled.bp3-active:hover{
        background:rgba(206, 217, 224, 0.7); }
  .bp3-file-upload-input:hover::after{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#ebf1f5; }
  .bp3-file-upload-input:active::after{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#d8e1e8;
    background-image:none; }
  .bp3-large .bp3-file-upload-input{
    height:40px;
    line-height:40px;
    font-size:16px;
    padding-right:95px; }
    .bp3-large .bp3-file-upload-input[type="search"], .bp3-large .bp3-file-upload-input.bp3-round{
      padding:0 15px; }
    .bp3-large .bp3-file-upload-input::after{
      min-width:30px;
      min-height:30px;
      margin:5px;
      width:85px;
      line-height:30px; }
  .bp3-dark .bp3-file-upload-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#f5f8fa;
    color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-file-upload-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-file-upload-input:disabled, .bp3-dark .bp3-file-upload-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(57, 75, 89, 0.5);
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::after{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#394b59;
      background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
      background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
      color:#f5f8fa; }
      .bp3-dark .bp3-file-upload-input::after:hover, .bp3-dark .bp3-file-upload-input::after:active, .bp3-dark .bp3-file-upload-input::after.bp3-active{
        color:#f5f8fa; }
      .bp3-dark .bp3-file-upload-input::after:hover{
        -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
        background-color:#30404d; }
      .bp3-dark .bp3-file-upload-input::after:active, .bp3-dark .bp3-file-upload-input::after.bp3-active{
        -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
                box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
        background-color:#202b33;
        background-image:none; }
      .bp3-dark .bp3-file-upload-input::after:disabled, .bp3-dark .bp3-file-upload-input::after.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none;
        background-color:rgba(57, 75, 89, 0.5);
        background-image:none;
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-file-upload-input::after:disabled.bp3-active, .bp3-dark .bp3-file-upload-input::after.bp3-disabled.bp3-active{
          background:rgba(57, 75, 89, 0.7); }
      .bp3-dark .bp3-file-upload-input::after .bp3-button-spinner .bp3-spinner-head{
        background:rgba(16, 22, 26, 0.5);
        stroke:#8a9ba8; }
    .bp3-dark .bp3-file-upload-input:hover::after{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#30404d; }
    .bp3-dark .bp3-file-upload-input:active::after{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#202b33;
      background-image:none; }

.bp3-file-upload-input::after{
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1); }
.bp3-form-group{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:0 0 15px; }
  .bp3-form-group label.bp3-label{
    margin-bottom:5px; }
  .bp3-form-group .bp3-control{
    margin-top:7px; }
  .bp3-form-group .bp3-form-helper-text{
    margin-top:5px;
    color:#5c7080;
    font-size:12px; }
  .bp3-form-group.bp3-intent-primary .bp3-form-helper-text{
    color:#106ba3; }
  .bp3-form-group.bp3-intent-success .bp3-form-helper-text{
    color:#0d8050; }
  .bp3-form-group.bp3-intent-warning .bp3-form-helper-text{
    color:#bf7326; }
  .bp3-form-group.bp3-intent-danger .bp3-form-helper-text{
    color:#c23030; }
  .bp3-form-group.bp3-inline{
    -webkit-box-orient:horizontal;
    -webkit-box-direction:normal;
        -ms-flex-direction:row;
            flex-direction:row;
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start; }
    .bp3-form-group.bp3-inline.bp3-large label.bp3-label{
      margin:0 10px 0 0;
      line-height:40px; }
    .bp3-form-group.bp3-inline label.bp3-label{
      margin:0 10px 0 0;
      line-height:30px; }
  .bp3-form-group.bp3-disabled .bp3-label,
  .bp3-form-group.bp3-disabled .bp3-text-muted,
  .bp3-form-group.bp3-disabled .bp3-form-helper-text{
    color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-dark .bp3-form-group.bp3-intent-primary .bp3-form-helper-text{
    color:#48aff0; }
  .bp3-dark .bp3-form-group.bp3-intent-success .bp3-form-helper-text{
    color:#3dcc91; }
  .bp3-dark .bp3-form-group.bp3-intent-warning .bp3-form-helper-text{
    color:#ffb366; }
  .bp3-dark .bp3-form-group.bp3-intent-danger .bp3-form-helper-text{
    color:#ff7373; }
  .bp3-dark .bp3-form-group .bp3-form-helper-text{
    color:#a7b6c2; }
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-label,
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-text-muted,
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-form-helper-text{
    color:rgba(167, 182, 194, 0.6) !important; }
.bp3-input-group{
  display:block;
  position:relative; }
  .bp3-input-group .bp3-input{
    position:relative;
    width:100%; }
    .bp3-input-group .bp3-input:not(:first-child){
      padding-left:30px; }
    .bp3-input-group .bp3-input:not(:last-child){
      padding-right:30px; }
  .bp3-input-group .bp3-input-action,
  .bp3-input-group > .bp3-button,
  .bp3-input-group > .bp3-icon{
    position:absolute;
    top:0; }
    .bp3-input-group .bp3-input-action:first-child,
    .bp3-input-group > .bp3-button:first-child,
    .bp3-input-group > .bp3-icon:first-child{
      left:0; }
    .bp3-input-group .bp3-input-action:last-child,
    .bp3-input-group > .bp3-button:last-child,
    .bp3-input-group > .bp3-icon:last-child{
      right:0; }
  .bp3-input-group .bp3-button{
    min-width:24px;
    min-height:24px;
    margin:3px;
    padding:0 7px; }
    .bp3-input-group .bp3-button:empty{
      padding:0; }
  .bp3-input-group > .bp3-icon{
    z-index:1;
    color:#5c7080; }
    .bp3-input-group > .bp3-icon:empty{
      line-height:1;
      font-family:"Icons16", sans-serif;
      font-size:16px;
      font-weight:400;
      font-style:normal;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased; }
  .bp3-input-group > .bp3-icon,
  .bp3-input-group .bp3-input-action > .bp3-spinner{
    margin:7px; }
  .bp3-input-group .bp3-tag{
    margin:5px; }
  .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus),
  .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus){
    color:#5c7080; }
    .bp3-dark .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus), .bp3-dark
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus){
      color:#a7b6c2; }
    .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-standard, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-large,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-standard,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-large{
      color:#5c7080; }
  .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled,
  .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled{
    color:rgba(92, 112, 128, 0.6) !important; }
    .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon-standard, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon-large,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon-standard,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon-large{
      color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-input-group.bp3-disabled{
    cursor:not-allowed; }
    .bp3-input-group.bp3-disabled .bp3-icon{
      color:rgba(92, 112, 128, 0.6); }
  .bp3-input-group.bp3-large .bp3-button{
    min-width:30px;
    min-height:30px;
    margin:5px; }
  .bp3-input-group.bp3-large > .bp3-icon,
  .bp3-input-group.bp3-large .bp3-input-action > .bp3-spinner{
    margin:12px; }
  .bp3-input-group.bp3-large .bp3-input{
    height:40px;
    line-height:40px;
    font-size:16px; }
    .bp3-input-group.bp3-large .bp3-input[type="search"], .bp3-input-group.bp3-large .bp3-input.bp3-round{
      padding:0 15px; }
    .bp3-input-group.bp3-large .bp3-input:not(:first-child){
      padding-left:40px; }
    .bp3-input-group.bp3-large .bp3-input:not(:last-child){
      padding-right:40px; }
  .bp3-input-group.bp3-small .bp3-button{
    min-width:20px;
    min-height:20px;
    margin:2px; }
  .bp3-input-group.bp3-small .bp3-tag{
    min-width:20px;
    min-height:20px;
    margin:2px; }
  .bp3-input-group.bp3-small > .bp3-icon,
  .bp3-input-group.bp3-small .bp3-input-action > .bp3-spinner{
    margin:4px; }
  .bp3-input-group.bp3-small .bp3-input{
    height:24px;
    padding-right:8px;
    padding-left:8px;
    line-height:24px;
    font-size:12px; }
    .bp3-input-group.bp3-small .bp3-input[type="search"], .bp3-input-group.bp3-small .bp3-input.bp3-round{
      padding:0 12px; }
    .bp3-input-group.bp3-small .bp3-input:not(:first-child){
      padding-left:24px; }
    .bp3-input-group.bp3-small .bp3-input:not(:last-child){
      padding-right:24px; }
  .bp3-input-group.bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    width:100%; }
  .bp3-input-group.bp3-round .bp3-button,
  .bp3-input-group.bp3-round .bp3-input,
  .bp3-input-group.bp3-round .bp3-tag{
    border-radius:30px; }
  .bp3-dark .bp3-input-group .bp3-icon{
    color:#a7b6c2; }
  .bp3-dark .bp3-input-group.bp3-disabled .bp3-icon{
    color:rgba(167, 182, 194, 0.6); }
  .bp3-input-group.bp3-intent-primary .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-primary .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-primary .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #137cbd;
              box-shadow:inset 0 0 0 1px #137cbd; }
    .bp3-input-group.bp3-intent-primary .bp3-input:disabled, .bp3-input-group.bp3-intent-primary .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-primary > .bp3-icon{
    color:#106ba3; }
    .bp3-dark .bp3-input-group.bp3-intent-primary > .bp3-icon{
      color:#48aff0; }
  .bp3-input-group.bp3-intent-success .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-success .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-success .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #0f9960;
              box-shadow:inset 0 0 0 1px #0f9960; }
    .bp3-input-group.bp3-intent-success .bp3-input:disabled, .bp3-input-group.bp3-intent-success .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-success > .bp3-icon{
    color:#0d8050; }
    .bp3-dark .bp3-input-group.bp3-intent-success > .bp3-icon{
      color:#3dcc91; }
  .bp3-input-group.bp3-intent-warning .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-warning .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-warning .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #d9822b;
              box-shadow:inset 0 0 0 1px #d9822b; }
    .bp3-input-group.bp3-intent-warning .bp3-input:disabled, .bp3-input-group.bp3-intent-warning .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-warning > .bp3-icon{
    color:#bf7326; }
    .bp3-dark .bp3-input-group.bp3-intent-warning > .bp3-icon{
      color:#ffb366; }
  .bp3-input-group.bp3-intent-danger .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-danger .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-danger .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #db3737;
              box-shadow:inset 0 0 0 1px #db3737; }
    .bp3-input-group.bp3-intent-danger .bp3-input:disabled, .bp3-input-group.bp3-intent-danger .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-danger > .bp3-icon{
    color:#c23030; }
    .bp3-dark .bp3-input-group.bp3-intent-danger > .bp3-icon{
      color:#ff7373; }
.bp3-input{
  outline:none;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
  background:#ffffff;
  height:30px;
  padding:0 10px;
  vertical-align:middle;
  line-height:30px;
  color:#182026;
  font-size:14px;
  font-weight:400;
  -webkit-transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  -webkit-appearance:none;
     -moz-appearance:none;
          appearance:none; }
  .bp3-input::-webkit-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input::-moz-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input:-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input::-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input::placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input:focus, .bp3-input.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-input[type="search"], .bp3-input.bp3-round{
    border-radius:30px;
    -webkit-box-sizing:border-box;
            box-sizing:border-box;
    padding-left:10px; }
  .bp3-input[readonly]{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-input:disabled, .bp3-input.bp3-disabled{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(206, 217, 224, 0.5);
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6);
    resize:none; }
  .bp3-input.bp3-large{
    height:40px;
    line-height:40px;
    font-size:16px; }
    .bp3-input.bp3-large[type="search"], .bp3-input.bp3-large.bp3-round{
      padding:0 15px; }
  .bp3-input.bp3-small{
    height:24px;
    padding-right:8px;
    padding-left:8px;
    line-height:24px;
    font-size:12px; }
    .bp3-input.bp3-small[type="search"], .bp3-input.bp3-small.bp3-round{
      padding:0 12px; }
  .bp3-input.bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    width:100%; }
  .bp3-dark .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#f5f8fa; }
    .bp3-dark .bp3-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-input:disabled, .bp3-dark .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(57, 75, 89, 0.5);
      color:rgba(167, 182, 194, 0.6); }
  .bp3-input.bp3-intent-primary{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-primary:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-primary[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #137cbd;
              box-shadow:inset 0 0 0 1px #137cbd; }
    .bp3-input.bp3-intent-primary:disabled, .bp3-input.bp3-intent-primary.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-primary:focus{
        -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-primary[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #137cbd;
                box-shadow:inset 0 0 0 1px #137cbd; }
      .bp3-dark .bp3-input.bp3-intent-primary:disabled, .bp3-dark .bp3-input.bp3-intent-primary.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-success{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-success:focus{
      -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-success[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #0f9960;
              box-shadow:inset 0 0 0 1px #0f9960; }
    .bp3-input.bp3-intent-success:disabled, .bp3-input.bp3-intent-success.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-success{
      -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-success:focus{
        -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #0f9960, 0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-success[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #0f9960;
                box-shadow:inset 0 0 0 1px #0f9960; }
      .bp3-dark .bp3-input.bp3-intent-success:disabled, .bp3-dark .bp3-input.bp3-intent-success.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-warning{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-warning:focus{
      -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-warning[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #d9822b;
              box-shadow:inset 0 0 0 1px #d9822b; }
    .bp3-input.bp3-intent-warning:disabled, .bp3-input.bp3-intent-warning.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-warning:focus{
        -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #d9822b, 0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-warning[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #d9822b;
                box-shadow:inset 0 0 0 1px #d9822b; }
      .bp3-dark .bp3-input.bp3-intent-warning:disabled, .bp3-dark .bp3-input.bp3-intent-warning.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-danger{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-danger:focus{
      -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-danger[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #db3737;
              box-shadow:inset 0 0 0 1px #db3737; }
    .bp3-input.bp3-intent-danger:disabled, .bp3-input.bp3-intent-danger.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-danger:focus{
        -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #db3737, 0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-danger[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #db3737;
                box-shadow:inset 0 0 0 1px #db3737; }
      .bp3-dark .bp3-input.bp3-intent-danger:disabled, .bp3-dark .bp3-input.bp3-intent-danger.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input::-ms-clear{
    display:none; }
textarea.bp3-input{
  max-width:100%;
  padding:10px; }
  textarea.bp3-input, textarea.bp3-input.bp3-large, textarea.bp3-input.bp3-small{
    height:auto;
    line-height:inherit; }
  textarea.bp3-input.bp3-small{
    padding:8px; }
  .bp3-dark textarea.bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#f5f8fa; }
    .bp3-dark textarea.bp3-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark textarea.bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark textarea.bp3-input:disabled, .bp3-dark textarea.bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(57, 75, 89, 0.5);
      color:rgba(167, 182, 194, 0.6); }
label.bp3-label{
  display:block;
  margin-top:0;
  margin-bottom:15px; }
  label.bp3-label .bp3-html-select,
  label.bp3-label .bp3-input,
  label.bp3-label .bp3-select,
  label.bp3-label .bp3-slider,
  label.bp3-label .bp3-popover-wrapper{
    display:block;
    margin-top:5px;
    text-transform:none; }
  label.bp3-label .bp3-button-group{
    margin-top:5px; }
  label.bp3-label .bp3-select select,
  label.bp3-label .bp3-html-select select{
    width:100%;
    vertical-align:top;
    font-weight:400; }
  label.bp3-label.bp3-disabled,
  label.bp3-label.bp3-disabled .bp3-text-muted{
    color:rgba(92, 112, 128, 0.6); }
  label.bp3-label.bp3-inline{
    line-height:30px; }
    label.bp3-label.bp3-inline .bp3-html-select,
    label.bp3-label.bp3-inline .bp3-input,
    label.bp3-label.bp3-inline .bp3-input-group,
    label.bp3-label.bp3-inline .bp3-select,
    label.bp3-label.bp3-inline .bp3-popover-wrapper{
      display:inline-block;
      margin:0 0 0 5px;
      vertical-align:top; }
    label.bp3-label.bp3-inline .bp3-button-group{
      margin:0 0 0 5px; }
    label.bp3-label.bp3-inline .bp3-input-group .bp3-input{
      margin-left:0; }
    label.bp3-label.bp3-inline.bp3-large{
      line-height:40px; }
  label.bp3-label:not(.bp3-inline) .bp3-popover-target{
    display:block; }
  .bp3-dark label.bp3-label{
    color:#f5f8fa; }
    .bp3-dark label.bp3-label.bp3-disabled,
    .bp3-dark label.bp3-label.bp3-disabled .bp3-text-muted{
      color:rgba(167, 182, 194, 0.6); }
.bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button{
  -webkit-box-flex:1;
      -ms-flex:1 1 14px;
          flex:1 1 14px;
  width:30px;
  min-height:0;
  padding:0; }
  .bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button:first-child{
    border-radius:0 3px 0 0; }
  .bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button:last-child{
    border-radius:0 0 3px 0; }

.bp3-numeric-input .bp3-button-group.bp3-vertical:first-child > .bp3-button:first-child{
  border-radius:3px 0 0 0; }

.bp3-numeric-input .bp3-button-group.bp3-vertical:first-child > .bp3-button:last-child{
  border-radius:0 0 0 3px; }

.bp3-numeric-input.bp3-large .bp3-button-group.bp3-vertical > .bp3-button{
  width:40px; }

form{
  display:block; }
.bp3-html-select select,
.bp3-select select{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  border:none;
  border-radius:3px;
  cursor:pointer;
  padding:5px 10px;
  vertical-align:middle;
  text-align:left;
  font-size:14px;
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
  background-color:#f5f8fa;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
  color:#182026;
  border-radius:3px;
  width:100%;
  height:30px;
  padding:0 25px 0 10px;
  -moz-appearance:none;
  -webkit-appearance:none; }
  .bp3-html-select select > *, .bp3-select select > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-html-select select > .bp3-fill, .bp3-select select > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-html-select select::before,
  .bp3-select select::before, .bp3-html-select select > *, .bp3-select select > *{
    margin-right:7px; }
  .bp3-html-select select:empty::before,
  .bp3-select select:empty::before,
  .bp3-html-select select > :last-child,
  .bp3-select select > :last-child{
    margin-right:0; }
  .bp3-html-select select:hover,
  .bp3-select select:hover{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#ebf1f5; }
  .bp3-html-select select:active,
  .bp3-select select:active, .bp3-html-select select.bp3-active,
  .bp3-select select.bp3-active{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#d8e1e8;
    background-image:none; }
  .bp3-html-select select:disabled,
  .bp3-select select:disabled, .bp3-html-select select.bp3-disabled,
  .bp3-select select.bp3-disabled{
    outline:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    background-color:rgba(206, 217, 224, 0.5);
    background-image:none;
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
    .bp3-html-select select:disabled.bp3-active,
    .bp3-select select:disabled.bp3-active, .bp3-html-select select:disabled.bp3-active:hover,
    .bp3-select select:disabled.bp3-active:hover, .bp3-html-select select.bp3-disabled.bp3-active,
    .bp3-select select.bp3-disabled.bp3-active, .bp3-html-select select.bp3-disabled.bp3-active:hover,
    .bp3-select select.bp3-disabled.bp3-active:hover{
      background:rgba(206, 217, 224, 0.7); }

.bp3-html-select.bp3-minimal select,
.bp3-select.bp3-minimal select{
  -webkit-box-shadow:none;
          box-shadow:none;
  background:none; }
  .bp3-html-select.bp3-minimal select:hover,
  .bp3-select.bp3-minimal select:hover{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(167, 182, 194, 0.3);
    text-decoration:none;
    color:#182026; }
  .bp3-html-select.bp3-minimal select:active,
  .bp3-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal select.bp3-active,
  .bp3-select.bp3-minimal select.bp3-active{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(115, 134, 148, 0.3);
    color:#182026; }
  .bp3-html-select.bp3-minimal select:disabled,
  .bp3-select.bp3-minimal select:disabled, .bp3-html-select.bp3-minimal select:disabled:hover,
  .bp3-select.bp3-minimal select:disabled:hover, .bp3-html-select.bp3-minimal select.bp3-disabled,
  .bp3-select.bp3-minimal select.bp3-disabled, .bp3-html-select.bp3-minimal select.bp3-disabled:hover,
  .bp3-select.bp3-minimal select.bp3-disabled:hover{
    background:none;
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
    .bp3-html-select.bp3-minimal select:disabled.bp3-active,
    .bp3-select.bp3-minimal select:disabled.bp3-active, .bp3-html-select.bp3-minimal select:disabled:hover.bp3-active,
    .bp3-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-html-select.bp3-minimal select.bp3-disabled.bp3-active,
    .bp3-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-disabled:hover.bp3-active,
    .bp3-select.bp3-minimal select.bp3-disabled:hover.bp3-active{
      background:rgba(115, 134, 148, 0.3); }
  .bp3-dark .bp3-html-select.bp3-minimal select, .bp3-html-select.bp3-minimal .bp3-dark select,
  .bp3-dark .bp3-select.bp3-minimal select, .bp3-select.bp3-minimal .bp3-dark select{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:none;
    color:inherit; }
    .bp3-dark .bp3-html-select.bp3-minimal select:hover, .bp3-html-select.bp3-minimal .bp3-dark select:hover,
    .bp3-dark .bp3-select.bp3-minimal select:hover, .bp3-select.bp3-minimal .bp3-dark select:hover, .bp3-dark .bp3-html-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal .bp3-dark select:active,
    .bp3-dark .bp3-select.bp3-minimal select:active, .bp3-select.bp3-minimal .bp3-dark select:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-active,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none; }
    .bp3-dark .bp3-html-select.bp3-minimal select:hover, .bp3-html-select.bp3-minimal .bp3-dark select:hover,
    .bp3-dark .bp3-select.bp3-minimal select:hover, .bp3-select.bp3-minimal .bp3-dark select:hover{
      background:rgba(138, 155, 168, 0.15); }
    .bp3-dark .bp3-html-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal .bp3-dark select:active,
    .bp3-dark .bp3-select.bp3-minimal select:active, .bp3-select.bp3-minimal .bp3-dark select:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-active,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-active{
      background:rgba(138, 155, 168, 0.3);
      color:#f5f8fa; }
    .bp3-dark .bp3-html-select.bp3-minimal select:disabled, .bp3-html-select.bp3-minimal .bp3-dark select:disabled,
    .bp3-dark .bp3-select.bp3-minimal select:disabled, .bp3-select.bp3-minimal .bp3-dark select:disabled, .bp3-dark .bp3-html-select.bp3-minimal select:disabled:hover, .bp3-html-select.bp3-minimal .bp3-dark select:disabled:hover,
    .bp3-dark .bp3-select.bp3-minimal select:disabled:hover, .bp3-select.bp3-minimal .bp3-dark select:disabled:hover, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled:hover,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled:hover{
      background:none;
      cursor:not-allowed;
      color:rgba(167, 182, 194, 0.6); }
      .bp3-dark .bp3-html-select.bp3-minimal select:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select:disabled.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select:disabled:hover.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-select.bp3-minimal .bp3-dark select:disabled:hover.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled:hover.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled:hover.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled:hover.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled:hover.bp3-active{
        background:rgba(138, 155, 168, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-primary,
  .bp3-select.bp3-minimal select.bp3-intent-primary{
    color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover,
    .bp3-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-html-select.bp3-minimal select.bp3-intent-primary:active,
    .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover,
    .bp3-select.bp3-minimal select.bp3-intent-primary:hover{
      background:rgba(19, 124, 189, 0.15);
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:active,
    .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active{
      background:rgba(19, 124, 189, 0.3);
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled{
      background:none;
      color:rgba(16, 107, 163, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active{
        background:rgba(19, 124, 189, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
      stroke:#106ba3; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary{
      color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.2);
        color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(72, 175, 240, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-success,
  .bp3-select.bp3-minimal select.bp3-intent-success{
    color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:hover,
    .bp3-select.bp3-minimal select.bp3-intent-success:hover, .bp3-html-select.bp3-minimal select.bp3-intent-success:active,
    .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:hover,
    .bp3-select.bp3-minimal select.bp3-intent-success:hover{
      background:rgba(15, 153, 96, 0.15);
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:active,
    .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active{
      background:rgba(15, 153, 96, 0.3);
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled{
      background:none;
      color:rgba(13, 128, 80, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active{
        background:rgba(15, 153, 96, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-success .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
      stroke:#0d8050; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success{
      color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.2);
        color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(61, 204, 145, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-warning,
  .bp3-select.bp3-minimal select.bp3-intent-warning{
    color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover,
    .bp3-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-html-select.bp3-minimal select.bp3-intent-warning:active,
    .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover,
    .bp3-select.bp3-minimal select.bp3-intent-warning:hover{
      background:rgba(217, 130, 43, 0.15);
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:active,
    .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active{
      background:rgba(217, 130, 43, 0.3);
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled{
      background:none;
      color:rgba(191, 115, 38, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active{
        background:rgba(217, 130, 43, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
      stroke:#bf7326; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning{
      color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.2);
        color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(255, 179, 102, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-danger,
  .bp3-select.bp3-minimal select.bp3-intent-danger{
    color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover,
    .bp3-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-html-select.bp3-minimal select.bp3-intent-danger:active,
    .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover,
    .bp3-select.bp3-minimal select.bp3-intent-danger:hover{
      background:rgba(219, 55, 55, 0.15);
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:active,
    .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active{
      background:rgba(219, 55, 55, 0.3);
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled{
      background:none;
      color:rgba(194, 48, 48, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active{
        background:rgba(219, 55, 55, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
      stroke:#c23030; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger{
      color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.2);
        color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(255, 115, 115, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }

.bp3-html-select.bp3-large select,
.bp3-select.bp3-large select{
  height:40px;
  padding-right:35px;
  font-size:16px; }

.bp3-dark .bp3-html-select select, .bp3-dark .bp3-select select{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
  background-color:#394b59;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
  color:#f5f8fa; }
  .bp3-dark .bp3-html-select select:hover, .bp3-dark .bp3-select select:hover, .bp3-dark .bp3-html-select select:active, .bp3-dark .bp3-select select:active, .bp3-dark .bp3-html-select select.bp3-active, .bp3-dark .bp3-select select.bp3-active{
    color:#f5f8fa; }
  .bp3-dark .bp3-html-select select:hover, .bp3-dark .bp3-select select:hover{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#30404d; }
  .bp3-dark .bp3-html-select select:active, .bp3-dark .bp3-select select:active, .bp3-dark .bp3-html-select select.bp3-active, .bp3-dark .bp3-select select.bp3-active{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#202b33;
    background-image:none; }
  .bp3-dark .bp3-html-select select:disabled, .bp3-dark .bp3-select select:disabled, .bp3-dark .bp3-html-select select.bp3-disabled, .bp3-dark .bp3-select select.bp3-disabled{
    -webkit-box-shadow:none;
            box-shadow:none;
    background-color:rgba(57, 75, 89, 0.5);
    background-image:none;
    color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-html-select select:disabled.bp3-active, .bp3-dark .bp3-select select:disabled.bp3-active, .bp3-dark .bp3-html-select select.bp3-disabled.bp3-active, .bp3-dark .bp3-select select.bp3-disabled.bp3-active{
      background:rgba(57, 75, 89, 0.7); }
  .bp3-dark .bp3-html-select select .bp3-button-spinner .bp3-spinner-head, .bp3-dark .bp3-select select .bp3-button-spinner .bp3-spinner-head{
    background:rgba(16, 22, 26, 0.5);
    stroke:#8a9ba8; }

.bp3-html-select select:disabled,
.bp3-select select:disabled{
  -webkit-box-shadow:none;
          box-shadow:none;
  background-color:rgba(206, 217, 224, 0.5);
  cursor:not-allowed;
  color:rgba(92, 112, 128, 0.6); }

.bp3-html-select .bp3-icon,
.bp3-select .bp3-icon, .bp3-select::after{
  position:absolute;
  top:7px;
  right:7px;
  color:#5c7080;
  pointer-events:none; }
  .bp3-html-select .bp3-disabled.bp3-icon,
  .bp3-select .bp3-disabled.bp3-icon, .bp3-disabled.bp3-select::after{
    color:rgba(92, 112, 128, 0.6); }
.bp3-html-select,
.bp3-select{
  display:inline-block;
  position:relative;
  vertical-align:middle;
  letter-spacing:normal; }
  .bp3-html-select select::-ms-expand,
  .bp3-select select::-ms-expand{
    display:none; }
  .bp3-html-select .bp3-icon,
  .bp3-select .bp3-icon{
    color:#5c7080; }
    .bp3-html-select .bp3-icon:hover,
    .bp3-select .bp3-icon:hover{
      color:#182026; }
    .bp3-dark .bp3-html-select .bp3-icon, .bp3-dark
    .bp3-select .bp3-icon{
      color:#a7b6c2; }
      .bp3-dark .bp3-html-select .bp3-icon:hover, .bp3-dark
      .bp3-select .bp3-icon:hover{
        color:#f5f8fa; }
  .bp3-html-select.bp3-large::after,
  .bp3-html-select.bp3-large .bp3-icon,
  .bp3-select.bp3-large::after,
  .bp3-select.bp3-large .bp3-icon{
    top:12px;
    right:12px; }
  .bp3-html-select.bp3-fill,
  .bp3-html-select.bp3-fill select,
  .bp3-select.bp3-fill,
  .bp3-select.bp3-fill select{
    width:100%; }
  .bp3-dark .bp3-html-select option, .bp3-dark
  .bp3-select option{
    background-color:#30404d;
    color:#f5f8fa; }
  .bp3-dark .bp3-html-select::after, .bp3-dark
  .bp3-select::after{
    color:#a7b6c2; }

.bp3-select::after{
  line-height:1;
  font-family:"Icons16", sans-serif;
  font-size:16px;
  font-weight:400;
  font-style:normal;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  content:""; }
.bp3-running-text table, table.bp3-html-table{
  border-spacing:0;
  font-size:14px; }
  .bp3-running-text table th, table.bp3-html-table th,
  .bp3-running-text table td,
  table.bp3-html-table td{
    padding:11px;
    vertical-align:top;
    text-align:left; }
  .bp3-running-text table th, table.bp3-html-table th{
    color:#182026;
    font-weight:600; }
  
  .bp3-running-text table td,
  table.bp3-html-table td{
    color:#182026; }
  .bp3-running-text table tbody tr:first-child th, table.bp3-html-table tbody tr:first-child th,
  .bp3-running-text table tbody tr:first-child td,
  table.bp3-html-table tbody tr:first-child td{
    -webkit-box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15); }
  .bp3-dark .bp3-running-text table th, .bp3-running-text .bp3-dark table th, .bp3-dark table.bp3-html-table th{
    color:#f5f8fa; }
  .bp3-dark .bp3-running-text table td, .bp3-running-text .bp3-dark table td, .bp3-dark table.bp3-html-table td{
    color:#f5f8fa; }
  .bp3-dark .bp3-running-text table tbody tr:first-child th, .bp3-running-text .bp3-dark table tbody tr:first-child th, .bp3-dark table.bp3-html-table tbody tr:first-child th,
  .bp3-dark .bp3-running-text table tbody tr:first-child td,
  .bp3-running-text .bp3-dark table tbody tr:first-child td,
  .bp3-dark table.bp3-html-table tbody tr:first-child td{
    -webkit-box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15);
            box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15); }

table.bp3-html-table.bp3-html-table-condensed th,
table.bp3-html-table.bp3-html-table-condensed td, table.bp3-html-table.bp3-small th,
table.bp3-html-table.bp3-small td{
  padding-top:6px;
  padding-bottom:6px; }

table.bp3-html-table.bp3-html-table-striped tbody tr:nth-child(odd) td{
  background:rgba(191, 204, 214, 0.15); }

table.bp3-html-table.bp3-html-table-bordered th:not(:first-child){
  -webkit-box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-html-table-bordered tbody tr td{
  -webkit-box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15); }
  table.bp3-html-table.bp3-html-table-bordered tbody tr td:not(:first-child){
    -webkit-box-shadow:inset 1px 1px 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 1px 1px 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td{
  -webkit-box-shadow:none;
          box-shadow:none; }
  table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td:not(:first-child){
    -webkit-box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-interactive tbody tr:hover td{
  background-color:rgba(191, 204, 214, 0.3);
  cursor:pointer; }

table.bp3-html-table.bp3-interactive tbody tr:active td{
  background-color:rgba(191, 204, 214, 0.4); }

.bp3-dark table.bp3-html-table.bp3-html-table-striped tbody tr:nth-child(odd) td{
  background:rgba(92, 112, 128, 0.15); }

.bp3-dark table.bp3-html-table.bp3-html-table-bordered th:not(:first-child){
  -webkit-box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15);
          box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15); }

.bp3-dark table.bp3-html-table.bp3-html-table-bordered tbody tr td{
  -webkit-box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15);
          box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15); }
  .bp3-dark table.bp3-html-table.bp3-html-table-bordered tbody tr td:not(:first-child){
    -webkit-box-shadow:inset 1px 1px 0 0 rgba(255, 255, 255, 0.15);
            box-shadow:inset 1px 1px 0 0 rgba(255, 255, 255, 0.15); }

.bp3-dark table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td{
  -webkit-box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15);
          box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15); }
  .bp3-dark table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td:first-child{
    -webkit-box-shadow:none;
            box-shadow:none; }

.bp3-dark table.bp3-html-table.bp3-interactive tbody tr:hover td{
  background-color:rgba(92, 112, 128, 0.3);
  cursor:pointer; }

.bp3-dark table.bp3-html-table.bp3-interactive tbody tr:active td{
  background-color:rgba(92, 112, 128, 0.4); }

.bp3-key-combo{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center; }
  .bp3-key-combo > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-key-combo > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-key-combo::before,
  .bp3-key-combo > *{
    margin-right:5px; }
  .bp3-key-combo:empty::before,
  .bp3-key-combo > :last-child{
    margin-right:0; }

.bp3-hotkey-dialog{
  top:40px;
  padding-bottom:0; }
  .bp3-hotkey-dialog .bp3-dialog-body{
    margin:0;
    padding:0; }
  .bp3-hotkey-dialog .bp3-hotkey-label{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1; }

.bp3-hotkey-column{
  margin:auto;
  max-height:80vh;
  overflow-y:auto;
  padding:30px; }
  .bp3-hotkey-column .bp3-heading{
    margin-bottom:20px; }
    .bp3-hotkey-column .bp3-heading:not(:first-child){
      margin-top:40px; }

.bp3-hotkey{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:justify;
      -ms-flex-pack:justify;
          justify-content:space-between;
  margin-right:0;
  margin-left:0; }
  .bp3-hotkey:not(:last-child){
    margin-bottom:10px; }
.bp3-icon{
  display:inline-block;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  vertical-align:text-bottom; }
  .bp3-icon:not(:empty)::before{
    content:"" !important;
    content:unset !important; }
  .bp3-icon > svg{
    display:block; }
    .bp3-icon > svg:not([fill]){
      fill:currentColor; }

.bp3-icon.bp3-intent-primary, .bp3-icon-standard.bp3-intent-primary, .bp3-icon-large.bp3-intent-primary{
  color:#106ba3; }
  .bp3-dark .bp3-icon.bp3-intent-primary, .bp3-dark .bp3-icon-standard.bp3-intent-primary, .bp3-dark .bp3-icon-large.bp3-intent-primary{
    color:#48aff0; }

.bp3-icon.bp3-intent-success, .bp3-icon-standard.bp3-intent-success, .bp3-icon-large.bp3-intent-success{
  color:#0d8050; }
  .bp3-dark .bp3-icon.bp3-intent-success, .bp3-dark .bp3-icon-standard.bp3-intent-success, .bp3-dark .bp3-icon-large.bp3-intent-success{
    color:#3dcc91; }

.bp3-icon.bp3-intent-warning, .bp3-icon-standard.bp3-intent-warning, .bp3-icon-large.bp3-intent-warning{
  color:#bf7326; }
  .bp3-dark .bp3-icon.bp3-intent-warning, .bp3-dark .bp3-icon-standard.bp3-intent-warning, .bp3-dark .bp3-icon-large.bp3-intent-warning{
    color:#ffb366; }

.bp3-icon.bp3-intent-danger, .bp3-icon-standard.bp3-intent-danger, .bp3-icon-large.bp3-intent-danger{
  color:#c23030; }
  .bp3-dark .bp3-icon.bp3-intent-danger, .bp3-dark .bp3-icon-standard.bp3-intent-danger, .bp3-dark .bp3-icon-large.bp3-intent-danger{
    color:#ff7373; }

span.bp3-icon-standard{
  line-height:1;
  font-family:"Icons16", sans-serif;
  font-size:16px;
  font-weight:400;
  font-style:normal;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  display:inline-block; }

span.bp3-icon-large{
  line-height:1;
  font-family:"Icons20", sans-serif;
  font-size:20px;
  font-weight:400;
  font-style:normal;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  display:inline-block; }

span.bp3-icon:empty{
  line-height:1;
  font-family:"Icons20";
  font-size:inherit;
  font-weight:400;
  font-style:normal; }
  span.bp3-icon:empty::before{
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased; }

.bp3-icon-add::before{
  content:""; }

.bp3-icon-add-column-left::before{
  content:""; }

.bp3-icon-add-column-right::before{
  content:""; }

.bp3-icon-add-row-bottom::before{
  content:""; }

.bp3-icon-add-row-top::before{
  content:""; }

.bp3-icon-add-to-artifact::before{
  content:""; }

.bp3-icon-add-to-folder::before{
  content:""; }

.bp3-icon-airplane::before{
  content:""; }

.bp3-icon-align-center::before{
  content:""; }

.bp3-icon-align-justify::before{
  content:""; }

.bp3-icon-align-left::before{
  content:""; }

.bp3-icon-align-right::before{
  content:""; }

.bp3-icon-alignment-bottom::before{
  content:""; }

.bp3-icon-alignment-horizontal-center::before{
  content:""; }

.bp3-icon-alignment-left::before{
  content:""; }

.bp3-icon-alignment-right::before{
  content:""; }

.bp3-icon-alignment-top::before{
  content:""; }

.bp3-icon-alignment-vertical-center::before{
  content:""; }

.bp3-icon-annotation::before{
  content:""; }

.bp3-icon-application::before{
  content:""; }

.bp3-icon-applications::before{
  content:""; }

.bp3-icon-archive::before{
  content:""; }

.bp3-icon-arrow-bottom-left::before{
  content:"↙"; }

.bp3-icon-arrow-bottom-right::before{
  content:"↘"; }

.bp3-icon-arrow-down::before{
  content:"↓"; }

.bp3-icon-arrow-left::before{
  content:"←"; }

.bp3-icon-arrow-right::before{
  content:"→"; }

.bp3-icon-arrow-top-left::before{
  content:"↖"; }

.bp3-icon-arrow-top-right::before{
  content:"↗"; }

.bp3-icon-arrow-up::before{
  content:"↑"; }

.bp3-icon-arrows-horizontal::before{
  content:"↔"; }

.bp3-icon-arrows-vertical::before{
  content:"↕"; }

.bp3-icon-asterisk::before{
  content:"*"; }

.bp3-icon-automatic-updates::before{
  content:""; }

.bp3-icon-badge::before{
  content:""; }

.bp3-icon-ban-circle::before{
  content:""; }

.bp3-icon-bank-account::before{
  content:""; }

.bp3-icon-barcode::before{
  content:""; }

.bp3-icon-blank::before{
  content:""; }

.bp3-icon-blocked-person::before{
  content:""; }

.bp3-icon-bold::before{
  content:""; }

.bp3-icon-book::before{
  content:""; }

.bp3-icon-bookmark::before{
  content:""; }

.bp3-icon-box::before{
  content:""; }

.bp3-icon-briefcase::before{
  content:""; }

.bp3-icon-bring-data::before{
  content:""; }

.bp3-icon-build::before{
  content:""; }

.bp3-icon-calculator::before{
  content:""; }

.bp3-icon-calendar::before{
  content:""; }

.bp3-icon-camera::before{
  content:""; }

.bp3-icon-caret-down::before{
  content:"⌄"; }

.bp3-icon-caret-left::before{
  content:"〈"; }

.bp3-icon-caret-right::before{
  content:"〉"; }

.bp3-icon-caret-up::before{
  content:"⌃"; }

.bp3-icon-cell-tower::before{
  content:""; }

.bp3-icon-changes::before{
  content:""; }

.bp3-icon-chart::before{
  content:""; }

.bp3-icon-chat::before{
  content:""; }

.bp3-icon-chevron-backward::before{
  content:""; }

.bp3-icon-chevron-down::before{
  content:""; }

.bp3-icon-chevron-forward::before{
  content:""; }

.bp3-icon-chevron-left::before{
  content:""; }

.bp3-icon-chevron-right::before{
  content:""; }

.bp3-icon-chevron-up::before{
  content:""; }

.bp3-icon-circle::before{
  content:""; }

.bp3-icon-circle-arrow-down::before{
  content:""; }

.bp3-icon-circle-arrow-left::before{
  content:""; }

.bp3-icon-circle-arrow-right::before{
  content:""; }

.bp3-icon-circle-arrow-up::before{
  content:""; }

.bp3-icon-citation::before{
  content:""; }

.bp3-icon-clean::before{
  content:""; }

.bp3-icon-clipboard::before{
  content:""; }

.bp3-icon-cloud::before{
  content:"☁"; }

.bp3-icon-cloud-download::before{
  content:""; }

.bp3-icon-cloud-upload::before{
  content:""; }

.bp3-icon-code::before{
  content:""; }

.bp3-icon-code-block::before{
  content:""; }

.bp3-icon-cog::before{
  content:""; }

.bp3-icon-collapse-all::before{
  content:""; }

.bp3-icon-column-layout::before{
  content:""; }

.bp3-icon-comment::before{
  content:""; }

.bp3-icon-comparison::before{
  content:""; }

.bp3-icon-compass::before{
  content:""; }

.bp3-icon-compressed::before{
  content:""; }

.bp3-icon-confirm::before{
  content:""; }

.bp3-icon-console::before{
  content:""; }

.bp3-icon-contrast::before{
  content:""; }

.bp3-icon-control::before{
  content:""; }

.bp3-icon-credit-card::before{
  content:""; }

.bp3-icon-cross::before{
  content:"✗"; }

.bp3-icon-crown::before{
  content:""; }

.bp3-icon-cube::before{
  content:""; }

.bp3-icon-cube-add::before{
  content:""; }

.bp3-icon-cube-remove::before{
  content:""; }

.bp3-icon-curved-range-chart::before{
  content:""; }

.bp3-icon-cut::before{
  content:""; }

.bp3-icon-dashboard::before{
  content:""; }

.bp3-icon-data-lineage::before{
  content:""; }

.bp3-icon-database::before{
  content:""; }

.bp3-icon-delete::before{
  content:""; }

.bp3-icon-delta::before{
  content:"Δ"; }

.bp3-icon-derive-column::before{
  content:""; }

.bp3-icon-desktop::before{
  content:""; }

.bp3-icon-diagram-tree::before{
  content:""; }

.bp3-icon-direction-left::before{
  content:""; }

.bp3-icon-direction-right::before{
  content:""; }

.bp3-icon-disable::before{
  content:""; }

.bp3-icon-document::before{
  content:""; }

.bp3-icon-document-open::before{
  content:""; }

.bp3-icon-document-share::before{
  content:""; }

.bp3-icon-dollar::before{
  content:"$"; }

.bp3-icon-dot::before{
  content:"•"; }

.bp3-icon-double-caret-horizontal::before{
  content:""; }

.bp3-icon-double-caret-vertical::before{
  content:""; }

.bp3-icon-double-chevron-down::before{
  content:""; }

.bp3-icon-double-chevron-left::before{
  content:""; }

.bp3-icon-double-chevron-right::before{
  content:""; }

.bp3-icon-double-chevron-up::before{
  content:""; }

.bp3-icon-doughnut-chart::before{
  content:""; }

.bp3-icon-download::before{
  content:""; }

.bp3-icon-drag-handle-horizontal::before{
  content:""; }

.bp3-icon-drag-handle-vertical::before{
  content:""; }

.bp3-icon-draw::before{
  content:""; }

.bp3-icon-drive-time::before{
  content:""; }

.bp3-icon-duplicate::before{
  content:""; }

.bp3-icon-edit::before{
  content:"✎"; }

.bp3-icon-eject::before{
  content:"⏏"; }

.bp3-icon-endorsed::before{
  content:""; }

.bp3-icon-envelope::before{
  content:"✉"; }

.bp3-icon-equals::before{
  content:""; }

.bp3-icon-eraser::before{
  content:""; }

.bp3-icon-error::before{
  content:""; }

.bp3-icon-euro::before{
  content:"€"; }

.bp3-icon-exchange::before{
  content:""; }

.bp3-icon-exclude-row::before{
  content:""; }

.bp3-icon-expand-all::before{
  content:""; }

.bp3-icon-export::before{
  content:""; }

.bp3-icon-eye-off::before{
  content:""; }

.bp3-icon-eye-on::before{
  content:""; }

.bp3-icon-eye-open::before{
  content:""; }

.bp3-icon-fast-backward::before{
  content:""; }

.bp3-icon-fast-forward::before{
  content:""; }

.bp3-icon-feed::before{
  content:""; }

.bp3-icon-feed-subscribed::before{
  content:""; }

.bp3-icon-film::before{
  content:""; }

.bp3-icon-filter::before{
  content:""; }

.bp3-icon-filter-keep::before{
  content:""; }

.bp3-icon-filter-list::before{
  content:""; }

.bp3-icon-filter-open::before{
  content:""; }

.bp3-icon-filter-remove::before{
  content:""; }

.bp3-icon-flag::before{
  content:"⚑"; }

.bp3-icon-flame::before{
  content:""; }

.bp3-icon-flash::before{
  content:""; }

.bp3-icon-floppy-disk::before{
  content:""; }

.bp3-icon-flow-branch::before{
  content:""; }

.bp3-icon-flow-end::before{
  content:""; }

.bp3-icon-flow-linear::before{
  content:""; }

.bp3-icon-flow-review::before{
  content:""; }

.bp3-icon-flow-review-branch::before{
  content:""; }

.bp3-icon-flows::before{
  content:""; }

.bp3-icon-folder-close::before{
  content:""; }

.bp3-icon-folder-new::before{
  content:""; }

.bp3-icon-folder-open::before{
  content:""; }

.bp3-icon-folder-shared::before{
  content:""; }

.bp3-icon-folder-shared-open::before{
  content:""; }

.bp3-icon-follower::before{
  content:""; }

.bp3-icon-following::before{
  content:""; }

.bp3-icon-font::before{
  content:""; }

.bp3-icon-fork::before{
  content:""; }

.bp3-icon-form::before{
  content:""; }

.bp3-icon-full-circle::before{
  content:""; }

.bp3-icon-full-stacked-chart::before{
  content:""; }

.bp3-icon-fullscreen::before{
  content:""; }

.bp3-icon-function::before{
  content:""; }

.bp3-icon-gantt-chart::before{
  content:""; }

.bp3-icon-geolocation::before{
  content:""; }

.bp3-icon-geosearch::before{
  content:""; }

.bp3-icon-git-branch::before{
  content:""; }

.bp3-icon-git-commit::before{
  content:""; }

.bp3-icon-git-merge::before{
  content:""; }

.bp3-icon-git-new-branch::before{
  content:""; }

.bp3-icon-git-pull::before{
  content:""; }

.bp3-icon-git-push::before{
  content:""; }

.bp3-icon-git-repo::before{
  content:""; }

.bp3-icon-glass::before{
  content:""; }

.bp3-icon-globe::before{
  content:""; }

.bp3-icon-globe-network::before{
  content:""; }

.bp3-icon-graph::before{
  content:""; }

.bp3-icon-graph-remove::before{
  content:""; }

.bp3-icon-greater-than::before{
  content:""; }

.bp3-icon-greater-than-or-equal-to::before{
  content:""; }

.bp3-icon-grid::before{
  content:""; }

.bp3-icon-grid-view::before{
  content:""; }

.bp3-icon-group-objects::before{
  content:""; }

.bp3-icon-grouped-bar-chart::before{
  content:""; }

.bp3-icon-hand::before{
  content:""; }

.bp3-icon-hand-down::before{
  content:""; }

.bp3-icon-hand-left::before{
  content:""; }

.bp3-icon-hand-right::before{
  content:""; }

.bp3-icon-hand-up::before{
  content:""; }

.bp3-icon-header::before{
  content:""; }

.bp3-icon-header-one::before{
  content:""; }

.bp3-icon-header-two::before{
  content:""; }

.bp3-icon-headset::before{
  content:""; }

.bp3-icon-heart::before{
  content:"♥"; }

.bp3-icon-heart-broken::before{
  content:""; }

.bp3-icon-heat-grid::before{
  content:""; }

.bp3-icon-heatmap::before{
  content:""; }

.bp3-icon-help::before{
  content:"?"; }

.bp3-icon-helper-management::before{
  content:""; }

.bp3-icon-highlight::before{
  content:""; }

.bp3-icon-history::before{
  content:""; }

.bp3-icon-home::before{
  content:"⌂"; }

.bp3-icon-horizontal-bar-chart::before{
  content:""; }

.bp3-icon-horizontal-bar-chart-asc::before{
  content:""; }

.bp3-icon-horizontal-bar-chart-desc::before{
  content:""; }

.bp3-icon-horizontal-distribution::before{
  content:""; }

.bp3-icon-id-number::before{
  content:""; }

.bp3-icon-image-rotate-left::before{
  content:""; }

.bp3-icon-image-rotate-right::before{
  content:""; }

.bp3-icon-import::before{
  content:""; }

.bp3-icon-inbox::before{
  content:""; }

.bp3-icon-inbox-filtered::before{
  content:""; }

.bp3-icon-inbox-geo::before{
  content:""; }

.bp3-icon-inbox-search::before{
  content:""; }

.bp3-icon-inbox-update::before{
  content:""; }

.bp3-icon-info-sign::before{
  content:"ℹ"; }

.bp3-icon-inheritance::before{
  content:""; }

.bp3-icon-inner-join::before{
  content:""; }

.bp3-icon-insert::before{
  content:""; }

.bp3-icon-intersection::before{
  content:""; }

.bp3-icon-ip-address::before{
  content:""; }

.bp3-icon-issue::before{
  content:""; }

.bp3-icon-issue-closed::before{
  content:""; }

.bp3-icon-issue-new::before{
  content:""; }

.bp3-icon-italic::before{
  content:""; }

.bp3-icon-join-table::before{
  content:""; }

.bp3-icon-key::before{
  content:""; }

.bp3-icon-key-backspace::before{
  content:""; }

.bp3-icon-key-command::before{
  content:""; }

.bp3-icon-key-control::before{
  content:""; }

.bp3-icon-key-delete::before{
  content:""; }

.bp3-icon-key-enter::before{
  content:""; }

.bp3-icon-key-escape::before{
  content:""; }

.bp3-icon-key-option::before{
  content:""; }

.bp3-icon-key-shift::before{
  content:""; }

.bp3-icon-key-tab::before{
  content:""; }

.bp3-icon-known-vehicle::before{
  content:""; }

.bp3-icon-label::before{
  content:""; }

.bp3-icon-layer::before{
  content:""; }

.bp3-icon-layers::before{
  content:""; }

.bp3-icon-layout::before{
  content:""; }

.bp3-icon-layout-auto::before{
  content:""; }

.bp3-icon-layout-balloon::before{
  content:""; }

.bp3-icon-layout-circle::before{
  content:""; }

.bp3-icon-layout-grid::before{
  content:""; }

.bp3-icon-layout-group-by::before{
  content:""; }

.bp3-icon-layout-hierarchy::before{
  content:""; }

.bp3-icon-layout-linear::before{
  content:""; }

.bp3-icon-layout-skew-grid::before{
  content:""; }

.bp3-icon-layout-sorted-clusters::before{
  content:""; }

.bp3-icon-learning::before{
  content:""; }

.bp3-icon-left-join::before{
  content:""; }

.bp3-icon-less-than::before{
  content:""; }

.bp3-icon-less-than-or-equal-to::before{
  content:""; }

.bp3-icon-lifesaver::before{
  content:""; }

.bp3-icon-lightbulb::before{
  content:""; }

.bp3-icon-link::before{
  content:""; }

.bp3-icon-list::before{
  content:"☰"; }

.bp3-icon-list-columns::before{
  content:""; }

.bp3-icon-list-detail-view::before{
  content:""; }

.bp3-icon-locate::before{
  content:""; }

.bp3-icon-lock::before{
  content:""; }

.bp3-icon-log-in::before{
  content:""; }

.bp3-icon-log-out::before{
  content:""; }

.bp3-icon-manual::before{
  content:""; }

.bp3-icon-manually-entered-data::before{
  content:""; }

.bp3-icon-map::before{
  content:""; }

.bp3-icon-map-create::before{
  content:""; }

.bp3-icon-map-marker::before{
  content:""; }

.bp3-icon-maximize::before{
  content:""; }

.bp3-icon-media::before{
  content:""; }

.bp3-icon-menu::before{
  content:""; }

.bp3-icon-menu-closed::before{
  content:""; }

.bp3-icon-menu-open::before{
  content:""; }

.bp3-icon-merge-columns::before{
  content:""; }

.bp3-icon-merge-links::before{
  content:""; }

.bp3-icon-minimize::before{
  content:""; }

.bp3-icon-minus::before{
  content:"−"; }

.bp3-icon-mobile-phone::before{
  content:""; }

.bp3-icon-mobile-video::before{
  content:""; }

.bp3-icon-moon::before{
  content:""; }

.bp3-icon-more::before{
  content:""; }

.bp3-icon-mountain::before{
  content:""; }

.bp3-icon-move::before{
  content:""; }

.bp3-icon-mugshot::before{
  content:""; }

.bp3-icon-multi-select::before{
  content:""; }

.bp3-icon-music::before{
  content:""; }

.bp3-icon-new-drawing::before{
  content:""; }

.bp3-icon-new-grid-item::before{
  content:""; }

.bp3-icon-new-layer::before{
  content:""; }

.bp3-icon-new-layers::before{
  content:""; }

.bp3-icon-new-link::before{
  content:""; }

.bp3-icon-new-object::before{
  content:""; }

.bp3-icon-new-person::before{
  content:""; }

.bp3-icon-new-prescription::before{
  content:""; }

.bp3-icon-new-text-box::before{
  content:""; }

.bp3-icon-ninja::before{
  content:""; }

.bp3-icon-not-equal-to::before{
  content:""; }

.bp3-icon-notifications::before{
  content:""; }

.bp3-icon-notifications-updated::before{
  content:""; }

.bp3-icon-numbered-list::before{
  content:""; }

.bp3-icon-numerical::before{
  content:""; }

.bp3-icon-office::before{
  content:""; }

.bp3-icon-offline::before{
  content:""; }

.bp3-icon-oil-field::before{
  content:""; }

.bp3-icon-one-column::before{
  content:""; }

.bp3-icon-outdated::before{
  content:""; }

.bp3-icon-page-layout::before{
  content:""; }

.bp3-icon-panel-stats::before{
  content:""; }

.bp3-icon-panel-table::before{
  content:""; }

.bp3-icon-paperclip::before{
  content:""; }

.bp3-icon-paragraph::before{
  content:""; }

.bp3-icon-path::before{
  content:""; }

.bp3-icon-path-search::before{
  content:""; }

.bp3-icon-pause::before{
  content:""; }

.bp3-icon-people::before{
  content:""; }

.bp3-icon-percentage::before{
  content:""; }

.bp3-icon-person::before{
  content:""; }

.bp3-icon-phone::before{
  content:"☎"; }

.bp3-icon-pie-chart::before{
  content:""; }

.bp3-icon-pin::before{
  content:""; }

.bp3-icon-pivot::before{
  content:""; }

.bp3-icon-pivot-table::before{
  content:""; }

.bp3-icon-play::before{
  content:""; }

.bp3-icon-plus::before{
  content:"+"; }

.bp3-icon-polygon-filter::before{
  content:""; }

.bp3-icon-power::before{
  content:""; }

.bp3-icon-predictive-analysis::before{
  content:""; }

.bp3-icon-prescription::before{
  content:""; }

.bp3-icon-presentation::before{
  content:""; }

.bp3-icon-print::before{
  content:"⎙"; }

.bp3-icon-projects::before{
  content:""; }

.bp3-icon-properties::before{
  content:""; }

.bp3-icon-property::before{
  content:""; }

.bp3-icon-publish-function::before{
  content:""; }

.bp3-icon-pulse::before{
  content:""; }

.bp3-icon-random::before{
  content:""; }

.bp3-icon-record::before{
  content:""; }

.bp3-icon-redo::before{
  content:""; }

.bp3-icon-refresh::before{
  content:""; }

.bp3-icon-regression-chart::before{
  content:""; }

.bp3-icon-remove::before{
  content:""; }

.bp3-icon-remove-column::before{
  content:""; }

.bp3-icon-remove-column-left::before{
  content:""; }

.bp3-icon-remove-column-right::before{
  content:""; }

.bp3-icon-remove-row-bottom::before{
  content:""; }

.bp3-icon-remove-row-top::before{
  content:""; }

.bp3-icon-repeat::before{
  content:""; }

.bp3-icon-reset::before{
  content:""; }

.bp3-icon-resolve::before{
  content:""; }

.bp3-icon-rig::before{
  content:""; }

.bp3-icon-right-join::before{
  content:""; }

.bp3-icon-ring::before{
  content:""; }

.bp3-icon-rotate-document::before{
  content:""; }

.bp3-icon-rotate-page::before{
  content:""; }

.bp3-icon-satellite::before{
  content:""; }

.bp3-icon-saved::before{
  content:""; }

.bp3-icon-scatter-plot::before{
  content:""; }

.bp3-icon-search::before{
  content:""; }

.bp3-icon-search-around::before{
  content:""; }

.bp3-icon-search-template::before{
  content:""; }

.bp3-icon-search-text::before{
  content:""; }

.bp3-icon-segmented-control::before{
  content:""; }

.bp3-icon-select::before{
  content:""; }

.bp3-icon-selection::before{
  content:"⦿"; }

.bp3-icon-send-to::before{
  content:""; }

.bp3-icon-send-to-graph::before{
  content:""; }

.bp3-icon-send-to-map::before{
  content:""; }

.bp3-icon-series-add::before{
  content:""; }

.bp3-icon-series-configuration::before{
  content:""; }

.bp3-icon-series-derived::before{
  content:""; }

.bp3-icon-series-filtered::before{
  content:""; }

.bp3-icon-series-search::before{
  content:""; }

.bp3-icon-settings::before{
  content:""; }

.bp3-icon-share::before{
  content:""; }

.bp3-icon-shield::before{
  content:""; }

.bp3-icon-shop::before{
  content:""; }

.bp3-icon-shopping-cart::before{
  content:""; }

.bp3-icon-signal-search::before{
  content:""; }

.bp3-icon-sim-card::before{
  content:""; }

.bp3-icon-slash::before{
  content:""; }

.bp3-icon-small-cross::before{
  content:""; }

.bp3-icon-small-minus::before{
  content:""; }

.bp3-icon-small-plus::before{
  content:""; }

.bp3-icon-small-tick::before{
  content:""; }

.bp3-icon-snowflake::before{
  content:""; }

.bp3-icon-social-media::before{
  content:""; }

.bp3-icon-sort::before{
  content:""; }

.bp3-icon-sort-alphabetical::before{
  content:""; }

.bp3-icon-sort-alphabetical-desc::before{
  content:""; }

.bp3-icon-sort-asc::before{
  content:""; }

.bp3-icon-sort-desc::before{
  content:""; }

.bp3-icon-sort-numerical::before{
  content:""; }

.bp3-icon-sort-numerical-desc::before{
  content:""; }

.bp3-icon-split-columns::before{
  content:""; }

.bp3-icon-square::before{
  content:""; }

.bp3-icon-stacked-chart::before{
  content:""; }

.bp3-icon-star::before{
  content:"★"; }

.bp3-icon-star-empty::before{
  content:"☆"; }

.bp3-icon-step-backward::before{
  content:""; }

.bp3-icon-step-chart::before{
  content:""; }

.bp3-icon-step-forward::before{
  content:""; }

.bp3-icon-stop::before{
  content:""; }

.bp3-icon-stopwatch::before{
  content:""; }

.bp3-icon-strikethrough::before{
  content:""; }

.bp3-icon-style::before{
  content:""; }

.bp3-icon-swap-horizontal::before{
  content:""; }

.bp3-icon-swap-vertical::before{
  content:""; }

.bp3-icon-symbol-circle::before{
  content:""; }

.bp3-icon-symbol-cross::before{
  content:""; }

.bp3-icon-symbol-diamond::before{
  content:""; }

.bp3-icon-symbol-square::before{
  content:""; }

.bp3-icon-symbol-triangle-down::before{
  content:""; }

.bp3-icon-symbol-triangle-up::before{
  content:""; }

.bp3-icon-tag::before{
  content:""; }

.bp3-icon-take-action::before{
  content:""; }

.bp3-icon-taxi::before{
  content:""; }

.bp3-icon-text-highlight::before{
  content:""; }

.bp3-icon-th::before{
  content:""; }

.bp3-icon-th-derived::before{
  content:""; }

.bp3-icon-th-disconnect::before{
  content:""; }

.bp3-icon-th-filtered::before{
  content:""; }

.bp3-icon-th-list::before{
  content:""; }

.bp3-icon-thumbs-down::before{
  content:""; }

.bp3-icon-thumbs-up::before{
  content:""; }

.bp3-icon-tick::before{
  content:"✓"; }

.bp3-icon-tick-circle::before{
  content:""; }

.bp3-icon-time::before{
  content:"⏲"; }

.bp3-icon-timeline-area-chart::before{
  content:""; }

.bp3-icon-timeline-bar-chart::before{
  content:""; }

.bp3-icon-timeline-events::before{
  content:""; }

.bp3-icon-timeline-line-chart::before{
  content:""; }

.bp3-icon-tint::before{
  content:""; }

.bp3-icon-torch::before{
  content:""; }

.bp3-icon-tractor::before{
  content:""; }

.bp3-icon-train::before{
  content:""; }

.bp3-icon-translate::before{
  content:""; }

.bp3-icon-trash::before{
  content:""; }

.bp3-icon-tree::before{
  content:""; }

.bp3-icon-trending-down::before{
  content:""; }

.bp3-icon-trending-up::before{
  content:""; }

.bp3-icon-truck::before{
  content:""; }

.bp3-icon-two-columns::before{
  content:""; }

.bp3-icon-unarchive::before{
  content:""; }

.bp3-icon-underline::before{
  content:"⎁"; }

.bp3-icon-undo::before{
  content:"⎌"; }

.bp3-icon-ungroup-objects::before{
  content:""; }

.bp3-icon-unknown-vehicle::before{
  content:""; }

.bp3-icon-unlock::before{
  content:""; }

.bp3-icon-unpin::before{
  content:""; }

.bp3-icon-unresolve::before{
  content:""; }

.bp3-icon-updated::before{
  content:""; }

.bp3-icon-upload::before{
  content:""; }

.bp3-icon-user::before{
  content:""; }

.bp3-icon-variable::before{
  content:""; }

.bp3-icon-vertical-bar-chart-asc::before{
  content:""; }

.bp3-icon-vertical-bar-chart-desc::before{
  content:""; }

.bp3-icon-vertical-distribution::before{
  content:""; }

.bp3-icon-video::before{
  content:""; }

.bp3-icon-volume-down::before{
  content:""; }

.bp3-icon-volume-off::before{
  content:""; }

.bp3-icon-volume-up::before{
  content:""; }

.bp3-icon-walk::before{
  content:""; }

.bp3-icon-warning-sign::before{
  content:""; }

.bp3-icon-waterfall-chart::before{
  content:""; }

.bp3-icon-widget::before{
  content:""; }

.bp3-icon-widget-button::before{
  content:""; }

.bp3-icon-widget-footer::before{
  content:""; }

.bp3-icon-widget-header::before{
  content:""; }

.bp3-icon-wrench::before{
  content:""; }

.bp3-icon-zoom-in::before{
  content:""; }

.bp3-icon-zoom-out::before{
  content:""; }

.bp3-icon-zoom-to-fit::before{
  content:""; }
.bp3-submenu > .bp3-popover-wrapper{
  display:block; }

.bp3-submenu .bp3-popover-target{
  display:block; }

.bp3-submenu.bp3-popover{
  -webkit-box-shadow:none;
          box-shadow:none;
  padding:0 5px; }
  .bp3-submenu.bp3-popover > .bp3-popover-content{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-submenu.bp3-popover, .bp3-submenu.bp3-popover.bp3-dark{
    -webkit-box-shadow:none;
            box-shadow:none; }
    .bp3-dark .bp3-submenu.bp3-popover > .bp3-popover-content, .bp3-submenu.bp3-popover.bp3-dark > .bp3-popover-content{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
.bp3-menu{
  margin:0;
  border-radius:3px;
  background:#ffffff;
  min-width:180px;
  padding:5px;
  list-style:none;
  text-align:left;
  color:#182026; }

.bp3-menu-divider{
  display:block;
  margin:5px;
  border-top:1px solid rgba(16, 22, 26, 0.15); }
  .bp3-dark .bp3-menu-divider{
    border-top-color:rgba(255, 255, 255, 0.15); }

.bp3-menu-item{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  border-radius:2px;
  padding:5px 7px;
  text-decoration:none;
  line-height:20px;
  color:inherit;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-menu-item > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-menu-item > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-menu-item::before,
  .bp3-menu-item > *{
    margin-right:7px; }
  .bp3-menu-item:empty::before,
  .bp3-menu-item > :last-child{
    margin-right:0; }
  .bp3-menu-item > .bp3-fill{
    word-break:break-word; }
  .bp3-menu-item:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
    background-color:rgba(167, 182, 194, 0.3);
    cursor:pointer;
    text-decoration:none; }
  .bp3-menu-item.bp3-disabled{
    background-color:inherit;
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-dark .bp3-menu-item{
    color:inherit; }
    .bp3-dark .bp3-menu-item:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
      background-color:rgba(138, 155, 168, 0.15);
      color:inherit; }
    .bp3-dark .bp3-menu-item.bp3-disabled{
      background-color:inherit;
      color:rgba(167, 182, 194, 0.6); }
  .bp3-menu-item.bp3-intent-primary{
    color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-primary::before, .bp3-menu-item.bp3-intent-primary::after,
    .bp3-menu-item.bp3-intent-primary .bp3-menu-item-label{
      color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-menu-item.bp3-intent-primary.bp3-active{
      background-color:#137cbd; }
    .bp3-menu-item.bp3-intent-primary:active{
      background-color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-menu-item.bp3-intent-primary:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-menu-item.bp3-intent-primary:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-primary:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-primary:active, .bp3-menu-item.bp3-intent-primary:active::before, .bp3-menu-item.bp3-intent-primary:active::after,
    .bp3-menu-item.bp3-intent-primary:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-primary.bp3-active, .bp3-menu-item.bp3-intent-primary.bp3-active::before, .bp3-menu-item.bp3-intent-primary.bp3-active::after,
    .bp3-menu-item.bp3-intent-primary.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-success{
    color:#0d8050; }
    .bp3-menu-item.bp3-intent-success .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-success::before, .bp3-menu-item.bp3-intent-success::after,
    .bp3-menu-item.bp3-intent-success .bp3-menu-item-label{
      color:#0d8050; }
    .bp3-menu-item.bp3-intent-success:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-menu-item.bp3-intent-success.bp3-active{
      background-color:#0f9960; }
    .bp3-menu-item.bp3-intent-success:active{
      background-color:#0d8050; }
    .bp3-menu-item.bp3-intent-success:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-menu-item.bp3-intent-success:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-menu-item.bp3-intent-success:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-success:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-success:active, .bp3-menu-item.bp3-intent-success:active::before, .bp3-menu-item.bp3-intent-success:active::after,
    .bp3-menu-item.bp3-intent-success:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-success.bp3-active, .bp3-menu-item.bp3-intent-success.bp3-active::before, .bp3-menu-item.bp3-intent-success.bp3-active::after,
    .bp3-menu-item.bp3-intent-success.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-warning{
    color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-warning::before, .bp3-menu-item.bp3-intent-warning::after,
    .bp3-menu-item.bp3-intent-warning .bp3-menu-item-label{
      color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-menu-item.bp3-intent-warning.bp3-active{
      background-color:#d9822b; }
    .bp3-menu-item.bp3-intent-warning:active{
      background-color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-menu-item.bp3-intent-warning:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-menu-item.bp3-intent-warning:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-warning:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-warning:active, .bp3-menu-item.bp3-intent-warning:active::before, .bp3-menu-item.bp3-intent-warning:active::after,
    .bp3-menu-item.bp3-intent-warning:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-warning.bp3-active, .bp3-menu-item.bp3-intent-warning.bp3-active::before, .bp3-menu-item.bp3-intent-warning.bp3-active::after,
    .bp3-menu-item.bp3-intent-warning.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-danger{
    color:#c23030; }
    .bp3-menu-item.bp3-intent-danger .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-danger::before, .bp3-menu-item.bp3-intent-danger::after,
    .bp3-menu-item.bp3-intent-danger .bp3-menu-item-label{
      color:#c23030; }
    .bp3-menu-item.bp3-intent-danger:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-menu-item.bp3-intent-danger.bp3-active{
      background-color:#db3737; }
    .bp3-menu-item.bp3-intent-danger:active{
      background-color:#c23030; }
    .bp3-menu-item.bp3-intent-danger:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-menu-item.bp3-intent-danger:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-menu-item.bp3-intent-danger:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-danger:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-danger:active, .bp3-menu-item.bp3-intent-danger:active::before, .bp3-menu-item.bp3-intent-danger:active::after,
    .bp3-menu-item.bp3-intent-danger:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-danger.bp3-active, .bp3-menu-item.bp3-intent-danger.bp3-active::before, .bp3-menu-item.bp3-intent-danger.bp3-active::after,
    .bp3-menu-item.bp3-intent-danger.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item::before{
    line-height:1;
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-weight:400;
    font-style:normal;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    margin-right:7px; }
  .bp3-menu-item::before,
  .bp3-menu-item > .bp3-icon{
    margin-top:2px;
    color:#5c7080; }
  .bp3-menu-item .bp3-menu-item-label{
    color:#5c7080; }
  .bp3-menu-item:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
    color:inherit; }
  .bp3-menu-item.bp3-active, .bp3-menu-item:active{
    background-color:rgba(115, 134, 148, 0.3); }
  .bp3-menu-item.bp3-disabled{
    outline:none !important;
    background-color:inherit !important;
    cursor:not-allowed !important;
    color:rgba(92, 112, 128, 0.6) !important; }
    .bp3-menu-item.bp3-disabled::before,
    .bp3-menu-item.bp3-disabled > .bp3-icon,
    .bp3-menu-item.bp3-disabled .bp3-menu-item-label{
      color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-large .bp3-menu-item{
    padding:9px 7px;
    line-height:22px;
    font-size:16px; }
    .bp3-large .bp3-menu-item .bp3-icon{
      margin-top:3px; }
    .bp3-large .bp3-menu-item::before{
      line-height:1;
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-weight:400;
      font-style:normal;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased;
      margin-top:1px;
      margin-right:10px; }

button.bp3-menu-item{
  border:none;
  background:none;
  width:100%;
  text-align:left; }
.bp3-menu-header{
  display:block;
  margin:5px;
  border-top:1px solid rgba(16, 22, 26, 0.15);
  cursor:default;
  padding-left:2px; }
  .bp3-dark .bp3-menu-header{
    border-top-color:rgba(255, 255, 255, 0.15); }
  .bp3-menu-header:first-of-type{
    border-top:none; }
  .bp3-menu-header > h6{
    color:#182026;
    font-weight:600;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    margin:0;
    padding:10px 7px 0 1px;
    line-height:17px; }
    .bp3-dark .bp3-menu-header > h6{
      color:#f5f8fa; }
  .bp3-menu-header:first-of-type > h6{
    padding-top:0; }
  .bp3-large .bp3-menu-header > h6{
    padding-top:15px;
    padding-bottom:5px;
    font-size:18px; }
  .bp3-large .bp3-menu-header:first-of-type > h6{
    padding-top:0; }

.bp3-dark .bp3-menu{
  background:#30404d;
  color:#f5f8fa; }

.bp3-dark .bp3-menu-item.bp3-intent-primary{
  color:#48aff0; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary .bp3-icon{
    color:inherit; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary::before, .bp3-dark .bp3-menu-item.bp3-intent-primary::after,
  .bp3-dark .bp3-menu-item.bp3-intent-primary .bp3-menu-item-label{
    color:#48aff0; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active{
    background-color:#137cbd; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary:active{
    background-color:#106ba3; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-primary:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-primary:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after,
  .bp3-dark .bp3-menu-item.bp3-intent-primary:hover .bp3-menu-item-label,
  .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label,
  .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-primary:active, .bp3-dark .bp3-menu-item.bp3-intent-primary:active::before, .bp3-dark .bp3-menu-item.bp3-intent-primary:active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-primary:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active .bp3-menu-item-label{
    color:#ffffff; }

.bp3-dark .bp3-menu-item.bp3-intent-success{
  color:#3dcc91; }
  .bp3-dark .bp3-menu-item.bp3-intent-success .bp3-icon{
    color:inherit; }
  .bp3-dark .bp3-menu-item.bp3-intent-success::before, .bp3-dark .bp3-menu-item.bp3-intent-success::after,
  .bp3-dark .bp3-menu-item.bp3-intent-success .bp3-menu-item-label{
    color:#3dcc91; }
  .bp3-dark .bp3-menu-item.bp3-intent-success:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active{
    background-color:#0f9960; }
  .bp3-dark .bp3-menu-item.bp3-intent-success:active{
    background-color:#0d8050; }
  .bp3-dark .bp3-menu-item.bp3-intent-success:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-success:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-success:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after,
  .bp3-dark .bp3-menu-item.bp3-intent-success:hover .bp3-menu-item-label,
  .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label,
  .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-success:active, .bp3-dark .bp3-menu-item.bp3-intent-success:active::before, .bp3-dark .bp3-menu-item.bp3-intent-success:active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-success:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active .bp3-menu-item-label{
    color:#ffffff; }

.bp3-dark .bp3-menu-item.bp3-intent-warning{
  color:#ffb366; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning .bp3-icon{
    color:inherit; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning::before, .bp3-dark .bp3-menu-item.bp3-intent-warning::after,
  .bp3-dark .bp3-menu-item.bp3-intent-warning .bp3-menu-item-label{
    color:#ffb366; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active{
    background-color:#d9822b; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning:active{
    background-color:#bf7326; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-warning:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-warning:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after,
  .bp3-dark .bp3-menu-item.bp3-intent-warning:hover .bp3-menu-item-label,
  .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label,
  .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-warning:active, .bp3-dark .bp3-menu-item.bp3-intent-warning:active::before, .bp3-dark .bp3-menu-item.bp3-intent-warning:active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-warning:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active .bp3-menu-item-label{
    color:#ffffff; }

.bp3-dark .bp3-menu-item.bp3-intent-danger{
  color:#ff7373; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger .bp3-icon{
    color:inherit; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger::before, .bp3-dark .bp3-menu-item.bp3-intent-danger::after,
  .bp3-dark .bp3-menu-item.bp3-intent-danger .bp3-menu-item-label{
    color:#ff7373; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active{
    background-color:#db3737; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger:active{
    background-color:#c23030; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-danger:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-danger:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after,
  .bp3-dark .bp3-menu-item.bp3-intent-danger:hover .bp3-menu-item-label,
  .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label,
  .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-danger:active, .bp3-dark .bp3-menu-item.bp3-intent-danger:active::before, .bp3-dark .bp3-menu-item.bp3-intent-danger:active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-danger:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active .bp3-menu-item-label{
    color:#ffffff; }

.bp3-dark .bp3-menu-item::before,
.bp3-dark .bp3-menu-item > .bp3-icon{
  color:#a7b6c2; }

.bp3-dark .bp3-menu-item .bp3-menu-item-label{
  color:#a7b6c2; }

.bp3-dark .bp3-menu-item.bp3-active, .bp3-dark .bp3-menu-item:active{
  background-color:rgba(138, 155, 168, 0.3); }

.bp3-dark .bp3-menu-item.bp3-disabled{
  color:rgba(167, 182, 194, 0.6) !important; }
  .bp3-dark .bp3-menu-item.bp3-disabled::before,
  .bp3-dark .bp3-menu-item.bp3-disabled > .bp3-icon,
  .bp3-dark .bp3-menu-item.bp3-disabled .bp3-menu-item-label{
    color:rgba(167, 182, 194, 0.6) !important; }

.bp3-dark .bp3-menu-divider,
.bp3-dark .bp3-menu-header{
  border-color:rgba(255, 255, 255, 0.15); }

.bp3-dark .bp3-menu-header > h6{
  color:#f5f8fa; }

.bp3-label .bp3-menu{
  margin-top:5px; }
.bp3-navbar{
  position:relative;
  z-index:10;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  background-color:#ffffff;
  width:100%;
  height:50px;
  padding:0 15px; }
  .bp3-navbar.bp3-dark,
  .bp3-dark .bp3-navbar{
    background-color:#394b59; }
  .bp3-navbar.bp3-dark{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-navbar{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-navbar.bp3-fixed-top{
    position:fixed;
    top:0;
    right:0;
    left:0; }

.bp3-navbar-heading{
  margin-right:15px;
  font-size:16px; }

.bp3-navbar-group{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  height:50px; }
  .bp3-navbar-group.bp3-align-left{
    float:left; }
  .bp3-navbar-group.bp3-align-right{
    float:right; }

.bp3-navbar-divider{
  margin:0 10px;
  border-left:1px solid rgba(16, 22, 26, 0.15);
  height:20px; }
  .bp3-dark .bp3-navbar-divider{
    border-left-color:rgba(255, 255, 255, 0.15); }
.bp3-non-ideal-state{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  width:100%;
  height:100%;
  text-align:center; }
  .bp3-non-ideal-state > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-non-ideal-state > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-non-ideal-state::before,
  .bp3-non-ideal-state > *{
    margin-bottom:20px; }
  .bp3-non-ideal-state:empty::before,
  .bp3-non-ideal-state > :last-child{
    margin-bottom:0; }
  .bp3-non-ideal-state > *{
    max-width:400px; }

.bp3-non-ideal-state-visual{
  color:rgba(92, 112, 128, 0.6);
  font-size:60px; }
  .bp3-dark .bp3-non-ideal-state-visual{
    color:rgba(167, 182, 194, 0.6); }

.bp3-overflow-list{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-wrap:nowrap;
      flex-wrap:nowrap;
  min-width:0; }

.bp3-overflow-list-spacer{
  -ms-flex-negative:1;
      flex-shrink:1;
  width:1px; }

body.bp3-overlay-open{
  overflow:hidden; }

.bp3-overlay{
  position:static;
  top:0;
  right:0;
  bottom:0;
  left:0;
  z-index:20; }
  .bp3-overlay:not(.bp3-overlay-open){
    pointer-events:none; }
  .bp3-overlay.bp3-overlay-container{
    position:fixed;
    overflow:hidden; }
    .bp3-overlay.bp3-overlay-container.bp3-overlay-inline{
      position:absolute; }
  .bp3-overlay.bp3-overlay-scroll-container{
    position:fixed;
    overflow:auto; }
    .bp3-overlay.bp3-overlay-scroll-container.bp3-overlay-inline{
      position:absolute; }
  .bp3-overlay.bp3-overlay-inline{
    display:inline;
    overflow:visible; }

.bp3-overlay-content{
  position:fixed;
  z-index:20; }
  .bp3-overlay-inline .bp3-overlay-content,
  .bp3-overlay-scroll-container .bp3-overlay-content{
    position:absolute; }

.bp3-overlay-backdrop{
  position:fixed;
  top:0;
  right:0;
  bottom:0;
  left:0;
  opacity:1;
  z-index:20;
  background-color:rgba(16, 22, 26, 0.7);
  overflow:auto;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-overlay-backdrop.bp3-overlay-enter, .bp3-overlay-backdrop.bp3-overlay-appear{
    opacity:0; }
  .bp3-overlay-backdrop.bp3-overlay-enter-active, .bp3-overlay-backdrop.bp3-overlay-appear-active{
    opacity:1;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-overlay-backdrop.bp3-overlay-exit{
    opacity:1; }
  .bp3-overlay-backdrop.bp3-overlay-exit-active{
    opacity:0;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-overlay-backdrop:focus{
    outline:none; }
  .bp3-overlay-inline .bp3-overlay-backdrop{
    position:absolute; }
.bp3-panel-stack{
  position:relative;
  overflow:hidden; }

.bp3-panel-stack-header{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-negative:0;
      flex-shrink:0;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  z-index:1;
  -webkit-box-shadow:0 1px rgba(16, 22, 26, 0.15);
          box-shadow:0 1px rgba(16, 22, 26, 0.15);
  height:30px; }
  .bp3-dark .bp3-panel-stack-header{
    -webkit-box-shadow:0 1px rgba(255, 255, 255, 0.15);
            box-shadow:0 1px rgba(255, 255, 255, 0.15); }
  .bp3-panel-stack-header > span{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-flex:1;
        -ms-flex:1;
            flex:1;
    -webkit-box-align:stretch;
        -ms-flex-align:stretch;
            align-items:stretch; }
  .bp3-panel-stack-header .bp3-heading{
    margin:0 5px; }

.bp3-button.bp3-panel-stack-header-back{
  margin-left:5px;
  padding-left:0;
  white-space:nowrap; }
  .bp3-button.bp3-panel-stack-header-back .bp3-icon{
    margin:0 2px; }

.bp3-panel-stack-view{
  position:absolute;
  top:0;
  right:0;
  bottom:0;
  left:0;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin-right:-1px;
  border-right:1px solid rgba(16, 22, 26, 0.15);
  background-color:#ffffff;
  overflow-y:auto; }
  .bp3-dark .bp3-panel-stack-view{
    background-color:#30404d; }

.bp3-panel-stack-push .bp3-panel-stack-enter, .bp3-panel-stack-push .bp3-panel-stack-appear{
  -webkit-transform:translateX(100%);
          transform:translateX(100%);
  opacity:0; }

.bp3-panel-stack-push .bp3-panel-stack-enter-active, .bp3-panel-stack-push .bp3-panel-stack-appear-active{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease;
  -webkit-transition-delay:0;
          transition-delay:0; }

.bp3-panel-stack-push .bp3-panel-stack-exit{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1; }

.bp3-panel-stack-push .bp3-panel-stack-exit-active{
  -webkit-transform:translateX(-50%);
          transform:translateX(-50%);
  opacity:0;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease;
  -webkit-transition-delay:0;
          transition-delay:0; }

.bp3-panel-stack-pop .bp3-panel-stack-enter, .bp3-panel-stack-pop .bp3-panel-stack-appear{
  -webkit-transform:translateX(-50%);
          transform:translateX(-50%);
  opacity:0; }

.bp3-panel-stack-pop .bp3-panel-stack-enter-active, .bp3-panel-stack-pop .bp3-panel-stack-appear-active{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease;
  -webkit-transition-delay:0;
          transition-delay:0; }

.bp3-panel-stack-pop .bp3-panel-stack-exit{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1; }

.bp3-panel-stack-pop .bp3-panel-stack-exit-active{
  -webkit-transform:translateX(100%);
          transform:translateX(100%);
  opacity:0;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease;
  -webkit-transition-delay:0;
          transition-delay:0; }
.bp3-popover{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  -webkit-transform:scale(1);
          transform:scale(1);
  display:inline-block;
  z-index:20;
  border-radius:3px; }
  .bp3-popover .bp3-popover-arrow{
    position:absolute;
    width:30px;
    height:30px; }
    .bp3-popover .bp3-popover-arrow::before{
      margin:5px;
      width:20px;
      height:20px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover{
    margin-top:-17px;
    margin-bottom:17px; }
    .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow{
      bottom:-11px; }
      .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(-90deg);
                transform:rotate(-90deg); }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover{
    margin-left:17px; }
    .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow{
      left:-11px; }
      .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(0);
                transform:rotate(0); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover{
    margin-top:17px; }
    .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow{
      top:-11px; }
      .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(90deg);
                transform:rotate(90deg); }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover{
    margin-right:17px;
    margin-left:-17px; }
    .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow{
      right:-11px; }
      .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(180deg);
                transform:rotate(180deg); }
  .bp3-tether-element-attached-middle > .bp3-popover > .bp3-popover-arrow{
    top:50%;
    -webkit-transform:translateY(-50%);
            transform:translateY(-50%); }
  .bp3-tether-element-attached-center > .bp3-popover > .bp3-popover-arrow{
    right:50%;
    -webkit-transform:translateX(50%);
            transform:translateX(50%); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow{
    top:-0.3934px; }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow{
    right:-0.3934px; }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow{
    left:-0.3934px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow{
    bottom:-0.3934px; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:top left;
            transform-origin:top left; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:top center;
            transform-origin:top center; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:top right;
            transform-origin:top right; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:center left;
            transform-origin:center left; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:center center;
            transform-origin:center center; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:center right;
            transform-origin:center right; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:bottom left;
            transform-origin:bottom left; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:bottom center;
            transform-origin:bottom center; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:bottom right;
            transform-origin:bottom right; }
  .bp3-popover .bp3-popover-content{
    background:#ffffff;
    color:inherit; }
  .bp3-popover .bp3-popover-arrow::before{
    -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2);
            box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2); }
  .bp3-popover .bp3-popover-arrow-border{
    fill:#10161a;
    fill-opacity:0.1; }
  .bp3-popover .bp3-popover-arrow-fill{
    fill:#ffffff; }
  .bp3-popover-enter > .bp3-popover, .bp3-popover-appear > .bp3-popover{
    -webkit-transform:scale(0.3);
            transform:scale(0.3); }
  .bp3-popover-enter-active > .bp3-popover, .bp3-popover-appear-active > .bp3-popover{
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-popover-exit > .bp3-popover{
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-popover-exit-active > .bp3-popover{
    -webkit-transform:scale(0.3);
            transform:scale(0.3);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-popover .bp3-popover-content{
    position:relative;
    border-radius:3px; }
  .bp3-popover.bp3-popover-content-sizing .bp3-popover-content{
    max-width:350px;
    padding:20px; }
  .bp3-popover-target + .bp3-overlay .bp3-popover.bp3-popover-content-sizing{
    width:350px; }
  .bp3-popover.bp3-minimal{
    margin:0 !important; }
    .bp3-popover.bp3-minimal .bp3-popover-arrow{
      display:none; }
    .bp3-popover.bp3-minimal.bp3-popover{
      -webkit-transform:scale(1);
              transform:scale(1); }
      .bp3-popover-enter > .bp3-popover.bp3-minimal.bp3-popover, .bp3-popover-appear > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1); }
      .bp3-popover-enter-active > .bp3-popover.bp3-minimal.bp3-popover, .bp3-popover-appear-active > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1);
        -webkit-transition-property:-webkit-transform;
        transition-property:-webkit-transform;
        transition-property:transform;
        transition-property:transform, -webkit-transform;
        -webkit-transition-duration:100ms;
                transition-duration:100ms;
        -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
                transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
        -webkit-transition-delay:0;
                transition-delay:0; }
      .bp3-popover-exit > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1); }
      .bp3-popover-exit-active > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1);
        -webkit-transition-property:-webkit-transform;
        transition-property:-webkit-transform;
        transition-property:transform;
        transition-property:transform, -webkit-transform;
        -webkit-transition-duration:100ms;
                transition-duration:100ms;
        -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
                transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
        -webkit-transition-delay:0;
                transition-delay:0; }
  .bp3-popover.bp3-dark,
  .bp3-dark .bp3-popover{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
    .bp3-popover.bp3-dark .bp3-popover-content,
    .bp3-dark .bp3-popover .bp3-popover-content{
      background:#30404d;
      color:inherit; }
    .bp3-popover.bp3-dark .bp3-popover-arrow::before,
    .bp3-dark .bp3-popover .bp3-popover-arrow::before{
      -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4);
              box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4); }
    .bp3-popover.bp3-dark .bp3-popover-arrow-border,
    .bp3-dark .bp3-popover .bp3-popover-arrow-border{
      fill:#10161a;
      fill-opacity:0.2; }
    .bp3-popover.bp3-dark .bp3-popover-arrow-fill,
    .bp3-dark .bp3-popover .bp3-popover-arrow-fill{
      fill:#30404d; }

.bp3-popover-arrow::before{
  display:block;
  position:absolute;
  -webkit-transform:rotate(45deg);
          transform:rotate(45deg);
  border-radius:2px;
  content:""; }

.bp3-tether-pinned .bp3-popover-arrow{
  display:none; }

.bp3-popover-backdrop{
  background:rgba(255, 255, 255, 0); }

.bp3-transition-container{
  opacity:1;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  z-index:20; }
  .bp3-transition-container.bp3-popover-enter, .bp3-transition-container.bp3-popover-appear{
    opacity:0; }
  .bp3-transition-container.bp3-popover-enter-active, .bp3-transition-container.bp3-popover-appear-active{
    opacity:1;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-transition-container.bp3-popover-exit{
    opacity:1; }
  .bp3-transition-container.bp3-popover-exit-active{
    opacity:0;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-transition-container:focus{
    outline:none; }
  .bp3-transition-container.bp3-popover-leave .bp3-popover-content{
    pointer-events:none; }
  .bp3-transition-container[data-x-out-of-boundaries]{
    display:none; }

span.bp3-popover-target{
  display:inline-block; }

.bp3-popover-wrapper.bp3-fill{
  width:100%; }

.bp3-portal{
  position:absolute;
  top:0;
  right:0;
  left:0; }
@-webkit-keyframes linear-progress-bar-stripes{
  from{
    background-position:0 0; }
  to{
    background-position:30px 0; } }
@keyframes linear-progress-bar-stripes{
  from{
    background-position:0 0; }
  to{
    background-position:30px 0; } }

.bp3-progress-bar{
  display:block;
  position:relative;
  border-radius:40px;
  background:rgba(92, 112, 128, 0.2);
  width:100%;
  height:8px;
  overflow:hidden; }
  .bp3-progress-bar .bp3-progress-meter{
    position:absolute;
    border-radius:40px;
    background:linear-gradient(-45deg, rgba(255, 255, 255, 0.2) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.2) 50%, rgba(255, 255, 255, 0.2) 75%, transparent 75%);
    background-color:rgba(92, 112, 128, 0.8);
    background-size:30px 30px;
    width:100%;
    height:100%;
    -webkit-transition:width 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:width 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-progress-bar:not(.bp3-no-animation):not(.bp3-no-stripes) .bp3-progress-meter{
    animation:linear-progress-bar-stripes 300ms linear infinite reverse; }
  .bp3-progress-bar.bp3-no-stripes .bp3-progress-meter{
    background-image:none; }

.bp3-dark .bp3-progress-bar{
  background:rgba(16, 22, 26, 0.5); }
  .bp3-dark .bp3-progress-bar .bp3-progress-meter{
    background-color:#8a9ba8; }

.bp3-progress-bar.bp3-intent-primary .bp3-progress-meter{
  background-color:#137cbd; }

.bp3-progress-bar.bp3-intent-success .bp3-progress-meter{
  background-color:#0f9960; }

.bp3-progress-bar.bp3-intent-warning .bp3-progress-meter{
  background-color:#d9822b; }

.bp3-progress-bar.bp3-intent-danger .bp3-progress-meter{
  background-color:#db3737; }
@-webkit-keyframes skeleton-glow{
  from{
    border-color:rgba(206, 217, 224, 0.2);
    background:rgba(206, 217, 224, 0.2); }
  to{
    border-color:rgba(92, 112, 128, 0.2);
    background:rgba(92, 112, 128, 0.2); } }
@keyframes skeleton-glow{
  from{
    border-color:rgba(206, 217, 224, 0.2);
    background:rgba(206, 217, 224, 0.2); }
  to{
    border-color:rgba(92, 112, 128, 0.2);
    background:rgba(92, 112, 128, 0.2); } }
.bp3-skeleton{
  border-color:rgba(206, 217, 224, 0.2) !important;
  border-radius:2px;
  -webkit-box-shadow:none !important;
          box-shadow:none !important;
  background:rgba(206, 217, 224, 0.2);
  background-clip:padding-box !important;
  cursor:default;
  color:transparent !important;
  -webkit-animation:1000ms linear infinite alternate skeleton-glow;
          animation:1000ms linear infinite alternate skeleton-glow;
  pointer-events:none;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-skeleton::before, .bp3-skeleton::after,
  .bp3-skeleton *{
    visibility:hidden !important; }
.bp3-slider{
  width:100%;
  min-width:150px;
  height:40px;
  position:relative;
  outline:none;
  cursor:default;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-slider:hover{
    cursor:pointer; }
  .bp3-slider:active{
    cursor:-webkit-grabbing;
    cursor:grabbing; }
  .bp3-slider.bp3-disabled{
    opacity:0.5;
    cursor:not-allowed; }
  .bp3-slider.bp3-slider-unlabeled{
    height:16px; }

.bp3-slider-track,
.bp3-slider-progress{
  top:5px;
  right:0;
  left:0;
  height:6px;
  position:absolute; }

.bp3-slider-track{
  border-radius:3px;
  overflow:hidden; }

.bp3-slider-progress{
  background:rgba(92, 112, 128, 0.2); }
  .bp3-dark .bp3-slider-progress{
    background:rgba(16, 22, 26, 0.5); }
  .bp3-slider-progress.bp3-intent-primary{
    background-color:#137cbd; }
  .bp3-slider-progress.bp3-intent-success{
    background-color:#0f9960; }
  .bp3-slider-progress.bp3-intent-warning{
    background-color:#d9822b; }
  .bp3-slider-progress.bp3-intent-danger{
    background-color:#db3737; }

.bp3-slider-handle{
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
  background-color:#f5f8fa;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
  color:#182026;
  position:absolute;
  top:0;
  left:0;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
  cursor:pointer;
  width:16px;
  height:16px; }
  .bp3-slider-handle:hover{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#ebf1f5; }
  .bp3-slider-handle:active, .bp3-slider-handle.bp3-active{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#d8e1e8;
    background-image:none; }
  .bp3-slider-handle:disabled, .bp3-slider-handle.bp3-disabled{
    outline:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    background-color:rgba(206, 217, 224, 0.5);
    background-image:none;
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
    .bp3-slider-handle:disabled.bp3-active, .bp3-slider-handle:disabled.bp3-active:hover, .bp3-slider-handle.bp3-disabled.bp3-active, .bp3-slider-handle.bp3-disabled.bp3-active:hover{
      background:rgba(206, 217, 224, 0.7); }
  .bp3-slider-handle:focus{
    z-index:1; }
  .bp3-slider-handle:hover{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#ebf1f5;
    z-index:2;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
    cursor:-webkit-grab;
    cursor:grab; }
  .bp3-slider-handle.bp3-active{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#d8e1e8;
    background-image:none;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 1px rgba(16, 22, 26, 0.1);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 1px rgba(16, 22, 26, 0.1);
    cursor:-webkit-grabbing;
    cursor:grabbing; }
  .bp3-disabled .bp3-slider-handle{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:#bfccd6;
    pointer-events:none; }
  .bp3-dark .bp3-slider-handle{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#394b59;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
    color:#f5f8fa; }
    .bp3-dark .bp3-slider-handle:hover, .bp3-dark .bp3-slider-handle:active, .bp3-dark .bp3-slider-handle.bp3-active{
      color:#f5f8fa; }
    .bp3-dark .bp3-slider-handle:hover{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#30404d; }
    .bp3-dark .bp3-slider-handle:active, .bp3-dark .bp3-slider-handle.bp3-active{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#202b33;
      background-image:none; }
    .bp3-dark .bp3-slider-handle:disabled, .bp3-dark .bp3-slider-handle.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(57, 75, 89, 0.5);
      background-image:none;
      color:rgba(167, 182, 194, 0.6); }
      .bp3-dark .bp3-slider-handle:disabled.bp3-active, .bp3-dark .bp3-slider-handle.bp3-disabled.bp3-active{
        background:rgba(57, 75, 89, 0.7); }
    .bp3-dark .bp3-slider-handle .bp3-button-spinner .bp3-spinner-head{
      background:rgba(16, 22, 26, 0.5);
      stroke:#8a9ba8; }
    .bp3-dark .bp3-slider-handle, .bp3-dark .bp3-slider-handle:hover{
      background-color:#394b59; }
    .bp3-dark .bp3-slider-handle.bp3-active{
      background-color:#293742; }
  .bp3-dark .bp3-disabled .bp3-slider-handle{
    border-color:#5c7080;
    -webkit-box-shadow:none;
            box-shadow:none;
    background:#5c7080; }
  .bp3-slider-handle .bp3-slider-label{
    margin-left:8px;
    border-radius:3px;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
    background:#394b59;
    color:#f5f8fa; }
    .bp3-dark .bp3-slider-handle .bp3-slider-label{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
      background:#e1e8ed;
      color:#394b59; }
    .bp3-disabled .bp3-slider-handle .bp3-slider-label{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-slider-handle.bp3-start, .bp3-slider-handle.bp3-end{
    width:8px; }
  .bp3-slider-handle.bp3-start{
    border-top-right-radius:0;
    border-bottom-right-radius:0; }
  .bp3-slider-handle.bp3-end{
    margin-left:8px;
    border-top-left-radius:0;
    border-bottom-left-radius:0; }
    .bp3-slider-handle.bp3-end .bp3-slider-label{
      margin-left:0; }

.bp3-slider-label{
  -webkit-transform:translate(-50%, 20px);
          transform:translate(-50%, 20px);
  display:inline-block;
  position:absolute;
  padding:2px 5px;
  vertical-align:top;
  line-height:1;
  font-size:12px; }

.bp3-slider.bp3-vertical{
  width:40px;
  min-width:40px;
  height:150px; }
  .bp3-slider.bp3-vertical .bp3-slider-track,
  .bp3-slider.bp3-vertical .bp3-slider-progress{
    top:0;
    bottom:0;
    left:5px;
    width:6px;
    height:auto; }
  .bp3-slider.bp3-vertical .bp3-slider-progress{
    top:auto; }
  .bp3-slider.bp3-vertical .bp3-slider-label{
    -webkit-transform:translate(20px, 50%);
            transform:translate(20px, 50%); }
  .bp3-slider.bp3-vertical .bp3-slider-handle{
    top:auto; }
    .bp3-slider.bp3-vertical .bp3-slider-handle .bp3-slider-label{
      margin-top:-8px;
      margin-left:0; }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-end, .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start{
      margin-left:0;
      width:16px;
      height:8px; }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start{
      border-top-left-radius:0;
      border-bottom-right-radius:3px; }
      .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start .bp3-slider-label{
        -webkit-transform:translate(20px);
                transform:translate(20px); }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-end{
      margin-bottom:8px;
      border-top-left-radius:3px;
      border-bottom-left-radius:0;
      border-bottom-right-radius:0; }

@-webkit-keyframes pt-spinner-animation{
  from{
    -webkit-transform:rotate(0deg);
            transform:rotate(0deg); }
  to{
    -webkit-transform:rotate(360deg);
            transform:rotate(360deg); } }

@keyframes pt-spinner-animation{
  from{
    -webkit-transform:rotate(0deg);
            transform:rotate(0deg); }
  to{
    -webkit-transform:rotate(360deg);
            transform:rotate(360deg); } }

.bp3-spinner{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  overflow:visible;
  vertical-align:middle; }
  .bp3-spinner svg{
    display:block; }
  .bp3-spinner path{
    fill-opacity:0; }
  .bp3-spinner .bp3-spinner-head{
    -webkit-transform-origin:center;
            transform-origin:center;
    -webkit-transition:stroke-dashoffset 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:stroke-dashoffset 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    stroke:rgba(92, 112, 128, 0.8);
    stroke-linecap:round; }
  .bp3-spinner .bp3-spinner-track{
    stroke:rgba(92, 112, 128, 0.2); }

.bp3-spinner-animation{
  -webkit-animation:pt-spinner-animation 500ms linear infinite;
          animation:pt-spinner-animation 500ms linear infinite; }
  .bp3-no-spin > .bp3-spinner-animation{
    -webkit-animation:none;
            animation:none; }

.bp3-dark .bp3-spinner .bp3-spinner-head{
  stroke:#8a9ba8; }

.bp3-dark .bp3-spinner .bp3-spinner-track{
  stroke:rgba(16, 22, 26, 0.5); }

.bp3-spinner.bp3-intent-primary .bp3-spinner-head{
  stroke:#137cbd; }

.bp3-spinner.bp3-intent-success .bp3-spinner-head{
  stroke:#0f9960; }

.bp3-spinner.bp3-intent-warning .bp3-spinner-head{
  stroke:#d9822b; }

.bp3-spinner.bp3-intent-danger .bp3-spinner-head{
  stroke:#db3737; }
.bp3-tabs.bp3-vertical{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex; }
  .bp3-tabs.bp3-vertical > .bp3-tab-list{
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column;
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start; }
    .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab{
      border-radius:3px;
      width:100%;
      padding:0 10px; }
      .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab[aria-selected="true"]{
        -webkit-box-shadow:none;
                box-shadow:none;
        background-color:rgba(19, 124, 189, 0.2); }
    .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab-indicator-wrapper .bp3-tab-indicator{
      top:0;
      right:0;
      bottom:0;
      left:0;
      border-radius:3px;
      background-color:rgba(19, 124, 189, 0.2);
      height:auto; }
  .bp3-tabs.bp3-vertical > .bp3-tab-panel{
    margin-top:0;
    padding-left:20px; }

.bp3-tab-list{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  -webkit-box-align:end;
      -ms-flex-align:end;
          align-items:flex-end;
  position:relative;
  margin:0;
  border:none;
  padding:0;
  list-style:none; }
  .bp3-tab-list > *:not(:last-child){
    margin-right:20px; }

.bp3-tab{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  position:relative;
  cursor:pointer;
  max-width:100%;
  vertical-align:top;
  line-height:30px;
  color:#182026;
  font-size:14px; }
  .bp3-tab a{
    display:block;
    text-decoration:none;
    color:inherit; }
  .bp3-tab-indicator-wrapper ~ .bp3-tab{
    -webkit-box-shadow:none !important;
            box-shadow:none !important;
    background-color:transparent !important; }
  .bp3-tab[aria-disabled="true"]{
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-tab[aria-selected="true"]{
    border-radius:0;
    -webkit-box-shadow:inset 0 -3px 0 #106ba3;
            box-shadow:inset 0 -3px 0 #106ba3; }
  .bp3-tab[aria-selected="true"], .bp3-tab:not([aria-disabled="true"]):hover{
    color:#106ba3; }
  .bp3-tab:focus{
    -moz-outline-radius:0; }
  .bp3-large > .bp3-tab{
    line-height:40px;
    font-size:16px; }

.bp3-tab-panel{
  margin-top:20px; }
  .bp3-tab-panel[aria-hidden="true"]{
    display:none; }

.bp3-tab-indicator-wrapper{
  position:absolute;
  top:0;
  left:0;
  -webkit-transform:translateX(0), translateY(0);
          transform:translateX(0), translateY(0);
  -webkit-transition:height, width, -webkit-transform;
  transition:height, width, -webkit-transform;
  transition:height, transform, width;
  transition:height, transform, width, -webkit-transform;
  -webkit-transition-duration:200ms;
          transition-duration:200ms;
  -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
          transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
  pointer-events:none; }
  .bp3-tab-indicator-wrapper .bp3-tab-indicator{
    position:absolute;
    right:0;
    bottom:0;
    left:0;
    background-color:#106ba3;
    height:3px; }
  .bp3-tab-indicator-wrapper.bp3-no-animation{
    -webkit-transition:none;
    transition:none; }

.bp3-dark .bp3-tab{
  color:#f5f8fa; }
  .bp3-dark .bp3-tab[aria-disabled="true"]{
    color:rgba(167, 182, 194, 0.6); }
  .bp3-dark .bp3-tab[aria-selected="true"]{
    -webkit-box-shadow:inset 0 -3px 0 #48aff0;
            box-shadow:inset 0 -3px 0 #48aff0; }
  .bp3-dark .bp3-tab[aria-selected="true"], .bp3-dark .bp3-tab:not([aria-disabled="true"]):hover{
    color:#48aff0; }

.bp3-dark .bp3-tab-indicator{
  background-color:#48aff0; }

.bp3-flex-expander{
  -webkit-box-flex:1;
      -ms-flex:1 1;
          flex:1 1; }
.bp3-tag{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  position:relative;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:none;
          box-shadow:none;
  background-color:#5c7080;
  min-width:20px;
  max-width:100%;
  min-height:20px;
  padding:2px 6px;
  line-height:16px;
  color:#f5f8fa;
  font-size:12px; }
  .bp3-tag.bp3-interactive{
    cursor:pointer; }
    .bp3-tag.bp3-interactive:hover{
      background-color:rgba(92, 112, 128, 0.85); }
    .bp3-tag.bp3-interactive.bp3-active, .bp3-tag.bp3-interactive:active{
      background-color:rgba(92, 112, 128, 0.7); }
  .bp3-tag > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-tag > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-tag::before,
  .bp3-tag > *{
    margin-right:4px; }
  .bp3-tag:empty::before,
  .bp3-tag > :last-child{
    margin-right:0; }
  .bp3-tag:focus{
    outline:rgba(19, 124, 189, 0.6) auto 2px;
    outline-offset:0;
    -moz-outline-radius:6px; }
  .bp3-tag.bp3-round{
    border-radius:30px;
    padding-right:8px;
    padding-left:8px; }
  .bp3-dark .bp3-tag{
    background-color:#bfccd6;
    color:#182026; }
    .bp3-dark .bp3-tag.bp3-interactive{
      cursor:pointer; }
      .bp3-dark .bp3-tag.bp3-interactive:hover{
        background-color:rgba(191, 204, 214, 0.85); }
      .bp3-dark .bp3-tag.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-interactive:active{
        background-color:rgba(191, 204, 214, 0.7); }
    .bp3-dark .bp3-tag > .bp3-icon, .bp3-dark .bp3-tag .bp3-icon-standard, .bp3-dark .bp3-tag .bp3-icon-large{
      fill:currentColor; }
  .bp3-tag > .bp3-icon, .bp3-tag .bp3-icon-standard, .bp3-tag .bp3-icon-large{
    fill:#ffffff; }
  .bp3-tag.bp3-large,
  .bp3-large .bp3-tag{
    min-width:30px;
    min-height:30px;
    padding:0 10px;
    line-height:20px;
    font-size:14px; }
    .bp3-tag.bp3-large::before,
    .bp3-tag.bp3-large > *,
    .bp3-large .bp3-tag::before,
    .bp3-large .bp3-tag > *{
      margin-right:7px; }
    .bp3-tag.bp3-large:empty::before,
    .bp3-tag.bp3-large > :last-child,
    .bp3-large .bp3-tag:empty::before,
    .bp3-large .bp3-tag > :last-child{
      margin-right:0; }
    .bp3-tag.bp3-large.bp3-round,
    .bp3-large .bp3-tag.bp3-round{
      padding-right:12px;
      padding-left:12px; }
  .bp3-tag.bp3-intent-primary{
    background:#137cbd;
    color:#ffffff; }
    .bp3-tag.bp3-intent-primary.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-primary.bp3-interactive:hover{
        background-color:rgba(19, 124, 189, 0.85); }
      .bp3-tag.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-primary.bp3-interactive:active{
        background-color:rgba(19, 124, 189, 0.7); }
  .bp3-tag.bp3-intent-success{
    background:#0f9960;
    color:#ffffff; }
    .bp3-tag.bp3-intent-success.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-success.bp3-interactive:hover{
        background-color:rgba(15, 153, 96, 0.85); }
      .bp3-tag.bp3-intent-success.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-success.bp3-interactive:active{
        background-color:rgba(15, 153, 96, 0.7); }
  .bp3-tag.bp3-intent-warning{
    background:#d9822b;
    color:#ffffff; }
    .bp3-tag.bp3-intent-warning.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-warning.bp3-interactive:hover{
        background-color:rgba(217, 130, 43, 0.85); }
      .bp3-tag.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-warning.bp3-interactive:active{
        background-color:rgba(217, 130, 43, 0.7); }
  .bp3-tag.bp3-intent-danger{
    background:#db3737;
    color:#ffffff; }
    .bp3-tag.bp3-intent-danger.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-danger.bp3-interactive:hover{
        background-color:rgba(219, 55, 55, 0.85); }
      .bp3-tag.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-danger.bp3-interactive:active{
        background-color:rgba(219, 55, 55, 0.7); }
  .bp3-tag.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-tag.bp3-minimal > .bp3-icon, .bp3-tag.bp3-minimal .bp3-icon-standard, .bp3-tag.bp3-minimal .bp3-icon-large{
    fill:#5c7080; }
  .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]){
    background-color:rgba(138, 155, 168, 0.2);
    color:#182026; }
    .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:hover{
        background-color:rgba(92, 112, 128, 0.3); }
      .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive.bp3-active, .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:active{
        background-color:rgba(92, 112, 128, 0.4); }
    .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]){
      color:#f5f8fa; }
      .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:hover{
          background-color:rgba(191, 204, 214, 0.3); }
        .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:active{
          background-color:rgba(191, 204, 214, 0.4); }
      .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) > .bp3-icon, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) .bp3-icon-standard, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) .bp3-icon-large{
        fill:#a7b6c2; }
  .bp3-tag.bp3-minimal.bp3-intent-primary{
    background-color:rgba(19, 124, 189, 0.15);
    color:#106ba3; }
    .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:hover{
        background-color:rgba(19, 124, 189, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:active{
        background-color:rgba(19, 124, 189, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-primary > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-primary .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-primary .bp3-icon-large{
      fill:#137cbd; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary{
      background-color:rgba(19, 124, 189, 0.25);
      color:#48aff0; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:hover{
          background-color:rgba(19, 124, 189, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:active{
          background-color:rgba(19, 124, 189, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-success{
    background-color:rgba(15, 153, 96, 0.15);
    color:#0d8050; }
    .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:hover{
        background-color:rgba(15, 153, 96, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:active{
        background-color:rgba(15, 153, 96, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-success > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-success .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-success .bp3-icon-large{
      fill:#0f9960; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success{
      background-color:rgba(15, 153, 96, 0.25);
      color:#3dcc91; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:hover{
          background-color:rgba(15, 153, 96, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:active{
          background-color:rgba(15, 153, 96, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-warning{
    background-color:rgba(217, 130, 43, 0.15);
    color:#bf7326; }
    .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:hover{
        background-color:rgba(217, 130, 43, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:active{
        background-color:rgba(217, 130, 43, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-warning > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-warning .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-warning .bp3-icon-large{
      fill:#d9822b; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning{
      background-color:rgba(217, 130, 43, 0.25);
      color:#ffb366; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:hover{
          background-color:rgba(217, 130, 43, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:active{
          background-color:rgba(217, 130, 43, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-danger{
    background-color:rgba(219, 55, 55, 0.15);
    color:#c23030; }
    .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:hover{
        background-color:rgba(219, 55, 55, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:active{
        background-color:rgba(219, 55, 55, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-danger > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-danger .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-danger .bp3-icon-large{
      fill:#db3737; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger{
      background-color:rgba(219, 55, 55, 0.25);
      color:#ff7373; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:hover{
          background-color:rgba(219, 55, 55, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:active{
          background-color:rgba(219, 55, 55, 0.45); }

.bp3-tag-remove{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  opacity:0.5;
  margin-top:-2px;
  margin-right:-6px !important;
  margin-bottom:-2px;
  border:none;
  background:none;
  cursor:pointer;
  padding:2px;
  padding-left:0;
  color:inherit; }
  .bp3-tag-remove:hover{
    opacity:0.8;
    background:none;
    text-decoration:none; }
  .bp3-tag-remove:active{
    opacity:1; }
  .bp3-tag-remove:empty::before{
    line-height:1;
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-weight:400;
    font-style:normal;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    content:""; }
  .bp3-large .bp3-tag-remove{
    margin-right:-10px !important;
    padding:5px;
    padding-left:0; }
    .bp3-large .bp3-tag-remove:empty::before{
      line-height:1;
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-weight:400;
      font-style:normal; }
.bp3-tag-input{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  cursor:text;
  height:auto;
  min-height:30px;
  padding-right:0;
  padding-left:5px;
  line-height:inherit; }
  .bp3-tag-input > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-tag-input > .bp3-tag-input-values{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-tag-input .bp3-tag-input-icon{
    margin-top:7px;
    margin-right:7px;
    margin-left:2px;
    color:#5c7080; }
  .bp3-tag-input .bp3-tag-input-values{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-orient:horizontal;
    -webkit-box-direction:normal;
        -ms-flex-direction:row;
            flex-direction:row;
    -ms-flex-wrap:wrap;
        flex-wrap:wrap;
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center;
    -ms-flex-item-align:stretch;
        align-self:stretch;
    margin-top:5px;
    margin-right:7px;
    min-width:0; }
    .bp3-tag-input .bp3-tag-input-values > *{
      -webkit-box-flex:0;
          -ms-flex-positive:0;
              flex-grow:0;
      -ms-flex-negative:0;
          flex-shrink:0; }
    .bp3-tag-input .bp3-tag-input-values > .bp3-fill{
      -webkit-box-flex:1;
          -ms-flex-positive:1;
              flex-grow:1;
      -ms-flex-negative:1;
          flex-shrink:1; }
    .bp3-tag-input .bp3-tag-input-values::before,
    .bp3-tag-input .bp3-tag-input-values > *{
      margin-right:5px; }
    .bp3-tag-input .bp3-tag-input-values:empty::before,
    .bp3-tag-input .bp3-tag-input-values > :last-child{
      margin-right:0; }
    .bp3-tag-input .bp3-tag-input-values:first-child .bp3-input-ghost:first-child{
      padding-left:5px; }
    .bp3-tag-input .bp3-tag-input-values > *{
      margin-bottom:5px; }
  .bp3-tag-input .bp3-tag{
    overflow-wrap:break-word; }
    .bp3-tag-input .bp3-tag.bp3-active{
      outline:rgba(19, 124, 189, 0.6) auto 2px;
      outline-offset:0;
      -moz-outline-radius:6px; }
  .bp3-tag-input .bp3-input-ghost{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    width:80px;
    line-height:20px; }
    .bp3-tag-input .bp3-input-ghost:disabled, .bp3-tag-input .bp3-input-ghost.bp3-disabled{
      cursor:not-allowed; }
  .bp3-tag-input .bp3-button,
  .bp3-tag-input .bp3-spinner{
    margin:3px;
    margin-left:0; }
  .bp3-tag-input .bp3-button{
    min-width:24px;
    min-height:24px;
    padding:0 7px; }
  .bp3-tag-input.bp3-large{
    height:auto;
    min-height:40px; }
    .bp3-tag-input.bp3-large::before,
    .bp3-tag-input.bp3-large > *{
      margin-right:10px; }
    .bp3-tag-input.bp3-large:empty::before,
    .bp3-tag-input.bp3-large > :last-child{
      margin-right:0; }
    .bp3-tag-input.bp3-large .bp3-tag-input-icon{
      margin-top:10px;
      margin-left:5px; }
    .bp3-tag-input.bp3-large .bp3-input-ghost{
      line-height:30px; }
    .bp3-tag-input.bp3-large .bp3-button{
      min-width:30px;
      min-height:30px;
      padding:5px 10px;
      margin:5px;
      margin-left:0; }
    .bp3-tag-input.bp3-large .bp3-spinner{
      margin:8px;
      margin-left:0; }
  .bp3-tag-input.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
    background-color:#ffffff; }
    .bp3-tag-input.bp3-active.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-success{
      -webkit-box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-tag-input .bp3-tag-input-icon, .bp3-tag-input.bp3-dark .bp3-tag-input-icon{
    color:#a7b6c2; }
  .bp3-dark .bp3-tag-input .bp3-input-ghost, .bp3-tag-input.bp3-dark .bp3-input-ghost{
    color:#f5f8fa; }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-webkit-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-moz-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost:-ms-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-ms-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::placeholder{
      color:rgba(167, 182, 194, 0.6); }
  .bp3-dark .bp3-tag-input.bp3-active, .bp3-tag-input.bp3-dark.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background-color:rgba(16, 22, 26, 0.3); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-primary, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-success, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-success{
      -webkit-box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-warning, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-danger, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-input-ghost{
  border:none;
  -webkit-box-shadow:none;
          box-shadow:none;
  background:none;
  padding:0; }
  .bp3-input-ghost::-webkit-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost::-moz-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost:-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost::-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost::placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost:focus{
    outline:none !important; }
.bp3-toast{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  position:relative !important;
  margin:20px 0 0;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  background-color:#ffffff;
  min-width:300px;
  max-width:500px;
  pointer-events:all; }
  .bp3-toast.bp3-toast-enter, .bp3-toast.bp3-toast-appear{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px); }
  .bp3-toast.bp3-toast-enter-active, .bp3-toast.bp3-toast-appear-active{
    -webkit-transform:translateY(0);
            transform:translateY(0);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-toast.bp3-toast-enter ~ .bp3-toast, .bp3-toast.bp3-toast-appear ~ .bp3-toast{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px); }
  .bp3-toast.bp3-toast-enter-active ~ .bp3-toast, .bp3-toast.bp3-toast-appear-active ~ .bp3-toast{
    -webkit-transform:translateY(0);
            transform:translateY(0);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-toast.bp3-toast-exit{
    opacity:1;
    -webkit-filter:blur(0);
            filter:blur(0); }
  .bp3-toast.bp3-toast-exit-active{
    opacity:0;
    -webkit-filter:blur(10px);
            filter:blur(10px);
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:opacity, filter;
    transition-property:opacity, filter, -webkit-filter;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-toast.bp3-toast-exit ~ .bp3-toast{
    -webkit-transform:translateY(0);
            transform:translateY(0); }
  .bp3-toast.bp3-toast-exit-active ~ .bp3-toast{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:50ms;
            transition-delay:50ms; }
  .bp3-toast .bp3-button-group{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    padding:5px;
    padding-left:0; }
  .bp3-toast > .bp3-icon{
    margin:12px;
    margin-right:0;
    color:#5c7080; }
  .bp3-toast.bp3-dark,
  .bp3-dark .bp3-toast{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
    background-color:#394b59; }
    .bp3-toast.bp3-dark > .bp3-icon,
    .bp3-dark .bp3-toast > .bp3-icon{
      color:#a7b6c2; }
  .bp3-toast[class*="bp3-intent-"] a{
    color:rgba(255, 255, 255, 0.7); }
    .bp3-toast[class*="bp3-intent-"] a:hover{
      color:#ffffff; }
  .bp3-toast[class*="bp3-intent-"] > .bp3-icon{
    color:#ffffff; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button, .bp3-toast[class*="bp3-intent-"] .bp3-button::before,
  .bp3-toast[class*="bp3-intent-"] .bp3-button .bp3-icon, .bp3-toast[class*="bp3-intent-"] .bp3-button:active{
    color:rgba(255, 255, 255, 0.7) !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:focus{
    outline-color:rgba(255, 255, 255, 0.5); }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:hover{
    background-color:rgba(255, 255, 255, 0.15) !important;
    color:#ffffff !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:active{
    background-color:rgba(255, 255, 255, 0.3) !important;
    color:#ffffff !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button::after{
    background:rgba(255, 255, 255, 0.3) !important; }
  .bp3-toast.bp3-intent-primary{
    background-color:#137cbd;
    color:#ffffff; }
  .bp3-toast.bp3-intent-success{
    background-color:#0f9960;
    color:#ffffff; }
  .bp3-toast.bp3-intent-warning{
    background-color:#d9822b;
    color:#ffffff; }
  .bp3-toast.bp3-intent-danger{
    background-color:#db3737;
    color:#ffffff; }

.bp3-toast-message{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  padding:11px;
  word-break:break-word; }

.bp3-toast-container{
  display:-webkit-box !important;
  display:-ms-flexbox !important;
  display:flex !important;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  position:fixed;
  right:0;
  left:0;
  z-index:40;
  overflow:hidden;
  padding:0 20px 20px;
  pointer-events:none; }
  .bp3-toast-container.bp3-toast-container-top{
    top:0;
    bottom:auto; }
  .bp3-toast-container.bp3-toast-container-bottom{
    -webkit-box-orient:vertical;
    -webkit-box-direction:reverse;
        -ms-flex-direction:column-reverse;
            flex-direction:column-reverse;
    top:auto;
    bottom:0; }
  .bp3-toast-container.bp3-toast-container-left{
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start; }
  .bp3-toast-container.bp3-toast-container-right{
    -webkit-box-align:end;
        -ms-flex-align:end;
            align-items:flex-end; }

.bp3-toast-container-bottom .bp3-toast.bp3-toast-enter:not(.bp3-toast-enter-active),
.bp3-toast-container-bottom .bp3-toast.bp3-toast-enter:not(.bp3-toast-enter-active) ~ .bp3-toast, .bp3-toast-container-bottom .bp3-toast.bp3-toast-appear:not(.bp3-toast-appear-active),
.bp3-toast-container-bottom .bp3-toast.bp3-toast-appear:not(.bp3-toast-appear-active) ~ .bp3-toast,
.bp3-toast-container-bottom .bp3-toast.bp3-toast-leave-active ~ .bp3-toast{
  -webkit-transform:translateY(60px);
          transform:translateY(60px); }
.bp3-tooltip{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  -webkit-transform:scale(1);
          transform:scale(1); }
  .bp3-tooltip .bp3-popover-arrow{
    position:absolute;
    width:22px;
    height:22px; }
    .bp3-tooltip .bp3-popover-arrow::before{
      margin:4px;
      width:14px;
      height:14px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip{
    margin-top:-11px;
    margin-bottom:11px; }
    .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow{
      bottom:-8px; }
      .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(-90deg);
                transform:rotate(-90deg); }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip{
    margin-left:11px; }
    .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow{
      left:-8px; }
      .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(0);
                transform:rotate(0); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip{
    margin-top:11px; }
    .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow{
      top:-8px; }
      .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(90deg);
                transform:rotate(90deg); }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip{
    margin-right:11px;
    margin-left:-11px; }
    .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow{
      right:-8px; }
      .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(180deg);
                transform:rotate(180deg); }
  .bp3-tether-element-attached-middle > .bp3-tooltip > .bp3-popover-arrow{
    top:50%;
    -webkit-transform:translateY(-50%);
            transform:translateY(-50%); }
  .bp3-tether-element-attached-center > .bp3-tooltip > .bp3-popover-arrow{
    right:50%;
    -webkit-transform:translateX(50%);
            transform:translateX(50%); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow{
    top:-0.22183px; }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow{
    right:-0.22183px; }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow{
    left:-0.22183px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow{
    bottom:-0.22183px; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:top left;
            transform-origin:top left; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:top center;
            transform-origin:top center; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:top right;
            transform-origin:top right; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:center left;
            transform-origin:center left; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:center center;
            transform-origin:center center; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:center right;
            transform-origin:center right; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:bottom left;
            transform-origin:bottom left; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:bottom center;
            transform-origin:bottom center; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:bottom right;
            transform-origin:bottom right; }
  .bp3-tooltip .bp3-popover-content{
    background:#394b59;
    color:#f5f8fa; }
  .bp3-tooltip .bp3-popover-arrow::before{
    -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2);
            box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2); }
  .bp3-tooltip .bp3-popover-arrow-border{
    fill:#10161a;
    fill-opacity:0.1; }
  .bp3-tooltip .bp3-popover-arrow-fill{
    fill:#394b59; }
  .bp3-popover-enter > .bp3-tooltip, .bp3-popover-appear > .bp3-tooltip{
    -webkit-transform:scale(0.8);
            transform:scale(0.8); }
  .bp3-popover-enter-active > .bp3-tooltip, .bp3-popover-appear-active > .bp3-tooltip{
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-popover-exit > .bp3-tooltip{
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-popover-exit-active > .bp3-tooltip{
    -webkit-transform:scale(0.8);
            transform:scale(0.8);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-tooltip .bp3-popover-content{
    padding:10px 12px; }
  .bp3-tooltip.bp3-dark,
  .bp3-dark .bp3-tooltip{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
    .bp3-tooltip.bp3-dark .bp3-popover-content,
    .bp3-dark .bp3-tooltip .bp3-popover-content{
      background:#e1e8ed;
      color:#394b59; }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow::before,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow::before{
      -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4);
              box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4); }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow-border,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow-border{
      fill:#10161a;
      fill-opacity:0.2; }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow-fill,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow-fill{
      fill:#e1e8ed; }
  .bp3-tooltip.bp3-intent-primary .bp3-popover-content{
    background:#137cbd;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-primary .bp3-popover-arrow-fill{
    fill:#137cbd; }
  .bp3-tooltip.bp3-intent-success .bp3-popover-content{
    background:#0f9960;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-success .bp3-popover-arrow-fill{
    fill:#0f9960; }
  .bp3-tooltip.bp3-intent-warning .bp3-popover-content{
    background:#d9822b;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-warning .bp3-popover-arrow-fill{
    fill:#d9822b; }
  .bp3-tooltip.bp3-intent-danger .bp3-popover-content{
    background:#db3737;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-danger .bp3-popover-arrow-fill{
    fill:#db3737; }

.bp3-tooltip-indicator{
  border-bottom:dotted 1px;
  cursor:help; }
.bp3-tree .bp3-icon, .bp3-tree .bp3-icon-standard, .bp3-tree .bp3-icon-large{
  color:#5c7080; }
  .bp3-tree .bp3-icon.bp3-intent-primary, .bp3-tree .bp3-icon-standard.bp3-intent-primary, .bp3-tree .bp3-icon-large.bp3-intent-primary{
    color:#137cbd; }
  .bp3-tree .bp3-icon.bp3-intent-success, .bp3-tree .bp3-icon-standard.bp3-intent-success, .bp3-tree .bp3-icon-large.bp3-intent-success{
    color:#0f9960; }
  .bp3-tree .bp3-icon.bp3-intent-warning, .bp3-tree .bp3-icon-standard.bp3-intent-warning, .bp3-tree .bp3-icon-large.bp3-intent-warning{
    color:#d9822b; }
  .bp3-tree .bp3-icon.bp3-intent-danger, .bp3-tree .bp3-icon-standard.bp3-intent-danger, .bp3-tree .bp3-icon-large.bp3-intent-danger{
    color:#db3737; }

.bp3-tree-node-list{
  margin:0;
  padding-left:0;
  list-style:none; }

.bp3-tree-root{
  position:relative;
  background-color:transparent;
  cursor:default;
  padding-left:0; }

.bp3-tree-node-content-0{
  padding-left:0px; }

.bp3-tree-node-content-1{
  padding-left:23px; }

.bp3-tree-node-content-2{
  padding-left:46px; }

.bp3-tree-node-content-3{
  padding-left:69px; }

.bp3-tree-node-content-4{
  padding-left:92px; }

.bp3-tree-node-content-5{
  padding-left:115px; }

.bp3-tree-node-content-6{
  padding-left:138px; }

.bp3-tree-node-content-7{
  padding-left:161px; }

.bp3-tree-node-content-8{
  padding-left:184px; }

.bp3-tree-node-content-9{
  padding-left:207px; }

.bp3-tree-node-content-10{
  padding-left:230px; }

.bp3-tree-node-content-11{
  padding-left:253px; }

.bp3-tree-node-content-12{
  padding-left:276px; }

.bp3-tree-node-content-13{
  padding-left:299px; }

.bp3-tree-node-content-14{
  padding-left:322px; }

.bp3-tree-node-content-15{
  padding-left:345px; }

.bp3-tree-node-content-16{
  padding-left:368px; }

.bp3-tree-node-content-17{
  padding-left:391px; }

.bp3-tree-node-content-18{
  padding-left:414px; }

.bp3-tree-node-content-19{
  padding-left:437px; }

.bp3-tree-node-content-20{
  padding-left:460px; }

.bp3-tree-node-content{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  width:100%;
  height:30px;
  padding-right:5px; }
  .bp3-tree-node-content:hover{
    background-color:rgba(191, 204, 214, 0.4); }

.bp3-tree-node-caret,
.bp3-tree-node-caret-none{
  min-width:30px; }

.bp3-tree-node-caret{
  color:#5c7080;
  -webkit-transform:rotate(0deg);
          transform:rotate(0deg);
  cursor:pointer;
  padding:7px;
  -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-tree-node-caret:hover{
    color:#182026; }
  .bp3-dark .bp3-tree-node-caret{
    color:#a7b6c2; }
    .bp3-dark .bp3-tree-node-caret:hover{
      color:#f5f8fa; }
  .bp3-tree-node-caret.bp3-tree-node-caret-open{
    -webkit-transform:rotate(90deg);
            transform:rotate(90deg); }
  .bp3-tree-node-caret.bp3-icon-standard::before{
    content:""; }

.bp3-tree-node-icon{
  position:relative;
  margin-right:7px; }

.bp3-tree-node-label{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  position:relative;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-tree-node-label span{
    display:inline; }

.bp3-tree-node-secondary-label{
  padding:0 5px;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-tree-node-secondary-label .bp3-popover-wrapper,
  .bp3-tree-node-secondary-label .bp3-popover-target{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center; }

.bp3-tree-node.bp3-disabled .bp3-tree-node-content{
  background-color:inherit;
  cursor:not-allowed;
  color:rgba(92, 112, 128, 0.6); }

.bp3-tree-node.bp3-disabled .bp3-tree-node-caret,
.bp3-tree-node.bp3-disabled .bp3-tree-node-icon{
  cursor:not-allowed;
  color:rgba(92, 112, 128, 0.6); }

.bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content{
  background-color:#137cbd; }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content,
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon, .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon-standard, .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon-large{
    color:#ffffff; }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-tree-node-caret::before{
    color:rgba(255, 255, 255, 0.7); }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-tree-node-caret:hover::before{
    color:#ffffff; }

.bp3-dark .bp3-tree-node-content:hover{
  background-color:rgba(92, 112, 128, 0.3); }

.bp3-dark .bp3-tree .bp3-icon, .bp3-dark .bp3-tree .bp3-icon-standard, .bp3-dark .bp3-tree .bp3-icon-large{
  color:#a7b6c2; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-primary, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-primary, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-primary{
    color:#137cbd; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-success, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-success, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-success{
    color:#0f9960; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-warning, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-warning, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-warning{
    color:#d9822b; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-danger, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-danger, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-danger{
    color:#db3737; }

.bp3-dark .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content{
  background-color:#137cbd; }
/*!

Copyright 2017-present Palantir Technologies, Inc. All rights reserved.
Licensed under the Apache License, Version 2.0.

*/
.bp3-omnibar{
  -webkit-filter:blur(0);
          filter:blur(0);
  opacity:1;
  top:20vh;
  left:calc(50% - 250px);
  z-index:21;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  background-color:#ffffff;
  width:500px; }
  .bp3-omnibar.bp3-overlay-enter, .bp3-omnibar.bp3-overlay-appear{
    -webkit-filter:blur(20px);
            filter:blur(20px);
    opacity:0.2; }
  .bp3-omnibar.bp3-overlay-enter-active, .bp3-omnibar.bp3-overlay-appear-active{
    -webkit-filter:blur(0);
            filter:blur(0);
    opacity:1;
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:filter, opacity;
    transition-property:filter, opacity, -webkit-filter;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-omnibar.bp3-overlay-exit{
    -webkit-filter:blur(0);
            filter:blur(0);
    opacity:1; }
  .bp3-omnibar.bp3-overlay-exit-active{
    -webkit-filter:blur(20px);
            filter:blur(20px);
    opacity:0.2;
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:filter, opacity;
    transition-property:filter, opacity, -webkit-filter;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-omnibar .bp3-input{
    border-radius:0;
    background-color:transparent; }
    .bp3-omnibar .bp3-input, .bp3-omnibar .bp3-input:focus{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-omnibar .bp3-menu{
    border-radius:0;
    -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
    background-color:transparent;
    max-height:calc(60vh - 40px);
    overflow:auto; }
    .bp3-omnibar .bp3-menu:empty{
      display:none; }
  .bp3-dark .bp3-omnibar, .bp3-omnibar.bp3-dark{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
    background-color:#30404d; }

.bp3-omnibar-overlay .bp3-overlay-backdrop{
  background-color:rgba(16, 22, 26, 0.2); }

.bp3-select-popover .bp3-popover-content{
  padding:5px; }

.bp3-select-popover .bp3-input-group{
  margin-bottom:0; }

.bp3-select-popover .bp3-menu{
  max-width:400px;
  max-height:300px;
  overflow:auto;
  padding:0; }
  .bp3-select-popover .bp3-menu:not(:first-child){
    padding-top:5px; }

.bp3-multi-select{
  min-width:150px; }

.bp3-multi-select-popover .bp3-menu{
  max-width:400px;
  max-height:300px;
  overflow:auto; }

.bp3-select-popover .bp3-popover-content{
  padding:5px; }

.bp3-select-popover .bp3-input-group{
  margin-bottom:0; }

.bp3-select-popover .bp3-menu{
  max-width:400px;
  max-height:300px;
  overflow:auto;
  padding:0; }
  .bp3-select-popover .bp3-menu:not(:first-child){
    padding-top:5px; }
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDhoLTIuODFjLS40NS0uNzgtMS4wNy0xLjQ1LTEuODItMS45NkwxNyA0LjQxIDE1LjU5IDNsLTIuMTcgMi4xN0MxMi45NiA1LjA2IDEyLjQ5IDUgMTIgNWMtLjQ5IDAtLjk2LjA2LTEuNDEuMTdMOC40MSAzIDcgNC40MWwxLjYyIDEuNjNDNy44OCA2LjU1IDcuMjYgNy4yMiA2LjgxIDhINHYyaDIuMDljLS4wNS4zMy0uMDkuNjYtLjA5IDF2MUg0djJoMnYxYzAgLjM0LjA0LjY3LjA5IDFINHYyaDIuODFjMS4wNCAxLjc5IDIuOTcgMyA1LjE5IDNzNC4xNS0xLjIxIDUuMTktM0gyMHYtMmgtMi4wOWMuMDUtLjMzLjA5LS42Ni4wOS0xdi0xaDJ2LTJoLTJ2LTFjMC0uMzQtLjA0LS42Ny0uMDktMUgyMFY4em0tNiA4aC00di0yaDR2MnptMC00aC00di0yaDR2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTYuMTdMNC44MyAxMmwtMS40MiAxLjQxTDkgMTkgMjEgN2wtMS40MS0xLjQxeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1pY29uLWJyYW5kMSBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNmZmYiPgogICAgPHBhdGggZD0iTTEwNSAxMjcuM2g0MHYxMi44aC00MHpNNTEuMSA3N0w3NCA5OS45bC0yMy4zIDIzLjMgMTAuNSAxMC41IDIzLjMtMjMuM0w5NSA5OS45IDg0LjUgODkuNCA2MS42IDY2LjV6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMSBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNGOUE4MjUiPgogICAgPHBhdGggZD0iTTIwLjIgMTEuOGMtMS42IDAtMS43LjUtMS43IDEgMCAuNC4xLjkuMSAxLjMuMS41LjEuOS4xIDEuMyAwIDEuNy0xLjQgMi4zLTMuNSAyLjNoLS45di0xLjloLjVjMS4xIDAgMS40IDAgMS40LS44IDAtLjMgMC0uNi0uMS0xIDAtLjQtLjEtLjgtLjEtMS4yIDAtMS4zIDAtMS44IDEuMy0yLTEuMy0uMi0xLjMtLjctMS4zLTIgMC0uNC4xLS44LjEtMS4yLjEtLjQuMS0uNy4xLTEgMC0uOC0uNC0uNy0xLjQtLjhoLS41VjQuMWguOWMyLjIgMCAzLjUuNyAzLjUgMi4zIDAgLjQtLjEuOS0uMSAxLjMtLjEuNS0uMS45LS4xIDEuMyAwIC41LjIgMSAxLjcgMXYxLjh6TTEuOCAxMC4xYzEuNiAwIDEuNy0uNSAxLjctMSAwLS40LS4xLS45LS4xLTEuMy0uMS0uNS0uMS0uOS0uMS0xLjMgMC0xLjYgMS40LTIuMyAzLjUtMi4zaC45djEuOWgtLjVjLTEgMC0xLjQgMC0xLjQuOCAwIC4zIDAgLjYuMSAxIDAgLjIuMS42LjEgMSAwIDEuMyAwIDEuOC0xLjMgMkM2IDExLjIgNiAxMS43IDYgMTNjMCAuNC0uMS44LS4xIDEuMi0uMS4zLS4xLjctLjEgMSAwIC44LjMuOCAxLjQuOGguNXYxLjloLS45Yy0yLjEgMC0zLjUtLjYtMy41LTIuMyAwLS40LjEtLjkuMS0xLjMuMS0uNS4xLS45LjEtMS4zIDAtLjUtLjItMS0xLjctMXYtMS45eiIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSIxMy44IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY3g9IjExIiBjeT0iOC4yIiByPSIyLjEiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgPGcgY2xhc3M9ImpwLWljb24td2FybjAiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4=);
  --jp-icon-listings-info: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pg0KPHN2ZyB2ZXJzaW9uPSIxLjEiIGlkPSJDYXBhXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4Ig0KCSB2aWV3Qm94PSIwIDAgNTAuOTc4IDUwLjk3OCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgNTAuOTc4IDUwLjk3ODsiIHhtbDpzcGFjZT0icHJlc2VydmUiPg0KPGc+DQoJPGc+DQoJCTxnPg0KCQkJPHBhdGggc3R5bGU9ImZpbGw6IzAxMDAwMjsiIGQ9Ik00My41Miw3LjQ1OEMzOC43MTEsMi42NDgsMzIuMzA3LDAsMjUuNDg5LDBDMTguNjcsMCwxMi4yNjYsMi42NDgsNy40NTgsNy40NTgNCgkJCQljLTkuOTQzLDkuOTQxLTkuOTQzLDI2LjExOSwwLDM2LjA2MmM0LjgwOSw0LjgwOSwxMS4yMTIsNy40NTYsMTguMDMxLDcuNDU4YzAsMCwwLjAwMSwwLDAuMDAyLDANCgkJCQljNi44MTYsMCwxMy4yMjEtMi42NDgsMTguMDI5LTcuNDU4YzQuODA5LTQuODA5LDcuNDU3LTExLjIxMiw3LjQ1Ny0xOC4wM0M1MC45NzcsMTguNjcsNDguMzI4LDEyLjI2Niw0My41Miw3LjQ1OHoNCgkJCQkgTTQyLjEwNiw0Mi4xMDVjLTQuNDMyLDQuNDMxLTEwLjMzMiw2Ljg3Mi0xNi42MTUsNi44NzJoLTAuMDAyYy02LjI4NS0wLjAwMS0xMi4xODctMi40NDEtMTYuNjE3LTYuODcyDQoJCQkJYy05LjE2Mi05LjE2My05LjE2Mi0yNC4wNzEsMC0zMy4yMzNDMTMuMzAzLDQuNDQsMTkuMjA0LDIsMjUuNDg5LDJjNi4yODQsMCwxMi4xODYsMi40NCwxNi42MTcsNi44NzINCgkJCQljNC40MzEsNC40MzEsNi44NzEsMTAuMzMyLDYuODcxLDE2LjYxN0M0OC45NzcsMzEuNzcyLDQ2LjUzNiwzNy42NzUsNDIuMTA2LDQyLjEwNXoiLz4NCgkJPC9nPg0KCQk8Zz4NCgkJCTxwYXRoIHN0eWxlPSJmaWxsOiMwMTAwMDI7IiBkPSJNMjMuNTc4LDMyLjIxOGMtMC4wMjMtMS43MzQsMC4xNDMtMy4wNTksMC40OTYtMy45NzJjMC4zNTMtMC45MTMsMS4xMS0xLjk5NywyLjI3Mi0zLjI1Mw0KCQkJCWMwLjQ2OC0wLjUzNiwwLjkyMy0xLjA2MiwxLjM2Ny0xLjU3NWMwLjYyNi0wLjc1MywxLjEwNC0xLjQ3OCwxLjQzNi0yLjE3NWMwLjMzMS0wLjcwNywwLjQ5NS0xLjU0MSwwLjQ5NS0yLjUNCgkJCQljMC0xLjA5Ni0wLjI2LTIuMDg4LTAuNzc5LTIuOTc5Yy0wLjU2NS0wLjg3OS0xLjUwMS0xLjMzNi0yLjgwNi0xLjM2OWMtMS44MDIsMC4wNTctMi45ODUsMC42NjctMy41NSwxLjgzMg0KCQkJCWMtMC4zMDEsMC41MzUtMC41MDMsMS4xNDEtMC42MDcsMS44MTRjLTAuMTM5LDAuNzA3LTAuMjA3LDEuNDMyLTAuMjA3LDIuMTc0aC0yLjkzN2MtMC4wOTEtMi4yMDgsMC40MDctNC4xMTQsMS40OTMtNS43MTkNCgkJCQljMS4wNjItMS42NCwyLjg1NS0yLjQ4MSw1LjM3OC0yLjUyN2MyLjE2LDAuMDIzLDMuODc0LDAuNjA4LDUuMTQxLDEuNzU4YzEuMjc4LDEuMTYsMS45MjksMi43NjQsMS45NSw0LjgxMQ0KCQkJCWMwLDEuMTQyLTAuMTM3LDIuMTExLTAuNDEsMi45MTFjLTAuMzA5LDAuODQ1LTAuNzMxLDEuNTkzLTEuMjY4LDIuMjQzYy0wLjQ5MiwwLjY1LTEuMDY4LDEuMzE4LTEuNzMsMi4wMDINCgkJCQljLTAuNjUsMC42OTctMS4zMTMsMS40NzktMS45ODcsMi4zNDZjLTAuMjM5LDAuMzc3LTAuNDI5LDAuNzc3LTAuNTY1LDEuMTk5Yy0wLjE2LDAuOTU5LTAuMjE3LDEuOTUxLTAuMTcxLDIuOTc5DQoJCQkJQzI2LjU4OSwzMi4yMTgsMjMuNTc4LDMyLjIxOCwyMy41NzgsMzIuMjE4eiBNMjMuNTc4LDM4LjIydi0zLjQ4NGgzLjA3NnYzLjQ4NEgyMy41Nzh6Ii8+DQoJCTwvZz4NCgk8L2c+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8L3N2Zz4NCg==);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMEQ0N0ExIj4KICAgIDxwYXRoIGQ9Ik0xMS4xIDYuOVY1LjhINi45YzAtLjUgMC0xLjMuMi0xLjYuNC0uNy44LTEuMSAxLjctMS40IDEuNy0uMyAyLjUtLjMgMy45LS4xIDEgLjEgMS45LjkgMS45IDEuOXY0LjJjMCAuNS0uOSAxLjYtMiAxLjZIOC44Yy0xLjUgMC0yLjQgMS40LTIuNCAyLjh2Mi4ySDQuN0MzLjUgMTUuMSAzIDE0IDMgMTMuMVY5Yy0uMS0xIC42LTIgMS44LTIgMS41LS4xIDYuMy0uMSA2LjMtLjF6Ii8+CiAgICA8cGF0aCBkPSJNMTAuOSAxNS4xdjEuMWg0LjJjMCAuNSAwIDEuMy0uMiAxLjYtLjQuNy0uOCAxLjEtMS43IDEuNC0xLjcuMy0yLjUuMy0zLjkuMS0xLS4xLTEuOS0uOS0xLjktMS45di00LjJjMC0uNS45LTEuNiAyLTEuNmgzLjhjMS41IDAgMi40LTEuNCAyLjQtMi44VjYuNmgxLjdDMTguNSA2LjkgMTkgOCAxOSA4LjlWMTNjMCAxLS43IDIuMS0xLjkgMi4xaC02LjJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiB3aWR0aD0iMjAiIGhlaWdodD0iMjAiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMikiIGZpbGw9IiMzMzMzMzMiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uLWFjY2VudDIganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGQ9Ik01LjA1NjY0IDguNzYxNzJDNS4wNTY2NCA4LjU5NzY2IDUuMDMxMjUgOC40NTMxMiA0Ljk4MDQ3IDguMzI4MTJDNC45MzM1OSA4LjE5OTIyIDQuODU1NDcgOC4wODIwMyA0Ljc0NjA5IDcuOTc2NTZDNC42NDA2MiA3Ljg3MTA5IDQuNSA3Ljc3NTM5IDQuMzI0MjIgNy42ODk0NUM0LjE1MjM0IDcuNTk5NjEgMy45NDMzNiA3LjUxMTcyIDMuNjk3MjcgNy40MjU3OEMzLjMwMjczIDcuMjg1MTYgMi45NDMzNiA3LjEzNjcyIDIuNjE5MTQgNi45ODA0N0MyLjI5NDkyIDYuODI0MjIgMi4wMTc1OCA2LjY0MjU4IDEuNzg3MTEgNi40MzU1NUMxLjU2MDU1IDYuMjI4NTIgMS4zODQ3NyA1Ljk4ODI4IDEuMjU5NzcgNS43MTQ4NEMxLjEzNDc3IDUuNDM3NSAxLjA3MjI3IDUuMTA5MzggMS4wNzIyNyA0LjczMDQ3QzEuMDcyMjcgNC4zOTg0NCAxLjEyODkxIDQuMDk1NyAxLjI0MjE5IDMuODIyMjdDMS4zNTU0NyAzLjU0NDkyIDEuNTE1NjIgMy4zMDQ2OSAxLjcyMjY2IDMuMTAxNTZDMS45Mjk2OSAyLjg5ODQ0IDIuMTc5NjkgMi43MzQzNyAyLjQ3MjY2IDIuNjA5MzhDMi43NjU2MiAyLjQ4NDM4IDMuMDkxOCAyLjQwNDMgMy40NTExNyAyLjM2OTE0VjEuMTA5MzhINC4zODg2N1YyLjM4MDg2QzQuNzQwMjMgMi40Mjc3MyA1LjA1NjY0IDIuNTIzNDQgNS4zMzc4OSAyLjY2Nzk3QzUuNjE5MTQgMi44MTI1IDUuODU3NDIgMy4wMDE5NSA2LjA1MjczIDMuMjM2MzNDNi4yNTE5NSAzLjQ2NjggNi40MDQzIDMuNzQwMjMgNi41MDk3NyA0LjA1NjY0QzYuNjE5MTQgNC4zNjkxNCA2LjY3MzgzIDQuNzIwNyA2LjY3MzgzIDUuMTExMzNINS4wNDQ5MkM1LjA0NDkyIDQuNjM4NjcgNC45Mzc1IDQuMjgxMjUgNC43MjI2NiA0LjAzOTA2QzQuNTA3ODEgMy43OTI5NyA0LjIxNjggMy42Njk5MiAzLjg0OTYxIDMuNjY5OTJDMy42NTAzOSAzLjY2OTkyIDMuNDc2NTYgMy42OTcyNyAzLjMyODEyIDMuNzUxOTVDMy4xODM1OSAzLjgwMjczIDMuMDY0NDUgMy44NzY5NSAyLjk3MDcgMy45NzQ2MUMyLjg3Njk1IDQuMDY4MzYgMi44MDY2NCA0LjE3OTY5IDIuNzU5NzcgNC4zMDg1OUMyLjcxNjggNC40Mzc1IDIuNjk1MzEgNC41NzgxMiAyLjY5NTMxIDQuNzMwNDdDMi42OTUzMSA0Ljg4MjgxIDIuNzE2OCA1LjAxOTUzIDIuNzU5NzcgNS4xNDA2MkMyLjgwNjY0IDUuMjU3ODEgMi44ODI4MSA1LjM2NzE5IDIuOTg4MjggNS40Njg3NUMzLjA5NzY2IDUuNTcwMzEgMy4yNDAyMyA1LjY2Nzk3IDMuNDE2MDIgNS43NjE3MkMzLjU5MTggNS44NTE1NiAzLjgxMDU1IDUuOTQzMzYgNC4wNzIyNyA2LjAzNzExQzQuNDY2OCA2LjE4NTU1IDQuODI0MjIgNi4zMzk4NCA1LjE0NDUzIDYuNUM1LjQ2NDg0IDYuNjU2MjUgNS43MzgyOCA2LjgzOTg0IDUuOTY0ODQgNy4wNTA3OEM2LjE5NTMxIDcuMjU3ODEgNi4zNzEwOSA3LjUgNi40OTIxOSA3Ljc3NzM0QzYuNjE3MTkgOC4wNTA3OCA2LjY3OTY5IDguMzc1IDYuNjc5NjkgOC43NUM2LjY3OTY5IDkuMDkzNzUgNi42MjMwNSA5LjQwNDMgNi41MDk3NyA5LjY4MTY0QzYuMzk2NDggOS45NTUwOCA2LjIzNDM4IDEwLjE5MTQgNi4wMjM0NCAxMC4zOTA2QzUuODEyNSAxMC41ODk4IDUuNTU4NTkgMTAuNzUgNS4yNjE3MiAxMC44NzExQzQuOTY0ODQgMTAuOTg4MyA0LjYzMjgxIDExLjA2NDUgNC4yNjU2MiAxMS4wOTk2VjEyLjI0OEgzLjMzMzk4VjExLjA5OTZDMy4wMDE5NSAxMS4wNjg0IDIuNjc5NjkgMTAuOTk2MSAyLjM2NzE5IDEwLjg4MjhDMi4wNTQ2OSAxMC43NjU2IDEuNzc3MzQgMTAuNTk3NyAxLjUzNTE2IDEwLjM3ODlDMS4yOTY4OCAxMC4xNjAyIDEuMTA1NDcgOS44ODQ3NyAwLjk2MDkzOCA5LjU1MjczQzAuODE2NDA2IDkuMjE2OCAwLjc0NDE0MSA4LjgxNDQ1IDAuNzQ0MTQxIDguMzQ1N0gyLjM3ODkxQzIuMzc4OTEgOC42MjY5NSAyLjQxOTkyIDguODYzMjggMi41MDE5NSA5LjA1NDY5QzIuNTgzOTggOS4yNDIxOSAyLjY4OTQ1IDkuMzkyNTggMi44MTgzNiA5LjUwNTg2QzIuOTUxMTcgOS42MTUyMyAzLjEwMTU2IDkuNjkzMzYgMy4yNjk1MyA5Ljc0MDIzQzMuNDM3NSA5Ljc4NzExIDMuNjA5MzggOS44MTA1NSAzLjc4NTE2IDkuODEwNTVDNC4yMDMxMiA5LjgxMDU1IDQuNTE5NTMgOS43MTI4OSA0LjczNDM4IDkuNTE3NThDNC45NDkyMiA5LjMyMjI3IDUuMDU2NjQgOS4wNzAzMSA1LjA1NjY0IDguNzYxNzJaTTEzLjQxOCAxMi4yNzE1SDguMDc0MjJWMTFIMTMuNDE4VjEyLjI3MTVaIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzLjk1MjY0IDYpIiBmaWxsPSJ3aGl0ZSIvPgo8L3N2Zz4K);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTUgMTVIM3YyaDEydi0yem0wLThIM3YyaDEyVjd6TTMgMTNoMTh2LTJIM3Yyem0wIDhoMTh2LTJIM3Yyek0zIDN2MmgxOFYzSDN6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}
.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}
.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}
.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}
.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}
.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}
.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}
.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}
.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}
.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}
.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}
.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}
.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}
.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}
.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}
.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}
.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}
.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}
.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}
.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}
.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}
.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}
.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}
.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}
.jp-FileIcon {
  background-image: var(--jp-icon-file);
}
.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}
.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}
.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}
.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}
.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}
.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}
.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}
.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}
.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}
.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}
.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}
.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}
.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}
.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}
.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}
.jp-ListIcon {
  background-image: var(--jp-icon-list);
}
.jp-ListingsInfoIcon {
  background-image: var(--jp-icon-listings-info);
}
.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}
.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}
.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}
.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}
.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}
.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}
.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}
.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}
.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}
.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}
.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}
.jp-RunIcon {
  background-image: var(--jp-icon-run);
}
.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}
.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}
.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}
.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}
.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}
.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}
.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}
.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}
.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}
.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}
.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}
.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}
.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

:root {
  --jp-icon-search-white: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
}

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}
/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}
/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}
/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}
.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}
.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}
.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}
.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}
.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}
.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}
.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}
.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}
/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}
.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}
.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}
.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}
.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}
.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}
.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}
/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}
.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}
.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}
.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}
.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}
.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}
.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

/* CSS for icons in selected items in the settings editor */
#setting-editor .jp-PluginList .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}
#setting-editor
  .jp-PluginList
  .jp-mod-selected
  .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* CSS for icons in selected tabs in the sidebar tab manager */
#tab-manager .lm-TabBar-tab.jp-mod-active .jp-icon-selectable[fill] {
  fill: #fff;
}

#tab-manager .lm-TabBar-tab.jp-mod-active .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}
#tab-manager
  .lm-TabBar-tab.jp-mod-active
  .jp-icon-hover
  :hover
  .jp-icon-selectable[fill] {
  fill: var(--jp-brand-color1);
}

#tab-manager
  .lm-TabBar-tab.jp-mod-active
  .jp-icon-hover
  :hover
  .jp-icon-selectable-inverse[fill] {
  fill: #fff;
}

/**
 * TODO: come up with non css-hack solution for showing the busy icon on top
 *  of the close icon
 * CSS for complex behavior of close icon of tabs in the sidebar tab manager
 */
#tab-manager
  .lm-TabBar-tab.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}
#tab-manager
  .lm-TabBar-tab.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

#tab-manager
  .lm-TabBar-tab.jp-mod-dirty.jp-mod-active
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: #fff;
}

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}
/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) svg {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

/* Override Blueprint's _reset.scss styles */
html {
  box-sizing: unset;
}

*,
*::before,
*::after {
  box-sizing: unset;
}

body {
  color: unset;
  font-family: var(--jp-ui-font-family);
}

p {
  margin-top: unset;
  margin-bottom: unset;
}

small {
  font-size: unset;
}

strong {
  font-weight: unset;
}

/* Override Blueprint's _typography.scss styles */
a {
  text-decoration: unset;
  color: unset;
}
a:hover {
  text-decoration: unset;
  color: unset;
}

/* Override Blueprint's _accessibility.scss styles */
:focus {
  outline: unset;
  outline-offset: unset;
  -moz-outline-radius: unset;
}

/* Styles for ui-components */
.jp-Button {
  border-radius: var(--jp-border-radius);
  padding: 0px 12px;
  font-size: var(--jp-ui-font-size1);
}

/* Use our own theme for hover styles */
button.jp-Button.bp3-button.bp3-minimal:hover {
  background-color: var(--jp-layout-color2);
}
.jp-Button.minimal {
  color: unset !important;
}

.jp-Button.jp-ToolbarButtonComponent {
  text-transform: none;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color3);
}

.jp-BPIcon {
  display: inline-block;
  vertical-align: middle;
  margin: auto;
}

/* Stop blueprint futzing with our icon fills */
.bp3-icon.jp-BPIcon > svg:not([fill]) {
  fill: var(--jp-inverse-layout-color3);
}

.jp-InputGroupAction {
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

/* Use our own theme for hover and option styles */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}
select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-top: 1px solid var(--jp-border-color2);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-Collapse-header {
  padding: 1px 12px;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size2);
}

.jp-Collapse-header:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Collapse-contents {
  padding: 0px 12px 0px 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0px;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0px 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.lm-CommandPalette-wrapper::after {
  content: ' ';
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  height: 30px;
  width: 10px;
  padding: 0px 10px;
  background-image: var(--jp-icon-search-white);
  background-size: 20px;
  background-repeat: no-repeat;
  background-position: center;
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color3);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0px;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color3);
}

.lm-CommandPalette-item.lm-mod-active {
  background: var(--jp-layout-color3);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  background: var(--jp-layout-color4);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color3);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.4;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty:after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0px 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0px;
  left: 0px;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px;
  padding-bottom: 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0px;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

.jp-Dialog-header {
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0px 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

.jp-HoverBox.jp-mod-outofview {
  display: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `p-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;

  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;

  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #aa00ff;

  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;

  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;

  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;

  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;

  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;

  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;

  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;

  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;

  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;

  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ffff00;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;

  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;

  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;

  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;

  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;

  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eeeeee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;

  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent:before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent:after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0px 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  height: 28px;
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  background-color: var(--jp-layout-color1);
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0px 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  height: 32px;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 1;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0px;
  margin: 0px;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0px 6px;
  margin: 0px;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent span {
  padding: 0px;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ body.p-mod-override-cursor *, /* </DEPRECATED> */
body.lm-mod-override-cursor * {
  cursor: inherit !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0px;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* BASICS */

.CodeMirror {
  /* Set height, width, borders, and global font properties here */
  font-family: monospace;
  height: 300px;
  color: black;
  direction: ltr;
}

/* PADDING */

.CodeMirror-lines {
  padding: 4px 0; /* Vertical padding around content */
}
.CodeMirror pre.CodeMirror-line,
.CodeMirror pre.CodeMirror-line-like {
  padding: 0 4px; /* Horizontal padding of content */
}

.CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler {
  background-color: white; /* The little square between H and V scrollbars */
}

/* GUTTER */

.CodeMirror-gutters {
  border-right: 1px solid #ddd;
  background-color: #f7f7f7;
  white-space: nowrap;
}
.CodeMirror-linenumbers {}
.CodeMirror-linenumber {
  padding: 0 3px 0 5px;
  min-width: 20px;
  text-align: right;
  color: #999;
  white-space: nowrap;
}

.CodeMirror-guttermarker { color: black; }
.CodeMirror-guttermarker-subtle { color: #999; }

/* CURSOR */

.CodeMirror-cursor {
  border-left: 1px solid black;
  border-right: none;
  width: 0;
}
/* Shown when moving in bi-directional text */
.CodeMirror div.CodeMirror-secondarycursor {
  border-left: 1px solid silver;
}
.cm-fat-cursor .CodeMirror-cursor {
  width: auto;
  border: 0 !important;
  background: #7e7;
}
.cm-fat-cursor div.CodeMirror-cursors {
  z-index: 1;
}
.cm-fat-cursor-mark {
  background-color: rgba(20, 255, 20, 0.5);
  -webkit-animation: blink 1.06s steps(1) infinite;
  -moz-animation: blink 1.06s steps(1) infinite;
  animation: blink 1.06s steps(1) infinite;
}
.cm-animate-fat-cursor {
  width: auto;
  border: 0;
  -webkit-animation: blink 1.06s steps(1) infinite;
  -moz-animation: blink 1.06s steps(1) infinite;
  animation: blink 1.06s steps(1) infinite;
  background-color: #7e7;
}
@-moz-keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}
@-webkit-keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}
@keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}

/* Can style cursor different in overwrite (non-insert) mode */
.CodeMirror-overwrite .CodeMirror-cursor {}

.cm-tab { display: inline-block; text-decoration: inherit; }

.CodeMirror-rulers {
  position: absolute;
  left: 0; right: 0; top: -50px; bottom: 0;
  overflow: hidden;
}
.CodeMirror-ruler {
  border-left: 1px solid #ccc;
  top: 0; bottom: 0;
  position: absolute;
}

/* DEFAULT THEME */

.cm-s-default .cm-header {color: blue;}
.cm-s-default .cm-quote {color: #090;}
.cm-negative {color: #d44;}
.cm-positive {color: #292;}
.cm-header, .cm-strong {font-weight: bold;}
.cm-em {font-style: italic;}
.cm-link {text-decoration: underline;}
.cm-strikethrough {text-decoration: line-through;}

.cm-s-default .cm-keyword {color: #708;}
.cm-s-default .cm-atom {color: #219;}
.cm-s-default .cm-number {color: #164;}
.cm-s-default .cm-def {color: #00f;}
.cm-s-default .cm-variable,
.cm-s-default .cm-punctuation,
.cm-s-default .cm-property,
.cm-s-default .cm-operator {}
.cm-s-default .cm-variable-2 {color: #05a;}
.cm-s-default .cm-variable-3, .cm-s-default .cm-type {color: #085;}
.cm-s-default .cm-comment {color: #a50;}
.cm-s-default .cm-string {color: #a11;}
.cm-s-default .cm-string-2 {color: #f50;}
.cm-s-default .cm-meta {color: #555;}
.cm-s-default .cm-qualifier {color: #555;}
.cm-s-default .cm-builtin {color: #30a;}
.cm-s-default .cm-bracket {color: #997;}
.cm-s-default .cm-tag {color: #170;}
.cm-s-default .cm-attribute {color: #00c;}
.cm-s-default .cm-hr {color: #999;}
.cm-s-default .cm-link {color: #00c;}

.cm-s-default .cm-error {color: #f00;}
.cm-invalidchar {color: #f00;}

.CodeMirror-composing { border-bottom: 2px solid; }

/* Default styles for common addons */

div.CodeMirror span.CodeMirror-matchingbracket {color: #0b0;}
div.CodeMirror span.CodeMirror-nonmatchingbracket {color: #a22;}
.CodeMirror-matchingtag { background: rgba(255, 150, 0, .3); }
.CodeMirror-activeline-background {background: #e8f2ff;}

/* STOP */

/* The rest of this file contains styles related to the mechanics of
   the editor. You probably shouldn't touch them. */

.CodeMirror {
  position: relative;
  overflow: hidden;
  background: white;
}

.CodeMirror-scroll {
  overflow: scroll !important; /* Things will break if this is overridden */
  /* 30px is the magic margin used to hide the element's real scrollbars */
  /* See overflow: hidden in .CodeMirror */
  margin-bottom: -30px; margin-right: -30px;
  padding-bottom: 30px;
  height: 100%;
  outline: none; /* Prevent dragging from highlighting the element */
  position: relative;
}
.CodeMirror-sizer {
  position: relative;
  border-right: 30px solid transparent;
}

/* The fake, visible scrollbars. Used to force redraw during scrolling
   before actual scrolling happens, thus preventing shaking and
   flickering artifacts. */
.CodeMirror-vscrollbar, .CodeMirror-hscrollbar, .CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler {
  position: absolute;
  z-index: 6;
  display: none;
}
.CodeMirror-vscrollbar {
  right: 0; top: 0;
  overflow-x: hidden;
  overflow-y: scroll;
}
.CodeMirror-hscrollbar {
  bottom: 0; left: 0;
  overflow-y: hidden;
  overflow-x: scroll;
}
.CodeMirror-scrollbar-filler {
  right: 0; bottom: 0;
}
.CodeMirror-gutter-filler {
  left: 0; bottom: 0;
}

.CodeMirror-gutters {
  position: absolute; left: 0; top: 0;
  min-height: 100%;
  z-index: 3;
}
.CodeMirror-gutter {
  white-space: normal;
  height: 100%;
  display: inline-block;
  vertical-align: top;
  margin-bottom: -30px;
}
.CodeMirror-gutter-wrapper {
  position: absolute;
  z-index: 4;
  background: none !important;
  border: none !important;
}
.CodeMirror-gutter-background {
  position: absolute;
  top: 0; bottom: 0;
  z-index: 4;
}
.CodeMirror-gutter-elt {
  position: absolute;
  cursor: default;
  z-index: 4;
}
.CodeMirror-gutter-wrapper ::selection { background-color: transparent }
.CodeMirror-gutter-wrapper ::-moz-selection { background-color: transparent }

.CodeMirror-lines {
  cursor: text;
  min-height: 1px; /* prevents collapsing before first draw */
}
.CodeMirror pre.CodeMirror-line,
.CodeMirror pre.CodeMirror-line-like {
  /* Reset some styles that the rest of the page might have set */
  -moz-border-radius: 0; -webkit-border-radius: 0; border-radius: 0;
  border-width: 0;
  background: transparent;
  font-family: inherit;
  font-size: inherit;
  margin: 0;
  white-space: pre;
  word-wrap: normal;
  line-height: inherit;
  color: inherit;
  z-index: 2;
  position: relative;
  overflow: visible;
  -webkit-tap-highlight-color: transparent;
  -webkit-font-variant-ligatures: contextual;
  font-variant-ligatures: contextual;
}
.CodeMirror-wrap pre.CodeMirror-line,
.CodeMirror-wrap pre.CodeMirror-line-like {
  word-wrap: break-word;
  white-space: pre-wrap;
  word-break: normal;
}

.CodeMirror-linebackground {
  position: absolute;
  left: 0; right: 0; top: 0; bottom: 0;
  z-index: 0;
}

.CodeMirror-linewidget {
  position: relative;
  z-index: 2;
  padding: 0.1px; /* Force widget margins to stay inside of the container */
}

.CodeMirror-widget {}

.CodeMirror-rtl pre { direction: rtl; }

.CodeMirror-code {
  outline: none;
}

/* Force content-box sizing for the elements where we expect it */
.CodeMirror-scroll,
.CodeMirror-sizer,
.CodeMirror-gutter,
.CodeMirror-gutters,
.CodeMirror-linenumber {
  -moz-box-sizing: content-box;
  box-sizing: content-box;
}

.CodeMirror-measure {
  position: absolute;
  width: 100%;
  height: 0;
  overflow: hidden;
  visibility: hidden;
}

.CodeMirror-cursor {
  position: absolute;
  pointer-events: none;
}
.CodeMirror-measure pre { position: static; }

div.CodeMirror-cursors {
  visibility: hidden;
  position: relative;
  z-index: 3;
}
div.CodeMirror-dragcursors {
  visibility: visible;
}

.CodeMirror-focused div.CodeMirror-cursors {
  visibility: visible;
}

.CodeMirror-selected { background: #d9d9d9; }
.CodeMirror-focused .CodeMirror-selected { background: #d7d4f0; }
.CodeMirror-crosshair { cursor: crosshair; }
.CodeMirror-line::selection, .CodeMirror-line > span::selection, .CodeMirror-line > span > span::selection { background: #d7d4f0; }
.CodeMirror-line::-moz-selection, .CodeMirror-line > span::-moz-selection, .CodeMirror-line > span > span::-moz-selection { background: #d7d4f0; }

.cm-searching {
  background-color: #ffa;
  background-color: rgba(255, 255, 0, .4);
}

/* Used to force a border model for a node */
.cm-force-border { padding-right: .1px; }

@media print {
  /* Hide the cursor when printing */
  .CodeMirror div.CodeMirror-cursors {
    visibility: hidden;
  }
}

/* See issue #2901 */
.cm-tab-wrap-hack:after { content: ''; }

/* Help users use markselection to safely style text background */
span.CodeMirror-selectedtext { background: none; }

.CodeMirror-dialog {
  position: absolute;
  left: 0; right: 0;
  background: inherit;
  z-index: 15;
  padding: .1em .8em;
  overflow: hidden;
  color: inherit;
}

.CodeMirror-dialog-top {
  border-bottom: 1px solid #eee;
  top: 0;
}

.CodeMirror-dialog-bottom {
  border-top: 1px solid #eee;
  bottom: 0;
}

.CodeMirror-dialog input {
  border: none;
  outline: none;
  background: transparent;
  width: 20em;
  color: inherit;
  font-family: monospace;
}

.CodeMirror-dialog button {
  font-size: 70%;
}

.CodeMirror-foldmarker {
  color: blue;
  text-shadow: #b9f 1px 1px 2px, #b9f -1px -1px 2px, #b9f 1px -1px 2px, #b9f -1px 1px 2px;
  font-family: arial;
  line-height: .3;
  cursor: pointer;
}
.CodeMirror-foldgutter {
  width: .7em;
}
.CodeMirror-foldgutter-open,
.CodeMirror-foldgutter-folded {
  cursor: pointer;
}
.CodeMirror-foldgutter-open:after {
  content: "\25BE";
}
.CodeMirror-foldgutter-folded:after {
  content: "\25B8";
}

/*
  Name:       material
  Author:     Mattia Astorino (http://github.com/equinusocio)
  Website:    https://material-theme.site/
*/

.cm-s-material.CodeMirror {
  background-color: #263238;
  color: #EEFFFF;
}

.cm-s-material .CodeMirror-gutters {
  background: #263238;
  color: #546E7A;
  border: none;
}

.cm-s-material .CodeMirror-guttermarker,
.cm-s-material .CodeMirror-guttermarker-subtle,
.cm-s-material .CodeMirror-linenumber {
  color: #546E7A;
}

.cm-s-material .CodeMirror-cursor {
  border-left: 1px solid #FFCC00;
}

.cm-s-material div.CodeMirror-selected {
  background: rgba(128, 203, 196, 0.2);
}

.cm-s-material.CodeMirror-focused div.CodeMirror-selected {
  background: rgba(128, 203, 196, 0.2);
}

.cm-s-material .CodeMirror-line::selection,
.cm-s-material .CodeMirror-line>span::selection,
.cm-s-material .CodeMirror-line>span>span::selection {
  background: rgba(128, 203, 196, 0.2);
}

.cm-s-material .CodeMirror-line::-moz-selection,
.cm-s-material .CodeMirror-line>span::-moz-selection,
.cm-s-material .CodeMirror-line>span>span::-moz-selection {
  background: rgba(128, 203, 196, 0.2);
}

.cm-s-material .CodeMirror-activeline-background {
  background: rgba(0, 0, 0, 0.5);
}

.cm-s-material .cm-keyword {
  color: #C792EA;
}

.cm-s-material .cm-operator {
  color: #89DDFF;
}

.cm-s-material .cm-variable-2 {
  color: #EEFFFF;
}

.cm-s-material .cm-variable-3,
.cm-s-material .cm-type {
  color: #f07178;
}

.cm-s-material .cm-builtin {
  color: #FFCB6B;
}

.cm-s-material .cm-atom {
  color: #F78C6C;
}

.cm-s-material .cm-number {
  color: #FF5370;
}

.cm-s-material .cm-def {
  color: #82AAFF;
}

.cm-s-material .cm-string {
  color: #C3E88D;
}

.cm-s-material .cm-string-2 {
  color: #f07178;
}

.cm-s-material .cm-comment {
  color: #546E7A;
}

.cm-s-material .cm-variable {
  color: #f07178;
}

.cm-s-material .cm-tag {
  color: #FF5370;
}

.cm-s-material .cm-meta {
  color: #FFCB6B;
}

.cm-s-material .cm-attribute {
  color: #C792EA;
}

.cm-s-material .cm-property {
  color: #C792EA;
}

.cm-s-material .cm-qualifier {
  color: #DECB6B;
}

.cm-s-material .cm-variable-3,
.cm-s-material .cm-type {
  color: #DECB6B;
}


.cm-s-material .cm-error {
  color: rgba(255, 255, 255, 1.0);
  background-color: #FF5370;
}

.cm-s-material .CodeMirror-matchingbracket {
  text-decoration: underline;
  color: white !important;
}
/**
 * "
 *  Using Zenburn color palette from the Emacs Zenburn Theme
 *  https://github.com/bbatsov/zenburn-emacs/blob/master/zenburn-theme.el
 *
 *  Also using parts of https://github.com/xavi/coderay-lighttable-theme
 * "
 * From: https://github.com/wisenomad/zenburn-lighttable-theme/blob/master/zenburn.css
 */

.cm-s-zenburn .CodeMirror-gutters { background: #3f3f3f !important; }
.cm-s-zenburn .CodeMirror-foldgutter-open, .CodeMirror-foldgutter-folded { color: #999; }
.cm-s-zenburn .CodeMirror-cursor { border-left: 1px solid white; }
.cm-s-zenburn { background-color: #3f3f3f; color: #dcdccc; }
.cm-s-zenburn span.cm-builtin { color: #dcdccc; font-weight: bold; }
.cm-s-zenburn span.cm-comment { color: #7f9f7f; }
.cm-s-zenburn span.cm-keyword { color: #f0dfaf; font-weight: bold; }
.cm-s-zenburn span.cm-atom { color: #bfebbf; }
.cm-s-zenburn span.cm-def { color: #dcdccc; }
.cm-s-zenburn span.cm-variable { color: #dfaf8f; }
.cm-s-zenburn span.cm-variable-2 { color: #dcdccc; }
.cm-s-zenburn span.cm-string { color: #cc9393; }
.cm-s-zenburn span.cm-string-2 { color: #cc9393; }
.cm-s-zenburn span.cm-number { color: #dcdccc; }
.cm-s-zenburn span.cm-tag { color: #93e0e3; }
.cm-s-zenburn span.cm-property { color: #dfaf8f; }
.cm-s-zenburn span.cm-attribute { color: #dfaf8f; }
.cm-s-zenburn span.cm-qualifier { color: #7cb8bb; }
.cm-s-zenburn span.cm-meta { color: #f0dfaf; }
.cm-s-zenburn span.cm-header { color: #f0efd0; }
.cm-s-zenburn span.cm-operator { color: #f0efd0; }
.cm-s-zenburn span.CodeMirror-matchingbracket { box-sizing: border-box; background: transparent; border-bottom: 1px solid; }
.cm-s-zenburn span.CodeMirror-nonmatchingbracket { border-bottom: 1px solid; background: none; }
.cm-s-zenburn .CodeMirror-activeline { background: #000000; }
.cm-s-zenburn .CodeMirror-activeline-background { background: #000000; }
.cm-s-zenburn div.CodeMirror-selected { background: #545454; }
.cm-s-zenburn .CodeMirror-focused div.CodeMirror-selected { background: #4f4f4f; }

.cm-s-abcdef.CodeMirror { background: #0f0f0f; color: #defdef; }
.cm-s-abcdef div.CodeMirror-selected { background: #515151; }
.cm-s-abcdef .CodeMirror-line::selection, .cm-s-abcdef .CodeMirror-line > span::selection, .cm-s-abcdef .CodeMirror-line > span > span::selection { background: rgba(56, 56, 56, 0.99); }
.cm-s-abcdef .CodeMirror-line::-moz-selection, .cm-s-abcdef .CodeMirror-line > span::-moz-selection, .cm-s-abcdef .CodeMirror-line > span > span::-moz-selection { background: rgba(56, 56, 56, 0.99); }
.cm-s-abcdef .CodeMirror-gutters { background: #555; border-right: 2px solid #314151; }
.cm-s-abcdef .CodeMirror-guttermarker { color: #222; }
.cm-s-abcdef .CodeMirror-guttermarker-subtle { color: azure; }
.cm-s-abcdef .CodeMirror-linenumber { color: #FFFFFF; }
.cm-s-abcdef .CodeMirror-cursor { border-left: 1px solid #00FF00; }

.cm-s-abcdef span.cm-keyword { color: darkgoldenrod; font-weight: bold; }
.cm-s-abcdef span.cm-atom { color: #77F; }
.cm-s-abcdef span.cm-number { color: violet; }
.cm-s-abcdef span.cm-def { color: #fffabc; }
.cm-s-abcdef span.cm-variable { color: #abcdef; }
.cm-s-abcdef span.cm-variable-2 { color: #cacbcc; }
.cm-s-abcdef span.cm-variable-3, .cm-s-abcdef span.cm-type { color: #def; }
.cm-s-abcdef span.cm-property { color: #fedcba; }
.cm-s-abcdef span.cm-operator { color: #ff0; }
.cm-s-abcdef span.cm-comment { color: #7a7b7c; font-style: italic;}
.cm-s-abcdef span.cm-string { color: #2b4; }
.cm-s-abcdef span.cm-meta { color: #C9F; }
.cm-s-abcdef span.cm-qualifier { color: #FFF700; }
.cm-s-abcdef span.cm-builtin { color: #30aabc; }
.cm-s-abcdef span.cm-bracket { color: #8a8a8a; }
.cm-s-abcdef span.cm-tag { color: #FFDD44; }
.cm-s-abcdef span.cm-attribute { color: #DDFF00; }
.cm-s-abcdef span.cm-error { color: #FF0000; }
.cm-s-abcdef span.cm-header { color: aquamarine; font-weight: bold; }
.cm-s-abcdef span.cm-link { color: blueviolet; }

.cm-s-abcdef .CodeMirror-activeline-background { background: #314151; }

/*

    Name:       Base16 Default Light
    Author:     Chris Kempson (http://chriskempson.com)

    CodeMirror template by Jan T. Sott (https://github.com/idleberg/base16-codemirror)
    Original Base16 color scheme by Chris Kempson (https://github.com/chriskempson/base16)

*/

.cm-s-base16-light.CodeMirror { background: #f5f5f5; color: #202020; }
.cm-s-base16-light div.CodeMirror-selected { background: #e0e0e0; }
.cm-s-base16-light .CodeMirror-line::selection, .cm-s-base16-light .CodeMirror-line > span::selection, .cm-s-base16-light .CodeMirror-line > span > span::selection { background: #e0e0e0; }
.cm-s-base16-light .CodeMirror-line::-moz-selection, .cm-s-base16-light .CodeMirror-line > span::-moz-selection, .cm-s-base16-light .CodeMirror-line > span > span::-moz-selection { background: #e0e0e0; }
.cm-s-base16-light .CodeMirror-gutters { background: #f5f5f5; border-right: 0px; }
.cm-s-base16-light .CodeMirror-guttermarker { color: #ac4142; }
.cm-s-base16-light .CodeMirror-guttermarker-subtle { color: #b0b0b0; }
.cm-s-base16-light .CodeMirror-linenumber { color: #b0b0b0; }
.cm-s-base16-light .CodeMirror-cursor { border-left: 1px solid #505050; }

.cm-s-base16-light span.cm-comment { color: #8f5536; }
.cm-s-base16-light span.cm-atom { color: #aa759f; }
.cm-s-base16-light span.cm-number { color: #aa759f; }

.cm-s-base16-light span.cm-property, .cm-s-base16-light span.cm-attribute { color: #90a959; }
.cm-s-base16-light span.cm-keyword { color: #ac4142; }
.cm-s-base16-light span.cm-string { color: #f4bf75; }

.cm-s-base16-light span.cm-variable { color: #90a959; }
.cm-s-base16-light span.cm-variable-2 { color: #6a9fb5; }
.cm-s-base16-light span.cm-def { color: #d28445; }
.cm-s-base16-light span.cm-bracket { color: #202020; }
.cm-s-base16-light span.cm-tag { color: #ac4142; }
.cm-s-base16-light span.cm-link { color: #aa759f; }
.cm-s-base16-light span.cm-error { background: #ac4142; color: #505050; }

.cm-s-base16-light .CodeMirror-activeline-background { background: #DDDCDC; }
.cm-s-base16-light .CodeMirror-matchingbracket { color: #f5f5f5 !important; background-color: #6A9FB5 !important}

/*

    Name:       Base16 Default Dark
    Author:     Chris Kempson (http://chriskempson.com)

    CodeMirror template by Jan T. Sott (https://github.com/idleberg/base16-codemirror)
    Original Base16 color scheme by Chris Kempson (https://github.com/chriskempson/base16)

*/

.cm-s-base16-dark.CodeMirror { background: #151515; color: #e0e0e0; }
.cm-s-base16-dark div.CodeMirror-selected { background: #303030; }
.cm-s-base16-dark .CodeMirror-line::selection, .cm-s-base16-dark .CodeMirror-line > span::selection, .cm-s-base16-dark .CodeMirror-line > span > span::selection { background: rgba(48, 48, 48, .99); }
.cm-s-base16-dark .CodeMirror-line::-moz-selection, .cm-s-base16-dark .CodeMirror-line > span::-moz-selection, .cm-s-base16-dark .CodeMirror-line > span > span::-moz-selection { background: rgba(48, 48, 48, .99); }
.cm-s-base16-dark .CodeMirror-gutters { background: #151515; border-right: 0px; }
.cm-s-base16-dark .CodeMirror-guttermarker { color: #ac4142; }
.cm-s-base16-dark .CodeMirror-guttermarker-subtle { color: #505050; }
.cm-s-base16-dark .CodeMirror-linenumber { color: #505050; }
.cm-s-base16-dark .CodeMirror-cursor { border-left: 1px solid #b0b0b0; }

.cm-s-base16-dark span.cm-comment { color: #8f5536; }
.cm-s-base16-dark span.cm-atom { color: #aa759f; }
.cm-s-base16-dark span.cm-number { color: #aa759f; }

.cm-s-base16-dark span.cm-property, .cm-s-base16-dark span.cm-attribute { color: #90a959; }
.cm-s-base16-dark span.cm-keyword { color: #ac4142; }
.cm-s-base16-dark span.cm-string { color: #f4bf75; }

.cm-s-base16-dark span.cm-variable { color: #90a959; }
.cm-s-base16-dark span.cm-variable-2 { color: #6a9fb5; }
.cm-s-base16-dark span.cm-def { color: #d28445; }
.cm-s-base16-dark span.cm-bracket { color: #e0e0e0; }
.cm-s-base16-dark span.cm-tag { color: #ac4142; }
.cm-s-base16-dark span.cm-link { color: #aa759f; }
.cm-s-base16-dark span.cm-error { background: #ac4142; color: #b0b0b0; }

.cm-s-base16-dark .CodeMirror-activeline-background { background: #202020; }
.cm-s-base16-dark .CodeMirror-matchingbracket { text-decoration: underline; color: white !important; }

/*

    Name:       dracula
    Author:     Michael Kaminsky (http://github.com/mkaminsky11)

    Original dracula color scheme by Zeno Rocha (https://github.com/zenorocha/dracula-theme)

*/


.cm-s-dracula.CodeMirror, .cm-s-dracula .CodeMirror-gutters {
  background-color: #282a36 !important;
  color: #f8f8f2 !important;
  border: none;
}
.cm-s-dracula .CodeMirror-gutters { color: #282a36; }
.cm-s-dracula .CodeMirror-cursor { border-left: solid thin #f8f8f0; }
.cm-s-dracula .CodeMirror-linenumber { color: #6D8A88; }
.cm-s-dracula .CodeMirror-selected { background: rgba(255, 255, 255, 0.10); }
.cm-s-dracula .CodeMirror-line::selection, .cm-s-dracula .CodeMirror-line > span::selection, .cm-s-dracula .CodeMirror-line > span > span::selection { background: rgba(255, 255, 255, 0.10); }
.cm-s-dracula .CodeMirror-line::-moz-selection, .cm-s-dracula .CodeMirror-line > span::-moz-selection, .cm-s-dracula .CodeMirror-line > span > span::-moz-selection { background: rgba(255, 255, 255, 0.10); }
.cm-s-dracula span.cm-comment { color: #6272a4; }
.cm-s-dracula span.cm-string, .cm-s-dracula span.cm-string-2 { color: #f1fa8c; }
.cm-s-dracula span.cm-number { color: #bd93f9; }
.cm-s-dracula span.cm-variable { color: #50fa7b; }
.cm-s-dracula span.cm-variable-2 { color: white; }
.cm-s-dracula span.cm-def { color: #50fa7b; }
.cm-s-dracula span.cm-operator { color: #ff79c6; }
.cm-s-dracula span.cm-keyword { color: #ff79c6; }
.cm-s-dracula span.cm-atom { color: #bd93f9; }
.cm-s-dracula span.cm-meta { color: #f8f8f2; }
.cm-s-dracula span.cm-tag { color: #ff79c6; }
.cm-s-dracula span.cm-attribute { color: #50fa7b; }
.cm-s-dracula span.cm-qualifier { color: #50fa7b; }
.cm-s-dracula span.cm-property { color: #66d9ef; }
.cm-s-dracula span.cm-builtin { color: #50fa7b; }
.cm-s-dracula span.cm-variable-3, .cm-s-dracula span.cm-type { color: #ffb86c; }

.cm-s-dracula .CodeMirror-activeline-background { background: rgba(255,255,255,0.1); }
.cm-s-dracula .CodeMirror-matchingbracket { text-decoration: underline; color: white !important; }

/*

    Name:       Hopscotch
    Author:     Jan T. Sott

    CodeMirror template by Jan T. Sott (https://github.com/idleberg/base16-codemirror)
    Original Base16 color scheme by Chris Kempson (https://github.com/chriskempson/base16)

*/

.cm-s-hopscotch.CodeMirror {background: #322931; color: #d5d3d5;}
.cm-s-hopscotch div.CodeMirror-selected {background: #433b42 !important;}
.cm-s-hopscotch .CodeMirror-gutters {background: #322931; border-right: 0px;}
.cm-s-hopscotch .CodeMirror-linenumber {color: #797379;}
.cm-s-hopscotch .CodeMirror-cursor {border-left: 1px solid #989498 !important;}

.cm-s-hopscotch span.cm-comment {color: #b33508;}
.cm-s-hopscotch span.cm-atom {color: #c85e7c;}
.cm-s-hopscotch span.cm-number {color: #c85e7c;}

.cm-s-hopscotch span.cm-property, .cm-s-hopscotch span.cm-attribute {color: #8fc13e;}
.cm-s-hopscotch span.cm-keyword {color: #dd464c;}
.cm-s-hopscotch span.cm-string {color: #fdcc59;}

.cm-s-hopscotch span.cm-variable {color: #8fc13e;}
.cm-s-hopscotch span.cm-variable-2 {color: #1290bf;}
.cm-s-hopscotch span.cm-def {color: #fd8b19;}
.cm-s-hopscotch span.cm-error {background: #dd464c; color: #989498;}
.cm-s-hopscotch span.cm-bracket {color: #d5d3d5;}
.cm-s-hopscotch span.cm-tag {color: #dd464c;}
.cm-s-hopscotch span.cm-link {color: #c85e7c;}

.cm-s-hopscotch .CodeMirror-matchingbracket { text-decoration: underline; color: white !important;}
.cm-s-hopscotch .CodeMirror-activeline-background { background: #302020; }

/****************************************************************/
/*   Based on mbonaci's Brackets mbo theme                      */
/*   https://github.com/mbonaci/global/blob/master/Mbo.tmTheme  */
/*   Create your own: http://tmtheme-editor.herokuapp.com       */
/****************************************************************/

.cm-s-mbo.CodeMirror { background: #2c2c2c; color: #ffffec; }
.cm-s-mbo div.CodeMirror-selected { background: #716C62; }
.cm-s-mbo .CodeMirror-line::selection, .cm-s-mbo .CodeMirror-line > span::selection, .cm-s-mbo .CodeMirror-line > span > span::selection { background: rgba(113, 108, 98, .99); }
.cm-s-mbo .CodeMirror-line::-moz-selection, .cm-s-mbo .CodeMirror-line > span::-moz-selection, .cm-s-mbo .CodeMirror-line > span > span::-moz-selection { background: rgba(113, 108, 98, .99); }
.cm-s-mbo .CodeMirror-gutters { background: #4e4e4e; border-right: 0px; }
.cm-s-mbo .CodeMirror-guttermarker { color: white; }
.cm-s-mbo .CodeMirror-guttermarker-subtle { color: grey; }
.cm-s-mbo .CodeMirror-linenumber { color: #dadada; }
.cm-s-mbo .CodeMirror-cursor { border-left: 1px solid #ffffec; }

.cm-s-mbo span.cm-comment { color: #95958a; }
.cm-s-mbo span.cm-atom { color: #00a8c6; }
.cm-s-mbo span.cm-number { color: #00a8c6; }

.cm-s-mbo span.cm-property, .cm-s-mbo span.cm-attribute { color: #9ddfe9; }
.cm-s-mbo span.cm-keyword { color: #ffb928; }
.cm-s-mbo span.cm-string { color: #ffcf6c; }
.cm-s-mbo span.cm-string.cm-property { color: #ffffec; }

.cm-s-mbo span.cm-variable { color: #ffffec; }
.cm-s-mbo span.cm-variable-2 { color: #00a8c6; }
.cm-s-mbo span.cm-def { color: #ffffec; }
.cm-s-mbo span.cm-bracket { color: #fffffc; font-weight: bold; }
.cm-s-mbo span.cm-tag { color: #9ddfe9; }
.cm-s-mbo span.cm-link { color: #f54b07; }
.cm-s-mbo span.cm-error { border-bottom: #636363; color: #ffffec; }
.cm-s-mbo span.cm-qualifier { color: #ffffec; }

.cm-s-mbo .CodeMirror-activeline-background { background: #494b41; }
.cm-s-mbo .CodeMirror-matchingbracket { color: #ffb928 !important; }
.cm-s-mbo .CodeMirror-matchingtag { background: rgba(255, 255, 255, .37); }

/*
  MDN-LIKE Theme - Mozilla
  Ported to CodeMirror by Peter Kroon <plakroon@gmail.com>
  Report bugs/issues here: https://github.com/codemirror/CodeMirror/issues
  GitHub: @peterkroon

  The mdn-like theme is inspired on the displayed code examples at: https://developer.mozilla.org/en-US/docs/Web/CSS/animation

*/
.cm-s-mdn-like.CodeMirror { color: #999; background-color: #fff; }
.cm-s-mdn-like div.CodeMirror-selected { background: #cfc; }
.cm-s-mdn-like .CodeMirror-line::selection, .cm-s-mdn-like .CodeMirror-line > span::selection, .cm-s-mdn-like .CodeMirror-line > span > span::selection { background: #cfc; }
.cm-s-mdn-like .CodeMirror-line::-moz-selection, .cm-s-mdn-like .CodeMirror-line > span::-moz-selection, .cm-s-mdn-like .CodeMirror-line > span > span::-moz-selection { background: #cfc; }

.cm-s-mdn-like .CodeMirror-gutters { background: #f8f8f8; border-left: 6px solid rgba(0,83,159,0.65); color: #333; }
.cm-s-mdn-like .CodeMirror-linenumber { color: #aaa; padding-left: 8px; }
.cm-s-mdn-like .CodeMirror-cursor { border-left: 2px solid #222; }

.cm-s-mdn-like .cm-keyword { color: #6262FF; }
.cm-s-mdn-like .cm-atom { color: #F90; }
.cm-s-mdn-like .cm-number { color:  #ca7841; }
.cm-s-mdn-like .cm-def { color: #8DA6CE; }
.cm-s-mdn-like span.cm-variable-2, .cm-s-mdn-like span.cm-tag { color: #690; }
.cm-s-mdn-like span.cm-variable-3, .cm-s-mdn-like span.cm-def, .cm-s-mdn-like span.cm-type { color: #07a; }

.cm-s-mdn-like .cm-variable { color: #07a; }
.cm-s-mdn-like .cm-property { color: #905; }
.cm-s-mdn-like .cm-qualifier { color: #690; }

.cm-s-mdn-like .cm-operator { color: #cda869; }
.cm-s-mdn-like .cm-comment { color:#777; font-weight:normal; }
.cm-s-mdn-like .cm-string { color:#07a; font-style:italic; }
.cm-s-mdn-like .cm-string-2 { color:#bd6b18; } /*?*/
.cm-s-mdn-like .cm-meta { color: #000; } /*?*/
.cm-s-mdn-like .cm-builtin { color: #9B7536; } /*?*/
.cm-s-mdn-like .cm-tag { color: #997643; }
.cm-s-mdn-like .cm-attribute { color: #d6bb6d; } /*?*/
.cm-s-mdn-like .cm-header { color: #FF6400; }
.cm-s-mdn-like .cm-hr { color: #AEAEAE; }
.cm-s-mdn-like .cm-link { color:#ad9361; font-style:italic; text-decoration:none; }
.cm-s-mdn-like .cm-error { border-bottom: 1px solid red; }

div.cm-s-mdn-like .CodeMirror-activeline-background { background: #efefff; }
div.cm-s-mdn-like span.CodeMirror-matchingbracket { outline:1px solid grey; color: inherit; }

.cm-s-mdn-like.CodeMirror { background-image: url(data:image/png;base64,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); }

/*

    Name:       seti
    Author:     Michael Kaminsky (http://github.com/mkaminsky11)

    Original seti color scheme by Jesse Weed (https://github.com/jesseweed/seti-syntax)

*/


.cm-s-seti.CodeMirror {
  background-color: #151718 !important;
  color: #CFD2D1 !important;
  border: none;
}
.cm-s-seti .CodeMirror-gutters {
  color: #404b53;
  background-color: #0E1112;
  border: none;
}
.cm-s-seti .CodeMirror-cursor { border-left: solid thin #f8f8f0; }
.cm-s-seti .CodeMirror-linenumber { color: #6D8A88; }
.cm-s-seti.CodeMirror-focused div.CodeMirror-selected { background: rgba(255, 255, 255, 0.10); }
.cm-s-seti .CodeMirror-line::selection, .cm-s-seti .CodeMirror-line > span::selection, .cm-s-seti .CodeMirror-line > span > span::selection { background: rgba(255, 255, 255, 0.10); }
.cm-s-seti .CodeMirror-line::-moz-selection, .cm-s-seti .CodeMirror-line > span::-moz-selection, .cm-s-seti .CodeMirror-line > span > span::-moz-selection { background: rgba(255, 255, 255, 0.10); }
.cm-s-seti span.cm-comment { color: #41535b; }
.cm-s-seti span.cm-string, .cm-s-seti span.cm-string-2 { color: #55b5db; }
.cm-s-seti span.cm-number { color: #cd3f45; }
.cm-s-seti span.cm-variable { color: #55b5db; }
.cm-s-seti span.cm-variable-2 { color: #a074c4; }
.cm-s-seti span.cm-def { color: #55b5db; }
.cm-s-seti span.cm-keyword { color: #ff79c6; }
.cm-s-seti span.cm-operator { color: #9fca56; }
.cm-s-seti span.cm-keyword { color: #e6cd69; }
.cm-s-seti span.cm-atom { color: #cd3f45; }
.cm-s-seti span.cm-meta { color: #55b5db; }
.cm-s-seti span.cm-tag { color: #55b5db; }
.cm-s-seti span.cm-attribute { color: #9fca56; }
.cm-s-seti span.cm-qualifier { color: #9fca56; }
.cm-s-seti span.cm-property { color: #a074c4; }
.cm-s-seti span.cm-variable-3, .cm-s-seti span.cm-type { color: #9fca56; }
.cm-s-seti span.cm-builtin { color: #9fca56; }
.cm-s-seti .CodeMirror-activeline-background { background: #101213; }
.cm-s-seti .CodeMirror-matchingbracket { text-decoration: underline; color: white !important; }

/*
Solarized theme for code-mirror
http://ethanschoonover.com/solarized
*/

/*
Solarized color palette
http://ethanschoonover.com/solarized/img/solarized-palette.png
*/

.solarized.base03 { color: #002b36; }
.solarized.base02 { color: #073642; }
.solarized.base01 { color: #586e75; }
.solarized.base00 { color: #657b83; }
.solarized.base0 { color: #839496; }
.solarized.base1 { color: #93a1a1; }
.solarized.base2 { color: #eee8d5; }
.solarized.base3  { color: #fdf6e3; }
.solarized.solar-yellow  { color: #b58900; }
.solarized.solar-orange  { color: #cb4b16; }
.solarized.solar-red { color: #dc322f; }
.solarized.solar-magenta { color: #d33682; }
.solarized.solar-violet  { color: #6c71c4; }
.solarized.solar-blue { color: #268bd2; }
.solarized.solar-cyan { color: #2aa198; }
.solarized.solar-green { color: #859900; }

/* Color scheme for code-mirror */

.cm-s-solarized {
  line-height: 1.45em;
  color-profile: sRGB;
  rendering-intent: auto;
}
.cm-s-solarized.cm-s-dark {
  color: #839496;
  background-color: #002b36;
  text-shadow: #002b36 0 1px;
}
.cm-s-solarized.cm-s-light {
  background-color: #fdf6e3;
  color: #657b83;
  text-shadow: #eee8d5 0 1px;
}

.cm-s-solarized .CodeMirror-widget {
  text-shadow: none;
}

.cm-s-solarized .cm-header { color: #586e75; }
.cm-s-solarized .cm-quote { color: #93a1a1; }

.cm-s-solarized .cm-keyword { color: #cb4b16; }
.cm-s-solarized .cm-atom { color: #d33682; }
.cm-s-solarized .cm-number { color: #d33682; }
.cm-s-solarized .cm-def { color: #2aa198; }

.cm-s-solarized .cm-variable { color: #839496; }
.cm-s-solarized .cm-variable-2 { color: #b58900; }
.cm-s-solarized .cm-variable-3, .cm-s-solarized .cm-type { color: #6c71c4; }

.cm-s-solarized .cm-property { color: #2aa198; }
.cm-s-solarized .cm-operator { color: #6c71c4; }

.cm-s-solarized .cm-comment { color: #586e75; font-style:italic; }

.cm-s-solarized .cm-string { color: #859900; }
.cm-s-solarized .cm-string-2 { color: #b58900; }

.cm-s-solarized .cm-meta { color: #859900; }
.cm-s-solarized .cm-qualifier { color: #b58900; }
.cm-s-solarized .cm-builtin { color: #d33682; }
.cm-s-solarized .cm-bracket { color: #cb4b16; }
.cm-s-solarized .CodeMirror-matchingbracket { color: #859900; }
.cm-s-solarized .CodeMirror-nonmatchingbracket { color: #dc322f; }
.cm-s-solarized .cm-tag { color: #93a1a1; }
.cm-s-solarized .cm-attribute { color: #2aa198; }
.cm-s-solarized .cm-hr {
  color: transparent;
  border-top: 1px solid #586e75;
  display: block;
}
.cm-s-solarized .cm-link { color: #93a1a1; cursor: pointer; }
.cm-s-solarized .cm-special { color: #6c71c4; }
.cm-s-solarized .cm-em {
  color: #999;
  text-decoration: underline;
  text-decoration-style: dotted;
}
.cm-s-solarized .cm-error,
.cm-s-solarized .cm-invalidchar {
  color: #586e75;
  border-bottom: 1px dotted #dc322f;
}

.cm-s-solarized.cm-s-dark div.CodeMirror-selected { background: #073642; }
.cm-s-solarized.cm-s-dark.CodeMirror ::selection { background: rgba(7, 54, 66, 0.99); }
.cm-s-solarized.cm-s-dark .CodeMirror-line::-moz-selection, .cm-s-dark .CodeMirror-line > span::-moz-selection, .cm-s-dark .CodeMirror-line > span > span::-moz-selection { background: rgba(7, 54, 66, 0.99); }

.cm-s-solarized.cm-s-light div.CodeMirror-selected { background: #eee8d5; }
.cm-s-solarized.cm-s-light .CodeMirror-line::selection, .cm-s-light .CodeMirror-line > span::selection, .cm-s-light .CodeMirror-line > span > span::selection { background: #eee8d5; }
.cm-s-solarized.cm-s-light .CodeMirror-line::-moz-selection, .cm-s-ligh .CodeMirror-line > span::-moz-selection, .cm-s-ligh .CodeMirror-line > span > span::-moz-selection { background: #eee8d5; }

/* Editor styling */



/* Little shadow on the view-port of the buffer view */
.cm-s-solarized.CodeMirror {
  -moz-box-shadow: inset 7px 0 12px -6px #000;
  -webkit-box-shadow: inset 7px 0 12px -6px #000;
  box-shadow: inset 7px 0 12px -6px #000;
}

/* Remove gutter border */
.cm-s-solarized .CodeMirror-gutters {
  border-right: 0;
}

/* Gutter colors and line number styling based of color scheme (dark / light) */

/* Dark */
.cm-s-solarized.cm-s-dark .CodeMirror-gutters {
  background-color: #073642;
}

.cm-s-solarized.cm-s-dark .CodeMirror-linenumber {
  color: #586e75;
  text-shadow: #021014 0 -1px;
}

/* Light */
.cm-s-solarized.cm-s-light .CodeMirror-gutters {
  background-color: #eee8d5;
}

.cm-s-solarized.cm-s-light .CodeMirror-linenumber {
  color: #839496;
}

/* Common */
.cm-s-solarized .CodeMirror-linenumber {
  padding: 0 5px;
}
.cm-s-solarized .CodeMirror-guttermarker-subtle { color: #586e75; }
.cm-s-solarized.cm-s-dark .CodeMirror-guttermarker { color: #ddd; }
.cm-s-solarized.cm-s-light .CodeMirror-guttermarker { color: #cb4b16; }

.cm-s-solarized .CodeMirror-gutter .CodeMirror-gutter-text {
  color: #586e75;
}

/* Cursor */
.cm-s-solarized .CodeMirror-cursor { border-left: 1px solid #819090; }

/* Fat cursor */
.cm-s-solarized.cm-s-light.cm-fat-cursor .CodeMirror-cursor { background: #77ee77; }
.cm-s-solarized.cm-s-light .cm-animate-fat-cursor { background-color: #77ee77; }
.cm-s-solarized.cm-s-dark.cm-fat-cursor .CodeMirror-cursor { background: #586e75; }
.cm-s-solarized.cm-s-dark .cm-animate-fat-cursor { background-color: #586e75; }

/* Active line */
.cm-s-solarized.cm-s-dark .CodeMirror-activeline-background {
  background: rgba(255, 255, 255, 0.06);
}
.cm-s-solarized.cm-s-light .CodeMirror-activeline-background {
  background: rgba(0, 0, 0, 0.06);
}

.cm-s-the-matrix.CodeMirror { background: #000000; color: #00FF00; }
.cm-s-the-matrix div.CodeMirror-selected { background: #2D2D2D; }
.cm-s-the-matrix .CodeMirror-line::selection, .cm-s-the-matrix .CodeMirror-line > span::selection, .cm-s-the-matrix .CodeMirror-line > span > span::selection { background: rgba(45, 45, 45, 0.99); }
.cm-s-the-matrix .CodeMirror-line::-moz-selection, .cm-s-the-matrix .CodeMirror-line > span::-moz-selection, .cm-s-the-matrix .CodeMirror-line > span > span::-moz-selection { background: rgba(45, 45, 45, 0.99); }
.cm-s-the-matrix .CodeMirror-gutters { background: #060; border-right: 2px solid #00FF00; }
.cm-s-the-matrix .CodeMirror-guttermarker { color: #0f0; }
.cm-s-the-matrix .CodeMirror-guttermarker-subtle { color: white; }
.cm-s-the-matrix .CodeMirror-linenumber { color: #FFFFFF; }
.cm-s-the-matrix .CodeMirror-cursor { border-left: 1px solid #00FF00; }

.cm-s-the-matrix span.cm-keyword { color: #008803; font-weight: bold; }
.cm-s-the-matrix span.cm-atom { color: #3FF; }
.cm-s-the-matrix span.cm-number { color: #FFB94F; }
.cm-s-the-matrix span.cm-def { color: #99C; }
.cm-s-the-matrix span.cm-variable { color: #F6C; }
.cm-s-the-matrix span.cm-variable-2 { color: #C6F; }
.cm-s-the-matrix span.cm-variable-3, .cm-s-the-matrix span.cm-type { color: #96F; }
.cm-s-the-matrix span.cm-property { color: #62FFA0; }
.cm-s-the-matrix span.cm-operator { color: #999; }
.cm-s-the-matrix span.cm-comment { color: #CCCCCC; }
.cm-s-the-matrix span.cm-string { color: #39C; }
.cm-s-the-matrix span.cm-meta { color: #C9F; }
.cm-s-the-matrix span.cm-qualifier { color: #FFF700; }
.cm-s-the-matrix span.cm-builtin { color: #30a; }
.cm-s-the-matrix span.cm-bracket { color: #cc7; }
.cm-s-the-matrix span.cm-tag { color: #FFBD40; }
.cm-s-the-matrix span.cm-attribute { color: #FFF700; }
.cm-s-the-matrix span.cm-error { color: #FF0000; }

.cm-s-the-matrix .CodeMirror-activeline-background { background: #040; }

/*
Copyright (C) 2011 by MarkLogic Corporation
Author: Mike Brevoort <mike@brevoort.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
*/
.cm-s-xq-light span.cm-keyword { line-height: 1em; font-weight: bold; color: #5A5CAD; }
.cm-s-xq-light span.cm-atom { color: #6C8CD5; }
.cm-s-xq-light span.cm-number { color: #164; }
.cm-s-xq-light span.cm-def { text-decoration:underline; }
.cm-s-xq-light span.cm-variable { color: black; }
.cm-s-xq-light span.cm-variable-2 { color:black; }
.cm-s-xq-light span.cm-variable-3, .cm-s-xq-light span.cm-type { color: black; }
.cm-s-xq-light span.cm-property {}
.cm-s-xq-light span.cm-operator {}
.cm-s-xq-light span.cm-comment { color: #0080FF; font-style: italic; }
.cm-s-xq-light span.cm-string { color: red; }
.cm-s-xq-light span.cm-meta { color: yellow; }
.cm-s-xq-light span.cm-qualifier { color: grey; }
.cm-s-xq-light span.cm-builtin { color: #7EA656; }
.cm-s-xq-light span.cm-bracket { color: #cc7; }
.cm-s-xq-light span.cm-tag { color: #3F7F7F; }
.cm-s-xq-light span.cm-attribute { color: #7F007F; }
.cm-s-xq-light span.cm-error { color: #f00; }

.cm-s-xq-light .CodeMirror-activeline-background { background: #e8f2ff; }
.cm-s-xq-light .CodeMirror-matchingbracket { outline:1px solid grey;color:black !important;background:yellow; }

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.CodeMirror {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;
  /* Changed to auto to autogrow */
}

.CodeMirror pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

/* This causes https://github.com/jupyter/jupyterlab/issues/522 */
/* May not cause it not because we changed it! */
.CodeMirror-lines {
  padding: var(--jp-code-padding) 0;
}

.CodeMirror-linenumber {
  padding: 0 8px;
}

.jp-CodeMirrorEditor-static {
  margin: var(--jp-code-padding);
}

.jp-CodeMirrorEditor,
.jp-CodeMirrorEditor-static {
  cursor: text;
}

.jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
  border-left: var(--jp-code-cursor-width0) solid var(--jp-editor-cursor-color);
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.CodeMirror.jp-mod-readOnly .CodeMirror-cursor {
  display: none;
}

.CodeMirror-gutters {
  border-right: 1px solid var(--jp-border-color2);
  background-color: var(--jp-layout-color0);
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.CodeMirror-selectedtext.cm-searching {
  background-color: var(--jp-search-selected-match-background-color) !important;
  color: var(--jp-search-selected-match-color) !important;
}

.cm-searching {
  background-color: var(
    --jp-search-unselected-match-background-color
  ) !important;
  color: var(--jp-search-unselected-match-color) !important;
}

.CodeMirror-focused .CodeMirror-selected {
  background-color: var(--jp-editor-selected-focused-background);
}

.CodeMirror-selected {
  background-color: var(--jp-editor-selected-background);
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/**
 * Here is our jupyter theme for CodeMirror syntax highlighting
 * This is used in our marked.js syntax highlighting and CodeMirror itself
 * The string "jupyter" is set in ../codemirror/widget.DEFAULT_CODEMIRROR_THEME
 * This came from the classic notebook, which came form highlight.js/GitHub
 */

/**
 * CodeMirror themes are handling the background/color in this way. This works
 * fine for CodeMirror editors outside the notebook, but the notebook styles
 * these things differently.
 */
.CodeMirror.cm-s-jupyter {
  background: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

/* In the notebook, we want this styling to be handled by its container */
.jp-CodeConsole .CodeMirror.cm-s-jupyter,
.jp-Notebook .CodeMirror.cm-s-jupyter {
  background: transparent;
}

.cm-s-jupyter .CodeMirror-cursor {
  border-left: var(--jp-code-cursor-width0) solid var(--jp-editor-cursor-color);
}
.cm-s-jupyter span.cm-keyword {
  color: var(--jp-mirror-editor-keyword-color);
  font-weight: bold;
}
.cm-s-jupyter span.cm-atom {
  color: var(--jp-mirror-editor-atom-color);
}
.cm-s-jupyter span.cm-number {
  color: var(--jp-mirror-editor-number-color);
}
.cm-s-jupyter span.cm-def {
  color: var(--jp-mirror-editor-def-color);
}
.cm-s-jupyter span.cm-variable {
  color: var(--jp-mirror-editor-variable-color);
}
.cm-s-jupyter span.cm-variable-2 {
  color: var(--jp-mirror-editor-variable-2-color);
}
.cm-s-jupyter span.cm-variable-3 {
  color: var(--jp-mirror-editor-variable-3-color);
}
.cm-s-jupyter span.cm-punctuation {
  color: var(--jp-mirror-editor-punctuation-color);
}
.cm-s-jupyter span.cm-property {
  color: var(--jp-mirror-editor-property-color);
}
.cm-s-jupyter span.cm-operator {
  color: var(--jp-mirror-editor-operator-color);
  font-weight: bold;
}
.cm-s-jupyter span.cm-comment {
  color: var(--jp-mirror-editor-comment-color);
  font-style: italic;
}
.cm-s-jupyter span.cm-string {
  color: var(--jp-mirror-editor-string-color);
}
.cm-s-jupyter span.cm-string-2 {
  color: var(--jp-mirror-editor-string-2-color);
}
.cm-s-jupyter span.cm-meta {
  color: var(--jp-mirror-editor-meta-color);
}
.cm-s-jupyter span.cm-qualifier {
  color: var(--jp-mirror-editor-qualifier-color);
}
.cm-s-jupyter span.cm-builtin {
  color: var(--jp-mirror-editor-builtin-color);
}
.cm-s-jupyter span.cm-bracket {
  color: var(--jp-mirror-editor-bracket-color);
}
.cm-s-jupyter span.cm-tag {
  color: var(--jp-mirror-editor-tag-color);
}
.cm-s-jupyter span.cm-attribute {
  color: var(--jp-mirror-editor-attribute-color);
}
.cm-s-jupyter span.cm-header {
  color: var(--jp-mirror-editor-header-color);
}
.cm-s-jupyter span.cm-quote {
  color: var(--jp-mirror-editor-quote-color);
}
.cm-s-jupyter span.cm-link {
  color: var(--jp-mirror-editor-link-color);
}
.cm-s-jupyter span.cm-error {
  color: var(--jp-mirror-editor-error-color);
}
.cm-s-jupyter span.cm-hr {
  color: #999;
}

.cm-s-jupyter span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}

.cm-s-jupyter .CodeMirror-activeline-background,
.cm-s-jupyter .CodeMirror-gutter {
  background-color: var(--jp-layout-color2);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0px;
  padding: 0px;
  line-height: normal;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}
.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}
.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}
.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}
.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}
.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}
.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}
.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}
.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}
.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
}
.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
}
.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
}
.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
}
.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
}
.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
}
.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
}
.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}
.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}
.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}
.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}
.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}
.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}
.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}
.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
}
.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
}
.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
}
.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
}
.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
}
.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
}
.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
}
.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}
.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}
.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0em;
}

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: 12px;
  table-layout: fixed;
  margin-left: auto;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon table {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0px;
}

.jp-RenderedHTMLCommon p {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}
[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}
/* ...or leave it untouched if they don't */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-dark-background {
}
[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-light-background {
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}
.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}
.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}
.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}
.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}
.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}
.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}
.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}
.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: 0.8em;
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser {
  display: flex;
  flex-direction: column;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  border-bottom: none;
  height: auto;
  margin: var(--jp-toolbar-header-margin);
  box-shadow: none;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 4px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0px 2px;
  padding: 0px 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0px;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar.jp-Toolbar {
  padding: 0px;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  justify-content: space-evenly;
}

.jp-FileBrowser-toolbar.jp-Toolbar .jp-Toolbar-item {
  flex: 1;
}

.jp-FileBrowser-toolbar.jp-Toolbar .jp-ToolbarButtonComponent {
  width: 100%;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px 12px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-item.jp-mod-selected {
  color: white;
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon:before {
  color: limegreen;
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0px;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-DirListing-deadSpace {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

.jp-FileDialog.jp-mod-conflict input {
  color: red;
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
}

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: flex;
  flex-direction: row;
}

.jp-OutputPrompt {
  flex: 0 0 var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);
  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-OutputArea-output {
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea-child .jp-OutputArea-output {
  flex-grow: 1;
  flex-shrink: 1;
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `p-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0px;
  padding: 0px;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0px;
  flex: 1 1 auto;
}

.jp-OutputArea-executeResult.jp-RenderedText {
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-OutputArea-stdin {
  line-height: var(--jp-code-line-height);
  padding-top: var(--jp-code-padding);
  display: flex;
}

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0px;
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;
  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0px;
  bottom: 0px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0px;
  width: 100%;
  padding: 0px;
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: flex;
  flex-direction: row;
}

.jp-InputArea-editor {
  flex: 1 1 auto;
}

.jp-InputArea-editor {
  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0px;
  background: var(--jp-cell-editor-background);
}

.jp-InputPrompt {
  flex: 0 0 var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);
  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: flex;
  flex-direction: row;
  flex: 1 1 auto;
}

.jp-Placeholder-prompt {
  box-sizing: border-box;
}

.jp-Placeholder-content {
  flex: 1 1 auto;
  border: none;
  background: transparent;
  height: 20px;
  box-sizing: border-box;
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0px 0px 2px 0px rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0px;
  margin: 0px;
  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 200px;
  box-shadow: inset 0 0 6px 2px rgba(0, 0, 0, 0.3);
  margin-left: var(--jp-private-cell-scrolling-output-offset);
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  flex: 0 0
    calc(
      var(--jp-cell-prompt-width) -
        var(--jp-private-cell-scrolling-output-offset)
    );
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  flex: 1 1 auto;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: 2px;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: flex;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0px rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0px;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0px rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-NotebookTools-tool {
  padding: 0px 12px 0 12px;
}

.jp-ActiveCellTool {
  padding: 12px;
  background-color: var(--jp-layout-color1);
  border-top: none !important;
}

.jp-ActiveCellTool .jp-InputArea-prompt {
  flex: 0 0 auto;
  padding-left: 0px;
}

.jp-ActiveCellTool .jp-InputArea-editor {
  flex: 1 1 auto;
  background: var(--jp-cell-editor-background);
  border-color: var(--jp-cell-editor-border-color);
}

.jp-ActiveCellTool .jp-InputArea-editor .CodeMirror {
  background: transparent;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0px 12px 0px;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label {
  line-height: 1.4;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

</style>

    <style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0px 2px 1px -1px var(--jp-shadow-umbra-color),
    0px 1px 1px 0px var(--jp-shadow-penumbra-color),
    0px 1px 3px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0px 3px 1px -2px var(--jp-shadow-umbra-color),
    0px 2px 2px 0px var(--jp-shadow-penumbra-color),
    0px 1px 5px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0px 2px 4px -1px var(--jp-shadow-umbra-color),
    0px 4px 5px 0px var(--jp-shadow-penumbra-color),
    0px 1px 10px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0px 3px 5px -1px var(--jp-shadow-umbra-color),
    0px 6px 10px 0px var(--jp-shadow-penumbra-color),
    0px 1px 18px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0px 5px 5px -3px var(--jp-shadow-umbra-color),
    0px 8px 10px 1px var(--jp-shadow-penumbra-color),
    0px 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0px 7px 8px -4px var(--jp-shadow-umbra-color),
    0px 12px 17px 2px var(--jp-shadow-penumbra-color),
    0px 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0px 8px 10px -5px var(--jp-shadow-umbra-color),
    0px 16px 24px 2px var(--jp-shadow-penumbra-color),
    0px 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0px 10px 13px -6px var(--jp-shadow-umbra-color),
    0px 20px 31px 3px var(--jp-shadow-penumbra-color),
    0px 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0px 11px 15px -7px var(--jp-shadow-umbra-color),
    0px 24px 38px 3px var(--jp-shadow-penumbra-color),
    0px 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;

  --jp-ui-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica,
    Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;

  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);

  --jp-content-link-color: var(--md-blue-700);

  --jp-content-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: Menlo, Consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-700);
  --jp-brand-color1: var(--md-blue-500);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);

  --jp-accent-color0: var(--md-green-700);
  --jp-accent-color1: var(--md-green-500);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-700);
  --jp-warn-color1: var(--md-orange-500);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);

  --jp-error-color0: var(--md-red-700);
  --jp-error-color1: var(--md-red-500);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);

  --jp-success-color0: var(--md-green-700);
  --jp-success-color1: var(--md-green-500);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);

  --jp-info-color0: var(--md-cyan-700);
  --jp-info-color1: var(--md-cyan-500);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;

  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;

  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);

  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: 'Source Code Pro', monospace;
  --jp-cell-prompt-letter-spacing: 0px;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);
  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;
  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0px 0px 2px 0px rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0px 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-border-color1);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: #05a;
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #aa22ff;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #aa22ff;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 180px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);
}
</style>

<style type="text/css">
a.anchor-link {
   display: none;
}
.highlight  {
    margin: 0.4em;
}

/* Input area styling */
.jp-InputArea {
    overflow: hidden;
}

.jp-InputArea-editor {
    overflow: hidden;
}

@media print {
  body {
    margin: 0;
  }
}
</style>



<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-MML-AM_CHTML-full,Safe"> </script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                CommonHTML: {
                    linebreaks: { 
                    automatic: true 
                    }
                },
                "HTML-CSS": {
                    linebreaks: { 
                    automatic: true 
                    }
                }
            });
        
            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
    <!-- End of mathjax configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">

<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h1 id="Compara&#231;&#227;o-do-tamanho-da-descri&#231;&#227;o-de-habilidades-com-a-data-de-lan&#231;amento-de-campe&#245;es-(LoL)">Compara&#231;&#227;o do tamanho da descri&#231;&#227;o de habilidades com a data de lan&#231;amento de campe&#245;es (LoL)<a class="anchor-link" href="#Compara&#231;&#227;o-do-tamanho-da-descri&#231;&#227;o-de-habilidades-com-a-data-de-lan&#231;amento-de-campe&#245;es-(LoL)">&#182;</a></h1><p>Objetivo: Verificar se a data de lançamento do campeão influencia no tamanho da descrição das habilidades.</p>
<p>Como: Usando data scraping através da library "BeautifulSoup" dos sites de fandom de LoL para obter os nomes das personagens, a descrição de suas habilidades, as datas de lançamento/rework.</p>
<p>Observação: Como os sites podem mudar facilmente de formato/conteúdo é provável que o código aqui utilizado não funcionará futuramente.</p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Passos:</p>

<pre><code>1) Obter as descrições das habilidades
2) Obter as datas de lançamento
3) Obter as datas de rework (o campeão pode ser "lançado" mais de uma vez)
4) Agregar tudo num dataframe para realizar a análise    
5) Extrair os dados para um arquivo json</code></pre>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h3 id="1)-Obtendo-as-descri&#231;&#245;es-das-habilidades-dos-campe&#245;es">1) Obtendo as descri&#231;&#245;es das habilidades dos campe&#245;es<a class="anchor-link" href="#1)-Obtendo-as-descri&#231;&#245;es-das-habilidades-dos-campe&#245;es">&#182;</a></h3><p>Cada habilidade, como pode ser visto utilizando o dev console (abaixo) fica dentro de uma âncora:</p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p><img src="data:image/png;base64,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" alt="image.png"></p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Dentro dela estão as imagens e as descrições:</p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p><img src="data:image/png;base64,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" alt="image1.png"></p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Utilizaremos BeautifulSoup para obtermos as informações desejadas e criar um dicionário para armazenar os dados de forma mais simples, facilitando a utilização.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs jp-mod-noInput ">

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs jp-mod-noInput ">

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Existem atualmente 156 personagens, sendo 1 deles recém-lançado: Akshan, que não consta nesta lista.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">
<pre>155
</pre>
</div>
</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Como pode-se ver acima, obtemos todas as habilidades de todos os heróis até agora. Para realizar a análise desejada é necessário obter mais dados, como a data de lançamento de todos os heróis (incluindo as datas de "relançamento", que será feito abaixo).</p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h3 id="2)-Obtendo-as-datas-de-lan&#231;amento">2) Obtendo as datas de lan&#231;amento<a class="anchor-link" href="#2)-Obtendo-as-datas-de-lan&#231;amento">&#182;</a></h3>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs jp-mod-noInput ">

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">



<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">
<pre>datetime.date(2009, 2, 21)</pre>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h3 id="3)-Obtendo-as-datas-de-atualiza&#231;&#227;o-dos-her&#243;is">3) Obtendo as datas de atualiza&#231;&#227;o dos her&#243;is<a class="anchor-link" href="#3)-Obtendo-as-datas-de-atualiza&#231;&#227;o-dos-her&#243;is">&#182;</a></h3>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">
<pre>Invalid isoformat string: &#39;2022-XX-XX&#39;
</pre>
</div>
</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">
<pre>74
</pre>
</div>
</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h3 id="4)-Juntamos-agora-as-habilidades-e-as-datas-de-lan&#231;amento-de-cada-campe&#227;o">4) Juntamos agora as habilidades e as datas de lan&#231;amento de cada campe&#227;o<a class="anchor-link" href="#4)-Juntamos-agora-as-habilidades-e-as-datas-de-lan&#231;amento-de-cada-campe&#227;o">&#182;</a></h3>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs jp-mod-noInput ">

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs jp-mod-noInput ">

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h3 id="5)-Agora-&#233;-poss&#237;vel-come&#231;ar-a-analisar-os-dados-obtidos">5) Agora &#233; poss&#237;vel come&#231;ar a analisar os dados obtidos<a class="anchor-link" href="#5)-Agora-&#233;-poss&#237;vel-come&#231;ar-a-analisar-os-dados-obtidos">&#182;</a></h3>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">
<pre>155
</pre>
</div>
</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">


<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>champion_name</th>
      <th>ability_len</th>
      <th>release_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Caitlyn</td>
      <td>1185.0</td>
      <td>2015-11-10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Fiddlesticks</td>
      <td>2030.0</td>
      <td>2020-04-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sylas</td>
      <td>2250.0</td>
      <td>2019-01-25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Senna</td>
      <td>2194.0</td>
      <td>2019-11-10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Tahm Kench</td>
      <td>3219.0</td>
      <td>2021-06-23</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>150</th>
      <td>Blitzcrank</td>
      <td>859.0</td>
      <td>2009-09-02</td>
    </tr>
    <tr>
      <th>151</th>
      <td>Cassiopeia</td>
      <td>804.0</td>
      <td>2016-05-04</td>
    </tr>
    <tr>
      <th>152</th>
      <td>Zoe</td>
      <td>558.0</td>
      <td>2017-11-21</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Taliyah</td>
      <td>1463.0</td>
      <td>2016-05-18</td>
    </tr>
    <tr>
      <th>154</th>
      <td>Nunu</td>
      <td>1327.0</td>
      <td>2018-08-28</td>
    </tr>
  </tbody>
</table>
<p>155 rows × 3 columns</p>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">


<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>champion_name</th>
      <th>ability_len</th>
      <th>release_date</th>
      <th>reworked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Caitlyn</td>
      <td>1185.0</td>
      <td>2015-11-10</td>
      <td>red</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Fiddlesticks</td>
      <td>2030.0</td>
      <td>2020-04-01</td>
      <td>red</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sylas</td>
      <td>2250.0</td>
      <td>2019-01-25</td>
      <td>blue</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Senna</td>
      <td>2194.0</td>
      <td>2019-11-10</td>
      <td>blue</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Tahm Kench</td>
      <td>3219.0</td>
      <td>2021-06-23</td>
      <td>red</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>150</th>
      <td>Blitzcrank</td>
      <td>859.0</td>
      <td>2009-09-02</td>
      <td>blue</td>
    </tr>
    <tr>
      <th>151</th>
      <td>Cassiopeia</td>
      <td>804.0</td>
      <td>2016-05-04</td>
      <td>red</td>
    </tr>
    <tr>
      <th>152</th>
      <td>Zoe</td>
      <td>558.0</td>
      <td>2017-11-21</td>
      <td>blue</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Taliyah</td>
      <td>1463.0</td>
      <td>2016-05-18</td>
      <td>blue</td>
    </tr>
    <tr>
      <th>154</th>
      <td>Nunu</td>
      <td>1327.0</td>
      <td>2018-08-28</td>
      <td>red</td>
    </tr>
  </tbody>
</table>
<p>155 rows × 4 columns</p>
</div>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h3 id="Abaixo,-mostro-em-vermelho-os-campe&#245;es-que-sofreram-rework-e-em-azul-os-que-n&#227;o-sofreram.">Abaixo, mostro em vermelho os campe&#245;es que sofreram rework e em azul os que n&#227;o sofreram.<a class="anchor-link" href="#Abaixo,-mostro-em-vermelho-os-campe&#245;es-que-sofreram-rework-e-em-azul-os-que-n&#227;o-sofreram.">&#182;</a></h3>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">



<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">
<pre>&lt;AxesSubplot:xlabel=&#39;release_date&#39;, ylabel=&#39;ability_len&#39;&gt;</pre>
</div>

</div>

<div class="jp-OutputArea-child">



<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Comparação da média de tamanho da descrição de habilidades de personagens que sofreram rework com os que não sofreram.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">
<pre>reworked mean:  1396.2567567567567
74
non-reworked mean:  1671.7777777777778
81
</pre>
</div>
</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Uso dos dados de campeões anuais para realizar análise.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs jp-mod-noInput ">

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">


<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Mean</th>
      <th>std</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2009.0</td>
      <td>905.538462</td>
      <td>300.028781</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010.0</td>
      <td>1216.666667</td>
      <td>376.113458</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011.0</td>
      <td>1174.384615</td>
      <td>495.684970</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2012.0</td>
      <td>1343.533333</td>
      <td>714.446326</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013.0</td>
      <td>1236.909091</td>
      <td>494.363521</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2014.0</td>
      <td>2021.833333</td>
      <td>1050.205939</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2015.0</td>
      <td>1375.700000</td>
      <td>375.856930</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2016.0</td>
      <td>1385.571429</td>
      <td>494.301079</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2017.0</td>
      <td>1474.230769</td>
      <td>916.802974</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2018.0</td>
      <td>1607.250000</td>
      <td>709.555142</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2019.0</td>
      <td>2311.900000</td>
      <td>2306.895290</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2020.0</td>
      <td>2628.777778</td>
      <td>886.396466</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2021.0</td>
      <td>2087.857143</td>
      <td>1134.709717</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell  jp-mod-noInput ">

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">



<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">
<pre>&lt;AxesSubplot:xlabel=&#39;Year&#39;, ylabel=&#39;Mean&#39;&gt;</pre>
</div>

</div>

<div class="jp-OutputArea-child">



<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAAEGCAYAAABy53LJAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8vihELAAAACXBIWXMAAAsTAAALEwEAmpwYAAAZvklEQVR4nO3df5Bd5X3f8ffnivWu6pVjIW3A1WqiX0AG0FqQ7TCNxrGCaScYVw3ZyDUlaGhFSEkLNbRImQTKlJYf1qR1YLBaBDEZx61xovVYCYTMMIAsT0jdrolY6jROG0uYlShaFhF2nd3Vwv32j3NudXW1P+7Zvefeu3c/r5kz597nuc+5z7O793z3eZ5zn6OIwMzMrFqFRlfAzMwWFwcOMzPLxIHDzMwyceAwM7NMHDjMzCyT8xpdgbytXr061q1b1+hqmJktKt/97nffjoiu6fJaPnCsW7eOgYGBRlfDzGxRkfT6THkeqjIzs0wcOMzMLBMHDjMzy8SBw8zMMnHgMDOzTBw4zMzqaGRsklffeJeRsclGV2XeWv5yXDOzZnHwyHH29A/SVigwVSyyt6+H7VvWNLpambnHYWZWByNjk+zpH2Riqsjo5PtMTBXZ3T+4KHseDhxmZnUwdGqctsLZp9y2QoGhU+MNqtH8OXCYmdVB98rlTBWLZ6VNFYt0r1zeoBrNnwOHmVkdrOpsZ29fDx1tBVa0n0dHW4G9fT2s6mxvdNUy8+S4mVmdbN+yhq2bVjN0apzulcsXZdAABw4zs7pa1dm+aANGiYeqzMwsEwcOMzPLxIHDzMwyceAwM7NMHDjMzCwTBw4zM8vEgcPMzDLJLXBIukjSS5JGJI1Kel7SxjTvmKQo246UldsqaVDSpKRXJF1ZTZ6ZmdVHnj2ONenx7wOeAq4BnizLPwzckG57ACR1AP3ACuBO4ALggKRls+Xl2AYzM6uQ5zfHX46IT5aeSLoRuKws/yjwbESMlqVdSxIQdkfEPkkXAvcC24CPzJL3Qo7tMDOzMrn1OCLidOmxpF7gfJJeRslO4D1JJyXtStPWp/vj6X4o3W+YI+8skm6VNCBpYHh4eGENMTOzs+Q+OS7pEuAgcAy4PU1+AvgscBNwGnhc0vrpiqf7yJIXEfsjojcieru6uhZQezMzq5TrIoeSLgVeBCaBqyPiTYCIeKDsNVcAdwEXkwxfAXSn+9I9FY+SDFXNlGdmZnWSW+CQtBY4RDJEdQ9wlaSrgO8BDwLPpe+/ExgHXgPeAU4Ct0kaBXaR9FQOAW2z5JmZWZ3kOVS1EegClgEPAV9Lt7fTtPuBh4HXgesj4kRETAA7gDHgEZJAsSMiPpgtL8c2mJlZhdx6HBFxiDPzEJU+PUu5w8DmrHlmZlYf/ua4mZll4sBhZmaZOHCYmVkmDhxmZpaJA4eZmWXiwGFmZpk4cJiZWSYOHGZmlokDh5mZZeLAYWZmmThwmJlZJg4cZmaWiQOHmZll4sBhZpYaGZvk1TfeZWRsstFVaWq53gHQzGyxOHjkOHv6B2krFJgqFtnb18P2LWvmLrgEucdhZkveyNgke/oHmZgqMjr5PhNTRXb3D7rnMQMHDjNb8oZOjdNWOPt02FYoMHRqvEE1am4OHGa25HWvXM5UsXhW2lSxSPfK5Q2qUXNz4DCzJW9VZzt7+3roaCuwov08OtoK7O3rYVVne6Or1pQ8OW5mBmzfsoatm1YzdGqc7pXLHTRmkVuPQ9JFkl6SNCJpVNLzkjbOlF5W7pikKNuOlOVtlTQoaVLSK5KuzKv+Zrb0rOps5+NrP+qgMYc8h6rWpMe/D3gKuAZ4cpb0coeBG9JtD4CkDqAfWAHcCVwAHJC0LMc2mJlZhTyHql6OiE+Wnki6EbhslvRyR4FnI2K0LO1akmCxOyL2SboQuBfYBryQTxPMzKxSbj2OiDhdeiypFzgfODxTekXxncB7kk5K2pWmrU/3x9P9ULrfUPnekm6VNCBpYHh4eOGNMTOz/y/3q6okXQIcBI4Bt8+VDjwBfBa4CTgNPC5pPedSuo/KjIjYHxG9EdHb1dVVg1aYmVlJrldVSboUeBGYBK6OiDdnSweIiAfKyl8B3AVcTDJ8BdCd7ktrAZTSzcysDnILHJLWAodIhqLuAa6SdBXwJ9OlR8TTkjYDDwLPpXXbCYwDrwHvACeB2ySNArtIeiuH8mqDmZmdK88ex0agNE70UFn6z86Q/jTwNrAMuB/4W8CfA78REScAJO0AvgQ8AnwP+OWI+CCvBpiZ2blyCxwRcYgz8xCVpk1Ph6w+PcsxDwObF1w5MzObNy85YmZmmThwmJlZJg4cZmaWiQOHmZll4sBhZmaZOHCYmVkmDhxmZpaJA4eZmWXiwGFmZpk4cJiZtaCRsUlefeNdRsYma35s33PczKzFHDxynD39g7QVCkwVi+zt62H7ljVzF6ySexxmZi1kZGySPf2DTEwVGZ18n4mpIrv7B2va83DgMDNrIUOnxmkrnH1qbysUGDo1XrP3cOAwM2sh3SuXM1UsnpU2VSzSvXJ5zd7DgcPMrIWs6mxnb18PHW0FVrSfR0dbgb19PazqbK/Ze3hy3MysxWzfsoatm1YzdGqc7pXLaxo0wIHDzKwlrepsr3nAKPFQlVmFPK9/N2sF7nGYlcn7+nezVpBbj0PSRZJekjQiaVTS85I2pnlbJQ1KmpT0iqQry8rNK89soepx/btZK8hzqGpNevz7gKeAa4AnJXUA/cAK4E7gAuCApGXzzcuxDbaE1OP6d7NWkOdQ1csR8cnSE0k3ApcB15Kc9HdHxD5JFwL3AtuAj8wz74Uc22FLRD2ufzdrBbn1OCLidOmxpF7gfOAwsD5NPp7uh9L9hgXknUXSrZIGJA0MDw8vpBm2hNTj+nezVpD75LikS4CDwDHgduCGypek+5iu+HzyImI/sB+gt7d3urJm08r7+nezVpBr4JB0KfAiMAlcHRFvSjqaZnen+9IlK0dJhqPmk2dWM3le/27WCnILHJLWAodIhqjuAa6SdBXwTeAkcJukUWAXSW/kENA2zzwzM6uTPK+q2gh0AcuAh4CvAV+LiAlgBzAGPEISDHZExAfzzcuxDWZmViG3HkdEHOLMPERl3mFgcy3zzMysPrzkiJmZZeLAYWZmmThwmJlZJg4cZmaWiQOHmZll4sBhZmaZOHCYmVkmDhxmZpaJA4eZmWVS1TfH0xVu/zWwjmQJEYCIiE/lVC8zM2tS1S458k3gkoo0L1duZrYEVTtUdT7wReBjJAsXdgE/nlelzMyseVUbOJ4ANgGdJD2N0mZmZktMtUNVv04SKD5TlhYZypuZWYuo9sR/GPcwzMyMKgNHRGzLuR5mZrZIVHs5roDPkdxEqSNNjoj4V3lVzMzMmlO1Q1VfAv4ZyXBV6a5+AThwmJktMdVeVXU98F/Tx/8SeAn4d7nUyMzMmlq1gWMl8G2S3sY7wAHgprwqZWZmzavawPF/SYa13iQZtvoPwIdnKyDpUUlvSQpJz6RpN6fPK7d1af6xivQjZcfbKmlQ0qSkVyRdmb25Zma2UNUGjnuAvyKZ05gA/hr4fBXlnq54/i3ghnS7CTgNvAUcL3vN4bLX7AGQ1AH0AyuAO4ELgAOSlmFmZnVV7eW4XwWQ9FHgJyJisooyd6Q9iTvK0o4CR9Nj/SLwIeDLETFVVvQo8GxEjJalXUsSLHZHxD5JFwL3AtuAF6ppg5mZ1UZVPQ5J6yT9d+Bt4BOSviXp/gW+968ARWB/RfpO4D1JJyXtStPWp/tSz2Qo3W+Yob63ShqQNDA8PLzAapqZWblqh6r+M9BNMjleJBlO+tx831TSRuBTwB9HxLGyrCeAz3JmGOtxSevPPcJZlwSfIyL2R0RvRPR2dXXNt5pmZjaNagPHTwOPlT3/K5JAMl+/QnLy/0/liRHxQEQcSIfGvk5y74+LSYe3yt5zTbo/ipmZ1VW1XwB8G7g8ffzjJL2NE7MVkHRdWZm1km4hmRx/HbgZ+CHwR2Wv3ww8CDyX1msnMA68RnIJ8EngNkmjwC7gGHCoyvqbmVmNZFlW/XMkvYT/Avx9zp2bqHQ38HD6uCc9xlbgF0ju5/FERBTLXv82SQ/j/rTc68D1EXEiIiaAHcAY8AhJENkRER9UWX8zM6uRaq+qekjScc4sq/6HEfG7c5TZNkt25WW6RMSbwKdnOd5hkrWyzMysgWYNHJJm+o++T9JTEeH7cZiZLTFznfhFcuXSCeDd3GtjZmZNb645jt8BfgSsJpmkvisiNpe2vCtnZmbNZ9bAERH/FLgQ+FVgLfDH6XpSP1ePypmZWfOZ86qqiPgb4Ack35k4TdL7WJFzvczMrEnNGjgk/bqk/w28CGwCbgc+FhG/X4/KmZlZ85lrcvzfk0yO/4Dkexbbge3JnWSJiPiH+VbPzMyaTTWX0wrYmG7lpl0nyswsDyNjkwydGqd75XJWdbY3ujpL2lyBY7oFBs3M6urgkePs6R+krVBgqlhkb18P27esmbug5WLWwBERr9erImZm0xkZm2RP/yATU0UmSFYp2t0/yNZNq93zaJBq16oyM2uIoVPjtBXOPlW1FQoMnRpvUI3MgcPMmlr3yuVMFYtnpU0Vi3SvXN6gGpkDh5k1tVWd7ezt66GjrcCK9vPoaCuwt6/Hw1QN5EUKzazpbd+yhq2bVvuqqibhwGFmi8KqznYHjCbhoSozM8vEgcPMzDJx4DAzs0wcOMzMLBMHDjMzyyS3wCHpUUlvSQpJz5SlH0vTStuRsrytkgYlTUp6RdKV1eSZmVn95N3jeHqG9MPADem2B0BSB9BPcpOoO4ELgAOSls2Wl2/1zcysUm7f44iIOyStA+6YJvso8GxEjJalXUsSEHZHxD5JFwL3AtuAj8yS90JebTAzs3M1ao5jJ/CepJOSdqVppSXcj6f7oXS/YY68c0i6VdKApIHh4eEaVtvMKo2MTfLqG+8yMjbZ6KpYnTTim+NPAN8HOoCHgcclvTjN65Tup7th1Gx5RMR+YD9Ab2+vbzhllhPfJ2NpqnvgiIgHSo8lXQHcBVxMMnwF0J3uS399R0mGqmbKM7MG8H0ylq7cAoek64DL06drJd0CfAd4EHgufe+dwDjwGvAOcBK4TdIosAs4BhwC2mbJM7MGKN0noxQ04Mx9Mhw4Wluecxx3kwxFAfSQDFF9BlgG3J/mvQ5cHxEnImIC2AGMAY+QBIodEfHBbHk51t/MZuH7ZCxdimjtKYDe3t4YGBhodDXMWtIfHDnObs9xtCRJ342I3unyvKy6mc2b75OxNDlwmNmC+D4ZS4/XqjIzs0wcOMzMLBMHDrMW5m91Wx48x2HWICNjk7lOKvtb3ZYXBw6zBsj7pO5vdVuePFRlVmflJ/XRyfeZmCqyu3+wpsNJpW91lyt9q9tsoRw4zOqsHid1f6vb8uTAYTXjidjq1OOkvqqznb19PXS0FVjRfh4dbQX29vV4mMpqwnMcVhOeiK1e6aReuVRHrU/q/la35cWBwxbME7HZ1euk7m91Wx4cOGzBvLz2/PikbouV5zhswTwRa7a0OHDYgnki1mxp8VCV1YQnYs2WDgcOqxmP2ZstDR6qMjOzTBw4zMwsk9wCh6RHJb0lKSQ9k6ZdJOklSSOSRiU9L2ljWZlj6etL25GyvK2SBiVNSnpF0pV51d3MzGaWd4/j6Yrna9L3vA94CrgGeLLiNYeBG9JtD4CkDqAfWAHcCVwAHJC0LLeam5nZtHKbHI+IOyStA+4oS345Ij5ZeiLpRuCyiqJHgWcjYrQs7VqSYLE7IvZJuhC4F9gGvJBD9a1J5X0PCzObW13nOCLidOmxpF7gfJIeRrmdwHuSTkralaatT/fH0/1Qut8w3ftIulXSgKSB4eHh2lTeGu7gkeNs/cKL/NKT32HrF17kD44cn7uQmdVcQybHJV0CHASOAbeXZT0BfBa4CTgNPC5p/TkHAKX7mO74EbE/Inojorerq6tm9c6DV5StTj3uYWFm1an79zgkXQq8CEwCV0fEm6W8iHig7HVXAHcBF5MMXwF0p/vSsqul9EXJK8pWz+thmTWP3AKHpOuAy9OnayXdAnyfZJL7fOAe4CpJV0XE05I2Aw8Cz6X12gmMA68B7wAngdskjQK7SHorh/Kqf968omw2Xg/LrHnkOVR1N/Bw+riHZBhqI9AFLAMeAr6WbgBvp+n3p+VeB66PiBMRMQHsAMaAR0iCyI6I+CDH+ufKt/bMxuthmTWPPK+q2jZD1u/M8Po3gU/PcrzDwOYFV6xJ+D/o7Lwelllz8DfHG6Se/0G30gT8qs52Pr72ow4aZg3kRQ4bqB7/QXsC3sxqzYGjwfJcUdYT8GaWBw9VtTBPwJtZHhw4Wpgn4M0sDw4cLcyXsJpZHjzH0eJ8CauZ1ZoDxxLgW7qaWS15qMrMzDJx4DAzs0wcOMzMLBMHDjMzy8SBw8zMMnHgMDOzTBw4zMwsEwcOMzPLxIHDzMwyceAwM7NMHDjMzCwTBw4zM8skt8Ah6VFJb0kKSc+UpW+VNChpUtIrkq5caJ6ZmdVP3j2Op8ufSOoA+oEVwJ3ABcABScvmm5dz/c3MrEJugSMi7gC+WJF8LclJf19E7AN+G1gPbFtAnpmZ1VG95zjWp/vj6X4o3W9YQN45JN0qaUDSwPDw8IIrbWZmZzR6clzpPmqYR0Tsj4jeiOjt6upaYBXNzKxcve8AeDTdd6f7NWXpH5lnnpmZ1VFugUPSdcDl6dO1km4BvgOcBG6TNArsAo4Bh4C2eeaZmVkd5TlUdTfwcPq4B3gC+ClgBzAGPEISDHZExAcRMTGfvBzrb2Zm08itxxER22bJ3jxDmcPzyTMzs/pp9OS4mZktMg4cZmaWiQPHDEbGJnn1jXcZGZtsdFXMzJpKvS/HXRQOHjnOnv5B2goFpopF9vb1sH3LmrkLmpktAe5xVBgZm2RP/yATU0VGJ99nYqrI7v5B9zzMzFIOHBWGTo3TVjj7x9JWKDB0arxBNTIzay4OHBW6Vy5nqlg8K22qWKR75fIG1cjMrLk4cFRY1dnO3r4eOtoKrGg/j462Anv7eljV2d7oqpmZNQVPjk9j+5Y1bN20mqFT43SvXO6gYWZWxoFjBqs62x0wzMym4aEqMzPLxIHDzMwyceAwM7NMHDjMzCwTBw4zM8tEEdPetrtlSBoGXm90PeawGni70ZWokVZpS6u0A9yWZrQY2vETEdE1XUbLB47FQNJARPQ2uh610CptaZV2gNvSjBZ7OzxUZWZmmThwmJlZJg4czWF/oytQQ63SllZpB7gtzWhRt8NzHGZmlol7HGZmlokDh5mZZeLAUWOSLpL0kqQRSaOSnpe0Mc3bKmlQ0qSkVyRdWVbuUUlvSQpJz1Qcc8Zyi6Udsx1vsbWlLL9D0vfT/McWa1skfVTSVyS9K2lM0uFF2o7PSzqWljsq6fa82zHftsz1eWjEZz4LB47aW0Pyc70PeAq4BnhSUgfQD6wA7gQuAA5IWlZW9unKg1VZLg81bcdMx8ut9lW89wLaUvJvgO5cajyzPNryZeBG4LeBzwP/J5ean63Wn5OLgC8CReAuoA14VNLaPBuRmk9bZvw8NPAzX72I8FbDDfhQxfMR4CRwPRDA3Wn6/enzT5W9dl2a9kxZ2pzlFkk7pj3eYvydpOk9wDhwd5r/2GJsC7AhTfsq8CFg2SJtxyVp2rfTxwPABNDVjG2Z7fPQqM98ls09jhqLiNOlx5J6gfOBw8D6NPl4uh9K9xvmOOR8yy1Irdsxy/FyV+u2SCqQ/Hf4JeB/1LSyc8jh7+vSdP93gB8BP5L0hdrUdmY5/H19H/g1YCvwF8AVwK0RMVzDas/03pnbMsfnoSGf+SwcOHIi6RLgIHAMmG6sVek+6/XQ8y03L7VuRxXHy00N2/JPSP7r/QrJkAPAj0madl2fPNSwLaXbXH4Y+EfAnwC7JV1Tg2rOqVbtSH/2twNHgJ8HXgUek1S3ocT5tKXKz0NdP/PVcODIgaRLgW8B7wNXR8SbwNE0u/SHXDrhHGV28y23YDVux0zHq4sat2Ut0EVycvpqmvZLwEM1q/AsatyWY+n+2xHxDeD30ue5X7hQ43b8bPrab0TEQeAbJHMEf7emlZ7BfNoyy+ehYZ/5qjV6rKzVNpKTykmSP4ZfAz6Xbh3AWyS//NtIuqFHSceUgeuAPST/VbwK3AJcNFe5RdSOaY+3SH8nlwK/mG73pfnPAT+1CNsiYDA95i8D/y099uWLrB29adpfALuA/5U+/3gz/k5m+zzM9TNohq3hFWi1DdiW/sGetaV5PwO8BpwG/gzoLSt3aJpyN89VbrG0Y7bjLba2zHDsek2O5/H3dRnwpySTyX8J/ONF2o67SE6wE8APgH/erL+TuT4Ps/0MmmHzkiNmZpaJ5zjMzCwTBw4zM8vEgcPMzDJx4DAzs0wcOMzMLBMHDrMakdQm6c8lfVC2CuqmdIXTNyR9uNF1NKsFBw6zGomIKeBfkHyufitN/o8kiwfeFRE/WsjxJZ23oAqa1YgDh1kNRcSLwNeBT0jaB/wD4HlgSNKfpve7+EtJN0CyxpKkP0vTxyR9W9Jlad7N6X0nvi7pe5xZDsSsofwFQLMak/S3SZa+WEHyzd+fAf6IZImJr5Csq3Q1yTIZbwC/CpwAPgbsBr4TEX9P0s0k92r4a5J7f/wwIr5Zz7aYTcddX7Mai4gTkn4T+LfA48BqkmWzzwceLHvp1SQ3Jfo5ksX4Squgbq445Jcj4tFcK22WgQOHWT5+WLYvBYSvAL9b9ppjwB3ATwOPAX9Iche+FRXHOpFbLc3mwXMcZvl7GXiHpGfxk8DlJCuiruFMUOkEPkH9b0VrlpkDh1nOIuId4DMk9/J+GPgN4G9IehyPktxF8OeBC4H/2ZBKmmXgyXEzM8vEPQ4zM8vEgcPMzDJx4DAzs0wcOMzMLBMHDjMzy8SBw8zMMnHgMDOzTP4fydkfPphZb7cAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h4 id="Olhando-a-m&#233;dia-anual-do-tamanho-da-descri&#231;&#227;o-de-campe&#245;es,-na-m&#233;dia-parece-haver-uma-tend&#234;ncia-de-aumento-da-descri&#231;&#227;o-das-habilidades.">Olhando a m&#233;dia anual do tamanho da descri&#231;&#227;o de campe&#245;es, na m&#233;dia parece haver uma tend&#234;ncia de aumento da descri&#231;&#227;o das habilidades.<a class="anchor-link" href="#Olhando-a-m&#233;dia-anual-do-tamanho-da-descri&#231;&#227;o-de-campe&#245;es,-na-m&#233;dia-parece-haver-uma-tend&#234;ncia-de-aumento-da-descri&#231;&#227;o-das-habilidades.">&#182;</a></h4>
</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>5) Por fim, irei extrair os dados para uso futuro num arquivo json para reutilizar futuramente com o objetivo de melhorar os gráficos. Como o objetivo principal era extrair os dados utilizando BeautifulSoup, considero concluído.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs jp-mod-noInput ">

</div>
</body>







</html>
