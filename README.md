<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />

<title>Predicting Building Energy Loads</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>



<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.7 (http://getbootstrap.com)
 * Copyright 2011-2016 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  color: #337ab7;
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.7.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
@font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.7.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.7.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff2?v=4.7.0') format('woff2'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.7.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.7.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.7.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
}
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.fa-pull-left {
  float: left;
}
.fa-pull-right {
  float: right;
}
.fa.fa-pull-left {
  margin-right: .3em;
}
.fa.fa-pull-right {
  margin-left: .3em;
}
/* Deprecated as of 4.4.0 */
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
.fa-pulse {
  -webkit-animation: fa-spin 1s infinite steps(8);
  animation: fa-spin 1s infinite steps(8);
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=1)";
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=2)";
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=3)";
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1)";
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1)";
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook-f:before,
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-feed:before,
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before,
.fa-gratipay:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper-pp:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-resistance:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-y-combinator-square:before,
.fa-yc-square:before,
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
.fa-buysellads:before {
  content: "\f20d";
}
.fa-connectdevelop:before {
  content: "\f20e";
}
.fa-dashcube:before {
  content: "\f210";
}
.fa-forumbee:before {
  content: "\f211";
}
.fa-leanpub:before {
  content: "\f212";
}
.fa-sellsy:before {
  content: "\f213";
}
.fa-shirtsinbulk:before {
  content: "\f214";
}
.fa-simplybuilt:before {
  content: "\f215";
}
.fa-skyatlas:before {
  content: "\f216";
}
.fa-cart-plus:before {
  content: "\f217";
}
.fa-cart-arrow-down:before {
  content: "\f218";
}
.fa-diamond:before {
  content: "\f219";
}
.fa-ship:before {
  content: "\f21a";
}
.fa-user-secret:before {
  content: "\f21b";
}
.fa-motorcycle:before {
  content: "\f21c";
}
.fa-street-view:before {
  content: "\f21d";
}
.fa-heartbeat:before {
  content: "\f21e";
}
.fa-venus:before {
  content: "\f221";
}
.fa-mars:before {
  content: "\f222";
}
.fa-mercury:before {
  content: "\f223";
}
.fa-intersex:before,
.fa-transgender:before {
  content: "\f224";
}
.fa-transgender-alt:before {
  content: "\f225";
}
.fa-venus-double:before {
  content: "\f226";
}
.fa-mars-double:before {
  content: "\f227";
}
.fa-venus-mars:before {
  content: "\f228";
}
.fa-mars-stroke:before {
  content: "\f229";
}
.fa-mars-stroke-v:before {
  content: "\f22a";
}
.fa-mars-stroke-h:before {
  content: "\f22b";
}
.fa-neuter:before {
  content: "\f22c";
}
.fa-genderless:before {
  content: "\f22d";
}
.fa-facebook-official:before {
  content: "\f230";
}
.fa-pinterest-p:before {
  content: "\f231";
}
.fa-whatsapp:before {
  content: "\f232";
}
.fa-server:before {
  content: "\f233";
}
.fa-user-plus:before {
  content: "\f234";
}
.fa-user-times:before {
  content: "\f235";
}
.fa-hotel:before,
.fa-bed:before {
  content: "\f236";
}
.fa-viacoin:before {
  content: "\f237";
}
.fa-train:before {
  content: "\f238";
}
.fa-subway:before {
  content: "\f239";
}
.fa-medium:before {
  content: "\f23a";
}
.fa-yc:before,
.fa-y-combinator:before {
  content: "\f23b";
}
.fa-optin-monster:before {
  content: "\f23c";
}
.fa-opencart:before {
  content: "\f23d";
}
.fa-expeditedssl:before {
  content: "\f23e";
}
.fa-battery-4:before,
.fa-battery:before,
.fa-battery-full:before {
  content: "\f240";
}
.fa-battery-3:before,
.fa-battery-three-quarters:before {
  content: "\f241";
}
.fa-battery-2:before,
.fa-battery-half:before {
  content: "\f242";
}
.fa-battery-1:before,
.fa-battery-quarter:before {
  content: "\f243";
}
.fa-battery-0:before,
.fa-battery-empty:before {
  content: "\f244";
}
.fa-mouse-pointer:before {
  content: "\f245";
}
.fa-i-cursor:before {
  content: "\f246";
}
.fa-object-group:before {
  content: "\f247";
}
.fa-object-ungroup:before {
  content: "\f248";
}
.fa-sticky-note:before {
  content: "\f249";
}
.fa-sticky-note-o:before {
  content: "\f24a";
}
.fa-cc-jcb:before {
  content: "\f24b";
}
.fa-cc-diners-club:before {
  content: "\f24c";
}
.fa-clone:before {
  content: "\f24d";
}
.fa-balance-scale:before {
  content: "\f24e";
}
.fa-hourglass-o:before {
  content: "\f250";
}
.fa-hourglass-1:before,
.fa-hourglass-start:before {
  content: "\f251";
}
.fa-hourglass-2:before,
.fa-hourglass-half:before {
  content: "\f252";
}
.fa-hourglass-3:before,
.fa-hourglass-end:before {
  content: "\f253";
}
.fa-hourglass:before {
  content: "\f254";
}
.fa-hand-grab-o:before,
.fa-hand-rock-o:before {
  content: "\f255";
}
.fa-hand-stop-o:before,
.fa-hand-paper-o:before {
  content: "\f256";
}
.fa-hand-scissors-o:before {
  content: "\f257";
}
.fa-hand-lizard-o:before {
  content: "\f258";
}
.fa-hand-spock-o:before {
  content: "\f259";
}
.fa-hand-pointer-o:before {
  content: "\f25a";
}
.fa-hand-peace-o:before {
  content: "\f25b";
}
.fa-trademark:before {
  content: "\f25c";
}
.fa-registered:before {
  content: "\f25d";
}
.fa-creative-commons:before {
  content: "\f25e";
}
.fa-gg:before {
  content: "\f260";
}
.fa-gg-circle:before {
  content: "\f261";
}
.fa-tripadvisor:before {
  content: "\f262";
}
.fa-odnoklassniki:before {
  content: "\f263";
}
.fa-odnoklassniki-square:before {
  content: "\f264";
}
.fa-get-pocket:before {
  content: "\f265";
}
.fa-wikipedia-w:before {
  content: "\f266";
}
.fa-safari:before {
  content: "\f267";
}
.fa-chrome:before {
  content: "\f268";
}
.fa-firefox:before {
  content: "\f269";
}
.fa-opera:before {
  content: "\f26a";
}
.fa-internet-explorer:before {
  content: "\f26b";
}
.fa-tv:before,
.fa-television:before {
  content: "\f26c";
}
.fa-contao:before {
  content: "\f26d";
}
.fa-500px:before {
  content: "\f26e";
}
.fa-amazon:before {
  content: "\f270";
}
.fa-calendar-plus-o:before {
  content: "\f271";
}
.fa-calendar-minus-o:before {
  content: "\f272";
}
.fa-calendar-times-o:before {
  content: "\f273";
}
.fa-calendar-check-o:before {
  content: "\f274";
}
.fa-industry:before {
  content: "\f275";
}
.fa-map-pin:before {
  content: "\f276";
}
.fa-map-signs:before {
  content: "\f277";
}
.fa-map-o:before {
  content: "\f278";
}
.fa-map:before {
  content: "\f279";
}
.fa-commenting:before {
  content: "\f27a";
}
.fa-commenting-o:before {
  content: "\f27b";
}
.fa-houzz:before {
  content: "\f27c";
}
.fa-vimeo:before {
  content: "\f27d";
}
.fa-black-tie:before {
  content: "\f27e";
}
.fa-fonticons:before {
  content: "\f280";
}
.fa-reddit-alien:before {
  content: "\f281";
}
.fa-edge:before {
  content: "\f282";
}
.fa-credit-card-alt:before {
  content: "\f283";
}
.fa-codiepie:before {
  content: "\f284";
}
.fa-modx:before {
  content: "\f285";
}
.fa-fort-awesome:before {
  content: "\f286";
}
.fa-usb:before {
  content: "\f287";
}
.fa-product-hunt:before {
  content: "\f288";
}
.fa-mixcloud:before {
  content: "\f289";
}
.fa-scribd:before {
  content: "\f28a";
}
.fa-pause-circle:before {
  content: "\f28b";
}
.fa-pause-circle-o:before {
  content: "\f28c";
}
.fa-stop-circle:before {
  content: "\f28d";
}
.fa-stop-circle-o:before {
  content: "\f28e";
}
.fa-shopping-bag:before {
  content: "\f290";
}
.fa-shopping-basket:before {
  content: "\f291";
}
.fa-hashtag:before {
  content: "\f292";
}
.fa-bluetooth:before {
  content: "\f293";
}
.fa-bluetooth-b:before {
  content: "\f294";
}
.fa-percent:before {
  content: "\f295";
}
.fa-gitlab:before {
  content: "\f296";
}
.fa-wpbeginner:before {
  content: "\f297";
}
.fa-wpforms:before {
  content: "\f298";
}
.fa-envira:before {
  content: "\f299";
}
.fa-universal-access:before {
  content: "\f29a";
}
.fa-wheelchair-alt:before {
  content: "\f29b";
}
.fa-question-circle-o:before {
  content: "\f29c";
}
.fa-blind:before {
  content: "\f29d";
}
.fa-audio-description:before {
  content: "\f29e";
}
.fa-volume-control-phone:before {
  content: "\f2a0";
}
.fa-braille:before {
  content: "\f2a1";
}
.fa-assistive-listening-systems:before {
  content: "\f2a2";
}
.fa-asl-interpreting:before,
.fa-american-sign-language-interpreting:before {
  content: "\f2a3";
}
.fa-deafness:before,
.fa-hard-of-hearing:before,
.fa-deaf:before {
  content: "\f2a4";
}
.fa-glide:before {
  content: "\f2a5";
}
.fa-glide-g:before {
  content: "\f2a6";
}
.fa-signing:before,
.fa-sign-language:before {
  content: "\f2a7";
}
.fa-low-vision:before {
  content: "\f2a8";
}
.fa-viadeo:before {
  content: "\f2a9";
}
.fa-viadeo-square:before {
  content: "\f2aa";
}
.fa-snapchat:before {
  content: "\f2ab";
}
.fa-snapchat-ghost:before {
  content: "\f2ac";
}
.fa-snapchat-square:before {
  content: "\f2ad";
}
.fa-pied-piper:before {
  content: "\f2ae";
}
.fa-first-order:before {
  content: "\f2b0";
}
.fa-yoast:before {
  content: "\f2b1";
}
.fa-themeisle:before {
  content: "\f2b2";
}
.fa-google-plus-circle:before,
.fa-google-plus-official:before {
  content: "\f2b3";
}
.fa-fa:before,
.fa-font-awesome:before {
  content: "\f2b4";
}
.fa-handshake-o:before {
  content: "\f2b5";
}
.fa-envelope-open:before {
  content: "\f2b6";
}
.fa-envelope-open-o:before {
  content: "\f2b7";
}
.fa-linode:before {
  content: "\f2b8";
}
.fa-address-book:before {
  content: "\f2b9";
}
.fa-address-book-o:before {
  content: "\f2ba";
}
.fa-vcard:before,
.fa-address-card:before {
  content: "\f2bb";
}
.fa-vcard-o:before,
.fa-address-card-o:before {
  content: "\f2bc";
}
.fa-user-circle:before {
  content: "\f2bd";
}
.fa-user-circle-o:before {
  content: "\f2be";
}
.fa-user-o:before {
  content: "\f2c0";
}
.fa-id-badge:before {
  content: "\f2c1";
}
.fa-drivers-license:before,
.fa-id-card:before {
  content: "\f2c2";
}
.fa-drivers-license-o:before,
.fa-id-card-o:before {
  content: "\f2c3";
}
.fa-quora:before {
  content: "\f2c4";
}
.fa-free-code-camp:before {
  content: "\f2c5";
}
.fa-telegram:before {
  content: "\f2c6";
}
.fa-thermometer-4:before,
.fa-thermometer:before,
.fa-thermometer-full:before {
  content: "\f2c7";
}
.fa-thermometer-3:before,
.fa-thermometer-three-quarters:before {
  content: "\f2c8";
}
.fa-thermometer-2:before,
.fa-thermometer-half:before {
  content: "\f2c9";
}
.fa-thermometer-1:before,
.fa-thermometer-quarter:before {
  content: "\f2ca";
}
.fa-thermometer-0:before,
.fa-thermometer-empty:before {
  content: "\f2cb";
}
.fa-shower:before {
  content: "\f2cc";
}
.fa-bathtub:before,
.fa-s15:before,
.fa-bath:before {
  content: "\f2cd";
}
.fa-podcast:before {
  content: "\f2ce";
}
.fa-window-maximize:before {
  content: "\f2d0";
}
.fa-window-minimize:before {
  content: "\f2d1";
}
.fa-window-restore:before {
  content: "\f2d2";
}
.fa-times-rectangle:before,
.fa-window-close:before {
  content: "\f2d3";
}
.fa-times-rectangle-o:before,
.fa-window-close-o:before {
  content: "\f2d4";
}
.fa-bandcamp:before {
  content: "\f2d5";
}
.fa-grav:before {
  content: "\f2d6";
}
.fa-etsy:before {
  content: "\f2d7";
}
.fa-imdb:before {
  content: "\f2d8";
}
.fa-ravelry:before {
  content: "\f2d9";
}
.fa-eercast:before {
  content: "\f2da";
}
.fa-microchip:before {
  content: "\f2db";
}
.fa-snowflake-o:before {
  content: "\f2dc";
}
.fa-superpowers:before {
  content: "\f2dd";
}
.fa-wpexplorer:before {
  content: "\f2de";
}
.fa-meetup:before {
  content: "\f2e0";
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
div.traceback-wrapper pre.traceback {
  max-height: 600px;
  overflow: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 5px;
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
[dir="rtl"] #ipython_notebook {
  margin-right: 10px;
  margin-left: 0;
}
[dir="rtl"] #ipython_notebook.pull-left {
  float: right !important;
  float: right;
}
.flex-spacer {
  flex: 1;
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#kernel_logo_widget {
  margin: 0 10px;
}
span#login_widget {
  float: right;
}
[dir="rtl"] span#login_widget {
  float: left;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
.modal-header {
  cursor: move;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
[dir="rtl"] .center-nav form.pull-left {
  float: right !important;
  float: right;
}
[dir="rtl"] .center-nav .navbar-text {
  float: right;
}
[dir="rtl"] .navbar-inner {
  text-align: right;
}
[dir="rtl"] div.text-left {
  text-align: right;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  position: absolute;
  display: block;
  width: 100%;
  height: 100%;
  overflow: hidden;
  cursor: pointer;
  opacity: 0;
  z-index: 2;
}
.alternate_upload .btn-xs > input.fileinput {
  margin: -1px -5px;
}
.alternate_upload .btn-upload {
  position: relative;
  height: 22px;
}
::-webkit-file-upload-button {
  cursor: pointer;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
ul#tabs {
  margin-bottom: 4px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
[dir="rtl"] ul#tabs.nav-tabs > li {
  float: right;
}
[dir="rtl"] ul#tabs.nav.nav-tabs {
  padding-right: 0;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
[dir="rtl"] .list_toolbar .tree-buttons .pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .list_toolbar .col-sm-4,
[dir="rtl"] .list_toolbar .col-sm-8 {
  float: right;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: text-bottom;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
[dir="rtl"] .list_item > div input {
  margin-right: 0;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_modified {
  margin-right: 7px;
  margin-left: 7px;
}
[dir="rtl"] .item_modified.pull-right {
  float: left !important;
  float: left;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
[dir="rtl"] .item_buttons.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .item_buttons .kernel-name {
  margin-left: 7px;
  float: right;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
.sort_button {
  display: inline-block;
  padding-left: 7px;
}
[dir="rtl"] .sort_button.pull-right {
  float: left !important;
  float: left;
}
#tree-selector {
  padding-right: 0px;
}
#button-select-all {
  min-width: 50px;
}
[dir="rtl"] #button-select-all.btn {
  float: right ;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
  margin-top: 2px;
  height: 16px;
}
[dir="rtl"] #select-all.pull-left {
  float: right !important;
  float: right;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.fa-pull-left {
  margin-right: .3em;
}
.folder_icon:before.fa-pull-right {
  margin-left: .3em;
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.fa-pull-left {
  margin-right: .3em;
}
.notebook_icon:before.fa-pull-right {
  margin-left: .3em;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.fa-pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.fa-pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.fa-pull-left {
  margin-right: .3em;
}
.file_icon:before.fa-pull-right {
  margin-left: .3em;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
#new-menu .dropdown-header {
  font-size: 10px;
  border-bottom: 1px solid #e5e5e5;
  padding: 0 0 3px;
  margin: -3px 20px 0;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.move-button {
  display: none;
}
.download-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
.CodeMirror-dialog {
  background-color: #fff;
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI escape sequences */
/* The color values are a mix of
   http://www.xcolors.net/dl/baskerville-ivorylight and
   http://www.xcolors.net/dl/euphrasia */
.ansi-black-fg {
  color: #3E424D;
}
.ansi-black-bg {
  background-color: #3E424D;
}
.ansi-black-intense-fg {
  color: #282C36;
}
.ansi-black-intense-bg {
  background-color: #282C36;
}
.ansi-red-fg {
  color: #E75C58;
}
.ansi-red-bg {
  background-color: #E75C58;
}
.ansi-red-intense-fg {
  color: #B22B31;
}
.ansi-red-intense-bg {
  background-color: #B22B31;
}
.ansi-green-fg {
  color: #00A250;
}
.ansi-green-bg {
  background-color: #00A250;
}
.ansi-green-intense-fg {
  color: #007427;
}
.ansi-green-intense-bg {
  background-color: #007427;
}
.ansi-yellow-fg {
  color: #DDB62B;
}
.ansi-yellow-bg {
  background-color: #DDB62B;
}
.ansi-yellow-intense-fg {
  color: #B27D12;
}
.ansi-yellow-intense-bg {
  background-color: #B27D12;
}
.ansi-blue-fg {
  color: #208FFB;
}
.ansi-blue-bg {
  background-color: #208FFB;
}
.ansi-blue-intense-fg {
  color: #0065CA;
}
.ansi-blue-intense-bg {
  background-color: #0065CA;
}
.ansi-magenta-fg {
  color: #D160C4;
}
.ansi-magenta-bg {
  background-color: #D160C4;
}
.ansi-magenta-intense-fg {
  color: #A03196;
}
.ansi-magenta-intense-bg {
  background-color: #A03196;
}
.ansi-cyan-fg {
  color: #60C6C8;
}
.ansi-cyan-bg {
  background-color: #60C6C8;
}
.ansi-cyan-intense-fg {
  color: #258F8F;
}
.ansi-cyan-intense-bg {
  background-color: #258F8F;
}
.ansi-white-fg {
  color: #C5C1B4;
}
.ansi-white-bg {
  background-color: #C5C1B4;
}
.ansi-white-intense-fg {
  color: #A1A6B2;
}
.ansi-white-intense-bg {
  background-color: #A1A6B2;
}
.ansi-default-inverse-fg {
  color: #FFFFFF;
}
.ansi-default-inverse-bg {
  background-color: #000000;
}
.ansi-bold {
  font-weight: bold;
}
.ansi-underline {
  text-decoration: underline;
}
/* The following styles are deprecated an will be removed in a future version */
.ansibold {
  font-weight: bold;
}
.ansi-inverse {
  outline: 0.5px dotted;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  position: relative;
  overflow: visible;
}
div.cell:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: transparent;
}
div.cell.jupyter-soft-selected {
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected,
div.cell.selected.jupyter-soft-selected {
  border-color: #ababab;
}
div.cell.selected:before,
div.cell.selected.jupyter-soft-selected:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: #42A5F5;
}
@media print {
  div.cell.selected,
  div.cell.selected.jupyter-soft-selected {
    border-color: transparent;
  }
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
}
.edit_mode div.cell.selected:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: #66BB6A;
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  min-width: 0;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  /* Note that this should set vertical padding only, since CodeMirror assumes
       that horizontal padding will be set on CodeMirror pre */
  padding: 0.4em 0;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. This sets horizontal padding only,
    use .CodeMirror-lines for vertical */
  padding: 0 0.4em;
  border: 0;
  border-radius: 0;
}
.CodeMirror-cursor {
  border-left: 1.4px solid black;
}
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .CodeMirror-cursor {
    border-left: 2px solid black;
  }
}
@media screen and (min-width: 4320px) {
  .CodeMirror-cursor {
    border-left: 4px solid black;
  }
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
div.output_area .mglyph > img {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 1px 0 1px 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul:not(.list-inline),
.rendered_html ol:not(.list-inline) {
  padding-left: 2em;
}
.rendered_html ul {
  list-style: disc;
}
.rendered_html ul ul {
  list-style: square;
  margin-top: 0;
}
.rendered_html ul ul ul {
  list-style: circle;
}
.rendered_html ol {
  list-style: decimal;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin-top: 0;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
  padding: 0px;
  background-color: #fff;
}
.rendered_html code {
  background-color: #eff0f1;
}
.rendered_html p code {
  padding: 1px 5px;
}
.rendered_html pre code {
  background-color: #fff;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  color: #000;
  font-size: 100%;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: none;
  border-collapse: collapse;
  border-spacing: 0;
  color: black;
  font-size: 12px;
  table-layout: fixed;
}
.rendered_html thead {
  border-bottom: 1px solid black;
  vertical-align: bottom;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  text-align: right;
  vertical-align: middle;
  padding: 0.5em 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html tbody tr:nth-child(odd) {
  background: #f5f5f5;
}
.rendered_html tbody tr:hover {
  background: rgba(66, 165, 245, 0.2);
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
.rendered_html .alert {
  margin-bottom: initial;
}
.rendered_html * + .alert {
  margin-top: 1em;
}
[dir="rtl"] .rendered_html p {
  text-align: right;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.rendered .rendered_html tr,
.text_cell.rendered .rendered_html th,
.text_cell.rendered .rendered_html td {
  max-width: none;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.text_cell .dropzone .input_area {
  border: 2px dashed #bababa;
  margin: -1px;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
.jupyter-keybindings {
  padding: 1px;
  line-height: 24px;
  border-bottom: 1px solid gray;
}
.jupyter-keybindings input {
  margin: 0;
  padding: 0;
  border: none;
}
.jupyter-keybindings i {
  padding: 6px;
}
.well code {
  background-color: #ffffff;
  border-color: #ababab;
  border-width: 1px;
  border-style: solid;
  padding: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.tags_button_container {
  width: 100%;
  display: flex;
}
.tag-container {
  display: flex;
  flex-direction: row;
  flex-grow: 1;
  overflow: hidden;
  position: relative;
}
.tag-container > * {
  margin: 0 4px;
}
.remove-tag-btn {
  margin-left: 4px;
}
.tags-input {
  display: flex;
}
.cell-tag:last-child:after {
  content: "";
  position: absolute;
  right: 0;
  width: 40px;
  height: 100%;
  /* Fade to background color of cell toolbar */
  background: linear-gradient(to right, rgba(0, 0, 0, 0), #EEE);
}
.tags-input > * {
  margin-left: 4px;
}
.cell-tag,
.tags-input input,
.tags-input button {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  box-shadow: none;
  width: inherit;
  font-size: inherit;
  height: 22px;
  line-height: 22px;
  padding: 0px 4px;
  display: inline-block;
}
.cell-tag:focus,
.tags-input input:focus,
.tags-input button:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.cell-tag::-moz-placeholder,
.tags-input input::-moz-placeholder,
.tags-input button::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.cell-tag:-ms-input-placeholder,
.tags-input input:-ms-input-placeholder,
.tags-input button:-ms-input-placeholder {
  color: #999;
}
.cell-tag::-webkit-input-placeholder,
.tags-input input::-webkit-input-placeholder,
.tags-input button::-webkit-input-placeholder {
  color: #999;
}
.cell-tag::-ms-expand,
.tags-input input::-ms-expand,
.tags-input button::-ms-expand {
  border: 0;
  background-color: transparent;
}
.cell-tag[disabled],
.tags-input input[disabled],
.tags-input button[disabled],
.cell-tag[readonly],
.tags-input input[readonly],
.tags-input button[readonly],
fieldset[disabled] .cell-tag,
fieldset[disabled] .tags-input input,
fieldset[disabled] .tags-input button {
  background-color: #eeeeee;
  opacity: 1;
}
.cell-tag[disabled],
.tags-input input[disabled],
.tags-input button[disabled],
fieldset[disabled] .cell-tag,
fieldset[disabled] .tags-input input,
fieldset[disabled] .tags-input button {
  cursor: not-allowed;
}
textarea.cell-tag,
textarea.tags-input input,
textarea.tags-input button {
  height: auto;
}
select.cell-tag,
select.tags-input input,
select.tags-input button {
  height: 30px;
  line-height: 30px;
}
textarea.cell-tag,
textarea.tags-input input,
textarea.tags-input button,
select[multiple].cell-tag,
select[multiple].tags-input input,
select[multiple].tags-input button {
  height: auto;
}
.cell-tag,
.tags-input button {
  padding: 0px 4px;
}
.cell-tag {
  background-color: #fff;
  white-space: nowrap;
}
.tags-input input[type=text]:focus {
  outline: none;
  box-shadow: none;
  border-color: #ccc;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
[dir="rtl"] #kernel_logo_widget {
  float: left !important;
  float: left;
}
.modal .modal-body .move-path {
  display: flex;
  flex-direction: row;
  justify-content: space;
  align-items: center;
}
.modal .modal-body .move-path .server-root {
  padding-right: 20px;
}
.modal .modal-body .move-path .path-input {
  flex: 1;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
[dir="rtl"] #menubar .navbar-toggle {
  float: right;
}
[dir="rtl"] #menubar .navbar-collapse {
  clear: right;
}
[dir="rtl"] #menubar .navbar-nav {
  float: right;
}
[dir="rtl"] #menubar .nav {
  padding-right: 0px;
}
[dir="rtl"] #menubar .navbar-nav > li {
  float: right;
}
[dir="rtl"] #menubar .navbar-right {
  float: left !important;
}
[dir="rtl"] ul.dropdown-menu {
  text-align: right;
  left: auto;
}
[dir="rtl"] ul#new-menu.dropdown-menu {
  right: auto;
  left: 0;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
[dir="rtl"] i.menu-icon.pull-right {
  float: left !important;
  float: left;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
[dir="rtl"] ul#help_menu li a {
  padding-left: 2.2em;
}
[dir="rtl"] ul#help_menu li a i {
  margin-right: 0;
  margin-left: -1.2em;
}
[dir="rtl"] ul#help_menu li a i.pull-right {
  float: left !important;
  float: left;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
[dir="rtl"] .dropdown-submenu > .dropdown-menu {
  right: 100%;
  margin-right: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.fa-pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.fa-pull-right {
  margin-left: .3em;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
[dir="rtl"] .dropdown-submenu > a:after {
  float: left;
  content: "\f0d9";
  margin-right: 0;
  margin-left: -10px;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
[dir="rtl"] #notification_area {
  float: left !important;
  float: left;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
[dir="rtl"] .indicator_area {
  float: left !important;
  float: left;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
[dir="rtl"] #kernel_indicator {
  float: left !important;
  float: left;
  border-left: 0;
  border-right: 1px solid;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
[dir="rtl"] #modal_indicator {
  float: left !important;
  float: left;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.fa-pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.fa-pull-right {
  margin-left: .3em;
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.fa-pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.fa-pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 21ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  height: 30px;
  margin-top: 4px;
  display: flex;
  justify-content: flex-start;
  align-items: baseline;
  width: 50%;
  flex: 1;
}
span.save_widget span.filename {
  height: 100%;
  line-height: 1em;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
[dir="rtl"] span.save_widget.pull-left {
  float: right !important;
  float: right;
}
[dir="rtl"] span.save_widget span.filename {
  margin-left: 0;
  margin-right: 16px;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
  white-space: nowrap;
  padding: 0 5px;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
    padding: 0 0 0 5px;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
.toolbar-btn-label {
  margin-left: 6px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
[dir="rtl"] .btn-group > .btn,
.btn-group-vertical > .btn {
  float: right;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
[dir="rtl"] ul.typeahead-list i {
  margin-left: 0;
  margin-right: -10px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
ul.typeahead-list  > li > a.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .typeahead-list {
  text-align: right;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  min-width: 20px;
  color: transparent;
}
[dir="rtl"] .no-shortcut.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .command-shortcut.pull-right {
  float: left !important;
  float: left;
}
.command-shortcut:before {
  content: "(command mode)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
[dir="rtl"] .edit-shortcut.pull-right {
  float: left !important;
  float: left;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
[dir="ltr"] #find-and-replace .input-group-btn + .form-control {
  border-left: none;
}
[dir="rtl"] #find-and-replace .input-group-btn + .form-control {
  border-right: none;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  width: 100%;
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal .xterm-rows {
  padding: 10px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sa { color: #BA2121 } /* Literal.String.Affix */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .dl { color: #BA2121 } /* Literal.String.Delimiter */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .fm { color: #0000FF } /* Name.Function.Magic */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .vm { color: #19177C } /* Name.Variable.Magic */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Comparing building heating and cooling loads with respect to building characteristics. The data contains 768 different building shapes and 8 characteristics.  The goal is to use the 8 building features to predict the heating and cooling load. The features are:</p>
<ul>
<li>relative compactness</li>
<li>surface area - in meters squared</li>
<li>wall area - in meters squared</li>
<li>roof area - in meters squared</li>
<li>overall height - in meters</li>
<li>orientation - 2: North, 3: East, 4: South, 5: West</li>
<li>glazing area - as a percentage of the floor area - 0%, 10%, 25%, and 40%</li>
<li>glazing area distribution: <ul>
<li>0: uniform - with 25% glazing on each side</li>
<li>1: north - 55% on the north side and 15% on each of the other sides</li>
<li>2: east - 55% on the east side and 15% on each of the other sides</li>
<li>3: south - 55% on the south side and 15% on each of the other sides</li>
<li>4: west - 55% on the west side and 15% on each of the other sides</li>
</ul>
</li>
</ul>
<p>The values to predict are the heating and cooling loads listed in kWh/m2.</p>
<p>12 buildings were modeled with different shapes, surface areas and dimensions.  The overall volume was kept the same for each building at 772 meters squared.  Considering twelve building forms with three glazing area variations, six glazing area distributions each (5 distributions + 1 with no glazing), for four orientations, we obtain 12 × 3 × 6 × 4 = 768 different building variations.</p>
<p>The dataset, which can be found <a href="https://archive.ics.uci.edu/ml/datasets/Energy+efficiency">here</a> was donated to the University of California at Irving.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>

<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="k">import</span> <span class="n">RandomForestRegressor</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">train_test_split</span>

<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;Energy data.csv&#39;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;relative_compactness&#39;</span><span class="p">,</span> <span class="s1">&#39;surface_area&#39;</span><span class="p">,</span> <span class="s1">&#39;wall_area&#39;</span><span class="p">,</span> <span class="s1">&#39;roof_area&#39;</span><span class="p">,</span> <span class="s1">&#39;overall_height&#39;</span><span class="p">,</span>
                <span class="s1">&#39;orientation&#39;</span><span class="p">,</span> <span class="s1">&#39;glazing_area&#39;</span><span class="p">,</span> <span class="s1">&#39;glazing_area_distribution&#39;</span><span class="p">,</span> <span class="s1">&#39;heating_load&#39;</span><span class="p">,</span> <span class="s1">&#39;cooling_load&#39;</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[4]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
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
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
      <th>heating_load</th>
      <th>cooling_load</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.55</td>
      <td>21.33</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.55</td>
      <td>21.33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>4</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.55</td>
      <td>21.33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>5</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.55</td>
      <td>21.33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.90</td>
      <td>563.5</td>
      <td>318.5</td>
      <td>122.50</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>20.84</td>
      <td>28.28</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[5]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
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
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
      <th>heating_load</th>
      <th>cooling_load</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.00000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.00000</td>
      <td>768.000000</td>
      <td>768.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.764167</td>
      <td>671.708333</td>
      <td>318.500000</td>
      <td>176.604167</td>
      <td>5.25000</td>
      <td>3.500000</td>
      <td>0.234375</td>
      <td>2.81250</td>
      <td>22.307201</td>
      <td>24.587760</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.105777</td>
      <td>88.086116</td>
      <td>43.626481</td>
      <td>45.165950</td>
      <td>1.75114</td>
      <td>1.118763</td>
      <td>0.133221</td>
      <td>1.55096</td>
      <td>10.090196</td>
      <td>9.513306</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.620000</td>
      <td>514.500000</td>
      <td>245.000000</td>
      <td>110.250000</td>
      <td>3.50000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>6.010000</td>
      <td>10.900000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.682500</td>
      <td>606.375000</td>
      <td>294.000000</td>
      <td>140.875000</td>
      <td>3.50000</td>
      <td>2.750000</td>
      <td>0.100000</td>
      <td>1.75000</td>
      <td>12.992500</td>
      <td>15.620000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.750000</td>
      <td>673.750000</td>
      <td>318.500000</td>
      <td>183.750000</td>
      <td>5.25000</td>
      <td>3.500000</td>
      <td>0.250000</td>
      <td>3.00000</td>
      <td>18.950000</td>
      <td>22.080000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.830000</td>
      <td>741.125000</td>
      <td>343.000000</td>
      <td>220.500000</td>
      <td>7.00000</td>
      <td>4.250000</td>
      <td>0.400000</td>
      <td>4.00000</td>
      <td>31.667500</td>
      <td>33.132500</td>
    </tr>
    <tr>
      <th>max</th>
      <td>0.980000</td>
      <td>808.500000</td>
      <td>416.500000</td>
      <td>220.500000</td>
      <td>7.00000</td>
      <td>5.000000</td>
      <td>0.400000</td>
      <td>5.00000</td>
      <td>43.100000</td>
      <td>48.030000</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>To simplify the model, we'll sum heating and cooling load into a new column called "energy load". Then we'll eliminate the heating and cooling load columns.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data_new</span> <span class="o">=</span> <span class="n">data</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data_new</span><span class="p">[</span><span class="s1">&#39;energy load&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">data</span><span class="p">[</span><span class="s1">&#39;heating_load&#39;</span><span class="p">]</span> <span class="o">+</span> <span class="n">data</span><span class="p">[</span><span class="s1">&#39;cooling_load&#39;</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data_new</span> <span class="o">=</span> <span class="n">data_new</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">&#39;heating_load&#39;</span><span class="p">,</span> <span class="s1">&#39;cooling_load&#39;</span><span class="p">])</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The new dataset:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data_new</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[9]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
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
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
      <th>energy load</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.88</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.88</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Correlation between variables</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Setting the format for diplaying the correlation table</span>
<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.float_format&#39;</span><span class="p">,</span> <span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s1">&#39;</span><span class="si">{:,.3f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data_new</span><span class="o">.</span><span class="n">corr</span><span class="p">()</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="s1">&#39;energy load&#39;</span><span class="p">,</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[11]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
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
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
      <th>energy load</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>energy load</th>
      <td>0.632</td>
      <td>-0.669</td>
      <td>0.445</td>
      <td>-0.867</td>
      <td>0.898</td>
      <td>0.006</td>
      <td>0.241</td>
      <td>0.070</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>overall_height</th>
      <td>0.828</td>
      <td>-0.858</td>
      <td>0.281</td>
      <td>-0.973</td>
      <td>1.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.898</td>
    </tr>
    <tr>
      <th>relative_compactness</th>
      <td>1.000</td>
      <td>-0.992</td>
      <td>-0.204</td>
      <td>-0.869</td>
      <td>0.828</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.632</td>
    </tr>
    <tr>
      <th>wall_area</th>
      <td>-0.204</td>
      <td>0.196</td>
      <td>1.000</td>
      <td>-0.292</td>
      <td>0.281</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>0.000</td>
      <td>0.445</td>
    </tr>
    <tr>
      <th>glazing_area</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>-0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.213</td>
      <td>0.241</td>
    </tr>
    <tr>
      <th>glazing_area_distribution</th>
      <td>0.000</td>
      <td>-0.000</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.213</td>
      <td>1.000</td>
      <td>0.070</td>
    </tr>
    <tr>
      <th>orientation</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.006</td>
    </tr>
    <tr>
      <th>surface_area</th>
      <td>-0.992</td>
      <td>1.000</td>
      <td>0.196</td>
      <td>0.881</td>
      <td>-0.858</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>-0.669</td>
    </tr>
    <tr>
      <th>roof_area</th>
      <td>-0.869</td>
      <td>0.881</td>
      <td>-0.292</td>
      <td>1.000</td>
      <td>-0.973</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>-0.000</td>
      <td>-0.867</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span><span class="mi">12</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">heatmap</span><span class="p">(</span><span class="n">data_new</span><span class="o">.</span><span class="n">corr</span><span class="p">(),</span> <span class="n">annot</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">linewidths</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">linecolor</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">);</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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j4CP8mjntbzLIfa/FMg5CP6+0PIpwJT92n4MfJzHPq4+2DFEREREJLKpwyAiIiIi4krkaKASQR2Go4CZ9SB469WcVjjn/vkDOUVEREQkrNRhOAo4574nOBlaRERERKRYqcMgIiIiIhFPk5696YvbRERERETEkyoMIiIiIhLxXECTnr2owiAiIiIiIp7UYRAREREREU8akiQiIiIiEU+Tnr2pwiAiIiIiIp5UYRARERGRiOf0Tc+eVGEQERERERFP6jCIiIiIiIgnDUkSERERkYinSc/eVGEQERERERFPqjCIiIiISMTTNz17U4VBREREREQ8qcMgIiIiIiKeNCRJRERERCKec+GOoORShUFERERERDypwyAiIiIiIp40JElEREREIp7ukuRNFQYREREREfGkCoOIiIiIRDxVGLypwiAiIiIiIp7UYRAREREREU8akiQiIiIiEU/fw+BNFQYREREREfGkCoOIiIiIRDxNevZmTvUXKQAz9AsjIiIihco5wn62vrxV97Cf4zScPyHsr0NeNCRJREREREQ8aUiSFFjKjM/DHUKRK9PhAgBqxrUIcyTFY33yQgC2nt8lvIEUk/gvpgBQKrp2eAMpBhnpawFI37Q8zJEUj+iqDQGYUfO8MEdS9Dqs/xKIjFwhsvLdm2vq4p/CHEnxiDn2tHCHAIBzJfLifomgCoOIiIiIiHhShUFEREREIp4LhDuCkksVBhERERER8aQOg4iIiIiIeNKQJBERERGJeAFNevakCoOIiIiIiHhShUFEREREIp5uq+pNFQYREREREfGkDoOIiIiIiHjSkCQRERERiXguoCFJXlRhEBERERERT6owiIiIiEjEcy7cEZRcqjCIiIiIiIgndRhERERERMSThiSJiIiISMTTpGdvqjCIiIiIiIgndRhERERERMSThiSJiIiISMQLOA1J8qIKg4iIiIiIeFKFQUREREQinlOFwZMqDCIiIiIi4kkdBhERERER8aQhSSIiIiIS8ZwLdwQllyoMIiIiIiLiSRUGEREREYl4uq2qN1UYRERERETEkzoMIiIiIiLiSUOSRERERCTi6XsYvKnCICIiIiIinlRhEBEREZGIp9uqelOHQcLq1z+WMPLf/yUQCHBel/YMOPe0XOsTNycz9PVP2bknlUDAcfvFPTi1bTPm/72GR9/6CgCH48bzutK1fYtw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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Correlation shows how features are related to each other using a linear correlation between variables.  Keep in mind that since it only find the linear relationship between variables, it will not be able to find the non-linear relationship.  A better metric to use is called <em>feature importance</em>, which we will determine after the model is built.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>On to the model</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">y</span> <span class="o">=</span> <span class="n">data_new</span><span class="p">[</span><span class="s1">&#39;energy load&#39;</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X</span> <span class="o">=</span> <span class="n">data_new</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="s1">&#39;energy load&#39;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">23</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model</span> <span class="o">=</span> <span class="n">RandomForestRegressor</span><span class="p">(</span><span class="n">n_estimators</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">23</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[16]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>RandomForestRegressor(bootstrap=True, criterion=&#39;mse&#39;, max_depth=None,
           max_features=&#39;auto&#39;, max_leaf_nodes=None,
           min_impurity_decrease=0.0, min_impurity_split=None,
           min_samples_leaf=1, min_samples_split=2,
           min_weight_fraction_leaf=0.0, n_estimators=100, n_jobs=None,
           oob_score=False, random_state=23, verbose=0, warm_start=False)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">predictions</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">r2_score</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">r2_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">predictions</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[19]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>0.9931211166410133</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The random forest model provides us with a highly accurate R2 score of 0.993</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">feature</span> <span class="ow">in</span> <span class="nb">zip</span><span class="p">(</span><span class="n">data_new</span><span class="o">.</span><span class="n">columns</span><span class="p">,</span> <span class="n">model</span><span class="o">.</span><span class="n">feature_importances_</span><span class="p">):</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">feature</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>(&#39;relative_compactness&#39;, 0.5060543116884478)
(&#39;surface_area&#39;, 0.14821753795820464)
(&#39;wall_area&#39;, 0.04233577705009435)
(&#39;roof_area&#39;, 0.08329432066422113)
(&#39;overall_height&#39;, 0.14625311504507843)
(&#39;orientation&#39;, 0.0023343330653874043)
(&#39;glazing_area&#39;, 0.06172701478673418)
(&#39;glazing_area_distribution&#39;, 0.009783589741831876)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>After training the model, relative compactness is the most important feature for predicting the heating and cooling load of a building.  The glazing area distribution is relatively unimportant.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The higher the feature importance score, the more relevant the feature is to the output variable, which is energy load in this case.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">feat_importances</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">model</span><span class="o">.</span><span class="n">feature_importances_</span><span class="p">,</span> <span class="n">index</span><span class="o">=</span><span class="n">X</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
<span class="n">feat_importances</span><span class="o">.</span><span class="n">nlargest</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s1">&#39;barh&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span> 
</pre></div>

    </div>
</div>
</div>

</div>
    </div>
  </div>
</body>

 


</html>