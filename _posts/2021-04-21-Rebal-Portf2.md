---
title: "Rebalanceamento de Ativos - Parte 2"
date: 2021-04-21
tags: jupyter-notebook python pandas
---
Objetivo: Aprofundar a análise de rebalanceamento de ativos.

<!--more-->


<html>
<head><meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Rebal-Portf2</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>




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
<h1 id="Aprofundamento-do-estudo-de-rebalanceamento-de-portf&#243;lio">Aprofundamento do estudo de rebalanceamento de portf&#243;lio<a class="anchor-link" href="#Aprofundamento-do-estudo-de-rebalanceamento-de-portf&#243;lio">&#182;</a></h1><p>Será feita uma análise mais detalhada do funcionamento do rebalanceamento numa carteira fictícia de investimentos e com técnicas de rebalanceamento mais refinadas.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">os</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="n">pd</span><span class="o">.</span><span class="n">options</span><span class="o">.</span><span class="n">mode</span><span class="o">.</span><span class="n">chained_assignment</span> <span class="o">=</span> <span class="kc">None</span>  <span class="c1"># default=&#39;warn&#39;</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h2 id="1)-Cria&#231;&#227;o-das-tabelas-que-ser&#227;o-utilizadas">1) Cria&#231;&#227;o das tabelas que ser&#227;o utilizadas<a class="anchor-link" href="#1)-Cria&#231;&#227;o-das-tabelas-que-ser&#227;o-utilizadas">&#182;</a></h2><h3 id="1.1)-Exporta-o-retorno-do-IBOV-para-um-dataframe">1.1) Exporta o retorno do IBOV para um dataframe<a class="anchor-link" href="#1.1)-Exporta-o-retorno-do-IBOV-para-um-dataframe">&#182;</a></h3>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">RV_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_excel</span><span class="p">(</span>
     <span class="s2">&quot;DADOS.xlsx&quot;</span><span class="p">,</span>
     <span class="n">engine</span><span class="o">=</span><span class="s1">&#39;openpyxl&#39;</span><span class="p">,</span>
     <span class="n">sheet_name</span><span class="o">=</span><span class="s1">&#39;Ibov 2001-2021&#39;</span><span class="p">,</span>
<span class="p">)</span>

<span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">]</span><span class="o">/</span><span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">shift</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
<span class="n">RV_df</span><span class="o">.</span><span class="n">index</span><span class="o">+=</span><span class="mi">1</span>
<span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;period&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Mês&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">str</span><span class="p">)</span> <span class="o">+</span> <span class="s1">&#39;/&#39;</span> <span class="o">+</span> <span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Ano&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">str</span><span class="p">)</span>

<span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">][</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="mi">1</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="n">RV_df</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">+</span><span class="mi">1</span><span class="p">):</span>
    <span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">][</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">][</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">*</span><span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">][</span><span class="n">i</span><span class="p">]</span>

<span class="n">display</span><span class="p">(</span><span class="n">RV_df</span><span class="p">);</span>
<span class="n">RV_df</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;period&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;Growth&#39;</span><span class="p">);</span>
<span class="n">RV_df</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;period&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;Valor&#39;</span><span class="p">);</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">


<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output " data-mime-type="text/html">
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
      <th>Mês</th>
      <th>Ano</th>
      <th>Valor</th>
      <th>Growth</th>
      <th>period</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2001</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>1/2001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2001</td>
      <td>0.899203</td>
      <td>0.899203</td>
      <td>2/2001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2001</td>
      <td>0.816989</td>
      <td>0.908569</td>
      <td>3/2001</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2001</td>
      <td>0.844097</td>
      <td>1.033182</td>
      <td>4/2001</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>2001</td>
      <td>0.828958</td>
      <td>0.982064</td>
      <td>5/2001</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>236</th>
      <td>8</td>
      <td>2020</td>
      <td>5.622726</td>
      <td>0.965572</td>
      <td>8/2020</td>
    </tr>
    <tr>
      <th>237</th>
      <td>9</td>
      <td>2020</td>
      <td>5.353059</td>
      <td>0.952040</td>
      <td>9/2020</td>
    </tr>
    <tr>
      <th>238</th>
      <td>10</td>
      <td>2020</td>
      <td>5.316224</td>
      <td>0.993119</td>
      <td>10/2020</td>
    </tr>
    <tr>
      <th>239</th>
      <td>11</td>
      <td>2020</td>
      <td>6.161644</td>
      <td>1.159026</td>
      <td>11/2020</td>
    </tr>
    <tr>
      <th>240</th>
      <td>12</td>
      <td>2020</td>
      <td>6.734498</td>
      <td>1.092971</td>
      <td>12/2020</td>
    </tr>
  </tbody>
</table>
<p>240 rows × 5 columns</p>
</div>
</div>

</div>

<div class="jp-OutputArea-child">



<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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
"
>
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
<h2 id="1.2)-Exporta-o-retorno-da-taxa-DI-para-um-dataframe">1.2) Exporta o retorno da taxa DI para um dataframe<a class="anchor-link" href="#1.2)-Exporta-o-retorno-da-taxa-DI-para-um-dataframe">&#182;</a></h2>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">RF_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_excel</span><span class="p">(</span>
     <span class="s2">&quot;DADOS.xlsx&quot;</span><span class="p">,</span>
     <span class="n">engine</span><span class="o">=</span><span class="s1">&#39;openpyxl&#39;</span><span class="p">,</span>
     <span class="n">sheet_name</span><span class="o">=</span><span class="s1">&#39;Taxa DI&#39;</span><span class="p">,</span>
<span class="p">)</span>

<span class="n">RF_df</span> <span class="o">=</span> <span class="n">RF_df</span><span class="o">.</span><span class="n">rename</span><span class="p">({</span><span class="s1">&#39;%&#39;</span><span class="p">:</span><span class="s1">&#39;Growth&#39;</span><span class="p">},</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;period&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Mês&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">str</span><span class="p">)</span> <span class="o">+</span> <span class="s1">&#39;/&#39;</span> <span class="o">+</span> <span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Ano&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">str</span><span class="p">)</span>

<span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span><span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>
<span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">]</span><span class="o">/</span><span class="mi">100</span><span class="p">)</span><span class="o">+</span><span class="mi">1</span>
<span class="n">RF_df</span><span class="o">.</span><span class="n">index</span><span class="o">+=</span><span class="mi">1</span>

<span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>
<span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">][</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="mi">1</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="n">RF_df</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">+</span><span class="mi">1</span><span class="p">):</span>
    <span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">][</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">][</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">*</span><span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">][</span><span class="n">i</span><span class="p">]</span>


<span class="n">display</span><span class="p">(</span><span class="n">RF_df</span><span class="p">);</span>
<span class="n">RF_df</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;period&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;Growth&#39;</span><span class="p">);</span>
<span class="n">RF_df</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;period&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;Valor&#39;</span><span class="p">);</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">


<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output " data-mime-type="text/html">
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
      <th>Mês</th>
      <th>Ano</th>
      <th>Growth</th>
      <th>period</th>
      <th>Valor</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2001</td>
      <td>NaN</td>
      <td>1/2001</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2001</td>
      <td>1.0101</td>
      <td>2/2001</td>
      <td>1.010100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2001</td>
      <td>1.0125</td>
      <td>3/2001</td>
      <td>1.022726</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2001</td>
      <td>1.0118</td>
      <td>4/2001</td>
      <td>1.034794</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>2001</td>
      <td>1.0133</td>
      <td>5/2001</td>
      <td>1.048557</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>236</th>
      <td>8</td>
      <td>2020</td>
      <td>1.0016</td>
      <td>8/2020</td>
      <td>9.694666</td>
    </tr>
    <tr>
      <th>237</th>
      <td>9</td>
      <td>2020</td>
      <td>1.0016</td>
      <td>9/2020</td>
      <td>9.710177</td>
    </tr>
    <tr>
      <th>238</th>
      <td>10</td>
      <td>2020</td>
      <td>1.0016</td>
      <td>10/2020</td>
      <td>9.725713</td>
    </tr>
    <tr>
      <th>239</th>
      <td>11</td>
      <td>2020</td>
      <td>1.0015</td>
      <td>11/2020</td>
      <td>9.740302</td>
    </tr>
    <tr>
      <th>240</th>
      <td>12</td>
      <td>2020</td>
      <td>1.0016</td>
      <td>12/2020</td>
      <td>9.755886</td>
    </tr>
  </tbody>
</table>
<p>240 rows × 5 columns</p>
</div>
</div>

</div>

<div class="jp-OutputArea-child">



<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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
"
>
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
<h2 id="1.3)-Cria-se-uma-c&#243;pia-de-um-dos-dataframes-para-utilizar-como-base">1.3) Cria-se uma c&#243;pia de um dos dataframes para utilizar como base<a class="anchor-link" href="#1.3)-Cria-se-uma-c&#243;pia-de-um-dos-dataframes-para-utilizar-como-base">&#182;</a></h2><p>Esta cópia é mais detalhada, e será usada para guardar valores dos ganhos de cada tipo de investimento ao longo do tempo.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">portfolio_df</span> <span class="o">=</span> <span class="n">RF_df</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="k">del</span> <span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">]</span>
<span class="k">del</span> <span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;Valor&#39;</span><span class="p">]</span>

<span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;RV_invested&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>
<span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;RV_returned&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>
<span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;RF_invested&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>
<span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;RF_returned&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>
<span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;Total&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>
<span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;Rebal&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>
<span class="n">portfolio_df</span><span class="p">[</span><span class="s1">&#39;RV_ratio&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">NaN</span>

<span class="n">display</span><span class="p">(</span><span class="n">portfolio_df</span><span class="p">);</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">


<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output " data-mime-type="text/html">
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
      <th>Mês</th>
      <th>Ano</th>
      <th>period</th>
      <th>RV_invested</th>
      <th>RV_returned</th>
      <th>RF_invested</th>
      <th>RF_returned</th>
      <th>Total</th>
      <th>Rebal</th>
      <th>RV_ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2001</td>
      <td>1/2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2001</td>
      <td>2/2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2001</td>
      <td>3/2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2001</td>
      <td>4/2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>2001</td>
      <td>5/2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>236</th>
      <td>8</td>
      <td>2020</td>
      <td>8/2020</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>237</th>
      <td>9</td>
      <td>2020</td>
      <td>9/2020</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>238</th>
      <td>10</td>
      <td>2020</td>
      <td>10/2020</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>239</th>
      <td>11</td>
      <td>2020</td>
      <td>11/2020</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>240</th>
      <td>12</td>
      <td>2020</td>
      <td>12/2020</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>240 rows × 10 columns</p>
</div>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h2 id="2)-Criados-nossos-dataframes-da-taxa-DI,-IBOV-e-base,-podemos-come&#231;ar-a-an&#225;lise.">2) Criados nossos dataframes da taxa DI, IBOV e base, podemos come&#231;ar a an&#225;lise.<a class="anchor-link" href="#2)-Criados-nossos-dataframes-da-taxa-DI,-IBOV-e-base,-podemos-come&#231;ar-a-an&#225;lise.">&#182;</a></h2><p>Aqui é feita uma análise mais refinada que a anterior, obtendo os valores da evolução mês a mês do portfólio. O rebalanceamento aqui é feito quando o capital fica muito 'longe' do valor inicial desejado. Isto é: caso decida-se alocar 50/50, caso max_var = 0.1, sempre que RV ou RF ficar com valor acima de 60% ou abaixo de 40%, será feita realocação de recursos de forma a reequilibrar a carteira.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">portfolio_growth</span><span class="p">(</span><span class="n">max_var</span><span class="p">,</span> <span class="n">initial_money</span><span class="p">,</span> <span class="n">RV</span><span class="p">):</span>
    <span class="n">portfolio_copy_df</span> <span class="o">=</span> <span class="n">portfolio_df</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
    <span class="n">RF</span> <span class="o">=</span> <span class="mi">1</span><span class="o">-</span><span class="n">RV</span>
    <span class="n">RV_value</span> <span class="o">=</span> <span class="n">portfolio_copy_df</span><span class="p">[</span><span class="s1">&#39;RV_invested&#39;</span><span class="p">]</span>
    <span class="n">RV_returned</span> <span class="o">=</span> <span class="n">portfolio_copy_df</span><span class="p">[</span><span class="s1">&#39;RV_returned&#39;</span><span class="p">]</span>
    
    <span class="n">RF_value</span> <span class="o">=</span> <span class="n">portfolio_copy_df</span><span class="p">[</span><span class="s1">&#39;RF_invested&#39;</span><span class="p">]</span>
    <span class="n">RF_returned</span> <span class="o">=</span> <span class="n">portfolio_copy_df</span><span class="p">[</span><span class="s1">&#39;RF_returned&#39;</span><span class="p">]</span>
    
    <span class="n">Total_value</span> <span class="o">=</span> <span class="n">portfolio_copy_df</span><span class="p">[</span><span class="s1">&#39;Total&#39;</span><span class="p">]</span>
    <span class="n">Rebal_value</span> <span class="o">=</span> <span class="n">portfolio_copy_df</span><span class="p">[</span><span class="s1">&#39;Rebal&#39;</span><span class="p">]</span>
    <span class="n">RV_ratio_value</span> <span class="o">=</span> <span class="n">portfolio_copy_df</span><span class="p">[</span><span class="s1">&#39;RV_ratio&#39;</span><span class="p">]</span>
        
    <span class="n">RV_value</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="n">initial_money</span><span class="o">*</span><span class="n">RV</span>
    <span class="n">RF_value</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="n">initial_money</span><span class="o">*</span><span class="n">RF</span>
    <span class="n">Total_value</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="n">RV_value</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span><span class="o">+</span><span class="n">RF_value</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span>
    
    <span class="n">last_month</span> <span class="o">=</span> <span class="n">portfolio_copy_df</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
    
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="n">last_month</span><span class="o">+</span><span class="mi">1</span><span class="p">):</span>
        
        <span class="k">if</span> <span class="p">(</span><span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">/</span><span class="n">Total_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span> <span class="o">&gt;</span> <span class="p">(</span><span class="n">RV</span><span class="o">+</span><span class="n">max_var</span><span class="p">):</span>
            <span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">Total_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span><span class="o">*</span><span class="n">RV</span><span class="o">-</span><span class="n">max_var</span><span class="o">/</span><span class="mi">2</span>
            <span class="n">RF_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">Total_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span><span class="o">*</span><span class="n">RF</span><span class="o">+</span><span class="n">max_var</span><span class="o">/</span><span class="mi">2</span>
            <span class="n">Rebal_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="kc">True</span>
            
        <span class="k">elif</span> <span class="p">(</span><span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">/</span><span class="n">Total_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span> <span class="o">&lt;</span> <span class="p">(</span><span class="n">RV</span><span class="o">-</span><span class="n">max_var</span><span class="p">):</span>
            <span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">Total_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span><span class="o">*</span><span class="n">RV</span><span class="o">+</span><span class="n">max_var</span><span class="o">/</span><span class="mi">2</span>
            <span class="n">RF_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">Total_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span><span class="o">*</span><span class="n">RF</span><span class="o">-</span><span class="n">max_var</span><span class="o">/</span><span class="mi">2</span>
            <span class="n">Rebal_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="kc">True</span>
        


        <span class="n">RV_returned</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">*</span><span class="p">(</span><span class="n">RV_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">][</span><span class="n">i</span><span class="p">]</span><span class="o">-</span><span class="mi">1</span><span class="p">)</span>
        <span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">+</span><span class="n">RV_returned</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>

        <span class="n">RF_returned</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="n">RF_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">*</span><span class="p">(</span><span class="n">RF_df</span><span class="p">[</span><span class="s1">&#39;Growth&#39;</span><span class="p">][</span><span class="n">i</span><span class="p">]</span><span class="o">-</span><span class="mi">1</span><span class="p">)</span>
        <span class="n">RF_value</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">RF_value</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">+</span><span class="n">RF_returned</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
        
        <span class="n">Total_value</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="p">]</span><span class="o">+</span><span class="n">RF_value</span><span class="p">[</span><span class="n">i</span><span class="p">]</span>
        
        <span class="n">RV_ratio_value</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">RV_value</span><span class="p">[</span><span class="n">i</span><span class="p">]</span><span class="o">/</span><span class="n">Total_value</span><span class="p">[</span><span class="n">i</span><span class="p">]</span>
        
    <span class="k">return</span> <span class="n">portfolio_copy_df</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Com a função feita, podemos estudar a evolução do portfolio ao longo do tempo:</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df_X</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">portfolio_growth</span><span class="p">(</span><span class="mf">0.1</span><span class="p">,</span> <span class="mi">100</span><span class="p">,</span> <span class="mf">0.2</span><span class="p">))</span>

<span class="n">IBOV_copy_df</span> <span class="o">=</span> <span class="n">RV_df</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">ax1</span> <span class="o">=</span> <span class="n">IBOV_copy_df</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;period&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;Valor&#39;</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;IBOV&#39;</span><span class="p">,</span> <span class="n">xticks</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">240</span><span class="p">,</span><span class="mi">59</span><span class="p">))</span>


<span class="c1">#df_X.plot(x=a, y=&#39;Rebal&#39;, ax=ax1, kind=&#39;bar&#39;, color=&#39;r&#39;,  xticks=np.arange(1,240,59)) / método alternativo de adicionar linha</span>
<span class="n">red_lines</span> <span class="o">=</span> <span class="n">df_X</span><span class="p">[</span><span class="n">df_X</span><span class="p">[</span><span class="s1">&#39;Rebal&#39;</span><span class="p">]</span><span class="o">==</span><span class="kc">True</span><span class="p">]</span>

<span class="k">for</span> <span class="n">xc</span> <span class="ow">in</span> <span class="n">red_lines</span><span class="o">.</span><span class="n">index</span><span class="p">:</span>
    <span class="n">ax1</span><span class="o">.</span><span class="n">axvline</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">xc</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;r&#39;</span><span class="p">)</span>


<span class="n">df_X</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">secondary_y</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;RV_ratio&#39;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">ax1</span><span class="p">,</span> <span class="n">kind</span><span class="o">=</span><span class="s1">&#39;bar&#39;</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;ratio&#39;</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;k&#39;</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">9</span><span class="p">,</span><span class="mi">5</span><span class="p">),</span> <span class="n">xticks</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">240</span><span class="p">,</span><span class="mi">59</span><span class="p">));</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

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
<p>No gráfico acima, a linha vermelha representa os meses onde existe rebalanceamento de carteira. Em cinza, podemos ver a divisão da carteira nos dois ativos (RF e RV) e em azul vemos a evolução do índice IBOV.
Como pode ser visto, o rebalanceamento pode agir como forma de 'market timing', evitando grandes perdas: quando o IBOV sobe demais e a carteira passa a ter uma concentração muito grande esse percentual é reduzido, diminuindo o risco do portfolio.</p>
<p>Mais especificamente a variação máxima permitida deste portfólio é de 10%, resultando em 4 rebalanceamentos ao longo dos 20 anos.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df_X</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">portfolio_growth</span><span class="p">(</span><span class="mf">0.05</span><span class="p">,</span> <span class="mi">100</span><span class="p">,</span> <span class="mf">0.2</span><span class="p">))</span>

<span class="n">IBOV_copy_df</span> <span class="o">=</span> <span class="n">RV_df</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">ax1</span> <span class="o">=</span> <span class="n">IBOV_copy_df</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;period&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;Valor&#39;</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;IBOV&#39;</span><span class="p">,</span> <span class="n">xticks</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">240</span><span class="p">,</span><span class="mi">59</span><span class="p">))</span>


<span class="c1">#df_X.plot(x=a, y=&#39;Rebal&#39;, ax=ax1, kind=&#39;bar&#39;, color=&#39;r&#39;,  xticks=np.arange(1,240,59)) / método alternativo de adicionar linha</span>
<span class="n">red_lines</span> <span class="o">=</span> <span class="n">df_X</span><span class="p">[</span><span class="n">df_X</span><span class="p">[</span><span class="s1">&#39;Rebal&#39;</span><span class="p">]</span><span class="o">==</span><span class="kc">True</span><span class="p">]</span>

<span class="k">for</span> <span class="n">xc</span> <span class="ow">in</span> <span class="n">red_lines</span><span class="o">.</span><span class="n">index</span><span class="p">:</span>
    <span class="n">ax1</span><span class="o">.</span><span class="n">axvline</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">xc</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;r&#39;</span><span class="p">)</span>


<span class="n">df_X</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">secondary_y</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;RV_ratio&#39;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">ax1</span><span class="p">,</span> <span class="n">kind</span><span class="o">=</span><span class="s1">&#39;bar&#39;</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;ratio&#39;</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;k&#39;</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">9</span><span class="p">,</span><span class="mi">5</span><span class="p">),</span> <span class="n">xticks</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">240</span><span class="p">,</span><span class="mi">59</span><span class="p">));</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">



<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAjIAAAFiCAYAAADsqjIzAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8vihELAAAACXBIWXMAAAsTAAALEwEAmpwYAABqmUlEQVR4nO3dd3ib1dn48e+xZVvee9uJnb2XExJIgLDKKIRVILSlLy0QSumgLbzwvh0v/FoKlC7aQiHQFgplldGyNwGyIHb2jhPb8d7blmxZ5/eHJMd2PGRbstb9uS5fsqVHz3PkR+PWOfe5j9JaI4QQQgjhi4I83QAhhBBCiLGSQEYIIYQQPksCGSGEEEL4LAlkhBBCCOGzJJARQgghhM+SQEYIIYQQPmvEQEYpdb1SSg/ykzMB7RNCCCGEGJIaqY6MUioXWG7/0wD8FWgEsrXW3YPdJygoSIeHh4+vZSaT7dJoHN9+Jnrf3nzsieJrj9Ffn2vCPQLhnAbCY+wr0B7vGHR0dGittVeO4hhG2kBrXQQUASilvgKEAn8bKogBCA8Pp729fXwtW73adrlhw/j2M9H79uZjTxRfe4z++lwT7hEI5zQQHmNfgfZ4x0Ap1enpNgxlxEBmgJsBK7B+4A1KqXXAOoDQ0NDxt0wIIYQQYgROdxMppaYC5wDvaK2LB96utV6vtV6qtV5qMIw2PhJCCCGEGL3RjHfdDCjgL25qixBCCCHEqDgVyCilQoHrgePAW+5skBBCCCGEs5ztkbkCSAYe11pb3dgeIYQQQginOZXMorV+HnjezW0RQgghhBgVr5wTLoQQQgjhDAlkhBBCCOGzJJARQgghhM+Sgi9CCCGEGJTZ0kOQUp5uxrCkR0YIIYQQg/rPjgqm/+RtTzdjWBLICJcpKCjwdBOEEEK4UG2b2dNNGJEEMkIIIYQYVG2rmegw785CkUBGCCGEEIOqbTOTFB3m6WYMSwIZIYQQQgyqrtVMcpQEMkIIIYTwQbVtZpKlR0YIIYQQvqiu1UxSVKinmzEsCWSEEEIIH1TdYuKD/dVu27+pu4cWk0V6ZIQQQgjhen/bVMSN/8hnb3mzW/ZfZ596LYGM6CV1VoQQQrhKaUMHAA99eMQt+69r6wIgSZJ9hRBCCOFqZY2dKAXv769mX4Xre2VqW6VHRgghhBBuUtrQwcULMog2GvijG3plfCWQ8e5yfUIIIYQ4SZvZQmNHN3PSY5iUEM7DHx+lob2LhEjXzTBy5MgkRkogI4QQQggXKm/sBCArPhxDUAQAlc2dLg1kalvNxEWEEGrw7sEb726dEEII4Ua+OgnDkeibnRBBSoytx6Sm1bULPNb6QFVfkB4ZIYQQwueUNdoCmaz4cDq7egCobXFtIFPXZvb6GUsgPTJCCCGEzylr7MQYEkRiZGhvMm5Nq8mlx/CF5QlAAhkRwHy1S1kIIcoaO8mKj0AphTEkmBijwT1DSxLICCGEEMLVShs7yI4P7/07JcZIjQuHltrNFjq6ekY1tKSUWqmU2q2UMiultiullgyyzalKqc1KqSb7z8tKqeQ+t+sBP/8e6biSIyOEEEL4mLLGTpZMiu/9OyU6zKVDS6NdnkApZQReBjqBHwI/AV5SSk3XWvf02XQGUAfcCZwJXAu0AN/ss83LwEv238tGOrb0yAghhBA+pMXUTXNnN1l9e2Siw6htc12PzBiK4V0IpAKPaK0fAf4K5AKrB2z3nNZ6jdb6MeBm+3VzB2yzH3hda/281nrjSAeWQEYIIYTwIWUNthoy2QkRvdc5hpa01i45hqNHJimqty6NQSmV3+dn3YC75Novyx3NtF9O6buR1rqrz5/n2y8/HbCvnwJtSqkSpdTFI7VVhpaEEEIIH9J36rVDSnQYZouVFpOF2PCQcR9jkB4Zi9Z66Sh2oeyXg0ZWSqmVwN+AAuDuPjc9AGwFkoHfAs8ppVK11h1DHUgCGSGEEMKHlPVW9T3RI+MIOGpbTS4JZBwrXydEOF0puMh+mWW/zHRcb8+fsTp6Y5RSZwBvAoXA+VrrNsdOtNZ3OX5XSl0AXAFkA4eGOrAMLYlxk2nMQggxcXaWNhERGkx8xImAJSXaCOCymUstpm6iwwwYgp0OE94GaoBblFK3ADcAxcAGbAnA2wHsM5neBoKBx4HzlFKX2G+7SCn1rFJqnVLqTmx5N7WcCJIGJT0yQgghhI947JOjvLarghtW5aKU6r3e1csUtHRaiBlFz47W2qSUugp4GHgI2AfcpLXu6dtOYAHg6Ep62H5ZArxuv0wHfo0t0MkHfjwgr+YkEsgIIYQQPuDVHWXc9/ZBLl6Qzv9eNLvfbSkuru7bYuom2ji6EEFr/Skwf5DrVZ/fnwSeHOL++4CzRnVQnBxaUkrFKaX+YS9e06aUGphhLIbhL0Mv/vI4hBDC11itmt+8e5jFk+L43dWLCA7q18tBVJiB8JBg1w0tdXaPqkfGk5wd/Pob8DVs88Jvw5agI3yQBCNCCOF7thyrp7ypk2+uzCXUcPJHt1KKlJgw1w0tmSzEGP0kkFFKTQEuB54D/gf4u9b6W+5umBDuIsGcEMLX/Cu/lGijgS/NSR1yG1dW97X1yPhG9okzPTJz7JfLgHagXSn1wMCN7FnG+UqpfIvF4so2Ci8lAYEQQrhfi6mbd/ZVsWZhBsaQ4CG3S452ZY9Mt//0yACOajiRwDXAJuC/lVLn9t1Ia71ea71Ua73UYPCNKE4IIYTwdm/ursTUbeWqpdnDbpcSbaTWBTkyVqumzTy6WUue5EwgU2y//Exr/Qrwov3vqW5pkRBCCOFmvtSj/OqOcqalRLEwK3bY7ZKjw2g1W+js6hl2u5G0mi1oDTGjnLXkKc4EMtuBPcA5SqmbsK1Q2YOtZ0YMw5deKEIIIbxPm9nC9pJGzpuTyoB6LCdx1RTsls5uAP/pkdG2FaiuBY4CfwISgG9orfe6uW1CCCHEmPnDl8ltxQ1YrJrTpiaOuK1jaYJW0/jyVFtM9kDGj3Jk0Frv01qfqrU2aq1naK2fdXfDhBCu5w9v7EKMli8/77ccrSc0OIilkxNG3DbMnghstljHdcyWTlsg5E+zloQP8+UXsBg7Oe9C+IdNhXUsnhRHeOjQs5Ucwuz1ZcyWkXNkvvvsdh7+ePCScH7ZIyNEX/IhKYQQ7tfY3sX+yhZOm5o05DZ9348dhfK6RuiR0Vrz0cEa/pVfOujtjhwZx1CVt7/nSyAjhBBCeAmtNS8VlLG/ooXPi+rRGk6bNnJ+DPTtkRk+kGnq6Kajq4fi+g7KGjtOur3FnmPjKz0yvjEA5qcKCgrIy8vzdDOEH5HnlBC+y9Jj5X9f3cOL+WWEBCumJkcRERrMwqw4p+4fZnAuR6a8qbP3982F9Vy9LKLf7Y4emSg/mn4thBBCuIW3D1tMFK013/nndl7ML+OW1VNZPTOFg1WtLMtJGHRtpYEKCgp6e2RGGloqa7QFMkrBxsK6k25vMXUTHWY4aWFKbyWBjJ8a6c1B3jyEEP5qqPc3b37fO1zdxnv7q7nt3OncecEs1l+Xx6NfX8LPLp4z8p3tnE32dfTInDE9mc1H67BVWTmhpdN3qvqCBDLCj3nzm5YQwnmB8Fr+orgBgCsWZwG21awvmJfOtJQop/fRO7TUPXyPTEVTJ+EhwXx5QTp1bV0cqm7td3uLqZtoHxlWAglkhAhIgfDBIIQv2VbUQGpMGNkJ4WPeR++spZ4RcmQaO8mMD2fVNNtsqI1H+g8v2Va+lh4ZMQryoeJe8v91zf9A/o9CuIfWmm3FDSzLSRhxGYLhOAKZkXpkyps6yYwLJyMunClJkWw5Wt/v9haTxWdmLIEEMuMWCG/u/vIY/eVxjEYgPmYhfE1ZYyeVzSaW5YxcvXc4wUGKkGDlVI5MZryt52fxpHh2lzf3u93WIyNDS2IMHB868uEjvIU8F4WnFBQUBMzzL7/Elh8z3kAGIDQ4aNjp1x1dFhrau8iMswUy8zJjqG01U9NyYqHJFlO39MgI4UmB8ubnDvK/E2LifVHUSLTRwMy0aKfvM9RrNSwkeNjp1xX2GUsnAplYAPZW2HplrFZNm1lmLQkhhBAu54u91gerWnjis2PDbrOtuIGlk+Odqtsy0mMPMwQNO7TkqCHjGFqanR6DUrCnrAWAVrMFrSFGZi0FrkDqDhVCCDG8578o5ZdvHmDzIIXnAApKGimsaWNZ7viHlcARyAzdI1M+oEcmKsxAblJkb4+Mo6qv9MiICSfBk5ho8pwTruSvz6faVjMAD753qF/hOatV8/DHhVz92BYy48K5dFGmS44XaggadmipvLETQ5AiNcbYe938zFj22RN+fW3la5BAxuc5++L31zeJQCbnVIj+vPE1UdNqwhCk2HG8iY8P1QC2IOan/9nLg+8e4sJ5abz1g9N7e0gGM5rHFWYIHrZHpqKpk7RYY79hrHkZsVQ0m6hvM9PSaV8wMtzglf/PwUggM0aePsGePr7wHhP9XJDnnhDOq24xc/7cNCYlRHDvmwd4qaCM/311D89+fpxbz5rKn65dTKwLh3FGypFx1JDpa25mDAD7KlqkRyaQjebNvaC1deSNJqAdQggh3EdrTU2riYw4Iz+/eA4VTSZu/9cunt9WyndWT+X2L80cVwG8wTgztORI9HWYm2GbubSnvLk3R8aVwZW7SSAT4PoGPgODIAmKhBBi7FrNFkzdVlKijZw7J5W995zPBz86k//cupI7znd9EAPDJ/t291ipajGd1CMTGx7CpIQI9pY302KyDy1Jj4wQwpdJECtczRenTo9XTYst0TclJgywVd6dlhLFwuy4QYMYV/yPWkoPD7lEQVWzCatm0HycFVMSeHtvFU9vKQYgSqZfCzHxAukN0lXc8T+T8yCcMdTzxJ+ePzWttmq5ydFhY7r/WP4XIcFqyEUje6dex58cyNyzZh7XrZhMcX0H0UaDUzVtvIUEMkIIl/CnDyDhG7z9OeeYel1z7MCEHTPEEIS5e/Bk3/LG/jVk+goPDeYXl83jmRuW88CVC9zaRleTQGYI3v4CcadAfuxi9OT5IjzNW5+D1fb1ixIiQyfsmKHD5Mg4emQyhpnqvWp6EhfNT3dL29xFAhkf460vWCGEAHmP6qumxUx4SDARocETdsyQoGECmcZOkqLCMIYE+9V5kkBGCCGEcIOaVjMpMWFumZ00lJBhpl9XNJ889dofBGQgU9Da6tZaLsL/+dO3GSGEe9S0mkjpk+g7VIkLV76fhNqTfa1WfdJt5Y2dZA0zrOSrAjKQEUIIIdytptVMSrTxpOvd+UUoJNj2sT5w5pLWmvKmTjLiTm6Pr5NARggh07CFcIPaFvOYp16PVYjB9rE+ME+mrq0Ls8U67JpOvkoCGSF8jAQIQni/ji4LrWZLv1WmJ0JosCOQ6T8F+0QNmYgJbc9EkEBG+IThPrzlg10EAnme+5beqr4T3CMTGmxLLB5Y3XeoGjIFBQU+/9xyKpBRShUrpXSfn51ubpfHjLTekK+fcE9x1f9N/v9CCG9292v7+M4/C6hp7b88wUQxDJEjU97UAQxe1ddVlFIrlVK7lVJmpdR2pdSSQbY5VSm1WSnVZP95WSmV3Of2y5RShUopk1Jqg1Iqd6TjjqZH5lPgWvvPnaO4n9v564ebvz4uMTbyfBDCu5U1dvD01hLe2lPFP+xrFg2W7OtOvUNLg/TIRIcZ3LaqtVLKCLwMRAM/BFKBl5RSA4vozADqsMURbwFXAL+27yMNeB5oAe4A8oCnRjr2aAKZIuBNrfXzWut3R3E/l5M3dCF8h7xehS9wRUmOv28qRgGJnWW8sbsS8MDQkmHoHBk315C5EFvw8ojW+hHgr0AusHrAds9prddorR8DbrZfN9d+eS0QBtyntf4T8CpwulJq6nAHHk0g8w2gRSlVo5S6YeCNSql1Sql8pVS+xWIZxW69gze/2Xpz2wYjNXpcw9fOuwhs/vJ8HWttlxZTNy9sK+XLC9L5zlnTAFvvSFyEe3pAhtI7/doycGjJNN4ZSwbHZ7z9Z92A2x1DQOX2yzL75ZS+G2mtu/r8eb798tPR7OOkho3UcrvHgUOAEbgfeEwp9ZHWuqhP49YD6wEiIyNPrsQjhAs53mTy8vI83BIhxHAKCgoC4nX6/BfHaTNbuOn0KZirrHy5Q3G0pm1Cq/oChBrsyb4DA5nGDpblxI9n1xat9dJRbO944IPGA0qplcDfgALg7rHsw8GpHhmt9b1a65e01s8ALwDB2Ma5hAgo/vKtUwjhWv94/WOWTo5nXmYsAH+4ZhGvfOe0CW9HSLAtJaVvINNi6qbFZCEjLtyd72GOjo0s+2Wm43qllFEp1btyplLqDOAd4Chwvta6baR9DHfgEQMZpdR8pdTrSqnvKKW+j22IqRPYM9J9hRAiEEnAG3iqW8zMyYjp/TskOIgDe3ZNeDtCHNOv++TIHK+3zVianODWGjJvAzXALUqpW4AbgGJgA7aYYTuAfSbT29g6RB4HzlNKXWLfx/NAF3CnUup7wOXARq310eEO7EyPTJ39gP8P27BSCXC51rrC+ccnxNjIB4IQYqK1my0cqGx2evs2s4U2s4X0WM9XzQ0dJEfmeIMtkJmUOHwgM573W621CbgKaAMewhbUXKW17hmw6QIgAggHHgaeA/5k30cltoTfOOA3wA7g+pGOPWIgo7Wu1FpfpLVO0lpHaK2XemrWknyo+RZfK7TkS20VYiIE4muioqmTyx/ZxB0v7aGkvt2p+1Taq+Z6wzpGgy1R0BvIONkjM9bzrrX+VGs9X2sdqrVerLXOt1+vtNbz7L8/af+7709On328orWeqrUO01qfMVJvDEhlXyG8fpaVv3yY+MvjCATe/ppwJVN3D1UtJkoaOrjxqXx+9MJOjtXaAhhHNdyRVDSbAMjwgnWMQnrryJzoCCmp7yAhMpRo48TOoJooEsgIIYSLSLDmWz47UsuNT22juK6dzu4eKpo6mZUezV+vXwZAdavJqf1U9PbIeD6QcSxR0Ley7/GGdrLdmx/jUc5OvxZCCCGc5gvTrv+xpQSlFHMyYgnp7uStH5xOQUEEMyfbpilX29dLGkllUydBClInuPjdYEIGqex7vKGDxdnjmnrt1fyqR8ad34bkm1ZgkvPuXXztfLiivd7wmL2hDe5Q1WxianIkMcb+3+mjwgyEhwT1Lvw4kvImEwmRob3rHHmSITiI4CDVmyPT3WOlosnE5BESfX2Z5//rQgghhAdUNptIihq8FyUhMnRUQ0vJXtAb4xAaHNQ7tFTe2EmPVfv10JJPBzL++i1B+A55Dgrhm7osPdS1mUmMHDwAiY8IpdbZoaXmziEDIk8ICwnqTfZ1zFhycw0Zj/LpQEb4LwkQhBDu1NDeDUBSVOigtzvbI2O1aiqaTaR4UyBjCOodWipxBDKJkZ5sklv5ZSAjH4JC+Ddve42P1B5va6+AujZbb0viMENLNS1mtB5+6cD69i66LFbvGloyBPUWxDte306oIWjCV+GeSH4ZyAjvJW/oYizkeSNczRHIDNcj09ndQ6vZ0u/6gc/FyubOYffjCWGG4N4emeMNHUxKiCAoaGIXr5xIEsgIj5IPKCEGJ68N96pv6wIgaYieioRIW2Ay0swlRw2ZpGjPV/V1sA0t2XJkSuo7mJwQ4dfPJwlkhEf42ovK19rrzeR/OT6O/5/8H8enrs1MdJiBiNDBy6nF9wYyw+fJbP58G4DXDS2ZLVa01hxv6PDrGUswAYGMvNiEr/H0GlHymvEdrjpX49nPRD5f/Om5Wd/WRVrs0L0oifZAZos9UBlKbasZY0jQSbVoPMmR7Fvf3kVHV49f15ABP++R8acXnRDCewTSWkT+qq7NPGwgEx9hC2Tq27tG3E9GXDhKeU8OiiNHptQ+Yyk7XgIZIYQQbjDYly35AjYx6trMpA8TyESEBhMRGkzDCIFMbauZjFjPr7HUV6jBVkemzL7opQwtCSGEl5IP/dGR/5dNd4+Vxs5u0oYJQJRSpMYYaeg4EciYunu47fkdfHK4loKCArp7rJQ3mciK965AJsxgq+zrCGQyvax9ruYTgYy8+PyfJDAKkPMvJkZNqxmtGbZHBmwJvI1tJwKZwpo2CmvbeeKzYwBsKqyjzWzh7Fkpbm3vaIUZgjF3Wylr7CA+IoSoMO/J33EHnwhk3EneOIUQYmw8nRg/VlX22i/D5cgAJ/XIFNe3A7YApq7NzGs7K4gKDebMmcnua+wYOGYtlTV2kuXn+TEggYwQwkN89UNQ+L7KZtuU6pFyW1Kiw2ho7+qt7ltcZwtkrBre21fFu/uqOG1qEmGGYPc2eJTCDEF0WXooa+zwumEvd5BARgghRECpsgcyI/fIhGGyWGmzV/ctqusgMTKEJZPi+Fd+Ge1dPV7XGwO2RSNNFivlTZ0SyAghnCM9C8IZ8jzxDpXNJqdqv6TYq/VW26v7Fte3kx4bzhVLsui2alKiw5iXGev29o5WmCGYLosVU7dVhpaEEMIT5ANfuFNlcydJUaEj1n5x9GYU17VTUFBAcV07mXHhXLIgA2NIEJcvziTYC9cwCjOc+GjvqDjswZZMDAlkhBBey18DGn99XL6isKaNtJiR10aalxmLIQjySxppM1uob+8iIy6c2IgQHvnaEn543owJaO3o9Q1kUrxoDSh38dpApqC1VapnCiGEF/LlQKzNbOFITRszUqNH3NYYEsy0lCjyixuotC8OmRFnCwxSoo0YQ7wrydehXyAT4z1rQLnLhAcyvvwCEEL4H399T/LXxzVee8qa0RqnAhmAOemx7C5rpsQ+9TojzvuTZ0PtgUx8RMiQi2L6E6/tkRFCCFeSD/YTAvl/sausCYDpTgcy0XT1WPnkcB1KjTzTyRs4poMHQqIvSCAjhBB+YSzBiT8HND1Wze3/2smCu9/lmke38Pintmq8u0qbmJQQQWx4iFP7mZUeA8DOsiYyYsO9rmbMYBxDS4Ew9RomMJDx5xeMEML3+et7lL8+rpHsLmviYFUbK6YkkhwTxmOfHqXbYmVXaRMLs+Oc3k9cRChTkyPRGnKSfKOHI1QCmYkRqC8uIYQQ7rfxSB0A910xn+tPy6GurYt391VR0WxiYdboar8sy0kAICcx0uXtdAcZWhJCjMjSY/V0E4QQw/issI6pyZEkRoWxeFI8GbFGnt5aAsCiUfTIACy1BzK5Sb4RyETZC/1NSpRARggxiA2Hali7fit1beaTbhtPT2Mg91K687EH8v81UHV0WdhxvJHF2fEABAcprlk2ifauHoKDFHMzRtcjc/r0JJKiQjklN8EdzXW5hVmxPHZdHmdO977lE9zB44GMvMkIX7PxSB0mi5XCmjZPN0UMYbgFKR3Xy3uP/9pb3kx3j2bRpLje665Zlk2Qgpmp0YSHji5hNzXGyJPfPIUFWXEjbusNlFKcPzeNIC+sOuwOTgcySimjUuqQUkorpf7szkYJ4c32lDcDUN7Y6eGWCCEGs+N4E2GGIGann5hinRZr5KunTOJbq3I92DLhDqPpkfk5kOWuhgjhC6xWzf6KFgDKxhnISI+A67jyfxmI58XfHvPO0iZOyU04aar02lMm8ZW8wPgY87dzOhynAhml1ALgh8Ddbm2NmwTSCRXuVdliotVsAaCsscPDrRm9ji7LmO73lw1H+ceWYtc2xg3ktS5qWk2UNnayalqSp5siJsiIgYxSKgh4AngY2DbMduuUUvlKqXyLZWxvlkJ4O0deTGRoMOVNvjW09MnhWr76+NZR5/a8v7+aB945yCvby2gxdbupdUK4xr5yW4/paGcmCd/lTI/MN4Ec4B9Apv26WKVUv3RorfV6rfVSrfVSg8H/13YQgelYTRuhwUEsyo5zamjJmxY+/fhgDRYrvL6rwun7VLeYuP1fu0iNCcNite0jUPhq746vtttV9lXYctjmZMR4uCViojgTyGQDycAu4Bn7dV8H7nNXo4TwVoW1bcxKjyYjLpyKpk56rNrTTXLaF0UNALy1p9Lp+zz2yVGsVs3z604lLjyE9/ZXA7D5aB1//rgQrX3n8YvAsK+ihfRYI9FG55YgEL7PmUDmReAq+8/d9uveAf7ipjYJ4ZW01hytaWNeZiwpMWFYrJrGjpNryYxk4DdmV3+D7u6x0jkgF6bNZOFAVQsp0WEcqWnjuH0l3+FYeqzsLm/m8iWZ5CZFsmJKIhsO1tBmsnDHv3bzzt4qdpQ2nXQ/s6XHVQ/FKwR6D4ev2V/ZwhQfKVwnXGPEQEZrvV9r/ZLW+iXgE/vVR7XW8uoWAaW0oZO2rh7mZcSSEm1bAbe6xblAZiI/DH/4wk5+8PzOfr0lB6qa0Rq+cepklILNR+tH3M/h6jZM3VaWTLIVFVsxJYH2rh5++cZ+yps6CVYnD1O9tquCteu3srmwzrUPSggntJktlNR3MCVZAhlPUEqtVErtVkqZlVLblVJLhtjuJaVU42DlXOzX9f3590jHHVVBPK31Bq210lp/dzT3c4Z86xHezlE/Zn5mLKkxYQDUtJg82aST5Bc38MbuSiqaTeyvbOm9fm95CyHBilOnJrJ0cjwbnQg0dpQ2ArDYXlRsQVYsUWEG9la28OUF6SzLSeDN3ZW9w2sl9e3c+dJuunt0byl4ISZSca0tkX1qcpSHWxJ4lFJG4GUgGtss51TgJaXUYNUHzcCrw+zuZeBa+89vRjq2xyv7CuErDlW3EqRgRloUydH2QKZ19ENL7mLq7uGxT4/1rnjbNzF3X0UzC7LiCDMEc+G8dIrrOyiqO3l46e+bithkD3J2HG8iNtzApATbei2hhmDOmZ1CmEHxvxfN5vQZydS0mtlf0UxzZzf3vX2AyDADZ05P4oMD1TR3ygwnMbGO2Z/TMrTkERdiC14e0Vo/AvwVyAVWD9xQa/01bBOIhrIfeF1r/bzWeuNIB5ZARggnHa9vJykqjDBDMGGGYJKiwqhxcmhpIvx1YxGVzSbuv2IB01Oi+MgeyHR0WSisbutdJ+asWSkAfFHUf3ip3Wzh5e3lPPDOQQB2HG9kZmo0Sp0oc373JXP5wzWLyIwLZ3luPOEhwby2q4KrHt1MVZOJP127mKuWZtPdo9lwKHBmOAnvcKyunaSoUOIjQz3dFH9kcJRYsf+sG3C7o2Ryuf2yzH45ZQzH+inQppQqUUpdPNLGEsgI4aSShg7SYoy9f2fGh1PtRT0y7+2vZl56DKumJ7F0cjw7Spto7uxme0kTFk1vIJOTGEFUaDA7S5v73b+k3lbgb3dZM7vLmjha287MtOh+28RHhpKdYPu2awwxcM7sFLYca6Cy2cTdl87j1KmJ5CRFsiArlvf3V8usJjFuT20u5pENzs2QO1rbzpyM2H7Bt3AZi6PEiv1n/QjbO07CaN8EHgCuANYB8cBzSqlhl/GWQEYIJ5U2dJAeeyKQyYoPp7bVO3JkrFbNkepWcu1JjstyEtAaNhXWce9bB4gMCWbpZFvSrlKK6anR7C5r6rePkj4zmf6y4SgAM9OGr8Vx4+lTWJQdxyu3nNavANlVS7Mpru9gd1nz0Hf2MZLHN/HaTBZ+/c5B3tpTxYbDtcNu22WxUtrQzlypH+MpRfZLxxoQjrpzRfa1Gp3qJtNa36W1/rfW+nHgfSAKWxmYIUkgI4QTOros1LV1kTYgkKlpMWP1gloy5U2ddHT1MDnRFshMS4kiKSqM9Z8c5VBVC3dcMLNfXY3pqVEcrGrtN1W6yB7InDs7ldLGTpSC6SnDJ00uyo7jl5fNY3pq/56bNQsziAozcO9bB1zWK1Pe1MktzxSw9djIM67E2HhbsPbW3krau3qICw/hV28ewNJjHXLbfRXNWKxIIOM5bwM1wC1KqVuAG4BiYAPQCWx3bKiUugb4sv3POUqpG5VS6Uqpi5RSz9pXCrgTW95NLSeCpEFJICMCktaaB945yKcjfMtzqGq29bz0C2Tiwum2amrbTh5emugPhMPVtgrCkxNtib5BQYqzZiZj0XD3mrkszUnot/30lCh6rJpjtSd6YUrqOogLD+Gm03N7t4kMG1uV7tjwEK4/LYcvihr40EXVgF/dXkZpYye3Pb+TFkkk9ntmSw+v7Sxn9cxkblk9lSM1bTzx2TGuXb+VG5/KP2ndsA8P1BCsYOVUWWPJE7TWJmz15tqAh7AFNVdprQcrLPUAcLv997OAx4GZQAmQDvwaW55MPvBlrXXXcMeWtQREQDre0MFnR+roev8wP3Nie0cgkx4T3ntdVrxt2La0oQNPj8gfrrZNO3XkrwDceeEscnQV3zg1h4KC/r0YM1KjgUaOVJ9YQqG4vp2MOCOn5CYwIyWKs2elAiMXzhvKl+akUtBu5u+bdrLu8mHfh5zyxu5K0mON1Leb+dNHFaxeuXzc+xSeZemxcvu/dnJnWAbJA277YH81TZ0WbjlzKsENRXza0MUbnxeSNiWeqhYTHxyo6R27ANuaYLPTYyTR14O01p8C8we5Xg34O2eY3Zw12uNKj4wISHvtC8vtLG2is3vkSrRVLSf3yEyzD7scGeUijO5wuLqV9FgjUX16UJKiwlgxxLfTxKgwUmPCentywBbIpMeGo5Tit1cv5K4LZ42rTUFBil9dMZ82k4VHPz06rn0dr2/nYFUraxak89/nz2LLsQbe2lM1rn0Kz6toMnGwqo1nth4/6bYPD9YwPSWKU3ITUErxp68u5qdfns3W/z2HpMhQXtt5ohhjZVMnh6pbWTE1cSKbL7yEBDIiIO2raMagIMwQRH17Fxp4f18Vnw+Rf1HZbCI2PIQo44lAITMuHKMhqF8w4CmHq1vtvSzOW5AV17sStqnbQnWLmYw4W6Dmqlkfs9JiWDElkRe2lY5r6YJPj9QRpGDl9CRuWJVLclQoL28vG/mOwqs58rK2HqunzXRiqMhs6eFYbRsLsk7MQEqPDWfFlETCDMGsmp7EJ4dreu/zub2UwIpcCWQCkdcFMt6WbCb8076KFrITI7l4QQZNHd0U17Xz0EeFPPjuod5t3tlbxb/ySwHb0NLkxP4zAIOCFNkJER4PZHqsmsKaNmakjq6a6aLsOMqaTDR3dp8YOosNH+Feo/flBek0dXQ7nY80kNaajYW1LM9NJCEyjKAgxRnTk/n0cK3kyvg4x0w5i1WTX9LQe/2BylYsVoYMzs+Ynkx3j2bzUVvxxq3HGpiVFt2vx1QEDq8LZIRwN601+yqamZocyVeXT0JrTXWLiaTIUPaUN/fOjHjs06M8vbWE6hYTlc2m3gq3fU1OjOjNT/GUqhYTZot1DD0ysQDsKm2ioskWyGS4IZCZnxnLjNQo3thdOaYZTAerWilrNHHJwoze606fkYzFqp1aM0p4r+K6DoyGIJKiwthadCKQcZQGGCo4n54axeTECD46WMPmwjr2V7bwpTmpE9Fk4YUCKpCR3h4B0NDeRV1bF1OSIlkyKY74iFAmJUbwzVW5mC1Wius7MHX3sLe8GauGlwrKqG0dPJCZlBBBbavZoz0DJfay7KMNZJZMiiciJJiXt5dR4ZiVFef6b7RKKb5xag5Ha9vZfrxp1Pd3fKitmnYi32dqciRTkiP55LBUD/ZlxfXtpMUaOXd2CtuLG3uHH3eWNhEfEUJSVNig91NKsWZhBnsrWvjqE58TGhzUL9AVgSWgAhkhAI46FpZLiUIpRVZ8OBmx4cy0BwKHq1s5Ut1Kd4/GaAjibxuL6NGcNLQE9AY3x+vHPrtnvI432CryTh/l0FJkmIEvzU3lzd2V7C1vIjEytF+ysCtdvjiT8JAgXioYfV5LUV0HIUGKzPgTvUVKKS5ZYPsgcwyLCd9TXN9OZlw4X5qbSkd3D1uP2XpldpU2MWPA8hgD3bAqlxtW5vC365fyxH8tPamWkQgcEsiIgHOsth2lIHfAwnKpMWEkRoZyuLqVA1W2vJerl2VT326bOjwp4eSF6BzBTUljp5tbfbLj9e28tquCHccbyU4IJyJ09EHIxQsysGpNfknToIGaq0SGGViQFdub0zAaRXVtpMUaCQ7q/6G2ZlEGWsO7+2T2ki+y9Fjt1bLDOW1qEuEhQbyYX0qb2cLR2vYRc77iIkK5fEkWZ89KJS5CplwHMglkRMA5WttGTmLkSR/8SikWZsdxuKqV/RXNzEiN4qJ56YQabC+TwT7ok6LCiA4zUDrBPTJaa372n718/7kd7KtsZcmk+DHtJy3WyPlz0wDIcfOKwQuy4iip76C6ZXQ9KEV1tm/tA01NjiIqzNA782qsvKEy80j2ljfz63cODlvZ1tfUtXXR3aPJiDNiDAlmzcIM3txdyVt7KoHRD5WKwCWBjAg4toXlBi9jvjArjtKmTvZVtJA3OYEoo4Hz5qRiNASRGnNy/oht3aIoiu0LLk6U2lYz9e3dfP/saTxx3VJ+e9XCMe/rRnsl39xE9wYyC7PiANhd2uT0fXqsmuL6jkEDGYC0mDBKG8f+v99d1sTV67d4/Urdr++u4NMjdZQ0TOzzzJ0qmmy9mI71y67MyyIpKpRntpYAMD1FAhnhHAlkREBp7uimptU85HosiybFoTV0dltZlmPr5bhnzVx+cdnck4Y2HGakRo/rw3Qs9lXaCvqtnJZEWpwRQ/DYX8pLJsVz14Wz+OrySa5q3qAmJ0aQFBXGrgGLVQ6nttVMl8VKxhCBTEq0kdJxfLi/s7cKU7eVHzy/k6om7821OWKfGTeex+ptKpttgYzj3EaEGvjheTOwatuwb9+aTUIMRwIZEVAO19hyX2alDf5tb6F9SjLYVpAG2/DR7PTYQbcHmJ4aTXOnhbpB1lxylwP2QGa2CxbIU0qxaloSiUPMEHEVpRSnTU1kV1mz09OwHd/aM4eYTZUaG0ZZY+eYF6bcWFhHVrwRrTX3vn0AkxNVnj3hkD1ny58CmYomE+EhwST0WVLgmqXZTE+J4swZAxcsEGJoEsiIgOLIp5iWPHggExcRSmackcTIELLinaup4pjt5PiwmQj7K1pIjQ4jps+K1r5g5bREGju6nc5rcQQyGUOci9QYI2aLlcaO4ddy0lqflF/S0tnNnvJmzpiezB/WLqKorp3nvji5VL6ntZstlNv/D6UeSCp3l8rmTiYnRvSbmWQIDuK3Vy3k7jVzPdgy4WskkBEBpbCmjdDg/lN5B1q7LJuvr5jsdJn+eZm2XpEdxxtd0kZn7K9sOWnWlS84zb7206ZC52YvlTd1EhVmIH6IWSmpMbZepOqW4XvDfvf+YdY9XdCvx2V3eTNaw+JJcZw9K5UZKVE898XxMffuuEvfYUu/6pFp7iRnkLysoCGGcIUYigQyIqAU1rSRFR8xZL4LwFmzUjlvTprT+4yLCCUnMYLP+1QmdSdTt4WiunafDGSyEyJIjzXywYGTk2vNlh6aBvSslDd1kpMUMWRQmRptG3IabiZUR5eFJzcVU9Nq7rfQ4M7jTUSHGXqTSi+Yl8bh6rbeYTtvUVJnC16y4o29NYN8XY9VU9VscvtMOREYJJARAaWwpo1sJ4eMRmNeRgwFJY0TMj22uL4DrWFKsm9+CJw9M4WNhXUnJdf+/v0jfPvpgn4F7iqaTOQmDV1PJMU+k6ymdegemff3V9NqthAfEcITG4/19rjsLG1kxdTE3kTp06cnERVm4B0vq0tT0tBOeEgwC7LifL5HRmvNtuJ6Ln9kExYrQ84eFGI0JJARAcPUbcs1yB5kqYHxmpcZR0dXD0dr3V9Pptj+DX24D3hvdt7cVIKDFO/s7x8w7C1vpq2rh/97bS9g66GpaTUN2/NkDAkmKSqU6iGq+/ZYNa/vqmDp5Hj+67QcDle3sbO0ieK6dqpazP2WPQgPNXDpogw2HqmjucN7FqM83tDJjNQo0mOMtJgs/VaJ9iXVLSa+9eQ27nn9AI0dXXz/7GlcPD/d080SfkACGREwyhptH3ZZbghk5mTYhif2lje7fN8DHatrIzrM0Jsf4muSosI4e1YKH+yvottyogfraG0bESHBvLuvms2FdZQ2dGDVMGWE4Yes+AiqWwcPZN7fX0VVi5kbVuVyxvQkkqLCeGTDUS57ZBPBipNmx3x1+SS6ejS/fveg1+TKlNS3MyM1ureOUdUoCwp6g2O1bdz67HY+L2rgxtNz+ejHq/nS3DTJhxEuIYGMCBhl9m55dwwtJUSGMSU5kr0V7g9kiuramZ0e43Qysjf66imTaOq09OYVdXRZqGw2cfniTOakx9iSc/9hW+R1pFygrPjwQZN9y5s6+fl/9pEea+RLc9MINQRz0+m5VLeYWJGbyP1XLjgpR2NuRixXLM7kn58f5987yl30aMeuob2Lxo5uZqZF9w6jjbYysjfYWFiHqdvKq99ZyWWLMgkZR90jIQaSZ5MIGKWNHQQHKTJiXR/IACzPTWB/RQs9bix539zZTdEwlYl9xRkzkkmJDuODA7bhpQp7b9nkxAge+doSVs9MIT3OyKLsWGYOUfPHITshgtpWU7//e1WziZ+8ugeLVfPTL8/uTe5ed8YUnrtpBY9el8fs9MH/h9eflsNF89P466Zifvf+YY8O5Ryutk3pn5EaTZq9Au5YF8k8WNXC/gkItAdTWNNGZEjwiOsnCTEWUjpRBIzShk4mJyQSYnBP/L48N5Enu3rcOuvlsU+OYrJY+UpeFuaqQrcdx92CgxRLJsfz2aFarFZNWZNjZk44OUmRfPfsaeTl5VFQEIIxJHjYfWXHR2CxnhhysVo19799AFO3lRduWE5n5ZHebZVSRI6wwndQkOJ3Vy+itugAf/zwCEH1x/hzzCRSx/mYx8IRyMxMi6as1UBseAjVrWNbW+qe1/aza+dBvn7xWa5solOOVLeRlRDu072IwntJj4wIGKWNHUxNcd83wmW5tkrA291UT6auzczfNhWxekYS8zKHrjTsK2anRdPe3cORmjbK7L1ljl6H0XAULnTM6HljTyWFte3cfEbumHuujCHB3HXhbN7+wemkRhv5zbuHPJIzs/FIHYmRIaRE2/KhshPCx9Qjo7Vmf2ULjR3dHKqeuMKNDoW1bW5JshcCJJARAaK7x0plUyfT3RjIZMQaiQgJHvdqzEN5dutxrFb4+ooct+x/os2yD+0UlDRS1mgiOz6cUMPwvS+DcXxAljV20m2x8pt3D5GbFMmZM1LG3cbZ6TFctiSTY3Xt7KuY2PoybSYLGw7Vcvr05N6ejEkJEdT0yZHp7rHSahp5hlVFs4nmTtt2G484V4zQVdpMFmpbzWTHSyAj3EMCGeGXTN09bC6so7iunTaThd+/fxiLhmluDGSUslUMPuaGKdg1rSY+OFjN11dMHlOvhTfKiDUSG25g+/FGyho7mJo8tnOTEWdEKXhtVwVPbDzG8YYO/uvUyS6bEbNqWiJRYQbe2+98fRlX5EltPlpHV4+138yq7PgIqlvMPPrJUa7/+xfM+OnbXPv453w8wurdB+xBmCEIPpvgQKa00fZ6yE5wT26aEE4FMkqpz5VSrUqpDqVUvlLqDHc3TIjxeGTDUX719kFW/2YD1z6xlUc2HGVFbgIXzHO+Yu9YZMYZKapzfSDz6eE6rBquzMt0+b49RSnFrLRo8osbqGjqHPOwX5ghmGWT49l4pJY391Rx6pRE8ibHu6ydxhADaxZlsKmwjhYnej/e2VvJNeu3cGScQzifHK4lNymyX/CdnRBBt1Vz/9sHyY6P4PtnTyckSLH1WP2w+3LkbZ05I4XPi+rpsrhnccxWU/dJhQ5LG2zrQ02K980CjsL7Odsjsxn4PvALYBHwhLsaJMR4mS09PLO1hEXZcfzq8vlcuTiLt39wOj+9eA4Roe7Nb8+Kj6C8qdPlqyhvOFRDfEQIc4aYaeOrZqbFUFzfQVePHrFezHB+fslcDvziAh79+hIe/6+lLk8qvWZpNmaL7rfEwWCsVs1v3zuMqdvKb947NObjVbeY2F3ezJqFGf0eyzmzU1g9I4lnb1zOLy6bxw/Pm8HkxMgR6xcdqGphUkIEp05NxNRt5aCbFji9/+2D3P7Szn75RMcbOggzBJHso3WPhPdzNpD5EfA68CFgBtxfh12IMfrkUC0N7V1cvTSLry6fxPUrc4acautqjsUoHas2j1VzRzd//riQujYzPVbNZ0fqyJsc73ezPmb3mVo93kTsMEMwWfERRI0wK2ksFmTFkhVv5IMD1cNut/lYPUdq2piZGsW7+6rHvCL667sq0BrWLMrod316bDi3nz+L0/pUJJ6WEsXe8pZhk5EPVLYyOz2a+ZmxBAcpdhxvIr+4gfxi164PtqmwjqZOW00gB8ew4XDrmwkxHs4GMrFALfA50AXcOHADpdQ6+7BTvsXimyW0he/TWvOfneXMTo9hvgdm9mTG2QKZ8nEGMp8eqeWdvVX8/v3DHK5upbmz26XDJd5ieuqJD7ix5shMBKUUU5OiOFo7dCK31poXtpUyJSmSe9bMIzEylKe3Fo/6WJYeK09uLmZWWpRT/5NpKVE0d3ZT3Tz4elOmbgvF9bYiipFhBhZnx/GvgjK+8ugW7n59P8eGeUyjUd9mprjeNnOs78yo0oZOt+amCeFsINMGfAnb8JIR+H8DN9Bar9daL9VaLzUYpDyN8IxNhfWUNHRyw6pcj/ReZDgCmcbxBTKOD8znt5Xy+q4KghQsyo4bb/O8jjHEwJz0GGKMBhIiQz3dnGFlxodT1tiJdYiej48O1lBU1853zppGlNHAd86axs7SZp79/PiojvPJ4VrKGju5emm2U9tPtS8eWlg3eEDiWGTUMSx54+lTWDUtkV9dPh9DEDy9tWRU7RtK31ldh+09UR1dFqpbzRLICLdyKpDRWlu01u9rrf8EfAGcpZRKGul+Qky013aVExkazCULPbMYnTEkmMy4cMoax7dKcWFNG3HhBoyGID49UsfiSfFEG0Nc1Ervsu6MKVyVl+XpZowoKz4CrcHUPfjI+lNbSkiKDOVS+3DQdSsms3RyHD/59x42HBx+VlGb2UKrqZseq+ZfBaXMTo9hWU6CU+2anBhBSLA6adq/1arRWvcmnzuGVy+Yl8ZdF87mq8snsWpaEi/ll9HZNf5e9H0VzUSGBhMXHtLbI+OYwefOsgdCjBjIKKXOV0r9VSl1g1LqbuA0oBoYPk1eiAmmtebjQ7UsnhxP2BjqkbjKlORIypvGtx7O0dp2pqVEcdMZU4CTFzf0J5cszODyJb4QyNh62zoHSeSuajbx2ZFazpuT2ruOUKghiP+5aDYrchP5/QeH2VXaNOh+G9u7+MFzO1h27wdc//cvKGs08d2zpjndoxhqCGZGajRHBwQyd7y0izMf3MD7+6qJNhp629/Xlxdk0Gq28PGhWqeONZx95S3k5SSQmxTZW5HYkSMkPTLCnZzpkWkAlgN/Bm4DNgKXaG9ZGlYIu6O17dS2mlnq4VySKUmRlDd2jrkSrNWqOVbbRlZ8BDedPoVLFqQ7Pcwg3McxbNjZdXIg897+KhTwpbn9FzIIMwTz6HV5ALy//+REYatV88MXd9LQ3sUFc9PYVtxATkLEqMsEzMuIpbC2rfc519zZzaHqNlpM3RyuaWNeRuyggdGstGjmZcbw5u6KcVUubmzvorihg+W5CUxOjOBIdRs9Vs2nR2qJCzcwxYvzn4TvGzGZRWu9DZg3AW0RYlwKShqAUPImeTiQSY6io7uH2tbBky9HUtNqxmyxkh0fQWSYgZvPnEparBHPr8Uc2BzDhqbunn7vnN09Vt7fX81ZpywjOfrk74ax4SFMTY7ii6IGzkrqnwf0Yn4pG0pCuemMKfxs7WLazBZ2bC8Y9QyfeVmx/MNk6U0y32efjv3Q2sWUHQnhjFMXDHo/pRTXnjKJ2wu2D5vIPJJt9tlPp+Qm0FoWgbnKSnljBx8f7GRpToLMWBJuJZV9hd/IL2lkQVYs8R5OGp1iT748OsYKv478miyphOp1piRHnjS09MH+aho7uvnq8klD3m9uZgw7S5sw9ylEZ7b08FJBGRfOS+NCew9MVJhhTLWOHDP0HPVk9tgvF2TGMistZth1jpbnJgKw/XjTqI/r8EVRAyHBigVZsUxOsD3/39pTSYvJwvJc53J9hBgrCWSEX2hs7+JQVSurZ45/fZ3xcnSjHxtiFslIHIGMrE3jfaYmR9HZ3YNjEMZq1Ty8oZC0mLBhn3tzM2Lp6rFypE9dmfziRkwWK1ctzRr3DLtZadGEGRRbj9l6RvaUN5MSHeZUUD8lKZKo0GB2jGOx0wNVLeQmRhJmCGZSoi0Af29/NWGGIBZPihvzfoVwhgQywi98eqQWq4azZno+KTY9xoghyLaI4ViUNXaSEBlKTLh/zlLyZVNTorBaNZYe28ylzcfq2VvewrWnTBp2+GSufRXuvX2mKG84VENIkGLFlMRxt8sYEszCrDg+OFCN1pq95c1MczIvJShIMTMtmh3j6JEpbegk1b4GmDHEwKSECLp6NKumJWEMkXIcwr0kkBF+YcOhWmLDDSzIivN0UwgKUkQbQ2jq6BrT/UsbOpz+EBITa6p9GQWzxYqlx8ozW4uZnhI1Yk9gtDGEWWnR/WqtfHK4lrmZsS5bNuOU3ETKGjvZX9lCcX0H01Kdfw7NTIvmUHUr7ebRT8PusWoqmjpJjTmxmOmMVFvF5nPnpA51NyFcRgIZ4fN6rJpPDteyZFK81yQVxhpDaGgfWyBT1tTJ1BRZYM8bOZZRMFmsPPfFccoaTfz4SzOdet4ty0ngQFULlh4rta0mDle3kefCYZdTcmxJ7s9/UWpr6yiC4VlpMWgNR2pGPxxa12bGYtWk9Qlk5mTEEKTgnFmeH+oV/k8CGeHzjtS00tDexVInC4hNhCijgcaOkVdKHqihvYvmTotXl+sPZCnRYQQFKerbzPz8tX0szIrl/LnO9TqckpuAqdvKvooWtpc0AbDEhaUCEqLCWJAVyw57vZrR1G5x9KAcqmoZYcuT1bTYaial9lkU8sbTc/n1VxaQ0ie4EcJdZPBS+Lz84kaCVBhLvCipMDY8hMYx9Mg4psBOTYmCtrEnXwr3UEoRHhJMl8nKJQsyWDsl2elE3eVTEjAEwa3PbkfXVpKemMukYWYTjcU5s1LZlm9b8yt2FDlWUUYD01OiOFg1+uUKqnsDmRNBS4wxhFlp/rVSu/Be0iMjfF5BSSNLvKyEf7QxZEw9Mo4F/CRHxntlxUeQERfOQ2sXjaqCdEq0kXsunUdEaDDH6to5c4bzQZCzzpltG8qZlzn6IGLxpDgOVbWOujBeVYsZpSA5KmzkjYVfU0qtVErtVkqZlVLblVJLhtjuJaVUo1JKK6X+POC2y5RShUopk1Jqg1Iqd6TjSiAjfFptq5kjNW2c5WVj8THhBpo6uhhtrdRjde2EBKneKrLC+8RHhJAYGTqmIGRhVhxvff907rpgFj86b4bL2zY3I4aVUxO5bFHmqO+7eFI8LSZLv4RkZ9S0mEiPMRJikI+TQKaUMgIvA9HAD4FU4CWl1GDRvhl4dZB9pAHPAy3AHUAe8NRIx5ZnnvBpnxy2rRGz2gumXfcVYzRgsWp6rKMLZYpq20mPNXpN0rJwPUNwEKumJ7klf0Qpxf9cNJsL549+0dQL5qYRbTTwizf2owENFFa39SviN5jqFhNZLh4iEz7pQmzByyNa60eAvwK5wOqBG2qtvwb8Y5B9XAuEAffZF6l+FThdKTV1uANLICN82pu7K0iMDGFOuneNxzuGuUYbyBTXt0tvjPCI+MhQrlsxmc+LGmju6KK4rp3bXtzJ2vVbqW8bermN6hazFG8MDAalVH6fn3UDbncMATlWUymzX04ZxTHGtA9J9hU+q7CmjY8PtXHVvHSX5xqMV0y4AegeVSDTY9UU13fwpWQJZIRnnD83jc9bOylt7CQyFFZNT2JfVSu37T3GKzNPXnKvy9JDfUcX2QnhQOvJOxT+xKK1XjqK7R1vyuNZYNqpfUiPjPAJzZ3dvLuvihe2HWfz0ToAXtxWSrTRwMULMzzcupM5emQsowhkalvNdFmspEuPjPCQ4CDFLy+bjyFIkZMUyV0XzOLV76xEa83P/73vpETgmlYzWstyGgKAIvtllv3SkahVpJQyKqWcWQRvyH0MdyfpkRFez9Tdww+e20FrdD3mquP8q+RzzklqY/Oxeu746jKiwsa+aq+7xPQOLVmdvk9ls21Jg8w4qb0hPGdRdhyW9BjSom0rrs9Mi2btKZP4+6EGCpJDWdrnO3l1i23IKSs+HKRaQKB7G6gBblFKtQI3AMXABsAC7APmASilrgEcz6Q5SqkbgTexJfreD9yplEoFLgc2aq2PDndg6ZERXu+jgzXUtXfx668s4JkbTuGyRZm8uaeK8JAgvrVqxJl5HnEikHH+PuVNjkBGemSEZw0cqD1/ThrZCeH8Y0sJ1j69jI4aMsOtri0Cg9baBFwFtAEPYQtqrtJaD5Yt/gBwu/33s4DHgZla60psCb9xwG+AHcD1Ix1bemSE13tlexkJESFcuSSLnTtq+N3VC0ntKicy1EBchDO9lRMvIjSY4CCFZRQ9MuWNnUSGxji1YrEQEynEEMSPzpvBdx7aw1t7K3HMiapuMWEIshXDq/RoC4U30Fp/Cswf5Ho14O+cYfbxCvDKaI4rPTLCqzV1dLHhUC1nzUzpnZKslOK8OWmcNi3Jw60bWlCQIi48ZFQ5MpXNneQkRXpd4rIQAGsWZpIWY+SFbaW911W3mEmJlnIBwrMkkBFe7dPDtVis2usK3jkjPjJ0VLOWyptM5CTJYpHCOwUHKVZOTWTL0XraTBasVs3h6lb7jCUhPEcCGeHVPjpYy7zMGJ/8gI+PCHE6kOmyWKluMTHFBx+nCBwrpiZisWryixvYWFhHTauZ1TN970uG8C+SIyO81tHaNgpr2/jlpVlAg6ebM2rxEc73yJQ2dmDVkJMYiS1XTgjvMzM1mpToHrYcq+Iox4kxGlie6z2rzovAJD0ywmu9sasSpeDiBaMvt+4N4iNCsTg5bamoth2A3GTpkRHeKyhI8aW5qeSXNPD+/mrOnpVC6CgWzhTCHSSQEV5Ja83ruyuYmx5DqhvWpJkI8ZGh9Gjnylo6FuqToSXh7c6fm4bZounu0XxpTqqnmyOEBDLC/e57+wAPvnNwVPcpqW+nsKaN02d412KQoxEfEYLWul/djaG8vbeSOenRXjudXAiHFVMSiQozkDc5nkmJEngLz5NARrhVm9nCU5uL2VRYR0eXxen7fXakjiAFK6cmurF17uWoB9M9QiBzvL6dg1WtnO7F08mFcAgJDuLuNXP43dULPd0UIQAJZISbfXakFlO3FYuG7SVNTt1Ha82nR+pYOS3Jp3so4u1tHyxPZsfxRj7YXwXAp0fqUApWSiAjfMSstBgmS2+M8BISyAiX69v/8P6+anKTIglS8EVRvVP331veQmWzyWeTfB0SIgdfONJs6eHWf27nDx8W8twXx9lYWMvy3AQSosI80UwhhPBpEsgIl3lnbxVfe2Ir+ypa2FfRwpajdRyuaeO6FZOZmhzF50XOTaF+Y3cFBmVLKvRlcUP0yLy9p5KKZhM5iRH85NU9lDWauHiB963gLYQQvkACGeESnV09PLKhkNKGTuIiQujosnDvWwcJCVJcvjiTuRkx7ChtwmwZbP2wE7TWvLG7ksWT4316WAkgwd7+7p4TPTItpm5eyC/j9OlJ3H/lAqYkR2FQcOE83w7ahBDCUySQES5xsKoFq4affHk2WXHhLMiKY3luPGsWZRAfGcq8zFi6LFaOVA9f7O1gVSvlTZ2cPt3380Viwh1DSyd6ZP704RFaTRbuvGAWUWEGXli3gl9/ZSGJMqwkhBBjIoGMcAlHHZS5GTEAhBmC+NnFc/nmytze65WCveXNgK3n5aOD1Ty1uZg284nZTJ8dqSXUEMTyXN+dreQQHKQIDlI0dXRT32bmic+O8fhnRZw/J5V5mbEAJEaFMSMt2sMtFUII3yVLFAiX2F/ZQlSYgcy4cKoHuT3aGMLM1Gg+O3KQe9/czxsf7aAypBpzVRlF67dy26JgzJYeNh6p46xTpxAZ5h+r6WbEGuns6OGWZ7bTk5jLhfPSuH6GrE0jhBCuMmKPjFJqulLqY6VUvVKqVSn1vlJq6kQ0TviOfRUtTEmKRKmhA5CzZ6VQ0tDJU1tKCA5S/Paqhfz0olkcqWnlO//czvy736Oho5vLFmVOYMvdKy4ilPlZseQkRbBmYQZ/vHYxhmDpCBVCCFdxpkcmE1vA83/ADOB7wBPAWW5sl/Ahlh4rBytbOHuEdYLuOH8my6ObOeO0U9i+fTt5eVkUUM2K5VP45ZN1LF06mSSTgQvnp1NQUDFBrXe/8JBgfv2VheTlLfZ0U4QQwu84E8hs1lqf6fhDKfU1YK77miR8TUVTJ2aLlSkjBDJKKaKMhpN6bfImx/PTi+eQlzeHgoJOdzZVCCGEnxmxj1tr3eX4XSm1FEgAPh24nVJqnVIqXymVb7E4X4pe+L5j9pWbZcFDIYQQE83pwXql1EzgP0AxtuGlfrTW67XWS7XWSw0GySEOJMfq2gk1BJEVH+HppgghhAgwTgUySqk5wCeABThba13p1lYJn3Ksro2ZqdGSxCqEEGLCOTNrKRvYACQBfwGWK6XWurldwkdorTlW295bP0YIIYSYSM6MAU0Fku2/39fn+udd3xzha97cU0mLycIpuQmgB6sgI4QQQriPM8m+G7TWauDPRDROeLeOLgu/eGM/05IjudSPar8IIYTwHZLUIMbs2c+PU9Nq5turpxIcJLGtEEKIiSeBjHBKj1VzsKoFrW0rORfWtPL6rgrWLpvErDTJjxFCCOEZEsgIp7y2q5zb/7WbfxWUAXD/24cwGoK54/yZHm6ZEEKIQCaBjHDKp4frAPjF6/v55HAtHxyo5sqlWSREhnq4ZUIIIQKZBDJiRFprNhbWMTc9mh6tefDdQ6REh7FmYbqnmyaEECLASSAjRlTa0EFtq5lzZqfyPxfOAuBH583AGCIVnIUQQniWfBKJEe0sbQKCWZAVx0UrJhPTvoQ1y7LZvr3W000TQggR4KRHRoxoV1kzkxMjSIs1opQiKz7ipBWshRBCCE+QQEYMy9JjZU9ZMyunJXm6KUIIIcRJJJAJMK/tLGdvebPT2+8qa6aju4eVUyWQEUII4X0kkAkgta1m1n9WxPee24HZ0uPUfV7fVYFBwWlTE93cOiGEEGL0JJAJIF8UNQBQVNfOKwXlI27f3NnN89uOs3pWCvFSL0YIIYQXkkAmgGw9Vo8xJIgL56XxYkEpJfXtw27/xq4KTN1WrlwiC0IKIYTwThLI+LnKps7e9ZE+L6pndloMd6+ZS0hQEL9888CQ9+vosvDGnkrOnZ1KdkLkRDVXCCGEGBUJZPzYP7YUc9PTBTy5uZjmzm4OV7cxPyuW1BgjV+Zl8v7+ag5WtQx634c/LqTVZOGW1VMnuNVCCCGE8ySQ8VNbj9Vz92v7MChbULK9xJYfMz/TtlL1moUZJEWF8tTmYrTWaK3psdp6bl7bWc7DHx/l3Nkp5E2O99hjEEII4TuUUiuVUruVUmal1Hal1JIhtrtMKVWolDIppTYopXL73KYH/Px7pONKIOOHjtW28eC7B5mfFcfPL5lLXVsXT2wswhgSxLTkaADCQw187+zp7Clv4c6Xd7Py/o/4yl82c97vPmH9Z0WcPzeV7541zcOPRAghhC9QShmBl4Fo4IdAKvCSUip4wHZpwPNAC3AHkAc8NWB3LwPX2n9+M9KxJZDxQ+s/PYbW8Ph1eSyZHM/p05No7rSQNzmeEMOJU37tKZNIizHyr4IypqVGs2ZhBpMSIrhgbhp/vHYxhmB5egghhHDKhdiCl0e01o8AfwVygdUDtrsWCAPu01r/CXgVOF0p1TePYT/wutb6ea31xpEOLGst+ZnG9i5e2VHD2bNTSYkxUgrcdu4MPvhsK6dNTQJOFMMLNQTx4FcWMHfhItJjwykoCCYvL4+CgiDCDMFDHkMIIUTAMSil8vv8vV5rvb7P347hIUdtjzL75RTgQye3O2r//afAz5RSx4FbtdZvDNsw59ovfMWbeyrpsoRx2aKM3uvyJsfz6yvnc+XKHA7s2dVv+/jIUNJjwye6mUIIIXyLRWu9dBTbOxbk06Pc7gFgK5AM/BZ4TimVqrXuGGoHEsj4uB6r5j87y3n1wyOc0ZnAW3sqOffU5WTF91/UcU5GLBGhcrqFEEK4RZH9Mst+6ShAVmTPn7FqrbuG2w5Aa32XY4dKqQuAK4Bs4NBQB5ZPNh9l6bHyYn4pv/5nAXXGLFR9LRsa9mM2WVh3xhRoKBp5J0IIIYRrvA3UALcopVqBG4BiYANgAfYB87Al+t4P3KmUSgUuBzZqrY8qpS4Cvm6/Tzy2vJtaTgQ/g5JAxkMsPVY2F9aRO6vrpNsa2s1091iHvO+GQzX84OkCmiOzyQoJ5tGvLyGxM5VJM+fxyeYoTslNoEACGSGEEBNEa21SSl0FPAw8hC1wuUlr3aOU6rtdpVLqWuBBbDOSPge+ab+5BEgHfg0EA/nAj+09OUOSQMZDnvviOL96+yB/2mMlL6KBs9vjqSmq4nc7tvLRxm38uDORswZZcLqkvp2f/mc7MSFB/OH6ZUS3HWfpvHQKCipIjTEyNTlq4h+MEEKIgKe1/hSYP8j1asDfrwCvDLLdPuCs0R5X5td6gAae2FjElKRI1i7LJr+4kXvfOsCfPy6kqLadrHgjL+aX9haoc2gxdfOrtw4QGWbg/106j7NmpdA30hVCCCECjfTIeEBzZzcl9R38cFk2P7h0HmsyTcyYt5ANm2K5aPVpPPKShd/tMLOrtIlTlp24309e3Ut1s4lXbltCUL0MHQkhhBDSIzPBNFDXamZSQgSnTkkEQClFjDGEzLhwDMFBLMuJJ8Zo4KOD1b3323y0jtd3VXD1smyW5SR4qPVCCCGEd5FAZoK1mix0dvdw4+m5BAcNPiwUagjmkoUZbDlWT6upG0uPlf/3+n6y4sO5Mi9r0PsIIYQQgUiGliZYVbOJIKX4Sl4WB/bUD7ndlXlZ/O0/mnte3099yTEO1kXx6NeXEGaumMDWCnewWCwUFRVRVFRERESEyy4Bl+/T3fsG3NLesey7vLycBQsWeOZJIYQYMwlkJlBdm4nuji4SIkNHLE63ODuO2enRvFRQhrmqinNPX8H5c9PYvl0CGV9XXV3N1KlTycnJYfbs2XR0dLjkEnDZviZq34Bb2jvafc+aNYuKigrKysoGP2lCCK8lgcwEentPFWu1JiEydMRtlVI8+JWFzFu4iE83f86Zpy2TGUp+oquri8TEREpKSjzdFGGnlCI2NhaTyeTppgghRmnEHBml1B+VUtVKKa2UGnbhJjE0s6WHd/dVER8RSpjB+dSkMEMwCZFhhI7iPsL7SVDqfeScCOGbnP10fH60Oy4oaRjtXfzaG7sqaeq0kBpr9HRThBBCCL8xYiCjtf4+8PvR7LS7x8rXnvic6hbppgWwWjWPfnKUyQnhxIaHeLo5QlBRUYFSittuu427776bpUuXopRixYoVTJs2jVdeOVF0s7Ozk9tuu40LLriA0NBQrrjiCh555BEA/vKXv7B06VLuu+++3u1NJhNRUVFcdNFFaD3SwrdCCDE+LhuvUEqtU0rlK6XysVqx9Gj+9NERV+3ep31RVM+RmjauystGOq+Ft7rtttu488476ejo4Fe/+hU1NTUA3HzzzTz00EPMmzePP/7xj4SEhHDrrbfy2muvceWVVxIUFMRLL73Uu58tW7bQ3t7OeeedJ8M1Qgi3c1kgo7Ver7VeqrVeGhJiYO0p2Tz/RSlVTYHdK6O15sWCMrITwlk1fZDFk4TwEgsWLGD58uWkpaUBtmni5eXlPPPMM2RnZ/PAAw/w7W9/mwceeACA9evXk5KSQl5eHtu3b6e8vByADz/8EIDzzjvPMw9ECBFQ3DZr6XtnT+elgjKe/aKEL5+z0l2H8XqbCus5XN3Gg5dPxRBc5+nmCC9zz+v72LhlNwn5XTSUHBzXJUBDyUFWVRi5OGP0bfnWt77V+/ull15KRkYGR48eRWvNKaecQnBwMAA5OTkkJCRQVVVFa2sr5513Htu2bePDDz/kggsuYOPGjeTk5DBv3jyX/I+EEGI4zsxa+jJwjf3PbKXUjUqp6SPdLzXGyH+dlsPHh2vZcbxxvO30SfsqmvnOPwtIiQ7jK1KRV3i5n//85zz00EOceuqpvPXWWxw8eHDIbfvmvpx99tkYDAY+/PBD3n//fdra2rjqqqsmoslCCOFUj8wdwJn23xcAjwPfBEZMgPnuWdN49o0N3PXyHu45LXzsrfRBHx+q4af/3su02Qv48RnzMYYEe7pJwgv93yVzKcgwkZeXR0FB6LguAfvvcykoKBh1W+bPn09ubi4hISFs2bKFjz76iKlTpwKwbds2rFYrAMXFxTQ2NpKWlkZ0dDRxcXGcffbZvPfee/z+97Z5Addcc82QxxFCCFcaMZDRWq8e686jjSF8e/VUHixo5akt1bxeYeS5tzazaLGJKdRQbkinsbyZBYusYz2EV2o3W7jj7d1kxoXz0i2nUXRwj6ebJMSINm3axP79+3n11VcB2xBSamoq1113HU8//TT//d//zdq1a/nNb34DwLp163rve8011/Dee+/x4YcfkpmZaQ+wRh9MCSHEaLm9su+KKYl8uVvxynufEVUbybKcBDqtmn/mH+el46GYqwp5szKc78wb++wGb5vi+cK2Uurawrnv7OkkRIZS5OkGCeGEP/zhDyilSE9P55vf/CYXXXQRBQUFPProoyQkJPDMM8+wadMm0tPTefjhh1m+fHnvfS+//HJuvvlmLBaLJPkKISbUhCxRcO9l84hpLeXWq1dTfewAeXl5fLI5hPSpc3jhbc3TR5q448BxXpo136n99Q1c3tlbxffWb+X/WVOY4QWjN2WNHby2q5xrL1rNjDSLp5sjxKAyMjLQWlNQUEBeXh6XXHJJby/KwN6UiIgI/vCHP3DdddcNuU18fDxbt26VnhghxISbkLr3cRGhfGVpFlnxEb3XRYUZmJEazUXz0/nnTctpNlm4+rEtlDV2DLmfVlM333tuB9f//Qt2lTZR22rizpd309Vj5X9e2cNjnxyluK4dq3Viemi6e6w8s7WYv20swtRtYW95M/e/dZCw4GDuOH/WhLRBCCGECGResWjkspwE7rt8PvdtM3PXy3uYu2DRSdtsP97Irf/cjjkuhzAN1z6+lfiOMrojsnho7WJ2mRJ49OUPeO83GwiqP8aKnRbSuyuYOtu5Xp7RMlt6uOWZAt7cVsarpUZCm4rpSagnzNTNHRfMJDk6jONuObIQQgghHLwikAHISYrk+XWLueT/DvM/r+zhrj63mS093Pn8DkINQbxw60oqC+P47Q4Lu46389Ctc8kOquGyvLnMCanDmpjLB5+2Ud7RzYadpXTE7OHG2a5ta5fFyj2v7eewNZlbzpzCRWedygPPNDJ7/iTOSUokyug1/1YhhBDCr3nVJ+60lGiuXJLFM0cb6ezuIdw+ZfmVgnJKG0L5+TnTmZcZi7kqjBe/vYwX3+7iqqVZbN9uK6U+JTmKvLxJTAuqJS8vjx8/UsvLe6tYFR9Bngvb+dv3DrG7vJk/f+9ccqgmLyeBuy6cTV7ePMkPEEIIISbQhOTIjMZ5c9IwhgRR32arVFra0MG/Ckq5eEE6C7PiereLMYaweFL8sGu5XL44k6SoMJ7cWOyymU0FJY089ukxLpyXxpVS5E4IIYTwKK8LZKKMBi5fnElTZzedXT3c8s8CgoIUP/ny6MeHwkMN/ODc6eytbOGDAzVO3+/VHWXc9fJufvf+4X7Jx6UNHfz+/UPMSI3ixtNzR90eIYQQQriWVw0tOfzXaTls1ZrC2jZK6jq484KZpMeGUzGGfa1dls0fXzDyf//Zy31nRg27raXHyl83HuOtyipi28386aMjmCoL2dWZSF6kiR/99XMsVnj4q0toKTs8tgcnxAAHDhxwyaXjd0eVX1fZv38/L774Iunp6b37vv7663nqqafYtm3bqFe4vv322+no6OCRRx4Z9PYnn3ySb37zmzz44IOcddZZw+7r7rvv5o033uAf//jHSY97165dvP7668yYMaP3tquvvppdu3Zx6NChUbVZCOG9vK5HBmBWWgzRxhCMIcG89r1VLMtJHPO+QoKDuO3cGVS1mPjrZ8eoaTFxvKGDqpYTq3LXtJh44rNjrLjvI17dUcH1p+Ww/ro8tv7POVw8P42/bSri5qfzqW01c/eaOUxPjXbFwxTCK1gsw9c72r9/P/fcc0+//K9bbrmFe++9t3cJA2cVFhayYcMGbrrppiHbcuaZZ3LvvfdyySWXjGrfA+3evZt77rmHw4dPfOlYt24dhw8f5qOPPhrXvoUQ3sMrAxmAyYkRTE+JIjcpctz7mpUWw7fPnMr7B2o4+7ef0NzZTW2rmX0VzVitmm8/U8AbuytYMimOuy+Zw91r5mIIDiI1xsi3V0/j799cxoy0aJ74r6XMSotxwaMTwnOKi4tZunQpp512GrfccguZmZk0NjayePFiVq1aRVRUFDfeeCP79u2joqKidwHIxx9/HKUU+fn5/OUvf+EnP/kJR48e7b3tsssuIzIykm984xts3Lhx0GM/99xzAL1Byuuvv45Sirvuuou5c+dy11138cknn/CTn/yE119/HYCPPvqINWvWMHny5N7qw3fffXe//X788cdMmjSJiy66iM8++4z8/HweeughAO655x6UUlRUVLB69WoiIiJ44YUXXP5/FUJ4htcGMmNfsGBwPzh3OrPSopiTEcOU5CiClOLBdw/x4YFqth9v4tazprH+G0tZmpNw0n3PmpnCg19ZyGlTk1zcKiE8Z8uWLcyePZtf/OIXKKW44ooruP3227nrrrs4fPgwt912G/Hx8dx2222AbZXr5557jilTpvTbz7Zt21i3bh3x8fH87ne/o6qqijVr1tDU1HTSMTdu3EhaWhqpqan9rt+6dSs333wzF198cb/ru7q6+NrXvkZjYyO33347u3fvHvSx5Ofns27dOmpqarj77ruZMmUKF1xwAQBXXnklzz33HPHx8RgMBmbMmMFnn302xv+aEMLbeG0g42phhmAe/MpCXrz5VCJDg0mJDmPDoVoe++wYeZPjOWdW6sg7EcKPLF68mO9///usW7eO7u5u3nnnHX75y1/ys5/9jI6ODvbs2UN4eDgrV64EYOrUqaxdu5aEhP7B/qZNmwC4+eabufnmm7n00ktpbGxk7969Jx3z+PHj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
"
>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Neste gráfico a máxima variação permitida é de 5%. Isto significa que provavelmente irão ocorrer um número muito maior de rebalanceamentos (como é o caso). Devido à alta frequência de rebalanceamentos, serve como reajuste de risco da carteira, porém ao mesmo tempo limita os ganhos quando comparado à técnica de rebalanceamento anterior, o que leva um retorno total menor.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">order_dict</span> <span class="o">=</span> <span class="p">{}</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="mf">0.08</span><span class="p">,</span><span class="mi">9</span><span class="p">):</span> <span class="c1">#max_var</span>
    <span class="n">order_dict</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="p">{}</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="mi">11</span><span class="p">):</span> <span class="c1">#divisão do portfolio</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">portfolio_growth</span><span class="p">(</span><span class="n">i</span><span class="p">,</span> <span class="mi">100</span><span class="p">,</span> <span class="n">j</span><span class="p">)</span>
        <span class="n">order_dict</span><span class="p">[</span><span class="n">i</span><span class="p">][</span><span class="n">j</span><span class="p">]</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">:][</span><span class="s1">&#39;Total&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">values</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df_Table</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">order_dict</span><span class="p">)</span>

<span class="n">df_Table</span><span class="o">.</span><span class="n">index</span> <span class="o">=</span> <span class="n">df_Table</span><span class="o">.</span><span class="n">index</span><span class="o">.</span><span class="n">to_series</span><span class="p">()</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="nb">round</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="mi">2</span><span class="p">))</span>

<span class="n">df_Table</span> <span class="o">=</span> <span class="n">df_Table</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>

<span class="n">df_Table</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="p">[</span><span class="s2">&quot;background: red&quot;</span> <span class="k">if</span> <span class="n">v</span> <span class="o">&gt;=</span> <span class="n">x</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="k">else</span> <span class="s2">&quot;&quot;</span> <span class="k">for</span> <span class="n">v</span> <span class="ow">in</span> <span class="n">x</span><span class="p">],</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">


<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<style  type="text/css" >
#T_d38be_row0_col0,#T_d38be_row0_col1,#T_d38be_row0_col2,#T_d38be_row0_col3,#T_d38be_row0_col4,#T_d38be_row0_col5,#T_d38be_row0_col6,#T_d38be_row0_col7,#T_d38be_row0_col8,#T_d38be_row1_col0,#T_d38be_row1_col1,#T_d38be_row1_col2,#T_d38be_row1_col3,#T_d38be_row1_col4,#T_d38be_row1_col5,#T_d38be_row1_col6,#T_d38be_row2_col0,#T_d38be_row2_col1,#T_d38be_row2_col2,#T_d38be_row2_col3,#T_d38be_row2_col4,#T_d38be_row2_col5,#T_d38be_row2_col6,#T_d38be_row2_col7,#T_d38be_row3_col0,#T_d38be_row3_col1,#T_d38be_row3_col2,#T_d38be_row3_col3,#T_d38be_row3_col4,#T_d38be_row3_col5,#T_d38be_row3_col6,#T_d38be_row3_col7,#T_d38be_row3_col8,#T_d38be_row4_col0,#T_d38be_row4_col1,#T_d38be_row4_col2,#T_d38be_row4_col3,#T_d38be_row4_col4,#T_d38be_row4_col5,#T_d38be_row4_col6,#T_d38be_row4_col7,#T_d38be_row4_col8,#T_d38be_row5_col0,#T_d38be_row5_col1,#T_d38be_row5_col2,#T_d38be_row5_col3,#T_d38be_row5_col4,#T_d38be_row5_col5,#T_d38be_row5_col6,#T_d38be_row5_col7,#T_d38be_row5_col8,#T_d38be_row6_col0,#T_d38be_row6_col1,#T_d38be_row6_col3,#T_d38be_row6_col4,#T_d38be_row6_col5,#T_d38be_row6_col6,#T_d38be_row6_col7,#T_d38be_row6_col8,#T_d38be_row7_col0,#T_d38be_row7_col1,#T_d38be_row7_col2,#T_d38be_row7_col3,#T_d38be_row7_col4,#T_d38be_row7_col5,#T_d38be_row7_col6,#T_d38be_row7_col7,#T_d38be_row7_col8,#T_d38be_row8_col0,#T_d38be_row8_col1,#T_d38be_row8_col2,#T_d38be_row8_col3,#T_d38be_row8_col4,#T_d38be_row8_col5,#T_d38be_row8_col6,#T_d38be_row8_col7,#T_d38be_row8_col8,#T_d38be_row9_col0,#T_d38be_row9_col1,#T_d38be_row9_col2,#T_d38be_row9_col3,#T_d38be_row9_col4,#T_d38be_row9_col5,#T_d38be_row10_col0,#T_d38be_row10_col1,#T_d38be_row10_col2,#T_d38be_row10_col3,#T_d38be_row10_col4,#T_d38be_row10_col5,#T_d38be_row10_col6,#T_d38be_row10_col7,#T_d38be_row10_col8{
            background:  red;
        }</style><table id="T_d38be_" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >0.0</th>        <th class="col_heading level0 col1" >0.01</th>        <th class="col_heading level0 col2" >0.02</th>        <th class="col_heading level0 col3" >0.03</th>        <th class="col_heading level0 col4" >0.04</th>        <th class="col_heading level0 col5" >0.05</th>        <th class="col_heading level0 col6" >0.06</th>        <th class="col_heading level0 col7" >0.07</th>        <th class="col_heading level0 col8" >0.08</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_d38be_level0_row0" class="row_heading level0 row0" >0.0</th>
                        <td id="T_d38be_row0_col0" class="data row0 col0" >975.590000</td>
                        <td id="T_d38be_row0_col1" class="data row0 col1" >975.590000</td>
                        <td id="T_d38be_row0_col2" class="data row0 col2" >975.590000</td>
                        <td id="T_d38be_row0_col3" class="data row0 col3" >975.590000</td>
                        <td id="T_d38be_row0_col4" class="data row0 col4" >975.590000</td>
                        <td id="T_d38be_row0_col5" class="data row0 col5" >975.590000</td>
                        <td id="T_d38be_row0_col6" class="data row0 col6" >975.590000</td>
                        <td id="T_d38be_row0_col7" class="data row0 col7" >975.590000</td>
                        <td id="T_d38be_row0_col8" class="data row0 col8" >975.590000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row1" class="row_heading level0 row1" >0.1</th>
                        <td id="T_d38be_row1_col0" class="data row1 col0" >993.430000</td>
                        <td id="T_d38be_row1_col1" class="data row1 col1" >1000.350000</td>
                        <td id="T_d38be_row1_col2" class="data row1 col2" >1018.270000</td>
                        <td id="T_d38be_row1_col3" class="data row1 col3" >1038.710000</td>
                        <td id="T_d38be_row1_col4" class="data row1 col4" >1013.050000</td>
                        <td id="T_d38be_row1_col5" class="data row1 col5" >1023.390000</td>
                        <td id="T_d38be_row1_col6" class="data row1 col6" >1059.360000</td>
                        <td id="T_d38be_row1_col7" class="data row1 col7" >945.370000</td>
                        <td id="T_d38be_row1_col8" class="data row1 col8" >945.370000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row2" class="row_heading level0 row2" >0.2</th>
                        <td id="T_d38be_row2_col0" class="data row2 col0" >999.620000</td>
                        <td id="T_d38be_row2_col1" class="data row2 col1" >1006.640000</td>
                        <td id="T_d38be_row2_col2" class="data row2 col2" >1021.360000</td>
                        <td id="T_d38be_row2_col3" class="data row2 col3" >1024.900000</td>
                        <td id="T_d38be_row2_col4" class="data row2 col4" >1022.550000</td>
                        <td id="T_d38be_row2_col5" class="data row2 col5" >1001.550000</td>
                        <td id="T_d38be_row2_col6" class="data row2 col6" >1039.990000</td>
                        <td id="T_d38be_row2_col7" class="data row2 col7" >1035.820000</td>
                        <td id="T_d38be_row2_col8" class="data row2 col8" >988.880000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row3" class="row_heading level0 row3" >0.3</th>
                        <td id="T_d38be_row3_col0" class="data row3 col0" >993.840000</td>
                        <td id="T_d38be_row3_col1" class="data row3 col1" >994.750000</td>
                        <td id="T_d38be_row3_col2" class="data row3 col2" >997.480000</td>
                        <td id="T_d38be_row3_col3" class="data row3 col3" >1017.220000</td>
                        <td id="T_d38be_row3_col4" class="data row3 col4" >1027.680000</td>
                        <td id="T_d38be_row3_col5" class="data row3 col5" >1018.360000</td>
                        <td id="T_d38be_row3_col6" class="data row3 col6" >1012.890000</td>
                        <td id="T_d38be_row3_col7" class="data row3 col7" >1019.480000</td>
                        <td id="T_d38be_row3_col8" class="data row3 col8" >1040.500000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row4" class="row_heading level0 row4" >0.4</th>
                        <td id="T_d38be_row4_col0" class="data row4 col0" >976.180000</td>
                        <td id="T_d38be_row4_col1" class="data row4 col1" >977.690000</td>
                        <td id="T_d38be_row4_col2" class="data row4 col2" >978.490000</td>
                        <td id="T_d38be_row4_col3" class="data row4 col3" >1008.120000</td>
                        <td id="T_d38be_row4_col4" class="data row4 col4" >986.580000</td>
                        <td id="T_d38be_row4_col5" class="data row4 col5" >1023.510000</td>
                        <td id="T_d38be_row4_col6" class="data row4 col6" >1021.300000</td>
                        <td id="T_d38be_row4_col7" class="data row4 col7" >997.450000</td>
                        <td id="T_d38be_row4_col8" class="data row4 col8" >1019.140000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row5" class="row_heading level0 row5" >0.5</th>
                        <td id="T_d38be_row5_col0" class="data row5 col0" >947.160000</td>
                        <td id="T_d38be_row5_col1" class="data row5 col1" >949.390000</td>
                        <td id="T_d38be_row5_col2" class="data row5 col2" >956.400000</td>
                        <td id="T_d38be_row5_col3" class="data row5 col3" >977.680000</td>
                        <td id="T_d38be_row5_col4" class="data row5 col4" >953.180000</td>
                        <td id="T_d38be_row5_col5" class="data row5 col5" >994.320000</td>
                        <td id="T_d38be_row5_col6" class="data row5 col6" >981.060000</td>
                        <td id="T_d38be_row5_col7" class="data row5 col7" >1005.010000</td>
                        <td id="T_d38be_row5_col8" class="data row5 col8" >973.270000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row6" class="row_heading level0 row6" >0.6</th>
                        <td id="T_d38be_row6_col0" class="data row6 col0" >907.650000</td>
                        <td id="T_d38be_row6_col1" class="data row6 col1" >909.010000</td>
                        <td id="T_d38be_row6_col2" class="data row6 col2" >906.640000</td>
                        <td id="T_d38be_row6_col3" class="data row6 col3" >939.500000</td>
                        <td id="T_d38be_row6_col4" class="data row6 col4" >945.840000</td>
                        <td id="T_d38be_row6_col5" class="data row6 col5" >912.420000</td>
                        <td id="T_d38be_row6_col6" class="data row6 col6" >964.510000</td>
                        <td id="T_d38be_row6_col7" class="data row6 col7" >984.070000</td>
                        <td id="T_d38be_row6_col8" class="data row6 col8" >945.240000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row7" class="row_heading level0 row7" >0.7</th>
                        <td id="T_d38be_row7_col0" class="data row7 col0" >858.920000</td>
                        <td id="T_d38be_row7_col1" class="data row7 col1" >859.350000</td>
                        <td id="T_d38be_row7_col2" class="data row7 col2" >863.870000</td>
                        <td id="T_d38be_row7_col3" class="data row7 col3" >888.020000</td>
                        <td id="T_d38be_row7_col4" class="data row7 col4" >880.330000</td>
                        <td id="T_d38be_row7_col5" class="data row7 col5" >881.910000</td>
                        <td id="T_d38be_row7_col6" class="data row7 col6" >881.870000</td>
                        <td id="T_d38be_row7_col7" class="data row7 col7" >890.240000</td>
                        <td id="T_d38be_row7_col8" class="data row7 col8" >948.370000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row8" class="row_heading level0 row8" >0.8</th>
                        <td id="T_d38be_row8_col0" class="data row8 col0" >802.470000</td>
                        <td id="T_d38be_row8_col1" class="data row8 col1" >806.120000</td>
                        <td id="T_d38be_row8_col2" class="data row8 col2" >816.760000</td>
                        <td id="T_d38be_row8_col3" class="data row8 col3" >833.500000</td>
                        <td id="T_d38be_row8_col4" class="data row8 col4" >819.710000</td>
                        <td id="T_d38be_row8_col5" class="data row8 col5" >826.990000</td>
                        <td id="T_d38be_row8_col6" class="data row8 col6" >851.040000</td>
                        <td id="T_d38be_row8_col7" class="data row8 col7" >870.810000</td>
                        <td id="T_d38be_row8_col8" class="data row8 col8" >824.530000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row9" class="row_heading level0 row9" >0.9</th>
                        <td id="T_d38be_row9_col0" class="data row9 col0" >740.030000</td>
                        <td id="T_d38be_row9_col1" class="data row9 col1" >747.740000</td>
                        <td id="T_d38be_row9_col2" class="data row9 col2" >745.680000</td>
                        <td id="T_d38be_row9_col3" class="data row9 col3" >752.740000</td>
                        <td id="T_d38be_row9_col4" class="data row9 col4" >742.130000</td>
                        <td id="T_d38be_row9_col5" class="data row9 col5" >760.910000</td>
                        <td id="T_d38be_row9_col6" class="data row9 col6" >714.690000</td>
                        <td id="T_d38be_row9_col7" class="data row9 col7" >714.700000</td>
                        <td id="T_d38be_row9_col8" class="data row9 col8" >720.330000</td>
            </tr>
            <tr>
                        <th id="T_d38be_level0_row10" class="row_heading level0 row10" >1.0</th>
                        <td id="T_d38be_row10_col0" class="data row10 col0" >673.450000</td>
                        <td id="T_d38be_row10_col1" class="data row10 col1" >673.450000</td>
                        <td id="T_d38be_row10_col2" class="data row10 col2" >673.450000</td>
                        <td id="T_d38be_row10_col3" class="data row10 col3" >673.450000</td>
                        <td id="T_d38be_row10_col4" class="data row10 col4" >673.450000</td>
                        <td id="T_d38be_row10_col5" class="data row10 col5" >673.450000</td>
                        <td id="T_d38be_row10_col6" class="data row10 col6" >673.450000</td>
                        <td id="T_d38be_row10_col7" class="data row10 col7" >673.450000</td>
                        <td id="T_d38be_row10_col8" class="data row10 col8" >673.450000</td>
            </tr>
    </tbody></table>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Conclusão: o rebalanceamento usado de forma correta pode ser uma ferramenta muito útil para a criação de capital, porém também pode resultar em perdas.</p>

</div>
</div>
</body>







</html>
