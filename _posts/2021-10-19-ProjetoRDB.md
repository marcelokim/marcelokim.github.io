---
title: "Projeto PLACEHOLDER: Modelagem do postgreSQL"
date: 2021-10-19
tags: jupyter-notebook projeto-tokenizer django postgresql
---

Objetivo: Melhoria da funcionalidade do webapp e criação de uma base de dados útil (espanhol ao invés de inglês)

<!--more-->

<html>
<head><meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Projeto, modelagem da rdb</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>




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

.cm-s-mdn-like.CodeMirror { background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFcAAAAyCAYAAAAp8UeFAAAHvklEQVR42s2b63bcNgyEQZCSHCdt2vd/0tWF7I+Q6XgMXiTtuvU5Pl57ZQKkKHzEAOtF5KeIJBGJ8uvL599FRFREZhFx8DeXv8trn68RuGaC8TRfo3SNp9dlDDHedyLyTUTeRWStXKPZrjtpZxaRw5hPqozRs1N8/enzIiQRWcCgy4MUA0f+XWliDhyL8Lfyvx7ei/Ae3iQFHyw7U/59pQVIMEEPEz0G7XiwdRjzSfC3UTtz9vchIntxvry5iMgfIhJoEflOz2CQr3F5h/HfeFe+GTdLaKcu9L8LTeQb/R/7GgbsfKedyNdoHsN31uRPWrfZ5wsj/NzzRQHuToIdU3ahwnsKPxXCjJITuOsi7XLc7SG/v5GdALs7wf8JjTFiB5+QvTEfRyGOfX3Lrx8wxyQi3sNq46O7QahQiCsRFgqddjBouVEHOKDgXAQHD9gJCr5sMKkEdjwsarG/ww3BMHBU7OBjXnzdyY7SfCxf5/z6ATccrwlKuwC/jhznnPF4CgVzhhVf4xp2EixcBActO75iZ8/fM9zAs2OMzKdslgXWJ9XG8PQoOAMA5fGcsvORgv0doBXyHrCwfLJAOwo71QLNkb8n2Pl6EWiR7OCibtkPaz4Kc/0NNAze2gju3zOwekALDaCFPI5vjPFmgGY5AZqyGEvH1x7QfIb8YtxMnA/b+QQ0aQDAwc6JMFg8CbQZ4qoYEEHbRwNojuK3EHwd7VALSgq+MNDKzfT58T8qdpADrgW0GmgcAS1lhzztJmkAzcPNOQbsWEALBDSlMKUG0Eq4CLAQWvEVQ9WU57gZJwZtgPO3r9oBTQ9WO8TjqXINx8R0EYpiZEUWOF3FxkbJkgU9B2f41YBrIj5ZfsQa0M5kTgiAAqM3ShXLgu8XMqcrQBvJ0CL5pnTsfMB13oB8athpAq2XOQmcGmoACCLydx7nToa23ATaSIY2ichfOdPTGxlasXMLaL0MLZAOwAKIM+y8CmicobGdCcbbK9DzN+yYGVoNNI5iUKTMyYOjPse4A8SM1MmcXgU0toOq1yO/v8FOxlASyc7TgeYaAMBJHcY1CcCwGI/TK4AmDbDyKYBBtFUkRwto8gygiQEaByFgJ00BH2M8JWwQS1nafDXQCidWyOI8AcjDCSjCLk8ngObuAm3JAHAdubAmOaK06V8MNEsKPJOhobSprwQa6gD7DclRQdqcwL4zxqgBrQcabUiBLclRDKAlWp+etPkBaNMA0AKlrHwTdEByZAA4GM+SNluSY6wAzcMNewxmgig5Ks0nkrSpBvSaQHMdKTBAnLojOdYyGpQ254602ZILPdTD1hdlggdIm74jbTp8vDwF5ZYUeLWGJpWsh6XNyXgcYwVoJQTEhhTYkxzZjiU5npU2TaB979TQehlaAVq4kaGpiPwwwLkYUuBbQwocyQTv1tA0+1UFWoJF3iv1oq+qoSk8EQdJmwHkziIF7oOZk14EGitibAdjLYYK78H5vZOhtWpoI0ATGHs0Q8OMb4Ey+2bU2UYztCtA0wFAs7TplGLRVQCcqaFdGSPCeTI1QNIC52iWNzof6Uib7xjEp07mNNoUYmVosVItHrHzRlLgBn9LFyRHaQCtVUMbtTNhoXWiTOO9k/V8BdAc1Oq0ArSQs6/5SU0hckNy9NnXqQY0PGYo5dWJ7nINaN6o958FWin27aBaWRka1r5myvLOAm0j30eBJqCxHLReVclxhxOEN2JfDWjxBtAC7MIH1fVaGdoOp4qJYDgKtKPSFNID2gSnGldrCqkFZ+5UeQXQBIRrSwocbdZYQT/2LwRahBPBXoHrB8nxaGROST62DKUbQOMMzZIC9abkuELfQzQALWTnDNAm8KHWFOJgJ5+SHIvTPcmx1xQyZRhNL5Qci689aXMEaN/uNIWkEwDAvFpOZmgsBaaGnbs1NPa1Jm32gBZAIh1pCtG7TSH4aE0y1uVY4uqoFPisGlpP2rSA5qTecWn5agK6BzSpgAyD+wFaqhnYoSZ1Vwr8CmlTQbrcO3ZaX0NAEyMbYaAlyquFoLKK3SPby9CeVUPThrSJmkCAE0CrKUQadi4DrdSlWhmah0YL9z9vClH59YGbHx1J8VZTyAjQepJjmXwAKTDQI3omc3p1U4gDUf6RfcdYfrUp5ClAi2J3Ba6UOXGo+K+bQrjjssitG2SJzshaLwMtXgRagUNpYYoVkMSBLM+9GGiJZMvduG6DRZ4qc04DMPtQQxOjEtACmhO7K1AbNbQDEggZyJwscFpAGwENhoBeUwh3bWolhe8BTYVKxQEWrSUn/uhcM5KhvUu/+eQu0Lzhi+VrK0PrZZNDQKs9cpYUuFYgMVpD4/NxenJTiMCNqdUEUf1qZWjppLT5qSkkUZbCwkbZMSuVnu80hfSkzRbQeqCZSAh6huR4VtoM2gHAlLf72smuWgE+VV7XpE25Ab2WFDgyhnSuKbs4GuGzCjR+tIoUuMFg3kgcWKLTwRqanJQ2W00hAsenfaApRC42hbCvK1SlE0HtE9BGgneJO+ELamitD1YjjOYnNYVcraGhtKkW0EqVVeDx733I2NH581k1NNxNLG0i0IJ8/NjVaOZ0tYZ2Vtr0Xv7tPV3hkWp9EFkgS/J0vosngTaSoaG06WHi+xObQkaAdlbanP8B2+2l0f90LmUAAAAASUVORK5CYII=); }

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
<p>Atualmente o web app roda localmente utilizando web server provido pelo Django + PostgreSQL. Realizando algumas melhorias, conseguimos melhorar o projeto incrementalmente da primeira versão:</p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p><img src="data:image/png;base64,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" alt="transliterator%202nd%20stepsv2.png"></p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Para uma segunda versão (utilizando JavaScript, CSS e HTML para melhorar presentabilidade e usabilidade):</p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p><img src="data:image/png;base64,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nHrqqUccccQZZ5xBUnzZsmWkpeXudJBi37Rp0+DBg7/97W9TK0h+f+ELX+jZs2efPn3u5cydO1cWBQAAAECTAQUOAAAAJEDy9Z133rnzzjuPOuoo8Qj6gQMH5L4mZvfu3Y888sjZZ59N8rtVq1af+MQnTj/99Guuueauu+4aOXLk+vXr9+zZI4tGQ/5TybvvvpvskPy+8MIL27dvP2XKlH379lFDDnI++ugjWRoAAAAATQYUOAAAAJAAqdONGzdeccUVRx555MCBA/fv31/AQ+CF8cILL3z3u9/95Cc/SfJbQCKcIE9IS19++eWVlZWyaATk6ocffviHP/zhmGOOIRn/la985Yknnqivr4fkBgAAAIoPFDgAAACQAInVxYsXn3XWWWecccasWbPozyIo8Hfeeeehhx668MILjz/+eFLOv/jFL9atW7dhw4YRI0a0adPmy1/+8plnnkmimv793Oc+R3unT5/+5ptvhh+Pf/fdd2fOnHnOOeeccsopt956K5V57733Dh48KHeHoKYdOHBgzZo1Dz/88Le+9a2LI7jkkkt++tOfjhs3bvbs2UuWLNmxY4c8HgAAAADRQIEDAAAACZBeHTZs2Omnn/6Vr3yF1KbMbTLEXes5c+ZQjUceeeQnP/lJUrwvv/yy3vvRRx+tWrWqR48eX//610877TSS1kcdddSnPvWpdu3a/f3vf6djxQcEVGz79u2PPfbY1VdffdJJJ337299+9dVXY259i3p37949b96873//+3QIKXxx+/0Tn/gEbZ966qlUneDEE0+kSsm9Y4899rLLLhsyZMhbb71FxxbzG/IAAABAiwMKHAAAAEiAFPhvfvMbkp0/+9nPXnnlFZnbZBw4cOCll176r//6L9K3JH0/+9nPTpgwwX77upDK77333urVq5955plhw4ZRGSp83HHH/fKXv3zxxRfF19RJDA8dOvSCCy4Q+nzAgAHxXxqnZq5cufJPf/oTKWrS2wRJ95KSElLgZPyrX/3q5MmTqbopnPvvv//SSy89+uijjzjiCFLp55577vXXX3/HHXcsWrRImgMAAABACChwAAAAIAGSpl/60pdIgXfu3Lmurk7mNhk7d+4sLS0955xzjj/++F/96lfLly8nsS1uawcQ98NJVy9dupS0N0nls846i7QxaW/KJ1d//vOfk5GLL7545MiRb775ZswL5D744AOq6IYbbiALpLdJXT/44INPP/20EPAkxUla0+FkliolyMkVK1YsWLBgxowZ3/3ud0866SQ66uSTT77lllvI25iKAAAAgMMZKHAAAAAgAdKT5513HinwP//5z2nePd5A1q5dS9WRcib9vHXrVpmbxKuvvkoK/IgjjujYsSNp4HffffeZZ5753Oc+R24PGDDgn//8pywXwcaNG0nDn3jiiVQvHfXoo4+SgG/fvv2pp5564YUX1tTURD2+vn///ldeeeWnP/3p6aef/olPfOLyyy+fPn363r175W4AAAAAWECBAwAAAAkUWYG//PLLZ5555jnnnLN+/fr0v/u9adMmrcB3797dt2/fT33qU8ccc8wXvvAFEuekk2W5EP/HX71WVVVFYvvcc8/t0qXL5s2bt2/f/sgjj7Ru3Zo8+Z//+R/KoWLyABdS5mT8nXfeeeKJJ0jAU5R69epF+l/uBgAAAIAFFDgAAACQwCFR4BdccMGuXbui7jyH0Qr87rvvJgH8xS9+8cgjj7z66qsfe+wxWSICquLDDz+8+eabjz766J///Ofr1q0jsb1y5co2bdocf/zx3/72t1944YU0HwTs2LHj9NNPJxHeqVMn8lzmAgAAAMACChwAAABIoEUocDrKVuCXXnrpcccdN2zYsJi73wLS21SmY8eOVOO0adPED5WNHDnyjDPOOOGEE8aMGUM5UTfAbd555x0ocAAAACAeKHAAAAAgDtKf//znP88991ySl0OGDHnvvffkjiZDfA+cqhs/fnx9fX2i+hUSeuDAgaTAL7roooceemj69Omf/vSnSUI//vjjshAv5oVEPrVxx44dGzdupNbR9gcffNCjR49jjjnm7LPPpkx5fBJQ4AAAAEAiUOAAAABAHCRHZ82addZZZ11wwQUTJ05M/8Xsgtm6desPf/hDkrKf//znKysrN2/efODAAZLKcrcL6ee9e/f+/e9/v+666z7xiU/ceOONCxcuvOWWW0499dQrrrjib3/7myi2e/du2n722WfFb4nF8PTTTz/66KNf/epXjz766JKSkjfffFNYSAQKHAAAAEgEChwAAACIg4TlXXfddfLJJ3/lK19ZvXo1iWG5o8kgkT9ixIh//dd/Peqoo0j5//a3v3355ZejHiZ/7733SDZff/31JLk/+clPjho1avz48Z/61Kfoz9tuu+3tt98WxWpqar72ta+deeaZp6WAjiX5TbV/6Utfwj1wAAAAoBGBAgcAAADiIBEr3kl2zTXX7N69O/0XswuGRP5bb71FQvp73/veSSedRJL4G9/4xtixY73fx966deu//du/HXfccVTyhhtuoAMHDx58wgknXHjhhatWrdK/CrZkyRJqBan6i11I4dOxRxxxRKtWrT7xiU+Q6j755JM//elPkwVq8i233LJjxw5hIR7y7fXXXydX6fA//vGPiT9+BgAAAByeQIEDAAAAcZCmvfbaa0mO/sd//Me+fftkbtNDYpuqu+mmm0488UTSxp///Oe3b9/+4Ycfyt2KlStXCvFMupf+/OijjwYNGkTeXnnllaJADFTF7NmzSeeffvrpJMKJU045hXJeeeUV8TXyTZs2RT39HoCk/l/+8peTTjrpvPPOGzZs2O7du+UOAAAAAFhAgQMAAABxvPDCC5dffjlp1I4dO4YFcJNC6nfr1q1du3Y95phjTj755G9961tz5szRkpjE9vvvv3/HHXcceeSRJJinT58uMtMrcGLPnj1vv/32jBkzfvKTn5ACP+GEE2pqatatW3f++eeTnJ40adKOHTvSiHCy0759ezr8O9/5zsaNGxNfwA4AAAAcnkCBAwAAAJGQ+Bw1atQZZ5xBEnfKlClF+BJ4GFLdX/ziF0ncHnvssT179nznnXdIZu/bt482Jk+eTFKZdpEOf/XVV6mwVuCXXHLJrl270ijhgwcPkn4ePHgwKfBTTz113rx5mzdv/va3v33iiSf+27/925/+9KdVq1Yl2tm6deuNN9543HHH3XDDDTILAAAAACGgwAEAAAA/JL/37t3bu3fvT37yk5/97GffeustEqtyXxEhH15//XUS4aSQzznnnO7du1PO+vXrO3fufMEFFxx11FEktl944QXx6QAp8CFDhpAmJ/18yy23kHhOvIP93nvvPfLIIxdddBE18xvf+AYd8uGHH44aNeriiy8+5phjxM1/EvMxdmjXtGnTyENS4L/73e9kLgAAAABCQIEDAAAAfvbv3//SSy9dc801n/jEJ77yla8sX778n//8J6lT0rqF4X2VWkpIV//rv/4rSdxTTjmFJPf5559/xhlnkMymzP/93/99//33RTGyP3/+/CuvvJJ2kQ7/wQ9+QE0gWR6ul3Iof/v27ZWVlSS/SWnTUVOmTHn33Xdp1zvvvDN79uwrrrjipJNO+sxnPlNWVrZo0SIytW3btkAE9u3b98Ybb/z85z8Xr3Cjo2QFAAAAAAgBBQ4AAAD42bt377Rp08477zzxkvAvf/nLQ4cOJY06vSBmzJjx3HPPbdy4kcyS9JV1pIY09qRJkz7/+c+Trj6e07p16x//+MdkVpZQ7NmzZ+zYsTfccANJdHL7rrvuevXVV0k2Cx0uhDfJ5vfee2/NmjW5XO7SSy899thjv/SlL40bN46OlVZ4jSTOae8xxxzzyU9+8uijj7744os7d+781FNPySZxnnnmmcGDB5P2Js3fp08fku7yeAAAAACEgAIHAAAA/Ozfv/9vf/vbt771LfHj2Mcdd9ypp55KsvbMQiExf/311z/44IPbtm3LV4QfPHjwn//8Z01NDalrASnh119//YMPPpAlFFSS1PXmzZs7dux48sknk8/XXXcdSeV3332XhDdBtT/00EO33377N7/5Tdp70kknXXXVVZMnTyb5bT9mT9u7d+9++umnScNffvnlpPzFC+EoAnYQTj/99FNOOYX2kobfsmUL3sEGAAAAxAAFDgAAAPghkUyid/ny5VOmTJk0adJ//ud/XnjhhRcUyrnnnkty98QTT7zkkkvmzJlja92m4MMPP1y6dGlJSQmp5aOOOuqKK65o06bNj370ox/+8IckyD/96U+LjxVo49Zbb/3rX/9aX18vj3Qhxf7WW28tWrTo2Wef7datG8ls2R6Xq6++esKECXvVz48DAAAAwAsUOAAAABCHfnK7gezYsePee++9+OKLv/vd765cubKpFThBbpMkLi8vP/nkk0lsf8LluOOOO//880eNGrV//34qKY+JgMcgIQiJRgAAAAAABQ4AAAAUgw8//LC+vn7r1q1vv/02bRdHr5Iw3r1796xZs/70pz+1dxk2bNjmzZv37NkD5QwAAAAUDShwAAAAAAAAAACgGECBAwAAAAAAAAAAxQAKHAAAAAAF8n//938HDx7cu3fvm2+++Y9//OOVV17ZsWMHvhMOAAAARAEFDgAAAIC8IY1NSvuDDz5Yt27dtGnT2rZte9JJJ11wwQXl5eVChMtyAAAAALCAAgcAAABA3uzfv//111/v37//9773vfPOO+/4448/8sgjjzrqqIsuuugvf/nLnj17ZDkAAAAAWECBAwAAAC2eg5ziPP5Ntezbt+/VV1+96667zj33XNLeZ555Jm1885vfPO20004++eTbbrtt69atsjQAAAAALKDAAQAAgJYNSeLdu3f/85//3Lt3b1M//k0K//3331+3bt0vf/nLo4466rjjjvv3f//3GTNm7NmzZ9euXf/zP/9z6qmnXnrppcuWLZMHAAAAAMACChwAAADIGxK6Bw8ePHDgQMGKl4599913lyxZsnz58v379+d775pqJ9G7evXqp59+etiwYT/60Y+uuuqqrl27vvPOO7JEYyNqnDdvXqdOnT73uc+dfvrpZ5xxxm9+85uNGzd+8MEHtJf+Xbx4sbgrPmfOHHkYAAAAACygwAEAAID8ILW5bdu2mTNnzp49e9++fTI3HSS89+7dS9p7xYoV999//3e+850f/OAHO3fuTFTydCBJXHGvmyDtPXLkyJ/+9Kef+tSnjjjiiE9wSPq+8cYb8oBGhdwj+f34449/7WtfO/bYY6miSy+9tEuXLhs2bNCfHezfv3/79u3/8i//cswxx9TU1BTheXgAAACgxQEFDgAAAOQBaVHSz/fee+8ll1xCKpSkuNyRAhKldXV1f/7zn0tKSi677LLTTjuNxCpJ1rfeeosEtizkgyrdsWPHwIED/+M//oM0MPGFL3zhnHPOISV8AufII48kBX700Udv2rRJHtN4iCfPx4wZc+GFF1KN559//j333LNs2TLS27bbtgKfOXPmwYMH5Q4AAAAAKKDAAQAAgFSQECUlTCLzwQcfbN269Sc5mzdvlrtjoQNJxJJc79Sp09lnn33ccccdddRRQjaToA0rcKqLFOyHH35Iap9E+5IlS37wgx+ceeaZJLZJ3xKnnHLKueee+9WvfvWhhx5atWrVf//3f6dR4Nrs3r1733nnnVc5VDuJZ1nChdymkiT+H3nkkYsuuojsX3nllc8888yuXbvIiCykoCbU19dfeuml1LTS0lKyT9XJfQAAAADgQIEDAAAAqSDtSlq0R48exx577BFHHNGqVSuS0IkKXIhekqNz58697bbbTjrppOOPP/6qq676xje+cdppp5Gdz33uc6SxtQIXOv+DDz4gLU3Ce/To0bfeeiuJbVL7J5544pe//OUSzu9///snn3xy9+7ddAhp+/bt2ycqcDJLsnnDhg3PP//8nDlz+vTpc/bZZ5OS//73v79lyxZZSCHcJv2/dOnSLl26nHPOOWScXH3iiSfIjizkItymwhQWKv/KK6+QBbJDyBIAAADAYQ8UOAAAAJCM+Pnrbt26nXfeecccc4yQxPEKnBQpHbVt2zZSrb/97W8vu+yyk08+mUTvL37xi2XLlq1YsYLULynw0tJSEq5CptIh9fX1JK1Jx15//fWXXHLJmWeeeeqpp55wwglXXnnl/fff/9JLL5FBYteuXSS8hRjWCpwci/oe+L59+1atWnXvvfeSer/wwgtJIVPt5P9RRx31r//6r6+++qosp7Q36efhw4f/5je/+epXv3oGh4T6s88+G/ND3+LAZ555htw46aSTxo0bRwKeypN7BxrwyjoAAAAgS0CBAwAAAH6EpBQvTvv73/9+6623kn4mPfzNb36zc+fOxx57rFeBi6N2795NYpi09K9//evLL7+ctDdBirpPnz6kosnm+PHjycJxxx1XUVFB5T/88EMSq6SE//jHP37hC18geUyq+/TTT7/44ot//OMf9+rVa8GCBWTTq2N37tx50003HX300aSl33rrLZnLPSHpS/Ke5Pr06dPJDhkUZs866yyqQtzG/+lPf/r222+LQ8gTcqO2tva//uu/LrjgAipMbpMP5NWKFSvIoCgWw5IlS77yla+ceOKJn//853/+85//4he/aN++/Zw5c8gNWQIAAAA4jIECBwAAAPyQ3H3vvff+8Y9/lJWVnXvuuSSYie9///uvvfbayJEjTzrpJK8CJxFLarN///7/8i//cvzxxx9zzDEksz/96U936dJl+/btpL337du3bdu2q6++mjTzVVddRdr4/fff37Jly+jRo7/4xS9SYTrkU5/61M033zxr1izxK98EaekoAbx+/fqvfe1rpKhJqNfX18tc7gmJ9sWLF//+978nyU3OkzC+5pprZs+e/e67727YsEE8uH7fffdRM6m8aO+IESNOPfVU8oHk9+c+97l77rln9erV4j62MBsPOXz//feTyKfgkBGCNPwXvvAFarIsAQAAABzGQIEDAAAAHkiL/v3vf//tb3/72c9+luTraaeddtlll3Xv3p2EK6ncqqoqEpa2Aif5un//ftKfdBSJ7TPPPJMKXHTRRd/5znf+8Ic//PWvf33nnXeoDKlosvzQQw+dd955JIlJZg8cOPDWW2+9/PLLzznnHFLIpNt/9atfPffccyTXScmTihb2oyBrkydPJg9bt25NVZO8pyrI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" alt="transliterator%204th%20steps.png"></p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Além disso, troquei o tokenizer como havia comentado anteriormente para um mais preciso.</p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>A estrutura básica de funcionalidade está pronta e o básico já foi feito, tendo algumas pendências:</p>

<pre><code>1) Criação do PostgreSQL com dados significados em espanhol (pois não encontrei nenhum dicionário português).
2) Colocar online.</code></pre>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Para criar o postgreSQL, preciso compreender melhor a estrutura do JMDict (dicionário), que é estruturada da seguinte forma:</p>
<p>&lt;!ELEMENT entry (ent_seq, k_ele*, r_ele+, sense+)&gt;</p>

<pre><code>&lt;!ELEMENT ent_seq (#PCDATA)&gt;

&lt;!ELEMENT k_ele (keb, ke_inf*, ke_pri*)&gt;
    &lt;!ELEMENT keb (#PCDATA)&gt;
        O mesmo k_ele pode possuir múltiplos keb (por exemplo, 曲げ物, 曲物, 綰物 / circular box).
    &lt;!ELEMENT ke_inf (#PCDATA)&gt; DESNECESSÁRIO   
    &lt;!ELEMENT ke_pri (#PCDATA)&gt; DESNECESSÁRIO

&lt;!ELEMENT r_ele (reb, re_nokanji?, re_restr*, re_inf*, re_pri*)&gt;
    Caso não haja k_ele, o r_ele será a própria palavra.

    &lt;!ELEMENT reb (#PCDATA)&gt;
        Leitura do elemento.
    &lt;!ELEMENT re_nokanji (#PCDATA)&gt;
        O elemento não é considerado uma leitura válida, porém japoneses podem usar este termo. É como se fosse um re_restr, porém para todas os kanjis. (por exemplo, ソラマメ).
    &lt;!ELEMENT re_restr (#PCDATA)&gt;
        Se este elemento existir, a leitura reb irá referenciar apenas os re_restr indicados.
    &lt;!ELEMENT re_inf (#PCDATA)&gt; DESNECESSÁRIO
    &lt;!ELEMENT re_pri (#PCDATA)&gt; DESNECESSÁRIO

&lt;!ELEMENT sense (stagk*, stagr*, pos*, xref*, ant*, field*, misc*, s_inf*, lsource*, dial*, gloss*)&gt;
     A mesma ENTRY pode ter múltiplos senses (significados).
     Observação: a maior parte dos elementos do sense pode ser ignorada, pois este é um dicionário focado para a tradução da língua japonesa-inglesa. Por esta razão, muitas informações são exclusivamente para o inglês. Por exemplo, 'pos': algumas palavras tem mais de um sense com diversas definições em inglês e algumas em outras línguas, porém o 'part-of-speech' é exclusivo para a tradução em inglês.
    &lt;!ELEMENT stagk (#PCDATA)&gt; NÃO POSSUI
    &lt;!ELEMENT stagr (#PCDATA)&gt; NÃO POSSUI
        DESNECESSÁRIO, pois os elementos 'gloss' não possuem stagk e star: assim como mencionado acima sobre 'pos', possui o mesmo problema: são elementos que, neste dicionário, apenas palavras em inglês possuem.
    &lt;!ELEMENT xref (#PCDATA)*&gt; DESNECESSÁRIO
    &lt;!ELEMENT ant (#PCDATA)*&gt; DESNECESSÁRIO
    &lt;!ELEMENT pos (#PCDATA)&gt; NÃO POSSUI
    &lt;!ELEMENT field (#PCDATA)&gt; DESNECESSÁRIO
    &lt;!ELEMENT misc (#PCDATA)&gt; DESNECESSÁRIO
    &lt;!ELEMENT lsource (#PCDATA)&gt; DESNECESSÁRIO
    &lt;!ATTLIST lsource xml:lang CDATA "eng"&gt; DESNECESSÁRIO
    &lt;!ATTLIST lsource ls_type CDATA #IMPLIED&gt; DESNECESSÁRIO
    &lt;!ATTLIST lsource ls_wasei CDATA #IMPLIED&gt; DESNECESSÁRIO
    &lt;!ELEMENT dial (#PCDATA)&gt; DESNECESSÁRIO
    &lt;!ELEMENT gloss (#PCDATA | pri)*&gt;
        Pode ter múltiplas 'gloss'.
    &lt;!ATTLIST gloss xml:lang CDATA "eng"&gt;
        Informação desejada: &lt;gloss xml:lang="spa"&gt;
    &lt;!ATTLIST gloss g_gend CDATA #IMPLIED&gt; DESNECESSÁRIO
    &lt;!ELEMENT pri (#PCDATA)&gt; DESNECESSÁRIO
    &lt;!ELEMENT s_inf (#PCDATA)&gt; DESNECESSÁRIO</code></pre>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Como podemos ver acima, muita informação foi considerada "desnecessária": não por não ser útil, porém para reduzir o tamanho da minha db e simplificar o projeto, estas informações foram escolhidas para serem removidas. Assim, podemos simplificar as informações desejadas para a seguinte estrutura:</p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>&lt;!ELEMENT entry (ent_seq, k_ele*, r_ele+, sense+)&gt;</p>

<pre><code>&lt;!ELEMENT ent_seq (#PCDATA)&gt;

&lt;!ELEMENT k_ele (keb, ke_inf*, ke_pri*)&gt;
    &lt;!ELEMENT keb (#PCDATA)&gt;
        O mesmo k_ele pode possuir múltiplos keb (por exemplo, 曲げ物, 曲物, 綰物 / circular box).

&lt;!ELEMENT r_ele (reb, re_nokanji?, re_restr*, re_inf*, re_pri*)&gt;
    Caso não haja k_ele, o r_ele será a própria palavra.
    &lt;!ELEMENT reb (#PCDATA)&gt;
        Leitura do elemento. O mesmo elemento pode possuir múltiplas 'reb'. (Por exemplo, 痔 / &lt;gloss&gt;piles&lt;/gloss&gt;, com leitura じ e ぢ; nesse caso, deve possuir uma leitura primária. Porém, como estou removendo algumas informações como re_inf e re_pri, que indicam prioridade da palavra, não será possível diferencial qual a leitura "correta" (mais usada)).
    &lt;!ELEMENT re_nokanji (#PCDATA)&gt;
        O elemento não é considerado uma leitura válida, porém japoneses podem usar este termo. É como se fosse um re_restr, porém para todas os kanjis. (por exemplo, ソラマメ).
    &lt;!ELEMENT re_restr (#PCDATA)&gt;
        Se este elemento existir, a leitura reb irá referenciar apenas os re_restr indicados.

&lt;!ELEMENT sense (stagk*, stagr*, pos*, xref*, ant*, field*, misc*, s_inf*, lsource*, dial*, gloss*)&gt;
    &lt;!ATTLIST gloss xml:lang CDATA "eng"&gt;
        Pode ter múltiplas 'gloss'. Se a palavra for apenas para cross reference, pode não possuir gloss.
        Informação desejada: &lt;gloss xml:lang="spa"&gt;</code></pre>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h4 id="Tentativa-de-ler-o-XML-para-passar-para-o-postgreSQL">Tentativa de ler o XML para passar para o postgreSQL<a class="anchor-link" href="#Tentativa-de-ler-o-XML-para-passar-para-o-postgreSQL">&#182;</a></h4>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">dict_path</span> <span class="o">=</span> <span class="s2">&quot;C:</span><span class="se">\\</span><span class="s2">Users</span><span class="se">\\</span><span class="s2">marce</span><span class="se">\\</span><span class="s2">Downloads</span><span class="se">\\</span><span class="s2">Ichi Moe Clone</span><span class="se">\\</span><span class="s2">JMdict</span><span class="se">\\</span><span class="s2">&quot;</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">xml.etree.ElementTree</span> <span class="k">as</span> <span class="nn">ET</span>
<span class="n">tree</span> <span class="o">=</span> <span class="n">ET</span><span class="o">.</span><span class="n">parse</span><span class="p">(</span><span class="n">dict_path</span><span class="o">+</span><span class="s1">&#39;JMdict.xml&#39;</span><span class="p">)</span>
<span class="n">root</span> <span class="o">=</span> <span class="n">tree</span><span class="o">.</span><span class="n">getroot</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">entry</span> <span class="ow">in</span> <span class="n">root</span><span class="p">:</span>
    <span class="c1">#print(entry.tag)</span>
    
    <span class="k">for</span> <span class="n">entry_tag</span> <span class="ow">in</span> <span class="n">entry</span><span class="p">:</span>
        <span class="k">if</span> <span class="n">entry_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;ent_seq&#39;</span><span class="p">:</span>
            <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Into Entry Table&#39;</span><span class="p">)</span>
            <span class="nb">print</span><span class="p">(</span><span class="n">entry_tag</span><span class="o">.</span><span class="n">tag</span><span class="p">,</span> <span class="n">entry_tag</span><span class="o">.</span><span class="n">text</span><span class="p">)</span>
        
        <span class="k">elif</span> <span class="n">entry_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;k_ele&#39;</span><span class="p">:</span>
            <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Into Kanji Table&#39;</span><span class="p">)</span>
            <span class="k">for</span> <span class="n">k_ele_tag</span> <span class="ow">in</span> <span class="n">entry_tag</span><span class="p">:</span>
                <span class="k">if</span> <span class="n">k_ele_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;keb&#39;</span><span class="p">:</span>
                    <span class="nb">print</span><span class="p">(</span><span class="n">k_ele_tag</span><span class="o">.</span><span class="n">tag</span><span class="p">,</span> <span class="n">k_ele_tag</span><span class="o">.</span><span class="n">text</span><span class="p">)</span>
            
        <span class="k">elif</span> <span class="n">entry_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;r_ele&#39;</span><span class="p">:</span>
            <span class="k">for</span> <span class="n">r_ele_tag</span> <span class="ow">in</span> <span class="n">entry_tag</span><span class="p">:</span>
                <span class="k">if</span> <span class="n">r_ele_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;reb&#39;</span><span class="p">:</span>
                    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Into Reading Table&#39;</span><span class="p">)</span>
                    <span class="nb">print</span><span class="p">(</span><span class="n">r_ele_tag</span><span class="o">.</span><span class="n">tag</span><span class="p">,</span> <span class="n">r_ele_tag</span><span class="o">.</span><span class="n">text</span><span class="p">)</span>
                    
                <span class="k">elif</span> <span class="n">r_ele_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;re_nokanji&#39;</span><span class="p">:</span>
                    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Into Reading Table&#39;</span><span class="p">)</span>
                    <span class="nb">print</span><span class="p">(</span><span class="n">r_ele_tag</span><span class="o">.</span><span class="n">tag</span><span class="p">,</span> <span class="n">r_ele_tag</span><span class="o">.</span><span class="n">text</span><span class="p">)</span>
                
                <span class="k">elif</span> <span class="n">r_ele_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;re_restr&#39;</span><span class="p">:</span>
                    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Into Re_Restr Table&#39;</span><span class="p">)</span>
                    <span class="nb">print</span><span class="p">(</span><span class="n">r_ele_tag</span><span class="o">.</span><span class="n">tag</span><span class="p">,</span> <span class="n">r_ele_tag</span><span class="o">.</span><span class="n">text</span><span class="p">)</span>
                    
        <span class="k">elif</span> <span class="n">entry_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;sense&#39;</span><span class="p">:</span>
             <span class="k">for</span> <span class="n">sense_tag</span> <span class="ow">in</span> <span class="n">entry_tag</span><span class="p">:</span>
                <span class="k">if</span> <span class="p">(</span><span class="n">sense_tag</span><span class="o">.</span><span class="n">tag</span> <span class="o">==</span> <span class="s1">&#39;gloss&#39;</span><span class="p">)</span> <span class="ow">and</span> <span class="p">(</span><span class="n">sense_tag</span><span class="o">.</span><span class="n">attrib</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="s1">&#39;{http://www.w3.org/XML/1998/namespace}lang&#39;</span><span class="p">)</span> <span class="o">==</span> <span class="s1">&#39;spa&#39;</span><span class="p">):</span>
                    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Into Gloss Table&#39;</span><span class="p">)</span>
                    <span class="nb">print</span><span class="p">(</span><span class="n">sense_tag</span><span class="o">.</span><span class="n">tag</span><span class="p">,</span> <span class="n">sense_tag</span><span class="o">.</span><span class="n">text</span><span class="p">)</span>

    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n\n</span><span class="s1">&#39;</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p><img src="data:image/png;base64,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" alt="image.png"></p>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

<pre><code>Entry: ID (Primary Key) [Integer] {AUTOINCREMENT} / Ent_seq [integer]

Kanji: ENTRY_ID (Foreign Key) [Integer] / Keb [String] / ID (Primary Key) [Integer] {AUTOINCREMENT}

Reading: ENTRY_ID (Foreign Key) [Integer] / Reb [String] / Re_nokanji [Boolean] / Re_restr [Boolean] / ID (Primary Key) [Integer] {AUTOINCREMENT}

Gloss: ENTRY_ID (Foreign Key) [Integer] / Gloss [String] / ID (Primary Key) [Integer] {AUTOINCREMENT}

Re_restr_table: READING_ID (Foreign Key) [Integer] / KANJI_ID (Foreign Key) [Integer] / ID (Primary Key) [Integer] {AUTOINCREMENT}

Obs.: Re_restr_table usa Foreign Key e não Composite Key para referenciar Kanji Table pois Entry+Keb não é necessariamente um elemento único. O mesmo keb pode possuir múltiplas leituras "únicas" a ele.

</code></pre>
<p>A tabela Entry conecta os kanjis com a leitura e significado corretos.</p>

<pre><code>Entry: Cada Entry é único.
Kanji: Possível múltiplos kanji para um mesmo Entry.
Reading: Possível múltiplas leituras para um mesmo Entry. Existe o "re_nokanji" caso a leitura não seja válida p/ o elemento.  O "re_restr" diz se possui leitura especial. Caso tiver, além da leitura originada da tabela 'Reading', terá também uma tabela referenciada 'Re_restr'.
Gloss: Possível múltiplos significados para um mesmo Entry. Especialmente para este caso (gloss xml:spa), TODOS os gloss irão valer para todos os kanji/reading.</code></pre>

</div>
</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Assim, temos o modelo desejado da base de dados; é necessário no entanto criá-la para passar estes dados e adaptar o web app de forma a usar a nova base de dados, o que será feito futuramente.</p>

</div>
</div>
</body>







</html>