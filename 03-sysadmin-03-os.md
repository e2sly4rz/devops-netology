      <!DOCTYPE html>
      <html>
        <head>
            <meta charset="utf-8" />
            <title>hw3</title>
            <style>.markdown-preview:not([data-use-github-style]) { padding: 2em; font-size: 1.2em; color: rgb(171, 178, 191); background-color: rgb(40, 44, 52); overflow: auto; }
.markdown-preview:not([data-use-github-style]) > :first-child { margin-top: 0px; }
.markdown-preview:not([data-use-github-style]) h1, .markdown-preview:not([data-use-github-style]) h2, .markdown-preview:not([data-use-github-style]) h3, .markdown-preview:not([data-use-github-style]) h4, .markdown-preview:not([data-use-github-style]) h5, .markdown-preview:not([data-use-github-style]) h6 { line-height: 1.2; margin-top: 1.5em; margin-bottom: 0.5em; color: rgb(255, 255, 255); }
.markdown-preview:not([data-use-github-style]) h1 { font-size: 2.4em; font-weight: 300; }
.markdown-preview:not([data-use-github-style]) h2 { font-size: 1.8em; font-weight: 400; }
.markdown-preview:not([data-use-github-style]) h3 { font-size: 1.5em; font-weight: 500; }
.markdown-preview:not([data-use-github-style]) h4 { font-size: 1.2em; font-weight: 600; }
.markdown-preview:not([data-use-github-style]) h5 { font-size: 1.1em; font-weight: 600; }
.markdown-preview:not([data-use-github-style]) h6 { font-size: 1em; font-weight: 600; }
.markdown-preview:not([data-use-github-style]) strong { color: rgb(255, 255, 255); }
.markdown-preview:not([data-use-github-style]) del { color: rgb(124, 135, 156); }
.markdown-preview:not([data-use-github-style]) a, .markdown-preview:not([data-use-github-style]) a code { color: rgb(82, 139, 255); }
.markdown-preview:not([data-use-github-style]) img { max-width: 100%; }
.markdown-preview:not([data-use-github-style]) > p { margin-top: 0px; margin-bottom: 1.5em; }
.markdown-preview:not([data-use-github-style]) > ul, .markdown-preview:not([data-use-github-style]) > ol { margin-bottom: 1.5em; }
.markdown-preview:not([data-use-github-style]) blockquote { margin: 1.5em 0px; font-size: inherit; color: rgb(124, 135, 156); border-color: rgb(75, 83, 98); border-width: 4px; }
.markdown-preview:not([data-use-github-style]) hr { margin: 3em 0px; border-top: 2px dashed rgb(75, 83, 98); background: none; }
.markdown-preview:not([data-use-github-style]) table { margin: 1.5em 0px; }
.markdown-preview:not([data-use-github-style]) th { color: rgb(255, 255, 255); }
.markdown-preview:not([data-use-github-style]) th, .markdown-preview:not([data-use-github-style]) td { padding: 0.66em 1em; border: 1px solid rgb(75, 83, 98); }
.markdown-preview:not([data-use-github-style]) code { color: rgb(255, 255, 255); background-color: rgb(58, 63, 75); }
.markdown-preview:not([data-use-github-style]) pre.editor-colors { margin: 1.5em 0px; padding: 1em; font-size: 0.92em; border-radius: 3px; background-color: rgb(49, 54, 63); }
.markdown-preview:not([data-use-github-style]) kbd { color: rgb(255, 255, 255); border-width: 1px 1px 2px; border-style: solid; border-color: rgb(75, 83, 98) rgb(75, 83, 98) rgb(62, 68, 81); border-image: initial; background-color: rgb(58, 63, 75); }
.markdown-preview[data-use-github-style] { font-family: "Helvetica Neue", Helvetica, "Segoe UI", Arial, freesans, sans-serif; line-height: 1.6; overflow-wrap: break-word; padding: 30px; font-size: 16px; color: rgb(51, 51, 51); background-color: rgb(255, 255, 255); overflow: scroll; }
.markdown-preview[data-use-github-style] > :first-child { margin-top: 0px !important; }
.markdown-preview[data-use-github-style] > :last-child { margin-bottom: 0px !important; }
.markdown-preview[data-use-github-style] a:not([href]) { color: inherit; text-decoration: none; }
.markdown-preview[data-use-github-style] .absent { color: rgb(204, 0, 0); }
.markdown-preview[data-use-github-style] .anchor { position: absolute; top: 0px; left: 0px; display: block; padding-right: 6px; padding-left: 30px; margin-left: -30px; }
.markdown-preview[data-use-github-style] .anchor:focus { outline: none; }
.markdown-preview[data-use-github-style] h1, .markdown-preview[data-use-github-style] h2, .markdown-preview[data-use-github-style] h3, .markdown-preview[data-use-github-style] h4, .markdown-preview[data-use-github-style] h5, .markdown-preview[data-use-github-style] h6 { position: relative; margin-top: 1em; margin-bottom: 16px; font-weight: bold; line-height: 1.4; }
.markdown-preview[data-use-github-style] h1 .octicon-link, .markdown-preview[data-use-github-style] h2 .octicon-link, .markdown-preview[data-use-github-style] h3 .octicon-link, .markdown-preview[data-use-github-style] h4 .octicon-link, .markdown-preview[data-use-github-style] h5 .octicon-link, .markdown-preview[data-use-github-style] h6 .octicon-link { display: none; color: rgb(0, 0, 0); vertical-align: middle; }
.markdown-preview[data-use-github-style] h1:hover .anchor, .markdown-preview[data-use-github-style] h2:hover .anchor, .markdown-preview[data-use-github-style] h3:hover .anchor, .markdown-preview[data-use-github-style] h4:hover .anchor, .markdown-preview[data-use-github-style] h5:hover .anchor, .markdown-preview[data-use-github-style] h6:hover .anchor { padding-left: 8px; margin-left: -30px; text-decoration: none; }
.markdown-preview[data-use-github-style] h1:hover .anchor .octicon-link, .markdown-preview[data-use-github-style] h2:hover .anchor .octicon-link, .markdown-preview[data-use-github-style] h3:hover .anchor .octicon-link, .markdown-preview[data-use-github-style] h4:hover .anchor .octicon-link, .markdown-preview[data-use-github-style] h5:hover .anchor .octicon-link, .markdown-preview[data-use-github-style] h6:hover .anchor .octicon-link { display: inline-block; }
.markdown-preview[data-use-github-style] h1 tt, .markdown-preview[data-use-github-style] h2 tt, .markdown-preview[data-use-github-style] h3 tt, .markdown-preview[data-use-github-style] h4 tt, .markdown-preview[data-use-github-style] h5 tt, .markdown-preview[data-use-github-style] h6 tt, .markdown-preview[data-use-github-style] h1 code, .markdown-preview[data-use-github-style] h2 code, .markdown-preview[data-use-github-style] h3 code, .markdown-preview[data-use-github-style] h4 code, .markdown-preview[data-use-github-style] h5 code, .markdown-preview[data-use-github-style] h6 code { font-size: inherit; }
.markdown-preview[data-use-github-style] h1 { padding-bottom: 0.3em; font-size: 2.25em; line-height: 1.2; border-bottom: 1px solid rgb(238, 238, 238); }
.markdown-preview[data-use-github-style] h1 .anchor { line-height: 1; }
.markdown-preview[data-use-github-style] h2 { padding-bottom: 0.3em; font-size: 1.75em; line-height: 1.225; border-bottom: 1px solid rgb(238, 238, 238); }
.markdown-preview[data-use-github-style] h2 .anchor { line-height: 1; }
.markdown-preview[data-use-github-style] h3 { font-size: 1.5em; line-height: 1.43; }
.markdown-preview[data-use-github-style] h3 .anchor { line-height: 1.2; }
.markdown-preview[data-use-github-style] h4 { font-size: 1.25em; }
.markdown-preview[data-use-github-style] h4 .anchor { line-height: 1.2; }
.markdown-preview[data-use-github-style] h5 { font-size: 1em; }
.markdown-preview[data-use-github-style] h5 .anchor { line-height: 1.1; }
.markdown-preview[data-use-github-style] h6 { font-size: 1em; color: rgb(119, 119, 119); }
.markdown-preview[data-use-github-style] h6 .anchor { line-height: 1.1; }
.markdown-preview[data-use-github-style] p, .markdown-preview[data-use-github-style] blockquote, .markdown-preview[data-use-github-style] ul, .markdown-preview[data-use-github-style] ol, .markdown-preview[data-use-github-style] dl, .markdown-preview[data-use-github-style] table, .markdown-preview[data-use-github-style] pre { margin-top: 0px; margin-bottom: 16px; }
.markdown-preview[data-use-github-style] hr { height: 4px; padding: 0px; margin: 16px 0px; background-color: rgb(231, 231, 231); border: 0px none; }
.markdown-preview[data-use-github-style] ul, .markdown-preview[data-use-github-style] ol { padding-left: 2em; }
.markdown-preview[data-use-github-style] ul.no-list, .markdown-preview[data-use-github-style] ol.no-list { padding: 0px; list-style-type: none; }
.markdown-preview[data-use-github-style] ul ul, .markdown-preview[data-use-github-style] ul ol, .markdown-preview[data-use-github-style] ol ol, .markdown-preview[data-use-github-style] ol ul { margin-top: 0px; margin-bottom: 0px; }
.markdown-preview[data-use-github-style] li > p { margin-top: 16px; }
.markdown-preview[data-use-github-style] dl { padding: 0px; }
.markdown-preview[data-use-github-style] dl dt { padding: 0px; margin-top: 16px; font-size: 1em; font-style: italic; font-weight: bold; }
.markdown-preview[data-use-github-style] dl dd { padding: 0px 16px; margin-bottom: 16px; }
.markdown-preview[data-use-github-style] blockquote { padding: 0px 15px; color: rgb(119, 119, 119); border-left: 4px solid rgb(221, 221, 221); }
.markdown-preview[data-use-github-style] blockquote > :first-child { margin-top: 0px; }
.markdown-preview[data-use-github-style] blockquote > :last-child { margin-bottom: 0px; }
.markdown-preview[data-use-github-style] table { display: block; width: 100%; overflow: auto; word-break: keep-all; }
.markdown-preview[data-use-github-style] table th { font-weight: bold; }
.markdown-preview[data-use-github-style] table th, .markdown-preview[data-use-github-style] table td { padding: 6px 13px; border: 1px solid rgb(221, 221, 221); }
.markdown-preview[data-use-github-style] table tr { background-color: rgb(255, 255, 255); border-top: 1px solid rgb(204, 204, 204); }
.markdown-preview[data-use-github-style] table tr:nth-child(2n) { background-color: rgb(248, 248, 248); }
.markdown-preview[data-use-github-style] img { max-width: 100%; box-sizing: border-box; }
.markdown-preview[data-use-github-style] .emoji { max-width: none; }
.markdown-preview[data-use-github-style] span.frame { display: block; overflow: hidden; }
.markdown-preview[data-use-github-style] span.frame > span { display: block; float: left; width: auto; padding: 7px; margin: 13px 0px 0px; overflow: hidden; border: 1px solid rgb(221, 221, 221); }
.markdown-preview[data-use-github-style] span.frame span img { display: block; float: left; }
.markdown-preview[data-use-github-style] span.frame span span { display: block; padding: 5px 0px 0px; clear: both; color: rgb(51, 51, 51); }
.markdown-preview[data-use-github-style] span.align-center { display: block; overflow: hidden; clear: both; }
.markdown-preview[data-use-github-style] span.align-center > span { display: block; margin: 13px auto 0px; overflow: hidden; text-align: center; }
.markdown-preview[data-use-github-style] span.align-center span img { margin: 0px auto; text-align: center; }
.markdown-preview[data-use-github-style] span.align-right { display: block; overflow: hidden; clear: both; }
.markdown-preview[data-use-github-style] span.align-right > span { display: block; margin: 13px 0px 0px; overflow: hidden; text-align: right; }
.markdown-preview[data-use-github-style] span.align-right span img { margin: 0px; text-align: right; }
.markdown-preview[data-use-github-style] span.float-left { display: block; float: left; margin-right: 13px; overflow: hidden; }
.markdown-preview[data-use-github-style] span.float-left span { margin: 13px 0px 0px; }
.markdown-preview[data-use-github-style] span.float-right { display: block; float: right; margin-left: 13px; overflow: hidden; }
.markdown-preview[data-use-github-style] span.float-right > span { display: block; margin: 13px auto 0px; overflow: hidden; text-align: right; }
.markdown-preview[data-use-github-style] code, .markdown-preview[data-use-github-style] tt { padding: 0.2em 0px; margin: 0px; font-size: 85%; background-color: rgba(0, 0, 0, 0.04); border-radius: 3px; }
.markdown-preview[data-use-github-style] code::before, .markdown-preview[data-use-github-style] tt::before, .markdown-preview[data-use-github-style] code::after, .markdown-preview[data-use-github-style] tt::after { letter-spacing: -0.2em; content: " "; }
.markdown-preview[data-use-github-style] code br, .markdown-preview[data-use-github-style] tt br { display: none; }
.markdown-preview[data-use-github-style] del code { text-decoration: inherit; }
.markdown-preview[data-use-github-style] pre > code { padding: 0px; margin: 0px; font-size: 100%; word-break: normal; white-space: pre; background: transparent; border: 0px; }
.markdown-preview[data-use-github-style] .highlight { margin-bottom: 16px; }
.markdown-preview[data-use-github-style] .highlight pre, .markdown-preview[data-use-github-style] pre { padding: 16px; overflow: auto; font-size: 85%; line-height: 1.45; background-color: rgb(247, 247, 247); border-radius: 3px; }
.markdown-preview[data-use-github-style] .highlight pre { margin-bottom: 0px; word-break: normal; }
.markdown-preview[data-use-github-style] pre { overflow-wrap: normal; }
.markdown-preview[data-use-github-style] pre code, .markdown-preview[data-use-github-style] pre tt { display: inline; max-width: initial; padding: 0px; margin: 0px; overflow: initial; line-height: inherit; overflow-wrap: normal; background-color: transparent; border: 0px; }
.markdown-preview[data-use-github-style] pre code::before, .markdown-preview[data-use-github-style] pre tt::before, .markdown-preview[data-use-github-style] pre code::after, .markdown-preview[data-use-github-style] pre tt::after { content: normal; }
.markdown-preview[data-use-github-style] kbd { display: inline-block; padding: 3px 5px; font-size: 11px; line-height: 10px; color: rgb(85, 85, 85); vertical-align: middle; background-color: rgb(252, 252, 252); border-width: 1px; border-style: solid; border-color: rgb(204, 204, 204) rgb(204, 204, 204) rgb(187, 187, 187); border-image: initial; border-radius: 3px; box-shadow: rgb(187, 187, 187) 0px -1px 0px inset; }
.markdown-preview[data-use-github-style] a { color: rgb(51, 122, 183); }
.markdown-preview[data-use-github-style] code { color: inherit; }
.markdown-preview[data-use-github-style] pre.editor-colors { padding: 0.8em 1em; margin-bottom: 1em; font-size: 0.85em; border-radius: 4px; overflow: auto; }
.markdown-preview pre.editor-colors { user-select: auto; }
.scrollbars-visible-always .markdown-preview pre.editor-colors .vertical-scrollbar, .scrollbars-visible-always .markdown-preview pre.editor-colors .horizontal-scrollbar { visibility: hidden; }
.scrollbars-visible-always .markdown-preview pre.editor-colors:hover .vertical-scrollbar, .scrollbars-visible-always .markdown-preview pre.editor-colors:hover .horizontal-scrollbar { visibility: visible; }
.markdown-preview .task-list-item input[type="checkbox"] { position: absolute; margin: 0.25em 0px 0px -1.4em; }
.markdown-preview .task-list-item { list-style-type: none; }
.bracket-matcher .region {
  border-bottom: 1px dotted lime;
  position: absolute;
}
.line-number.bracket-matcher.bracket-matcher {
  color: #abb2bf;
  background-color: #3a3f4b;
}

.spell-check-misspelling .region {
  border-bottom: 2px dotted rgba(255, 51, 51, 0.75);
}
.spell-check-corrections {
  width: 25em !important;
}

pre.editor-colors {
  background-color: #282c34;
  color: #abb2bf;
}
pre.editor-colors .line.cursor-line {
  background-color: rgba(153, 187, 255, 0.04);
}
pre.editor-colors .invisible {
  color: #abb2bf;
}
pre.editor-colors .cursor {
  border-left: 2px solid #528bff;
}
pre.editor-colors .selection .region {
  background-color: #3e4451;
}
pre.editor-colors .bracket-matcher .region {
  border-bottom: 1px solid #528bff;
  box-sizing: border-box;
}
pre.editor-colors .invisible-character {
  color: rgba(171, 178, 191, 0.15);
}
pre.editor-colors .indent-guide {
  color: rgba(171, 178, 191, 0.15);
}
pre.editor-colors .wrap-guide {
  background-color: rgba(171, 178, 191, 0.15);
}
pre.editor-colors .find-result .region.region.region,
pre.editor-colors .current-result .region.region.region {
  border-radius: 2px;
  background-color: rgba(82, 139, 255, 0.24);
  transition: border-color 0.4s;
}
pre.editor-colors .find-result .region.region.region {
  border: 2px solid transparent;
}
pre.editor-colors .current-result .region.region.region {
  border: 2px solid #528bff;
  transition-duration: .1s;
}
pre.editor-colors .gutter .line-number {
  color: #636d83;
  -webkit-font-smoothing: antialiased;
}
pre.editor-colors .gutter .line-number.cursor-line {
  color: #abb2bf;
  background-color: #3a3f4b;
}
pre.editor-colors .gutter .line-number.cursor-line-no-selection {
  background-color: transparent;
}
pre.editor-colors .gutter .line-number .icon-right {
  color: #abb2bf;
}
pre.editor-colors .gutter:not(.git-diff-icon) .line-number.git-line-removed.git-line-removed::before {
  bottom: -3px;
}
pre.editor-colors .gutter:not(.git-diff-icon) .line-number.git-line-removed::after {
  content: "";
  position: absolute;
  left: 0px;
  bottom: 0px;
  width: 25px;
  border-bottom: 1px dotted rgba(224, 82, 82, 0.5);
  pointer-events: none;
}
pre.editor-colors .gutter .line-number.folded,
pre.editor-colors .gutter .line-number:after,
pre.editor-colors .fold-marker:after {
  color: #abb2bf;
}
.syntax--comment {
  color: #5c6370;
  font-style: italic;
}
.syntax--comment .syntax--markup.syntax--link {
  color: #5c6370;
}
.syntax--entity.syntax--name.syntax--type {
  color: #e5c07b;
}
.syntax--entity.syntax--other.syntax--inherited-class {
  color: #e5c07b;
}
.syntax--keyword {
  color: #c678dd;
}
.syntax--keyword.syntax--control {
  color: #c678dd;
}
.syntax--keyword.syntax--operator {
  color: #c678dd;
}
.syntax--keyword.syntax--other.syntax--special-method {
  color: #61afef;
}
.syntax--keyword.syntax--other.syntax--unit {
  color: #d19a66;
}
.syntax--storage {
  color: #c678dd;
}
.syntax--storage.syntax--type.syntax--annotation,
.syntax--storage.syntax--type.syntax--primitive {
  color: #c678dd;
}
.syntax--storage.syntax--modifier.syntax--package,
.syntax--storage.syntax--modifier.syntax--import {
  color: #abb2bf;
}
.syntax--constant {
  color: #d19a66;
}
.syntax--constant.syntax--variable {
  color: #d19a66;
}
.syntax--constant.syntax--character.syntax--escape {
  color: #56b6c2;
}
.syntax--constant.syntax--numeric {
  color: #d19a66;
}
.syntax--constant.syntax--other.syntax--color {
  color: #56b6c2;
}
.syntax--constant.syntax--other.syntax--symbol {
  color: #56b6c2;
}
.syntax--variable {
  color: #e06c75;
}
.syntax--variable.syntax--interpolation {
  color: #be5046;
}
.syntax--variable.syntax--parameter {
  color: #abb2bf;
}
.syntax--string {
  color: #98c379;
}
.syntax--string > .syntax--source,
.syntax--string .syntax--embedded {
  color: #abb2bf;
}
.syntax--string.syntax--regexp {
  color: #56b6c2;
}
.syntax--string.syntax--regexp .syntax--source.syntax--ruby.syntax--embedded {
  color: #e5c07b;
}
.syntax--string.syntax--other.syntax--link {
  color: #e06c75;
}
.syntax--punctuation.syntax--definition.syntax--comment {
  color: #5c6370;
}
.syntax--punctuation.syntax--definition.syntax--method-parameters,
.syntax--punctuation.syntax--definition.syntax--function-parameters,
.syntax--punctuation.syntax--definition.syntax--parameters,
.syntax--punctuation.syntax--definition.syntax--separator,
.syntax--punctuation.syntax--definition.syntax--seperator,
.syntax--punctuation.syntax--definition.syntax--array {
  color: #abb2bf;
}
.syntax--punctuation.syntax--definition.syntax--heading,
.syntax--punctuation.syntax--definition.syntax--identity {
  color: #61afef;
}
.syntax--punctuation.syntax--definition.syntax--bold {
  color: #e5c07b;
  font-weight: bold;
}
.syntax--punctuation.syntax--definition.syntax--italic {
  color: #c678dd;
  font-style: italic;
}
.syntax--punctuation.syntax--section.syntax--embedded {
  color: #be5046;
}
.syntax--punctuation.syntax--section.syntax--method,
.syntax--punctuation.syntax--section.syntax--class,
.syntax--punctuation.syntax--section.syntax--inner-class {
  color: #abb2bf;
}
.syntax--support.syntax--class {
  color: #e5c07b;
}
.syntax--support.syntax--type {
  color: #56b6c2;
}
.syntax--support.syntax--function {
  color: #56b6c2;
}
.syntax--support.syntax--function.syntax--any-method {
  color: #61afef;
}
.syntax--entity.syntax--name.syntax--function {
  color: #61afef;
}
.syntax--entity.syntax--name.syntax--class,
.syntax--entity.syntax--name.syntax--type.syntax--class {
  color: #e5c07b;
}
.syntax--entity.syntax--name.syntax--section {
  color: #61afef;
}
.syntax--entity.syntax--name.syntax--tag {
  color: #e06c75;
}
.syntax--entity.syntax--other.syntax--attribute-name {
  color: #d19a66;
}
.syntax--entity.syntax--other.syntax--attribute-name.syntax--id {
  color: #61afef;
}
.syntax--meta.syntax--class {
  color: #e5c07b;
}
.syntax--meta.syntax--class.syntax--body {
  color: #abb2bf;
}
.syntax--meta.syntax--method-call,
.syntax--meta.syntax--method {
  color: #abb2bf;
}
.syntax--meta.syntax--definition.syntax--variable {
  color: #e06c75;
}
.syntax--meta.syntax--link {
  color: #d19a66;
}
.syntax--meta.syntax--require {
  color: #61afef;
}
.syntax--meta.syntax--selector {
  color: #c678dd;
}
.syntax--meta.syntax--separator {
  color: #abb2bf;
}
.syntax--meta.syntax--tag {
  color: #abb2bf;
}
.syntax--underline {
  text-decoration: underline;
}
.syntax--none {
  color: #abb2bf;
}
.syntax--invalid.syntax--deprecated {
  color: #523d14 !important;
  background-color: #e0c285 !important;
}
.syntax--invalid.syntax--illegal {
  color: white !important;
  background-color: #e05252 !important;
}
.syntax--markup.syntax--bold {
  color: #d19a66;
  font-weight: bold;
}
.syntax--markup.syntax--changed {
  color: #c678dd;
}
.syntax--markup.syntax--deleted {
  color: #e06c75;
}
.syntax--markup.syntax--italic {
  color: #c678dd;
  font-style: italic;
}
.syntax--markup.syntax--heading {
  color: #e06c75;
}
.syntax--markup.syntax--heading .syntax--punctuation.syntax--definition.syntax--heading {
  color: #61afef;
}
.syntax--markup.syntax--link {
  color: #56b6c2;
}
.syntax--markup.syntax--inserted {
  color: #98c379;
}
.syntax--markup.syntax--quote {
  color: #d19a66;
}
.syntax--markup.syntax--raw {
  color: #98c379;
}
.syntax--source.syntax--cs .syntax--keyword.syntax--operator {
  color: #c678dd;
}
.syntax--source.syntax--css .syntax--property-name,
.syntax--source.syntax--css .syntax--property-value {
  color: #828997;
}
.syntax--source.syntax--css .syntax--property-name.syntax--support,
.syntax--source.syntax--css .syntax--property-value.syntax--support {
  color: #abb2bf;
}
.syntax--source.syntax--elixir .syntax--source.syntax--embedded.syntax--source {
  color: #abb2bf;
}
.syntax--source.syntax--elixir .syntax--constant.syntax--language,
.syntax--source.syntax--elixir .syntax--constant.syntax--numeric,
.syntax--source.syntax--elixir .syntax--constant.syntax--definition {
  color: #61afef;
}
.syntax--source.syntax--elixir .syntax--variable.syntax--definition,
.syntax--source.syntax--elixir .syntax--variable.syntax--anonymous {
  color: #c678dd;
}
.syntax--source.syntax--elixir .syntax--parameter.syntax--variable.syntax--function {
  color: #d19a66;
  font-style: italic;
}
.syntax--source.syntax--elixir .syntax--quoted {
  color: #98c379;
}
.syntax--source.syntax--elixir .syntax--keyword.syntax--special-method,
.syntax--source.syntax--elixir .syntax--embedded.syntax--section,
.syntax--source.syntax--elixir .syntax--embedded.syntax--source.syntax--empty {
  color: #e06c75;
}
.syntax--source.syntax--elixir .syntax--readwrite.syntax--module .syntax--punctuation {
  color: #e06c75;
}
.syntax--source.syntax--elixir .syntax--regexp.syntax--section,
.syntax--source.syntax--elixir .syntax--regexp.syntax--string {
  color: #be5046;
}
.syntax--source.syntax--elixir .syntax--separator,
.syntax--source.syntax--elixir .syntax--keyword.syntax--operator {
  color: #d19a66;
}
.syntax--source.syntax--elixir .syntax--variable.syntax--constant {
  color: #e5c07b;
}
.syntax--source.syntax--elixir .syntax--array,
.syntax--source.syntax--elixir .syntax--scope,
.syntax--source.syntax--elixir .syntax--section {
  color: #828997;
}
.syntax--source.syntax--gfm .syntax--markup {
  -webkit-font-smoothing: auto;
}
.syntax--source.syntax--gfm .syntax--link .syntax--entity {
  color: #61afef;
}
.syntax--source.syntax--ini .syntax--keyword.syntax--other.syntax--definition.syntax--ini {
  color: #e06c75;
}
.syntax--source.syntax--java .syntax--storage.syntax--modifier.syntax--import {
  color: #e5c07b;
}
.syntax--source.syntax--java .syntax--storage.syntax--type {
  color: #e5c07b;
}
.syntax--source.syntax--java .syntax--keyword.syntax--operator.syntax--instanceof {
  color: #c678dd;
}
.syntax--source.syntax--java-properties .syntax--meta.syntax--key-pair {
  color: #e06c75;
}
.syntax--source.syntax--java-properties .syntax--meta.syntax--key-pair > .syntax--punctuation {
  color: #abb2bf;
}
.syntax--source.syntax--ts .syntax--keyword.syntax--operator {
  color: #56b6c2;
}
.syntax--source.syntax--flow .syntax--keyword.syntax--operator {
  color: #56b6c2;
}
.syntax--source.syntax--json .syntax--meta.syntax--structure.syntax--dictionary.syntax--json > .syntax--string.syntax--quoted.syntax--json {
  color: #e06c75;
}
.syntax--source.syntax--json .syntax--meta.syntax--structure.syntax--dictionary.syntax--json > .syntax--string.syntax--quoted.syntax--json > .syntax--punctuation.syntax--string {
  color: #e06c75;
}
.syntax--source.syntax--json .syntax--meta.syntax--structure.syntax--dictionary.syntax--json > .syntax--value.syntax--json > .syntax--string.syntax--quoted.syntax--json,
.syntax--source.syntax--json .syntax--meta.syntax--structure.syntax--array.syntax--json > .syntax--value.syntax--json > .syntax--string.syntax--quoted.syntax--json,
.syntax--source.syntax--json .syntax--meta.syntax--structure.syntax--dictionary.syntax--json > .syntax--value.syntax--json > .syntax--string.syntax--quoted.syntax--json > .syntax--punctuation,
.syntax--source.syntax--json .syntax--meta.syntax--structure.syntax--array.syntax--json > .syntax--value.syntax--json > .syntax--string.syntax--quoted.syntax--json > .syntax--punctuation {
  color: #98c379;
}
.syntax--source.syntax--json .syntax--meta.syntax--structure.syntax--dictionary.syntax--json > .syntax--constant.syntax--language.syntax--json,
.syntax--source.syntax--json .syntax--meta.syntax--structure.syntax--array.syntax--json > .syntax--constant.syntax--language.syntax--json {
  color: #56b6c2;
}
.syntax--ng.syntax--interpolation {
  color: #e06c75;
}
.syntax--ng.syntax--interpolation.syntax--begin,
.syntax--ng.syntax--interpolation.syntax--end {
  color: #61afef;
}
.syntax--ng.syntax--interpolation .syntax--function {
  color: #e06c75;
}
.syntax--ng.syntax--interpolation .syntax--function.syntax--begin,
.syntax--ng.syntax--interpolation .syntax--function.syntax--end {
  color: #61afef;
}
.syntax--ng.syntax--interpolation .syntax--bool {
  color: #d19a66;
}
.syntax--ng.syntax--interpolation .syntax--bracket {
  color: #abb2bf;
}
.syntax--ng.syntax--pipe,
.syntax--ng.syntax--operator {
  color: #abb2bf;
}
.syntax--ng.syntax--tag {
  color: #56b6c2;
}
.syntax--ng.syntax--attribute-with-value .syntax--attribute-name {
  color: #e5c07b;
}
.syntax--ng.syntax--attribute-with-value .syntax--string {
  color: #c678dd;
}
.syntax--ng.syntax--attribute-with-value .syntax--string.syntax--begin,
.syntax--ng.syntax--attribute-with-value .syntax--string.syntax--end {
  color: #abb2bf;
}
.syntax--source.syntax--php .syntax--class.syntax--bracket {
  color: #abb2bf;
}
/*
   This defines styling rules for syntax classes.

   See the naming conventions for a list of syntax classes:
   https://flight-manual.atom.io/hacking-atom/sections/syntax-naming-conventions

   When styling rules conflict:
   - The last rule overrides previous rules.
   - The rule with most classes and pseudo-classes overrides the last rule.
*/
.syntax--keyword {
  color: #c678dd;
}
.syntax--keyword.syntax--type {
  color: #56b6c2;
}
.syntax--keyword.syntax--function {
  color: #e06c75;
}
.syntax--keyword.syntax--variable {
  color: #e06c75;
}
.syntax--entity {
  color: #abb2bf;
}
.syntax--entity.syntax--parameter {
  color: #abb2bf;
}
.syntax--entity.syntax--support {
  color: #e06c75;
}
.syntax--entity.syntax--decorator:last-child {
  color: #61afef;
}
.syntax--entity.syntax--label {
  text-decoration: underline;
}
.syntax--entity.syntax--function {
  color: #61afef;
}
.syntax--entity.syntax--operator {
  color: #61afef;
}
.syntax--entity.syntax--operator.syntax--symbolic {
  color: #abb2bf;
}
.syntax--entity.syntax--type {
  color: #56b6c2;
}
.syntax--entity.syntax--tag {
  color: #e06c75;
}
.syntax--entity.syntax--attribute {
  color: #d19a66;
}
.syntax--punctuation {
  color: #abb2bf;
}
.syntax--punctuation.syntax--accessor {
  color: #abb2bf;
}
.syntax--punctuation.syntax--accessor.syntax--member,
.syntax--punctuation.syntax--accessor.syntax--scope {
  color: #c678dd;
}
.syntax--punctuation.syntax--embedded {
  color: #c678dd;
}
.syntax--string {
  color: #98c379;
}
.syntax--string.syntax--immutable {
  color: #98c379;
}
.syntax--string.syntax--part {
  color: #56b6c2;
}
.syntax--string.syntax--interpolation {
  color: #c678dd;
}
.syntax--string.syntax--regexp {
  color: #98c379;
}
.syntax--string.syntax--regexp.syntax--language {
  color: #c678dd;
}
.syntax--string.syntax--regexp.syntax--variable {
  color: #61afef;
}
.syntax--string.syntax--regexp.syntax--punctuation {
  color: #c678dd;
}
.syntax--constant {
  color: #d19a66;
}
.syntax--constant.syntax--character {
  color: #98c379;
}
.syntax--constant.syntax--character.syntax--escape {
  color: #98c379;
}
.syntax--constant.syntax--character.syntax--code {
  color: #56b6c2;
}
.syntax--text {
  color: #abb2bf;
}
.syntax--markup.syntax--heading {
  color: #e06c75;
}
.syntax--markup.syntax--list.syntax--punctuation {
  color: #e06c75;
}
.syntax--markup.syntax--quote {
  color: #5c6370;
  font-style: italic;
}
.syntax--markup.syntax--bold {
  color: #d19a66;
  font-weight: bold;
}
.syntax--markup.syntax--italic {
  color: #c678dd;
  font-style: italic;
}
.syntax--markup.syntax--underline {
  color: #56b6c2;
  text-decoration: underline;
}
.syntax--markup.syntax--strike {
  color: #e06c75;
}
.syntax--markup.syntax--raw {
  color: #98c379;
}
.syntax--markup.syntax--link {
  color: #56b6c2;
}
.syntax--markup.syntax--alt {
  color: #61afef;
}
.syntax--markup.syntax--inserted {
  color: #98c379;
}
.syntax--markup.syntax--inserted .syntax--punctuation {
  color: #98c379;
}
.syntax--markup.syntax--highlighted {
  color: #98c379;
}
.syntax--markup.syntax--highlighted .syntax--punctuation {
  color: #98c379;
}
.syntax--markup.syntax--deleted {
  color: #e06c75;
}
.syntax--markup.syntax--deleted .syntax--punctuation {
  color: #e06c75;
}
.syntax--markup.syntax--changed {
  color: #c678dd;
}
.syntax--markup.syntax--changed .syntax--punctuation {
  color: #c678dd;
}
.syntax--markup.syntax--commented {
  color: #5c6370;
}
.syntax--markup.syntax--commented .syntax--punctuation {
  color: #5c6370;
}
.syntax--comment {
  color: #5c6370;
  font-style: italic;
}
.syntax--comment.syntax--caption {
  color: #6a7181;
  font-weight: bold;
}
.syntax--comment.syntax--term {
  color: #707989;
}
.syntax--comment.syntax--punctuation {
  color: #5c6370;
  font-weight: normal;
}
.syntax--invalid:not(.syntax--punctuation).syntax--illegal {
  color: white !important;
  background-color: #e05252 !important;
}
.syntax--invalid:not(.syntax--punctuation).syntax--deprecated {
  color: #523d14 !important;
  background-color: #e0c285 !important;
}
.syntax--source.syntax--css .syntax--entity.syntax--function {
  color: #828997;
}
.syntax--source.syntax--css .syntax--entity.syntax--function.syntax--support {
  color: #56b6c2;
}
.syntax--source.syntax--css .syntax--entity.syntax--selector {
  color: #d19a66;
}
.syntax--source.syntax--css .syntax--entity.syntax--selector.syntax--tag {
  color: #e06c75;
}
.syntax--source.syntax--css .syntax--entity.syntax--selector.syntax--id {
  color: #61afef;
}
.syntax--source.syntax--css .syntax--entity.syntax--property {
  color: #828997;
}
.syntax--source.syntax--css .syntax--entity.syntax--property.syntax--support {
  color: #abb2bf;
}
.syntax--source.syntax--css .syntax--entity.syntax--variable {
  color: #e06c75;
}
.syntax--source.syntax--css .syntax--constant {
  color: #828997;
}
.syntax--source.syntax--css .syntax--constant.syntax--support {
  color: #abb2bf;
}
.syntax--source.syntax--css .syntax--constant.syntax--numeric {
  color: #d19a66;
}
.syntax--source.syntax--css .syntax--constant.syntax--media {
  color: #d19a66;
}
.syntax--source.syntax--css .syntax--constant.syntax--color {
  color: #d19a66;
}
.syntax--source.syntax--css .syntax--constant.syntax--offset {
  color: #abb2bf;
}
.syntax--source.syntax--css .syntax--constant.syntax--attribute-value {
  color: #98c379;
}
.syntax--source.syntax--css .syntax--punctuation.syntax--selector {
  color: #d19a66;
}
.syntax--source.syntax--css .syntax--punctuation.syntax--selector.syntax--wildcard {
  color: #e06c75;
}
.syntax--source.syntax--css .syntax--punctuation.syntax--selector.syntax--id {
  color: #61afef;
}
.syntax--source.syntax--css .syntax--punctuation.syntax--selector.syntax--attribute {
  color: #abb2bf;
}
</style>
        </head>
        <body class='markdown-preview' data-use-github-style><h2 id="домашнее-задание-к-занятию-33-операционные-системы-лекция-1">Домашнее задание к занятию "3.3. Операционные системы, лекция 1"</h2>
<h5 id="1-какой-системный-вызов-делает-команда-cd-в-прошлом-дз-мы-выяснили-что-cd-не-является-самостоятельной-программой-это-shell-builtin-поэтому-запустить-strace-непосредственно-на-cd-не-получится-тем-не-менее-вы-можете-запустить-strace-на-binbash--c-cd-tmp-в-этом-случае-вы-увидите-полный-список-системных-вызовов-которые-делает-сам-bash-при-старте-вам-нужно-найти-тот-единственный-который-относится-именно-к-cd">1. Какой системный вызов делает команда <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">cd</code>? В прошлом ДЗ мы выяснили, что <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">cd</code> не является самостоятельной программой, это shell builtin, поэтому запустить <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">strace</code> непосредственно на <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">cd</code> не получится. Тем не менее, вы можете запустить <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">strace</code> на <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">/bin/bash -c 'cd /tmp'</code>. В этом случае вы увидите полный список системных вызовов, которые делает сам bash при старте. Вам нужно найти тот единственный, который относится именно к <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">cd</code>.</h5>
<pre class="editor-colors lang-bash"><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">chdir(<span class="syntax--string">"/tmp"</span></span>)</span></div></pre>
<h5 id="2-попробуйте-использовать-команду-file-на-объекты-разных-типов-на-файловой-системе-например">2. Попробуйте использовать команду <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">file</code> на объекты разных типов на файловой системе. Например:</h5>
<pre class="editor-colors lang-bash"><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">vagrant@netology1:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">file</span></span> /dev/tty</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">/dev/tty:</span> character special (<span class="syntax--entity syntax--name syntax--function">5/0</span>)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">vagrant@netology1:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">file</span></span> /dev/sda</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">/dev/sda:</span> block special (<span class="syntax--entity syntax--name syntax--function">8/0</span>)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">vagrant@netology1:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">file</span></span> /bin/bash</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">/bin/bash:</span> ELF 64-bit LSB shared object, x86-64</span></div></pre>
<h5 id="используя-strace-выясните-где-находится-база-данных-file-на-основании-которой-она-делает-свои-догадки">Используя <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">strace</code> выясните, где находится база данных <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">file</code> на основании которой она делает свои догадки.</h5>
<pre class="editor-colors lang-bash"><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Согласно приоритету сначала проверяются пользовательские каталоги на наличие пользовательского файла</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">stat(<span class="syntax--string">"/home/asamarskii/.magic.mgc"</span>,</span> 0x7ffe42697210) = <span class="syntax--entity syntax--other syntax--attribute-name">-1</span> ENOENT (<span class="syntax--entity syntax--name syntax--function">No</span> such file or directory)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">stat(<span class="syntax--string">"/home/asamarskii/.magic"</span>,</span> 0x7ffe42697210) = <span class="syntax--entity syntax--other syntax--attribute-name">-1</span> ENOENT (<span class="syntax--entity syntax--name syntax--function">No</span> such file or directory)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Затем проверяются "стандартные" расположения на наличие файла</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">openat(AT_FDCWD,</span> <span class="syntax--string">"/etc/magic.mgc"</span>, O_RDONLY) = <span class="syntax--entity syntax--other syntax--attribute-name">-1</span> ENOENT (<span class="syntax--entity syntax--name syntax--function">No</span> such file or directory)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">stat(<span class="syntax--string">"/etc/magic"</span>,</span> {st_mode=S_IFREG<span class="syntax--keyword syntax--operator">|</span><span class="syntax--entity syntax--name syntax--function">0644,</span> st_size=111, ...}) = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">openat(AT_FDCWD,</span> <span class="syntax--string">"/etc/magic"</span>, O_RDONLY) = 3</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">fstat(3,</span> {st_mode=S_IFREG<span class="syntax--keyword syntax--operator">|</span><span class="syntax--entity syntax--name syntax--function">0644,</span> st_size=111, ...}) = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">read(3,</span> <span class="syntax--string">"# Magic local data for file(1) c"</span>..., 4096) = 111</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">read(3,</span> <span class="syntax--string">""</span>, 4096)                       = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">close</span>(3)                                = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell"># Файл найден</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">openat(AT_FDCWD,</span> <span class="syntax--string">"/usr/share/misc/magic.mgc"</span>, O_RDONLY) = 3</span></div></pre>
<h5 id="3-предположим-приложение-пишет-лог-в-текстовый-файл-этот-файл-оказался-удален-deleted-в-lsof-однако-возможности-сигналом-сказать-приложению-переоткрыть-файлы-или-просто-перезапустить-приложение--нет-так-как-приложение-продолжает-писать-в-удаленный-файл-место-на-диске-постепенно-заканчивается-основываясь-на-знаниях-о-перенаправлении-потоков-предложите-способ-обнуления-открытого-удаленного-файла-чтобы-освободить-место-на-файловой-системе">3. Предположим, приложение пишет лог в текстовый файл. Этот файл оказался удален (deleted в lsof), однако возможности сигналом сказать приложению переоткрыть файлы или просто перезапустить приложение – нет. Так как приложение продолжает писать в удаленный файл, место на диске постепенно заканчивается. Основываясь на знаниях о перенаправлении потоков предложите способ обнуления открытого удаленного файла (чтобы освободить место на файловой системе).</h5>
<p>По-простому не получилось, пришлось делать так:</p>
<pre class="editor-colors lang-bash"><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Создаем отдельный дескриптор с перенаправлением (для наглядности)</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">exec</span></span> <span class="syntax--constant syntax--numeric">5</span><span class="syntax--keyword syntax--operator">&gt;</span> /tmp/ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Запускаем логирование ping в файл</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">ping</span></span> 8.8.8.8 <span class="syntax--keyword syntax--operator">&gt;&amp;</span>5</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Ищем PID процесса</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">sudo</span></span> lsof <span class="syntax--keyword syntax--operator">|</span> <span class="syntax--entity syntax--name syntax--function">grep</span> ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">bash</span>      1048                       e2sly4rz    5w      REG              253,0     1081     539668 /tmp/ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">ping</span>      1187                       e2sly4rz    1w      REG              253,0     1081     539668 /tmp/ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">ping</span>      1187                       e2sly4rz    5w      REG              253,0     1081     539668 /tmp/ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Видим, что файл постепенно растет в размере</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">sudo</span></span> lsof <span class="syntax--keyword syntax--operator">|</span> <span class="syntax--entity syntax--name syntax--function">grep</span> ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">bash</span>      1048                       e2sly4rz    5w      REG              253,0     1191     539668 /tmp/ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">ping</span>      1187                       e2sly4rz    1w      REG              253,0     1191     539668 /tmp/ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">ping</span>      1187                       e2sly4rz    5w      REG              253,0     1191     539668 /tmp/ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Удаляем файл</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">rm</span></span> /tmp/ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">sudo</span></span> lsof <span class="syntax--keyword syntax--operator">|</span> <span class="syntax--entity syntax--name syntax--function">grep</span> ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">bash</span>      1048                       e2sly4rz    5w      REG              253,0     1741     539668 /tmp/ping.md (<span class="syntax--entity syntax--name syntax--function">deleted</span>)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">ping</span>      1187                       e2sly4rz    1w      REG              253,0     1741     539668 /tmp/ping.md (<span class="syntax--entity syntax--name syntax--function">deleted</span>)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">ping</span>      1187                       e2sly4rz    5w      REG              253,0     1741     539668 /tmp/ping.md (<span class="syntax--entity syntax--name syntax--function">deleted</span>)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Останавливаем ping т.к. команда судя по всему постоянно переписывает файл в полном объеме, но у нас есть "копия"</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">sudo</span></span> lsof <span class="syntax--keyword syntax--operator">|</span> <span class="syntax--entity syntax--name syntax--function">grep</span> ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">bash</span>      1048                       e2sly4rz    5w      REG              253,0     2168     539668 /tmp/ping.md (<span class="syntax--entity syntax--name syntax--function">deleted</span>)</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Обнуляем файл дескриптор</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">cat</span></span> /dev/null <span class="syntax--keyword syntax--operator">&gt;</span> /proc/1048/fd/5</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Проверяем результат</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">e2sly4rz@ubuntu:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">sudo</span></span> lsof <span class="syntax--keyword syntax--operator">|</span> <span class="syntax--entity syntax--name syntax--function">grep</span> ping.md</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">bash</span>      1048                       e2sly4rz    5w      REG              253,0        0     539668 /tmp/ping.md (<span class="syntax--entity syntax--name syntax--function">deleted</span>)</span></div></pre>
<h5 id="4-занимают-ли-зомби-процессы-какие-то-ресурсы-в-ос-cpu-ram-io">4. Занимают ли зомби-процессы какие-то ресурсы в ОС (CPU, RAM, IO)?</h5>
<p>Нет.
Зомби процессы - это завершившиеся процессы, которые ждут принятия их кода возврата.</p>
<h5 id="5-в-iovisor-bcc-есть-утилита-opensnoop">5. В iovisor BCC есть утилита opensnoop:</h5>
<pre class="editor-colors lang-bash"><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">root@vagrant:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">dpkg</span></span> <span class="syntax--entity syntax--other syntax--attribute-name">-L</span> bpfcc-tools <span class="syntax--keyword syntax--operator">|</span> <span class="syntax--entity syntax--name syntax--function">grep</span> sbin/opensnoop</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">/usr/sbin/opensnoop-bpfcc</span></span></div></pre>
<h5 id="на-какие-файлы-вы-увидели-вызовы-группы-open-за-первую-секунду-работы-утилиты-воспользуйтесь-пакетом-bpfcc-tools-для-ubuntu-2004-дополнительные-сведения-по-установке">На какие файлы вы увидели вызовы группы open за первую секунду работы утилиты? Воспользуйтесь пакетом bpfcc-tools для Ubuntu 20.04. Дополнительные сведения по установке.</h5>
<pre class="editor-colors lang-bash"><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">asamarskii@asm-tst:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">sudo</span></span> opensnoop-bpfcc <span class="syntax--entity syntax--other syntax--attribute-name">-d</span> 1</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">PID</span>    COMM               FD ERR PATH</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head                3   0 /etc/ld.so.cache</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head                3   0 /lib/x86_64-linux-gnu/libc.so.6</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head                3   0 /usr/lib/locale/locale-archive</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head                3   0 /usr/share/locale/locale.alias</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8018</span>   head                3   0 /proc/meminfo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /etc/ld.so.cache</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /lib/x86_64-linux-gnu/libc.so.6</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /usr/lib/locale/locale-archive</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /usr/share/locale/locale.alias</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /proc/stat</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /proc/version</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /proc/uptime</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /proc/loadavg</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /proc/sys/fs/file-nr</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8019</span>   head                3   0 /proc/sys/kernel/hostname</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail                3   0 /etc/ld.so.cache</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail                3   0 /lib/x86_64-linux-gnu/libc.so.6</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail                3   0 /usr/lib/locale/locale-archive</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail                3   0 /usr/share/locale/locale.alias</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail               <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8020</span>   tail                3   0 /proc/net/dev</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                  3   0 /etc/ld.so.cache</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                  3   0 /lib/x86_64-linux-gnu/libc.so.6</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                  3   0</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                  3   0 /usr/share/locale/locale.alias</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru_RU/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale/ru/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru_RU/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru.UTF-8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru.utf8/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                 <span class="syntax--entity syntax--other syntax--attribute-name">-1</span>   2 /usr/share/locale-langpack/ru/LC_MESSAGES/coreutils.mo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                  3   0 /proc/self/mountinfo</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8021</span>   df                  3   0 /usr/lib/x86_64-linux-gnu/gconv/gconv-modules.cache</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8022</span>   who                 3   0 /etc/ld.so.cache</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8022</span>   who                 3   0 /lib/x86_64-linux-gnu/libc.so.6</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8022</span>   who                 3   0 /usr/lib/locale/locale-archive</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8022</span>   who                 3   0 /var/run/utmp</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8022</span>   who                 3   0 /etc/localtime</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8023</span>   sleep               3   0 /etc/ld.so.cache</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8023</span>   sleep               3   0 /lib/x86_64-linux-gnu/libc.so.6</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">8023</span>   sleep               3   0 /usr/lib/locale/locale-archive</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">1</span>      systemd            12   0 /proc/651/cgroup</span></div></pre>
<h5 id="6-какой-системный-вызов-использует-uname--a-приведите-цитату-из-man-по-этому-системному-вызову-где-описывается-альтернативное-местоположение-в-proc-где-можно-узнать-версию-ядра-и-релиз-ос">6. Какой системный вызов использует uname -a? Приведите цитату из man по этому системному вызову, где описывается альтернативное местоположение в /proc, где можно узнать версию ядра и релиз ОС.</h5>
<p>Команда использует одноименный системный вызов:</p>
<pre class="editor-colors lang-bash"><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">asamarskii@asm-tst:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">strace</span></span> uname <span class="syntax--entity syntax--other syntax--attribute-name">-a</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">uname({sysname=<span class="syntax--string">"Linux"</span>,</span> nodename=<span class="syntax--string">"asm-tst"</span>, ...}) = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">fstat(1,</span> {st_mode=S_IFCHR<span class="syntax--keyword syntax--operator">|</span><span class="syntax--entity syntax--name syntax--function">0620,</span> st_rdev=makedev(<span class="syntax--entity syntax--name syntax--function">0x88,</span> 0)<span class="syntax--entity syntax--name syntax--function">,</span> ...}) = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">uname({sysname=<span class="syntax--string">"Linux"</span>,</span> nodename=<span class="syntax--string">"asm-tst"</span>, ...}) = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">uname({sysname=<span class="syntax--string">"Linux"</span>,</span> nodename=<span class="syntax--string">"asm-tst"</span>, ...}) = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">write(1,</span> <span class="syntax--string">"Linux asm-tst 5.4.0-99-generic #"</span>..., 106Linux asm-tst 5.4.0-99-generic <span class="syntax--comment syntax--block">#112-Ubuntu SMP Thu Feb 3 13:50:55 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux</span></span></div><div class="line"><span class="syntax--source syntax--shell">) = <span class="syntax--entity syntax--name syntax--function">106</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">close</span>(1)                                = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell">close(2)                                = <span class="syntax--variable syntax--other syntax--member">0</span></span></div><div class="line"><span class="syntax--source syntax--shell">exit_group(<span class="syntax--variable syntax--other syntax--member">0</span>)                           = <span class="syntax--variable syntax--other syntax--member">?</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">+++</span> exited with 0 +++</span></div></pre>
<p>Цитата из <code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">man 2 uname</code>:</p>
<blockquote>
<p>Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}.</p>
</blockquote>
<h5 id="7-чем-отличается-последовательность-команд-через--и-через--в-bash-например">7. Чем отличается последовательность команд через ; и через &amp;&amp; в bash? Например:</h5>
<pre class="editor-colors lang-bash"><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Команды будут выполнены последовательно не зависимо от кода возврата.</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">root@netology1:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">test</span></span> <span class="syntax--entity syntax--other syntax--attribute-name">-d</span> /tmp/some_dir; <span class="syntax--entity syntax--name syntax--function"><span class="syntax--support syntax--function">echo</span></span> Hi</span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">Hi</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Команды будут выполнены последовательно.</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--comment syntax--block"># Выполнение следующей команды произойдет только при возврате успешного статуса предыдущей команды.</span></span></div><div class="line"><span class="syntax--source syntax--shell"><span class="syntax--entity syntax--name syntax--function">root@netology1:~<span class="syntax--punctuation syntax--section syntax--embedded">$</span> <span class="syntax--variable syntax--other syntax--member">test</span></span> <span class="syntax--entity syntax--other syntax--attribute-name">-d</span> /tmp/some_dir <span class="syntax--keyword syntax--operator">&amp;&amp;</span> <span class="syntax--entity syntax--name syntax--function"><span class="syntax--support syntax--function">echo</span></span> Hi</span></div></pre>
<h5 id="есть-ли-смысл-использовать-в-bash--если-применить-set--e">Есть ли смысл использовать в bash &amp;&amp;, если применить set -e?</h5>
<p><code style="font-family: Menlo, Consolas, &quot;DejaVu Sans Mono&quot;, monospace;">set -e</code> - завершит текущую сессию оболочки при ненулевом возврате одной из комманд за исключением комманд в составе операторов while, until, if, &amp;&amp; и ||, кроме последней в списке.</p>
<p>Смысл есть т.к. поведение оболочки при &amp;&amp; будет различаться.</p>
<h5 id="8-из-каких-опций-состоит-режим-bash-set--euxo-pipefail-и-почему-его-хорошо-было-бы-использовать-в-сценариях">8. Из каких опций состоит режим bash set -euxo pipefail и почему его хорошо было бы использовать в сценариях?</h5>
<ul>
<li><strong>errexit</strong> - прекращает выполнение скрипта при ненулевом возврате одной из комманд за исключением комманд в составе операторов while, until, if, &amp;&amp; и ||, кроме последней в списке.</li>
<li><strong>nounset</strong> -прекращает выполнение скрипта, если встретилась несуществующая переменная.</li>
<li><strong>xtrace</strong> - выводит выполняемые команды в stdout перед выполненинем.</li>
<li><strong>pipefail</strong> - прекращает выполнение скрипта, даже если одна из частей | завершилась ошибкой.</li>
</ul>
<p>В целом, все опции полезны для безопасного дебага скрипта</p>
<h5 id="9-используя--o-stat-для-ps-определите-какой-наиболее-часто-встречающийся-статус-у-процессов-в-системе-в-man-ps-ознакомьтесь-process-state-codes-что-значат-дополнительные-к-основной-заглавной-буквы-статуса-процессов-его-можно-не-учитывать-при-расчете-считать-s-ss-или-ssl-равнозначными">9. Используя -o stat для ps, определите, какой наиболее часто встречающийся статус у процессов в системе. В man ps ознакомьтесь (/PROCESS STATE CODES) что значат дополнительные к основной заглавной буквы статуса процессов. Его можно не учитывать при расчете (считать S, Ss или Ssl равнозначными).</h5>
<p>Большинство процессов имеют статус:</p>
<ul>
<li>I&lt; - высокоприоритетные системные процессы</li>
<li>S  - в ожидании (прерывистый сон)</li>
</ul></body>
      </html>
